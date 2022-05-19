##### Virtual machine: 2x CPU, 4Gb RAM, 8Gb SSD
##### OS: debian 10
##### MongoDB v.5.0.8 [installed]

### Сборка шардированного отказоустойчивого кластера.

Создаем replicaset с конфигурацией шарда
```
sudo mkdir /var/lib/mongo/{dbc1,dbc2,dbc3} && sudo chmod 777 /var/lib/mongo/{dbc1,dbc2,dbc3}
mongod --configsvr --dbpath /var/lib/mongo/dbc1 --port 27001 --replSet RScfg --fork --logpath /var/lib/mongo/dbc1/dbc1.log --pidfilepath /var/lib/mongo/dbc1/dbc1.pid
mongod --configsvr --dbpath /var/lib/mongo/dbc2 --port 27002 --replSet RScfg --fork --logpath /var/lib/mongo/dbc2/dbc2.log --pidfilepath /var/lib/mongo/dbc2/dbc2.pid
mongod --configsvr --dbpath /var/lib/mongo/dbc3 --port 27003 --replSet RScfg --fork --logpath /var/lib/mongo/dbc3/dbc3.log --pidfilepath /var/lib/mongo/dbc3/dbc3.pid
```
Инициализируем конфиг-кластер
```
mongo --port 27001
rs.initiate({"_id" : "RScfg", configsvr: true, members : [{"_id" : 0, priority : 3, host : "127.0.0.1:27001"},{"_id" : 1, host : "127.0.0.1:27002"},{"_id" : 2, host : "127.0.0.1:27003"}]});

{
        "ok" : 1,
        "$gleStats" : {
                "lastOpTime" : Timestamp(1652956661, 1),
                "electionId" : ObjectId("000000000000000000000000")
        },
        "lastCommittedOpTime" : Timestamp(1652956661, 1),
        "$clusterTime" : {
                "clusterTime" : Timestamp(1652956661, 1),
                "signature" : {
                        "hash" : BinData(0,"AAAAAAAAAAAAAAAAAAAAAAAAAAA="),
                        "keyId" : NumberLong(0)
                }
        },
        "operationTime" : Timestamp(1652956661, 1)
}

```

Далее запускаем 9 инстансов mongo (3 replicaset, в каждом PRIMARY, SECONDARY и ARBITER)
```
sudo sudo mkdir /var/lib/mongo/{db1,db2,db3,db4,db5,db6,db7,db8,db9} && sudo chmod 777 /var/lib/mongo/{db1,db2,db3,db4,db5,db6,db7,db8,db9}
mongod --shardsvr --dbpath /var/lib/mongo/db1 --port 27011 --replSet RS1 --fork --logpath /var/lib/mongo/db1/db1.log --pidfilepath /var/lib/mongo/db1/db1.pid
mongod --shardsvr --dbpath /var/lib/mongo/db2 --port 27012 --replSet RS1 --fork --logpath /var/lib/mongo/db2/db2.log --pidfilepath /var/lib/mongo/db2/db2.pid
mongod --shardsvr --dbpath /var/lib/mongo/db3 --port 27013 --replSet RS1 --fork --logpath /var/lib/mongo/db3/db3.log --pidfilepath /var/lib/mongo/db3/db3.pid
mongod --shardsvr --dbpath /var/lib/mongo/db4 --port 27021 --replSet RS2 --fork --logpath /var/lib/mongo/db4/db4.log --pidfilepath /var/lib/mongo/db4/db4.pid
mongod --shardsvr --dbpath /var/lib/mongo/db5 --port 27022 --replSet RS2 --fork --logpath /var/lib/mongo/db5/db5.log --pidfilepath /var/lib/mongo/db5/db5.pid
mongod --shardsvr --dbpath /var/lib/mongo/db6 --port 27023 --replSet RS2 --fork --logpath /var/lib/mongo/db6/db6.log --pidfilepath /var/lib/mongo/db6/db6.pid
mongod --shardsvr --dbpath /var/lib/mongo/db7 --port 27031 --replSet RS3 --fork --logpath /var/lib/mongo/db7/db7.log --pidfilepath /var/lib/mongo/db7/db7.pid
mongod --shardsvr --dbpath /var/lib/mongo/db8 --port 27032 --replSet RS3 --fork --logpath /var/lib/mongo/db8/db8.log --pidfilepath /var/lib/mongo/db8/db8.pid
mongod --shardsvr --dbpath /var/lib/mongo/db9 --port 27033 --replSet RS3 --fork --logpath /var/lib/mongo/db9/db9.log --pidfilepath /var/lib/mongo/db9/db9.pid
```

Инстансы запущены, собираем каждый replicaset
```
mongo --port 27011
rs.initiate({"_id" : "RS1", members : [{"_id" : 0, priority : 3, host : "127.0.0.1:27011"},{"_id" : 1, host : "127.0.0.1:27012"},{"_id" : 2, host : "127.0.0.1:27013", arbiterOnly : true}]});

mongo --port 27021
rs.initiate({"_id" : "RS2", members : [{"_id" : 0, priority : 3, host : "127.0.0.1:27021"},{"_id" : 1, host : "127.0.0.1:27022"},{"_id" : 2, host : "127.0.0.1:27023", arbiterOnly : true}]});

mongo --port 27031
rs.initiate({"_id" : "RS3", members : [{"_id" : 0, priority : 3, host : "127.0.0.1:27031"},{"_id" : 1, host : "127.0.0.1:27032"},{"_id" : 2, host : "127.0.0.1:27033", arbiterOnly : true}]});
```
Далее поднимаем 2 ноды mongos для отказоустойчивости

```
mongos --configdb RScfg/127.0.0.1:27001,127.0.0.1:27002,127.0.0.1:27003 --port 27000 --fork --logpath /var/lib/mongo/dbc1/dbs.log --pidfilepath /var/lib/mongo/dbc1/dbs.pid 
mongos --configdb RScfg/127.0.0.1:27001,127.0.0.1:27002,127.0.0.1:27003 --port 27100 --fork --logpath /var/lib/mongo/dbc1/dbs2.log --pidfilepath /var/lib/mongo/dbc1/dbs2.pid
```

После чего добавляем каждый шард в кластер
```
mongo --port 27000
sh.addShard("RS1/127.0.0.1:27011,127.0.0.1:27012,127.0.0.1:27013")

{
        "shardAdded" : "RS1",
        "ok" : 1,
        "$clusterTime" : {
                "clusterTime" : Timestamp(1652957313, 5),
                "signature" : {
                        "hash" : BinData(0,"AAAAAAAAAAAAAAAAAAAAAAAAAAA="),
                        "keyId" : NumberLong(0)
                }
        },
        "operationTime" : Timestamp(1652957313, 5)
}

sh.addShard("RS2/127.0.0.1:27021,127.0.0.1:27022,127.0.0.1:27023")

{
        "shardAdded" : "RS2",
        "ok" : 1,
        "$clusterTime" : {
                "clusterTime" : Timestamp(1652957315, 4),
                "signature" : {
                        "hash" : BinData(0,"AAAAAAAAAAAAAAAAAAAAAAAAAAA="),
                        "keyId" : NumberLong(0)
                }
        },
        "operationTime" : Timestamp(1652957315, 4)
}

sh.addShard("RS3/127.0.0.1:27031,127.0.0.1:27032,127.0.0.1:27033")

{
        "shardAdded" : "RS3",
        "ok" : 1,
        "$clusterTime" : {
                "clusterTime" : Timestamp(1652957318, 3),
                "signature" : {
                        "hash" : BinData(0,"AAAAAAAAAAAAAAAAAAAAAAAAAAA="),
                        "keyId" : NumberLong(0)
                }
        },
        "operationTime" : Timestamp(1652957318, 3)
}

```

Проверяем статус шардированного кластера и видим что shards корректно отображаются. Каждый shard - отдельный replicaset.

```
sh.status()

--- Sharding Status ---
  sharding version: {
        "_id" : 1,
        "minCompatibleVersion" : 5,
        "currentVersion" : 6,
        "clusterId" : ObjectId("62861e015eb46c0c2d8abfa3")
  }
  shards:
        {  "_id" : "RS1",  "host" : "RS1/127.0.0.1:27011,127.0.0.1:27012",  "state" : 1,  "topologyTime" : Timestamp(1652957313, 2) }
        {  "_id" : "RS2",  "host" : "RS2/127.0.0.1:27021,127.0.0.1:27022",  "state" : 1,  "topologyTime" : Timestamp(1652957315, 2) }
        {  "_id" : "RS3",  "host" : "RS3/127.0.0.1:27031,127.0.0.1:27032",  "state" : 1,  "topologyTime" : Timestamp(1652957318, 1) }
  active mongoses:
        "5.0.8" : 2
  autosplit:
        Currently enabled: yes
  balancer:
        Currently enabled: yes
        Currently running: no
        Failed balancer rounds in last 5 attempts: 0
        Migration results for the last 24 hours:
                No recent migrations
  databases:
        {  "_id" : "config",  "primary" : "config",  "partitioned" : true }
```

Включим шардирование для БД test

```
use test
sh.enableSharding("test")

{
        "ok" : 1,
        "$clusterTime" : {
                "clusterTime" : Timestamp(1652957524, 18),
                "signature" : {
                        "hash" : BinData(0,"AAAAAAAAAAAAAAAAAAAAAAAAAAA="),
                        "keyId" : NumberLong(0)
                }
        },
        "operationTime" : Timestamp(1652957524, 8)
}
```

Установим размер чанка в 1Мб, чтобы небольшой объем данных был распределен по всему кластеру
```
use config
db.settings.save({ _id:"chunksize", value: 1})

WriteResult({ "nMatched" : 0, "nUpserted" : 1, "nModified" : 0, "_id" : "chunksize" })
```

Заполним тестовыми данными коллекцию sales (продажи по дням с кодом продавца)
```
use test
for (var i=0; i<100000; i++) { db.sales.insert({date: new Date(new Date("2022-05-19") - (Math.floor(Math.random() * 3650) * 24 * 60 * 60000)), saler_code: (Math.random()+1).toString(36).substring(2),  amount: Math.floor(Math.random() * 1000)}) }
```

Вот что получилось сгенерировать
```
db.sales.find().limit(10);
{ "_id" : ObjectId("62863553bea4dbf071e9a3a7"), "date" : ISODate("2020-06-09T00:00:00Z"), "saler_code" : "ro9z2rvxgu", "amount" : 365 }
{ "_id" : ObjectId("62863553bea4dbf071e9a3a9"), "date" : ISODate("2020-03-23T00:00:00Z"), "saler_code" : "6ob0pvac17j", "amount" : 407 }
{ "_id" : ObjectId("62863553bea4dbf071e9a3ab"), "date" : ISODate("2021-10-01T00:00:00Z"), "saler_code" : "d5qh3buld4j", "amount" : 697 }
{ "_id" : ObjectId("62863553bea4dbf071e9a3ae"), "date" : ISODate("2019-06-29T00:00:00Z"), "saler_code" : "n3jw0ovspz", "amount" : 970 }
{ "_id" : ObjectId("62863553bea4dbf071e9a3b0"), "date" : ISODate("2019-12-05T00:00:00Z"), "saler_code" : "9zkknwvuzc", "amount" : 727 }
{ "_id" : ObjectId("62863553bea4dbf071e9a3b7"), "date" : ISODate("2020-03-13T00:00:00Z"), "saler_code" : "u6fytumfzi", "amount" : 499 }
{ "_id" : ObjectId("62863553bea4dbf071e9a3be"), "date" : ISODate("2018-11-13T00:00:00Z"), "saler_code" : "ua39f6532a", "amount" : 790 }
{ "_id" : ObjectId("62863553bea4dbf071e9a3c0"), "date" : ISODate("2020-05-25T00:00:00Z"), "saler_code" : "vsvf3f7snu", "amount" : 899 }
{ "_id" : ObjectId("62863553bea4dbf071e9a3c1"), "date" : ISODate("2022-04-21T00:00:00Z"), "saler_code" : "x1w4w7ktfa", "amount" : 70 }
{ "_id" : ObjectId("62863553bea4dbf071e9a3c2"), "date" : ISODate("2019-06-26T00:00:00Z"), "saler_code" : "9vs9if563u", "amount" : 7 }
```

Далее создаем индекс по полю data
```
db.sales.createIndex({date: 1})

{
        "raw" : {
                "RS2/127.0.0.1:27021,127.0.0.1:27022" : {
                        "numIndexesBefore" : 1,
                        "numIndexesAfter" : 2,
                        "createdCollectionAutomatically" : false,
                        "commitQuorum" : "votingMembers",
                        "ok" : 1
                }
        },
        "ok" : 1,
        "$clusterTime" : {
                "clusterTime" : Timestamp(1652963413, 7),
                "signature" : {
                        "hash" : BinData(0,"AAAAAAAAAAAAAAAAAAAAAAAAAAA="),
                        "keyId" : NumberLong(0)
                }
        },
        "operationTime" : Timestamp(1652963413, 7)
}

```

После чего выполняем шардирование по данному индексу
```
sh.shardCollection("test.sales",{date: 1})

{
        "collectionsharded" : "test.sales",
        "ok" : 1,
        "$clusterTime" : {
                "clusterTime" : Timestamp(1652963455, 36),
                "signature" : {
                        "hash" : BinData(0,"AAAAAAAAAAAAAAAAAAAAAAAAAAA="),
                        "keyId" : NumberLong(0)
                }
        },
        "operationTime" : Timestamp(1652963455, 32)
}

```

И запускаем процесс шардирования в кластере
```
use admin
db.runCommand({shardCollection: "test.sales", key: {date: 1}})

{
        "collectionsharded" : "test.sales",
        "ok" : 1,
        "$clusterTime" : {
                "clusterTime" : Timestamp(1652963472, 10),
                "signature" : {
                        "hash" : BinData(0,"AAAAAAAAAAAAAAAAAAAAAAAAAAA="),
                        "keyId" : NumberLong(0)
                }
        },
        "operationTime" : Timestamp(1652963472, 6)
}
```

Проверяем статус шардированного кластера. Видим что test.sales был успешно разделен по ключу date. Также включена и работает балансировка.

```
sh.status()

--- Sharding Status ---
  sharding version: {
        "_id" : 1,
        "minCompatibleVersion" : 5,
        "currentVersion" : 6,
        "clusterId" : ObjectId("62861e015eb46c0c2d8abfa3")
  }
  shards:
        {  "_id" : "RS1",  "host" : "RS1/127.0.0.1:27011,127.0.0.1:27012",  "state" : 1,  "topologyTime" : Timestamp(1652957313, 2) }
        {  "_id" : "RS2",  "host" : "RS2/127.0.0.1:27021,127.0.0.1:27022",  "state" : 1,  "topologyTime" : Timestamp(1652957315, 2) }
        {  "_id" : "RS3",  "host" : "RS3/127.0.0.1:27031,127.0.0.1:27032",  "state" : 1,  "topologyTime" : Timestamp(1652957318, 1) }
  active mongoses:
        "5.0.8" : 2
  autosplit:
        Currently enabled: yes
  balancer:
        Currently enabled: yes
        Currently running: no
        Failed balancer rounds in last 5 attempts: 0
        Migration results for the last 24 hours:
                687 : Success
  databases:
        {  "_id" : "config",  "primary" : "config",  "partitioned" : true }
                config.system.sessions
                        shard key: { "_id" : 1 }
                        unique: false
                        balancing: true
                        chunks:
                                RS1     342
                                RS2     341
                                RS3     341
                        too many chunks to print, use verbose if you want to force print
        {  "_id" : "test",  "primary" : "RS2",  "partitioned" : true,  "version" : {  "uuid" : UUID("60d93313-a928-45bf-8e7d-c5e7d4c0812a"),  "timestamp" : Timestamp(1652957524, 6),  "lastMod" : 1 } }
                test.sales
                        shard key: { "date" : 1 }
                        unique: false
                        balancing: true
                        chunks:
                                RS1     2
                                RS2     3
                                RS3     3
                        { "date" : { "$minKey" : 1 } } -->> { "date" : ISODate("2013-09-16T00:00:00Z") } on : RS1 Timestamp(2, 0)
                        { "date" : ISODate("2013-09-16T00:00:00Z") } -->> { "date" : ISODate("2015-01-09T00:00:00Z") } on : RS3 Timestamp(3, 0)
                        { "date" : ISODate("2015-01-09T00:00:00Z") } -->> { "date" : ISODate("2016-05-06T00:00:00Z") } on : RS1 Timestamp(4, 0)
                        { "date" : ISODate("2016-05-06T00:00:00Z") } -->> { "date" : ISODate("2017-09-02T00:00:00Z") } on : RS3 Timestamp(5, 0)
                        { "date" : ISODate("2017-09-02T00:00:00Z") } -->> { "date" : ISODate("2018-11-02T00:00:00Z") } on : RS3 Timestamp(6, 0)
                        { "date" : ISODate("2018-11-02T00:00:00Z") } -->> { "date" : ISODate("2020-01-07T00:00:00Z") } on : RS2 Timestamp(6, 1)
                        { "date" : ISODate("2020-01-07T00:00:00Z") } -->> { "date" : ISODate("2021-03-13T00:00:00Z") } on : RS2 Timestamp(1, 6)
                        { "date" : ISODate("2021-03-13T00:00:00Z") } -->> { "date" : { "$maxKey" : 1 } } on : RS2 Timestamp(1, 7)

sh.balancerCollectionStatus("test.sales")
{
        "balancerCompliant" : true,
        "ok" : 1,
        "$clusterTime" : {
                "clusterTime" : Timestamp(1652963503, 2),
                "signature" : {
                        "hash" : BinData(0,"AAAAAAAAAAAAAAAAAAAAAAAAAAA="),
                        "keyId" : NumberLong(0)
                }
        },
        "operationTime" : Timestamp(1652963503, 2)
}

```
Данные добавлены, шардированный кластер собран. 

### Проверка отказоустойчивости

Проверим что сейчас запущено из mongo
```
ps aux | grep mongo| grep -Ev "grep"
user      1616  1.4  4.4 2102876 181624 ?      Sl   06:34   2:26 mongod --configsvr --dbpath /var/lib/mongo/dbc1 --port 27001 --replSet RScfg --fork --logpath /var/lib/mongo/dbc1/dbc1.log --pidfilepath /var/lib/mongo/dbc1/dbc1.pid
user      1680  1.1  4.7 2002624 190376 ?      Sl   06:34   1:58 mongod --configsvr --dbpath /var/lib/mongo/dbc2 --port 27002 --replSet RScfg --fork --logpath /var/lib/mongo/dbc2/dbc2.log --pidfilepath /var/lib/mongo/dbc2/dbc2.pid
user      1747  1.1  4.7 2002288 192620 ?      Sl   06:34   1:58 mongod --configsvr --dbpath /var/lib/mongo/dbc3 --port 27003 --replSet RScfg --fork --logpath /var/lib/mongo/dbc3/dbc3.log --pidfilepath /var/lib/mongo/dbc3/dbc3.pid
user      4558  1.0  4.7 2129428 193564 ?      Sl   06:41   1:38 mongod --shardsvr --dbpath /var/lib/mongo/db1 --port 27011 --replSet RS1 --fork --logpath /var/lib/mongo/db1/db1.log --pidfilepath /var/lib/mongo/db1/db1.pid
user      4612  0.9  4.8 2044024 196932 ?      Sl   06:41   1:28 mongod --shardsvr --dbpath /var/lib/mongo/db2 --port 27012 --replSet RS1 --fork --logpath /var/lib/mongo/db2/db2.log --pidfilepath /var/lib/mongo/db2/db2.pid
user      4672  0.4  3.6 1757484 148964 ?      Sl   06:41   0:43 mongod --shardsvr --dbpath /var/lib/mongo/db3 --port 27013 --replSet RS1 --fork --logpath /var/lib/mongo/db3/db3.log --pidfilepath /var/lib/mongo/db3/db3.pid
user      4732  2.7  5.7 2209512 231012 ?      Sl   06:41   4:27 mongod --shardsvr --dbpath /var/lib/mongo/db4 --port 27021 --replSet RS2 --fork --logpath /var/lib/mongo/db4/db4.log --pidfilepath /var/lib/mongo/db4/db4.pid
user      4792  2.7  5.7 2091460 233384 ?      Sl   06:41   4:21 mongod --shardsvr --dbpath /var/lib/mongo/db5 --port 27022 --replSet RS2 --fork --logpath /var/lib/mongo/db5/db5.log --pidfilepath /var/lib/mongo/db5/db5.pid
user      4852  0.4  3.4 1751360 141220 ?      Sl   06:41   0:43 mongod --shardsvr --dbpath /var/lib/mongo/db6 --port 27023 --replSet RS2 --fork --logpath /var/lib/mongo/db6/db6.log --pidfilepath /var/lib/mongo/db6/db6.pid
user      4906  0.8  4.7 2106604 190732 ?      Sl   06:41   1:20 mongod --shardsvr --dbpath /var/lib/mongo/db7 --port 27031 --replSet RS3 --fork --logpath /var/lib/mongo/db7/db7.log --pidfilepath /var/lib/mongo/db7/db7.pid
user      4967  0.7  4.8 2048488 197228 ?      Sl   06:41   1:14 mongod --shardsvr --dbpath /var/lib/mongo/db8 --port 27032 --replSet RS3 --fork --logpath /var/lib/mongo/db8/db8.log --pidfilepath /var/lib/mongo/db8/db8.pid
user      5039  0.4  3.5 1752368 141628 ?      Sl   06:41   0:43 mongod --shardsvr --dbpath /var/lib/mongo/db9 --port 27033 --replSet RS3 --fork --logpath /var/lib/mongo/db9/db9.log --pidfilepath /var/lib/mongo/db9/db9.pid
user      7214  0.7  1.3 1449044 54092 ?       Sl   06:46   1:12 mongos --configdb RScfg/127.0.0.1:27001,127.0.0.1:27002,127.0.0.1:27003 --port 27000 --fork --logpath /var/lib/mongo/dbc1/dbs.log --pidfilepath /var/lib/mongo/dbc1/dbs.pid
user      7290  0.2  1.2 1439696 49928 ?       Sl   06:46   0:19 mongos --configdb RScfg/127.0.0.1:27001,127.0.0.1:27002,127.0.0.1:27003 --port 27100 --fork --logpath /var/lib/mongo/dbc1/dbs2.log --pidfilepath /var/lib/mongo/dbc1/dbs2.pid
```

Принудительно завершим по одному процессу в каждом репликасете (пусть это будут все текущие PRIMARY ноды и mongos на порту 27000)
```
kill 1616 4558 4732 4906 7214

ps aux | grep mongo| grep -Ev "grep"
user      1680  1.1  4.7 2057912 193180 ?      Sl   06:34   2:03 mongod --configsvr --dbpath /var/lib/mongo/dbc2 --port 27002 --replSet RScfg --fork --logpath /var/lib/mongo/dbc2/dbc2.log --pidfilepath /var/lib/mongo/dbc2/dbc2.pid
user      1747  1.1  4.7 2061716 193816 ?      Sl   06:34   2:03 mongod --configsvr --dbpath /var/lib/mongo/dbc3 --port 27003 --replSet RScfg --fork --logpath /var/lib/mongo/dbc3/dbc3.log --pidfilepath /var/lib/mongo/dbc3/dbc3.pid
user      4524  0.0  1.2 1165332 51576 pts/0   SLl+ 09:26   0:00 mongo --port 27100
user      4612  0.9  4.9 2194624 199796 ?      Sl   06:41   1:32 mongod --shardsvr --dbpath /var/lib/mongo/db2 --port 27012 --replSet RS1 --fork --logpath /var/lib/mongo/db2/db2.log --pidfilepath /var/lib/mongo/db2/db2.pid
user      4672  0.4  3.7 1773876 149596 ?      Sl   06:41   0:45 mongod --shardsvr --dbpath /var/lib/mongo/db3 --port 27013 --replSet RS1 --fork --logpath /var/lib/mongo/db3/db3.log --pidfilepath /var/lib/mongo/db3/db3.pid
user      4792  2.6  5.8 2238976 234656 ?      Sl   06:41   4:25 mongod --shardsvr --dbpath /var/lib/mongo/db5 --port 27022 --replSet RS2 --fork --logpath /var/lib/mongo/db5/db5.log --pidfilepath /var/lib/mongo/db5/db5.pid
user      4852  0.4  3.5 1767752 141924 ?      Sl   06:41   0:45 mongod --shardsvr --dbpath /var/lib/mongo/db6 --port 27023 --replSet RS2 --fork --logpath /var/lib/mongo/db6/db6.log --pidfilepath /var/lib/mongo/db6/db6.pid
user      4967  0.7  4.9 2182696 201784 ?      Sl   06:41   1:17 mongod --shardsvr --dbpath /var/lib/mongo/db8 --port 27032 --replSet RS3 --fork --logpath /var/lib/mongo/db8/db8.log --pidfilepath /var/lib/mongo/db8/db8.pid
user      5039  0.4  3.5 1776956 144452 ?      Sl   06:41   0:45 mongod --shardsvr --dbpath /var/lib/mongo/db9 --port 27033 --replSet RS3 --fork --logpath /var/lib/mongo/db9/db9.log --pidfilepath /var/lib/mongo/db9/db9.pid
user      7290  0.2  1.2 1440724 50516 ?       Sl   06:46   0:20 mongos --configdb RScfg/127.0.0.1:27001,127.0.0.1:27002,127.0.0.1:27003 --port 27100 --fork --logpath /var/lib/mongo/dbc1/dbs2.log --pidfilepath /var/lib/mongo/dbc1/dbs2.pid

```

Проверим насколько остался работоспобным кластер- подключимся к mongos на порту 27100, проверим статус кластера и выберем произвольный набор данных из test и попробуем что-нибудь записать

```
--- Sharding Status ---
  sharding version: {
        "_id" : 1,
        "minCompatibleVersion" : 5,
        "currentVersion" : 6,
        "clusterId" : ObjectId("62861e015eb46c0c2d8abfa3")
  }
  shards:
        {  "_id" : "RS1",  "host" : "RS1/127.0.0.1:27011,127.0.0.1:27012",  "state" : 1,  "topologyTime" : Timestamp(1652957313, 2) }
        {  "_id" : "RS2",  "host" : "RS2/127.0.0.1:27021,127.0.0.1:27022",  "state" : 1,  "topologyTime" : Timestamp(1652957315, 2) }
        {  "_id" : "RS3",  "host" : "RS3/127.0.0.1:27031,127.0.0.1:27032",  "state" : 1,  "topologyTime" : Timestamp(1652957318, 1) }
  active mongoses:
        "5.0.8" : 1
  autosplit:
        Currently enabled: yes
  balancer:
        Currently enabled: yes
        Currently running: no
        Failed balancer rounds in last 5 attempts: 0
        Migration results for the last 24 hours:
                687 : Success
  databases:
        {  "_id" : "config",  "primary" : "config",  "partitioned" : true }
                config.system.sessions
                        shard key: { "_id" : 1 }
                        unique: false
                        balancing: true
                        chunks:
                                RS1     342
                                RS2     341
                                RS3     341
                        too many chunks to print, use verbose if you want to force print
        {  "_id" : "test",  "primary" : "RS2",  "partitioned" : true,  "version" : {  "uuid" : UUID("60d93313-a928-45bf-8e7d-c5e7d4c0812a"),  "timestamp" : Timestamp(1652957524, 6),  "lastMod" : 1 } }
                test.sales
                        shard key: { "date" : 1 }
                        unique: false
                        balancing: true
                        chunks:
                                RS1     2
                                RS2     3
                                RS3     3
                        { "date" : { "$minKey" : 1 } } -->> { "date" : ISODate("2013-09-16T00:00:00Z") } on : RS1 Timestamp(2, 0)
                        { "date" : ISODate("2013-09-16T00:00:00Z") } -->> { "date" : ISODate("2015-01-09T00:00:00Z") } on : RS3 Timestamp(3, 0)
                        { "date" : ISODate("2015-01-09T00:00:00Z") } -->> { "date" : ISODate("2016-05-06T00:00:00Z") } on : RS1 Timestamp(4, 0)
                        { "date" : ISODate("2016-05-06T00:00:00Z") } -->> { "date" : ISODate("2017-09-02T00:00:00Z") } on : RS3 Timestamp(5, 0)
                        { "date" : ISODate("2017-09-02T00:00:00Z") } -->> { "date" : ISODate("2018-11-02T00:00:00Z") } on : RS3 Timestamp(6, 0)
                        { "date" : ISODate("2018-11-02T00:00:00Z") } -->> { "date" : ISODate("2020-01-07T00:00:00Z") } on : RS2 Timestamp(6, 1)
                        { "date" : ISODate("2020-01-07T00:00:00Z") } -->> { "date" : ISODate("2021-03-13T00:00:00Z") } on : RS2 Timestamp(1, 6)
                        { "date" : ISODate("2021-03-13T00:00:00Z") } -->> { "date" : { "$maxKey" : 1 } } on : RS2 Timestamp(1, 7)


db.sales.find({date: {$gte:ISODate("2015-01-01T00:00:00.000Z"), $lt:ISODate("2016-01-01T00:00:00.000Z")}}).limit(10)
{ "_id" : ObjectId("6286355cbea4dbf071e9ab51"), "date" : ISODate("2015-01-09T00:00:00Z"), "saler_code" : "7hdhatiunw", "amount" : 982 }
{ "_id" : ObjectId("62863561bea4dbf071e9af4e"), "date" : ISODate("2015-01-09T00:00:00Z"), "saler_code" : "o9p5xpr5xx", "amount" : 274 }
{ "_id" : ObjectId("62863565bea4dbf071e9b214"), "date" : ISODate("2015-01-09T00:00:00Z"), "saler_code" : "pych2kt7u4j", "amount" : 133 }
{ "_id" : ObjectId("62863566bea4dbf071e9b363"), "date" : ISODate("2015-01-09T00:00:00Z"), "saler_code" : "xa7lv7quth", "amount" : 683 }
{ "_id" : ObjectId("62863575bea4dbf071e9bdf1"), "date" : ISODate("2015-01-09T00:00:00Z"), "saler_code" : "z0s6nthfih", "amount" : 432 }
{ "_id" : ObjectId("628635abbea4dbf071e9e5c9"), "date" : ISODate("2015-01-09T00:00:00Z"), "saler_code" : "7xgggxjoux", "amount" : 331 }
{ "_id" : ObjectId("628635aebea4dbf071e9e7e1"), "date" : ISODate("2015-01-09T00:00:00Z"), "saler_code" : "nzporxv1xif", "amount" : 23 }
{ "_id" : ObjectId("628635adbea4dbf071e9e6e5"), "date" : ISODate("2015-01-09T00:00:00Z"), "saler_code" : "nx68uriup9", "amount" : 563 }
{ "_id" : ObjectId("628635e5bea4dbf071ea107f"), "date" : ISODate("2015-01-09T00:00:00Z"), "saler_code" : "007un00tf5", "amount" : 181 }
{ "_id" : ObjectId("628635e6bea4dbf071ea119f"), "date" : ISODate("2015-01-09T00:00:00Z"), "saler_code" : "39vhhg6u3v", "amount" : 532 }

db.sales.insert({date:ISODate("2022-05-19T00:00:00Z"),saler_code : "aaaaa11111", amount : 500},{ writeConcern: { wtimeout: 5 }})
WriteResult({ "nInserted" : 1 })

```

Кластер остался работоспособен. 

### Настройка авторизации

Запустим отдельный инстанс mongo
```
mongod --dbpath /var/lib/mongo/db10 --port 27333 --fork --logpath /var/lib/mongo/db10/db10.log --pidfilepath /var/lib/mongo/db10/db10.pid
```
Создадим новую роль с полными правами (ServiceAdmins) и пользователя (DutyDBA)

```
mongo --port 27333
db = db.getSiblingDB("admin")
db.createRole(
    {      
     role: "ServiceAdmins",      
     privileges:[
        { resource: {anyResource:true}, actions: ["anyAction"]}
     ],      
     roles:[] 
    }
)

{
        "role" : "ServiceAdmins",
        "privileges" : [
                {
                        "resource" : {
                                "anyResource" : true
                        },
                        "actions" : [
                                "anyAction"
                        ]
                }
        ],
        "roles" : [ ]
}

db.createUser({      
     user: "DutyDBA",      
     pwd: "24oclock",      
     roles: ["ServiceAdmins"] 
})

Successfully added user: { "user" : "DutyDBA", "roles" : [ "ServiceAdmins" ] }
```

Проверим что пользователь добавлен
```
use admin
db.system.roles.find()
{ "_id" : "admin.ServiceAdmins", "role" : "ServiceAdmins", "db" : "admin", "privileges" : [ { "resource" : { "anyResource" : true }, "actions" : [ "anyAction" ] } ], "roles" : [ ] }

db.system.users.find()
{ "_id" : "admin.DutyDBA", "userId" : UUID("15209f3c-0b29-4999-aba1-c933255911b5"), "user" : "DutyDBA", "db" : "admin", "credentials" : { "SCRAM-SHA-1" : { "iterationCount" : 10000, "salt" : "0+36luQQ2QXMe6A/AxUtDA==", "storedKey" : "/eBtTQgXTV36IuA6dAHTDO8WwOc=", "serverKey" : "20N5/4ey4ubfOVrFPJarbdrnx2g=" }, "SCRAM-SHA-256" : { "iterationCount" : 15000, "salt" : "+tToBcPYpUzTbVbr9jfPIS7Qj7FIpBGoGfuUKw==", "storedKey" : "eKaokWxUgKo/i4hVrAiKCVQGCF4/dsDoVhxxqHyrxFs=", "serverKey" : "h/4ibrCarYwHRc6RGuFwvZZLRTHUyCZdQ4eNlIPGRvQ=" } }, "roles" : [ { "role" : "ServiceAdmins", "db" : "admin" } ] }
```

Перезапустим инстанс с параметром авторизации --auth

```
db.shutdownServer()
mongod --dbpath /var/lib/mongo/db10 --port 27333 --auth --fork --logpath /var/lib/mongo/db10/db10.log --pidfilepath /var/lib/mongo/db10/db10.pid
```

Проверим авторизацию
```
mongo --port 27333
MongoDB shell version v5.0.8
connecting to: mongodb://127.0.0.1:27333/?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("4ed7c123-75d6-467c-9682-196497bf096f") }
MongoDB server version: 5.0.8
================
Warning: the "mongo" shell has been superseded by "mongosh",
which delivers improved usability and compatibility.The "mongo" shell has been deprecated and will be removed in
an upcoming release.
For installation instructions, see
https://docs.mongodb.com/mongodb-shell/install/
================
> show databases
```

Без указания пользователя подключится удается, но данные не отображаются

Проверим авторизацию под новым пользователем
```
mongo --port 27333 -u DutyDBA -p 24oclock --authenticationDatabase "admin"
show databases

admin   0.000GB
config  0.000GB
local   0.000GB
```

Авторизация под новым пользователем успешна
