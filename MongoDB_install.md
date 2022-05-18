##### Virtual machine: 1x CPU, 1Gb RAM, 8Gb SSD
##### OS: debian 10

### Install:
> apt-get install gnupg </br>
> wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add - </br>
> echo "deb http://repo.mongodb.org/apt/debian buster/mongodb-org/5.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list </br>
> apt-get update </br>
> apt-get install -y mongodb-org </br>
> systemctl start mongod </br>

### Import data
> mongoimport -d uber -c pickups --type csv --file /tmp/Uber-Jan-Feb-FOIL.csv --headerline </br>
```
2022-05-18T02:25:31.812-0400    connected to: mongodb://localhost/ </br>
2022-05-18T02:25:31.841-0400    354 document(s) imported successfully. 0 document(s) failed to import. </br>
```
### Usage
> mongo </br>
> show dbs; </br>
```
admin   0.000GB </br>
config  0.000GB </br>
local   0.000GB </br>
uber    0.000GB </br>
```
> use uber; </br>
```
switched to db uber </br>
```
> db.pickups.find(); </br>

```
{ "_id" : ObjectId("6284915b0fbdf92118fe376c"), "dispatching_base_number" : "B02512", "date" : "1/1/2015", "active_vehicles" : 190, "trips" : 1132 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe376d"), "dispatching_base_number" : "B02765", "date" : "1/1/2015", "active_vehicles" : 225, "trips" : 1765 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe376e"), "dispatching_base_number" : "B02764", "date" : "1/1/2015", "active_vehicles" : 3427, "trips" : 29421 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe376f"), "dispatching_base_number" : "B02682", "date" : "1/1/2015", "active_vehicles" : 945, "trips" : 7679 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3770"), "dispatching_base_number" : "B02617", "date" : "1/1/2015", "active_vehicles" : 1228, "trips" : 9537 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3771"), "dispatching_base_number" : "B02598", "date" : "1/1/2015", "active_vehicles" : 870, "trips" : 6903 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3772"), "dispatching_base_number" : "B02598", "date" : "1/2/2015", "active_vehicles" : 785, "trips" : 4768 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3773"), "dispatching_base_number" : "B02617", "date" : "1/2/2015", "active_vehicles" : 1137, "trips" : 7065 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3774"), "dispatching_base_number" : "B02512", "date" : "1/2/2015", "active_vehicles" : 175, "trips" : 875 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3775"), "dispatching_base_number" : "B02682", "date" : "1/2/2015", "active_vehicles" : 890, "trips" : 5506 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3776"), "dispatching_base_number" : "B02765", "date" : "1/2/2015", "active_vehicles" : 196, "trips" : 1001 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3777"), "dispatching_base_number" : "B02764", "date" : "1/2/2015", "active_vehicles" : 3147, "trips" : 19974 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3778"), "dispatching_base_number" : "B02765", "date" : "1/3/2015", "active_vehicles" : 201, "trips" : 1526 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3779"), "dispatching_base_number" : "B02617", "date" : "1/3/2015", "active_vehicles" : 1188, "trips" : 10664 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe377a"), "dispatching_base_number" : "B02598", "date" : "1/3/2015", "active_vehicles" : 818, "trips" : 7432 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe377b"), "dispatching_base_number" : "B02682", "date" : "1/3/2015", "active_vehicles" : 915, "trips" : 8010 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe377c"), "dispatching_base_number" : "B02512", "date" : "1/3/2015", "active_vehicles" : 173, "trips" : 1088 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe377d"), "dispatching_base_number" : "B02764", "date" : "1/3/2015", "active_vehicles" : 3215, "trips" : 29729 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe377e"), "dispatching_base_number" : "B02512", "date" : "1/4/2015", "active_vehicles" : 147, "trips" : 791 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe377f"), "dispatching_base_number" : "B02682", "date" : "1/4/2015", "active_vehicles" : 812, "trips" : 5621 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3780"), "dispatching_base_number" : "B02598", "date" : "1/4/2015", "active_vehicles" : 746, "trips" : 5223 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3781"), "dispatching_base_number" : "B02765", "date" : "1/4/2015", "active_vehicles" : 183, "trips" : 993 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3782"), "dispatching_base_number" : "B02617", "date" : "1/4/2015", "active_vehicles" : 1088, "trips" : 7729 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3783"), "dispatching_base_number" : "B02764", "date" : "1/4/2015", "active_vehicles" : 2862, "trips" : 20441 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3784"), "dispatching_base_number" : "B02512", "date" : "1/5/2015", "active_vehicles" : 194, "trips" : 984 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3785"), "dispatching_base_number" : "B02682", "date" : "1/5/2015", "active_vehicles" : 951, "trips" : 6012 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3786"), "dispatching_base_number" : "B02617", "date" : "1/5/2015", "active_vehicles" : 1218, "trips" : 7899 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3787"), "dispatching_base_number" : "B02764", "date" : "1/5/2015", "active_vehicles" : 3387, "trips" : 20926 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3788"), "dispatching_base_number" : "B02598", "date" : "1/5/2015", "active_vehicles" : 907, "trips" : 5798 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3789"), "dispatching_base_number" : "B02765", "date" : "1/5/2015", "active_vehicles" : 227, "trips" : 1133 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe378a"), "dispatching_base_number" : "B02764", "date" : "1/6/2015", "active_vehicles" : 3473, "trips" : 25301 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe378b"), "dispatching_base_number" : "B02682", "date" : "1/6/2015", "active_vehicles" : 1022, "trips" : 7491 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe378c"), "dispatching_base_number" : "B02617", "date" : "1/6/2015", "active_vehicles" : 1336, "trips" : 10128 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe378d"), "dispatching_base_number" : "B02765", "date" : "1/6/2015", "active_vehicles" : 234, "trips" : 1376 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe378e"), "dispatching_base_number" : "B02512", "date" : "1/6/2015", "active_vehicles" : 218, "trips" : 1314 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe378f"), "dispatching_base_number" : "B02598", "date" : "1/6/2015", "active_vehicles" : 933, "trips" : 6816 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3790"), "dispatching_base_number" : "B02617", "date" : "1/7/2015", "active_vehicles" : 1363, "trips" : 11528 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3791"), "dispatching_base_number" : "B02682", "date" : "1/7/2015", "active_vehicles" : 1039, "trips" : 9078 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3792"), "dispatching_base_number" : "B02764", "date" : "1/7/2015", "active_vehicles" : 3603, "trips" : 29949 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3793"), "dispatching_base_number" : "B02765", "date" : "1/7/2015", "active_vehicles" : 248, "trips" : 1704 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3794"), "dispatching_base_number" : "B02512", "date" : "1/7/2015", "active_vehicles" : 217, "trips" : 1446 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3795"), "dispatching_base_number" : "B02598", "date" : "1/7/2015", "active_vehicles" : 974, "trips" : 8397 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3796"), "dispatching_base_number" : "B02765", "date" : "1/8/2015", "active_vehicles" : 262, "trips" : 1911 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3797"), "dispatching_base_number" : "B02598", "date" : "1/8/2015", "active_vehicles" : 1070, "trips" : 10050 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3798"), "dispatching_base_number" : "B02512", "date" : "1/8/2015", "active_vehicles" : 238, "trips" : 1772 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3799"), "dispatching_base_number" : "B02682", "date" : "1/8/2015", "active_vehicles" : 1135, "trips" : 10416 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe379a"), "dispatching_base_number" : "B02764", "date" : "1/8/2015", "active_vehicles" : 3831, "trips" : 33802 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe379b"), "dispatching_base_number" : "B02617", "date" : "1/8/2015", "active_vehicles" : 1463, "trips" : 13462 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe379c"), "dispatching_base_number" : "B02617", "date" : "1/9/2015", "active_vehicles" : 1455, "trips" : 13165 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe379d"), "dispatching_base_number" : "B02512", "date" : "1/9/2015", "active_vehicles" : 224, "trips" : 1560 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe379e"), "dispatching_base_number" : "B02764", "date" : "1/9/2015", "active_vehicles" : 3820, "trips" : 33517 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe379f"), "dispatching_base_number" : "B02682", "date" : "1/9/2015", "active_vehicles" : 1140, "trips" : 10477 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37a0"), "dispatching_base_number" : "B02598", "date" : "1/9/2015", "active_vehicles" : 1070, "trips" : 9538 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37a1"), "dispatching_base_number" : "B02765", "date" : "1/9/2015", "active_vehicles" : 280, "trips" : 2039 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37a2"), "dispatching_base_number" : "B02682", "date" : "1/10/2015", "active_vehicles" : 1057, "trips" : 11629 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37a3"), "dispatching_base_number" : "B02617", "date" : "1/10/2015", "active_vehicles" : 1331, "trips" : 13856 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37a4"), "dispatching_base_number" : "B02598", "date" : "1/10/2015", "active_vehicles" : 949, "trips" : 10287 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37a5"), "dispatching_base_number" : "B02512", "date" : "1/10/2015", "active_vehicles" : 206, "trips" : 1646 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37a6"), "dispatching_base_number" : "B02764", "date" : "1/10/2015", "active_vehicles" : 3558, "trips" : 38864 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37a7"), "dispatching_base_number" : "B02765", "date" : "1/10/2015", "active_vehicles" : 245, "trips" : 2202 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37a8"), "dispatching_base_number" : "B02765", "date" : "1/11/2015", "active_vehicles" : 220, "trips" : 1672 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37a9"), "dispatching_base_number" : "B02598", "date" : "1/11/2015", "active_vehicles" : 832, "trips" : 7176 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37aa"), "dispatching_base_number" : "B02682", "date" : "1/11/2015", "active_vehicles" : 943, "trips" : 8461 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37ab"), "dispatching_base_number" : "B02764", "date" : "1/11/2015", "active_vehicles" : 3186, "trips" : 27681 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37ac"), "dispatching_base_number" : "B02617", "date" : "1/11/2015", "active_vehicles" : 1228, "trips" : 10932 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37ad"), "dispatching_base_number" : "B02512", "date" : "1/11/2015", "active_vehicles" : 162, "trips" : 1104 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37ae"), "dispatching_base_number" : "B02764", "date" : "1/12/2015", "active_vehicles" : 3499, "trips" : 26852 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37af"), "dispatching_base_number" : "B02765", "date" : "1/12/2015", "active_vehicles" : 279, "trips" : 1711 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37b0"), "dispatching_base_number" : "B02512", "date" : "1/12/2015", "active_vehicles" : 217, "trips" : 1399 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37b1"), "dispatching_base_number" : "B02598", "date" : "1/12/2015", "active_vehicles" : 964, "trips" : 7915 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37b2"), "dispatching_base_number" : "B02682", "date" : "1/12/2015", "active_vehicles" : 1082, "trips" : 9107 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37b3"), "dispatching_base_number" : "B02617", "date" : "1/12/2015", "active_vehicles" : 1323, "trips" : 10662 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37b4"), "dispatching_base_number" : "B02765", "date" : "1/13/2015", "active_vehicles" : 258, "trips" : 1697 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37b5"), "dispatching_base_number" : "B02598", "date" : "1/13/2015", "active_vehicles" : 975, "trips" : 8713 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37b6"), "dispatching_base_number" : "B02617", "date" : "1/13/2015", "active_vehicles" : 1342, "trips" : 11825 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37b7"), "dispatching_base_number" : "B02512", "date" : "1/13/2015", "active_vehicles" : 234, "trips" : 1652 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37b8"), "dispatching_base_number" : "B02764", "date" : "1/13/2015", "active_vehicles" : 3658, "trips" : 29983 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37b9"), "dispatching_base_number" : "B02682", "date" : "1/13/2015", "active_vehicles" : 1092, "trips" : 9629 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37ba"), "dispatching_base_number" : "B02764", "date" : "1/14/2015", "active_vehicles" : 3736, "trips" : 29550 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37bb"), "dispatching_base_number" : "B02765", "date" : "1/14/2015", "active_vehicles" : 271, "trips" : 1600 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37bc"), "dispatching_base_number" : "B02598", "date" : "1/14/2015", "active_vehicles" : 1030, "trips" : 8870 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37bd"), "dispatching_base_number" : "B02512", "date" : "1/14/2015", "active_vehicles" : 233, "trips" : 1582 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37be"), "dispatching_base_number" : "B02617", "date" : "1/14/2015", "active_vehicles" : 1405, "trips" : 11965 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37bf"), "dispatching_base_number" : "B02682", "date" : "1/14/2015", "active_vehicles" : 1174, "trips" : 9762 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37c0"), "dispatching_base_number" : "B02512", "date" : "1/15/2015", "active_vehicles" : 237, "trips" : 1636 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37c1"), "dispatching_base_number" : "B02682", "date" : "1/15/2015", "active_vehicles" : 1208, "trips" : 10391 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37c2"), "dispatching_base_number" : "B02617", "date" : "1/15/2015", "active_vehicles" : 1457, "trips" : 12539 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37c3"), "dispatching_base_number" : "B02765", "date" : "1/15/2015", "active_vehicles" : 270, "trips" : 1797 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37c4"), "dispatching_base_number" : "B02764", "date" : "1/15/2015", "active_vehicles" : 3840, "trips" : 31214 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37c5"), "dispatching_base_number" : "B02598", "date" : "1/15/2015", "active_vehicles" : 1068, "trips" : 9152 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37c6"), "dispatching_base_number" : "B02617", "date" : "1/16/2015", "active_vehicles" : 1445, "trips" : 12977 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37c7"), "dispatching_base_number" : "B02765", "date" : "1/16/2015", "active_vehicles" : 290, "trips" : 2082 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37c8"), "dispatching_base_number" : "B02764", "date" : "1/16/2015", "active_vehicles" : 3975, "trips" : 34822 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37c9"), "dispatching_base_number" : "B02682", "date" : "1/16/2015", "active_vehicles" : 1250, "trips" : 11280 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37ca"), "dispatching_base_number" : "B02512", "date" : "1/16/2015", "active_vehicles" : 234, "trips" : 1481 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37cb"), "dispatching_base_number" : "B02598", "date" : "1/16/2015", "active_vehicles" : 1079, "trips" : 9838 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37cc"), "dispatching_base_number" : "B02598", "date" : "1/17/2015", "active_vehicles" : 974, "trips" : 9546 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37cd"), "dispatching_base_number" : "B02512", "date" : "1/17/2015", "active_vehicles" : 201, "trips" : 1281 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37ce"), "dispatching_base_number" : "B02682", "date" : "1/17/2015", "active_vehicles" : 1137, "trips" : 11382 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37cf"), "dispatching_base_number" : "B02765", "date" : "1/17/2015", "active_vehicles" : 252, "trips" : 2160 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37d0"), "dispatching_base_number" : "B02617", "date" : "1/17/2015", "active_vehicles" : 1306, "trips" : 12676 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37d1"), "dispatching_base_number" : "B02764", "date" : "1/17/2015", "active_vehicles" : 3657, "trips" : 36318 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37d2"), "dispatching_base_number" : "B02512", "date" : "1/18/2015", "active_vehicles" : 177, "trips" : 1521 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37d3"), "dispatching_base_number" : "B02598", "date" : "1/18/2015", "active_vehicles" : 869, "trips" : 9443 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37d4"), "dispatching_base_number" : "B02765", "date" : "1/18/2015", "active_vehicles" : 248, "trips" : 2287 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37d5"), "dispatching_base_number" : "B02764", "date" : "1/18/2015", "active_vehicles" : 3290, "trips" : 35182 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37d6"), "dispatching_base_number" : "B02682", "date" : "1/18/2015", "active_vehicles" : 1056, "trips" : 11161 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37d7"), "dispatching_base_number" : "B02617", "date" : "1/18/2015", "active_vehicles" : 1223, "trips" : 12879 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37d8"), "dispatching_base_number" : "B02682", "date" : "1/19/2015", "active_vehicles" : 883, "trips" : 7028 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37d9"), "dispatching_base_number" : "B02617", "date" : "1/19/2015", "active_vehicles" : 992, "trips" : 7775 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37da"), "dispatching_base_number" : "B02765", "date" : "1/19/2015", "active_vehicles" : 238, "trips" : 1568 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37db"), "dispatching_base_number" : "B02764", "date" : "1/19/2015", "active_vehicles" : 2958, "trips" : 22750 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37dc"), "dispatching_base_number" : "B02512", "date" : "1/19/2015", "active_vehicles" : 168, "trips" : 1025 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37dd"), "dispatching_base_number" : "B02598", "date" : "1/19/2015", "active_vehicles" : 706, "trips" : 5609 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37de"), "dispatching_base_number" : "B02598", "date" : "1/20/2015", "active_vehicles" : 944, "trips" : 7206 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37df"), "dispatching_base_number" : "B02682", "date" : "1/20/2015", "active_vehicles" : 1151, "trips" : 8496 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37e0"), "dispatching_base_number" : "B02512", "date" : "1/20/2015", "active_vehicles" : 221, "trips" : 1310 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37e1"), "dispatching_base_number" : "B02764", "date" : "1/20/2015", "active_vehicles" : 3654, "trips" : 26137 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37e2"), "dispatching_base_number" : "B02765", "date" : "1/20/2015", "active_vehicles" : 272, "trips" : 1608 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37e3"), "dispatching_base_number" : "B02617", "date" : "1/20/2015", "active_vehicles" : 1350, "trips" : 10015 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37e4"), "dispatching_base_number" : "B02764", "date" : "1/21/2015", "active_vehicles" : 3718, "trips" : 27344 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37e5"), "dispatching_base_number" : "B02512", "date" : "1/21/2015", "active_vehicles" : 242, "trips" : 1519 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37e6"), "dispatching_base_number" : "B02682", "date" : "1/21/2015", "active_vehicles" : 1228, "trips" : 9472 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37e7"), "dispatching_base_number" : "B02598", "date" : "1/21/2015", "active_vehicles" : 1035, "trips" : 8041 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37e8"), "dispatching_base_number" : "B02765", "date" : "1/21/2015", "active_vehicles" : 296, "trips" : 1774 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37e9"), "dispatching_base_number" : "B02617", "date" : "1/21/2015", "active_vehicles" : 1429, "trips" : 10997 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37ea"), "dispatching_base_number" : "B02617", "date" : "1/22/2015", "active_vehicles" : 1471, "trips" : 12143 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37eb"), "dispatching_base_number" : "B02764", "date" : "1/22/2015", "active_vehicles" : 3889, "trips" : 30091 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37ec"), "dispatching_base_number" : "B02512", "date" : "1/22/2015", "active_vehicles" : 246, "trips" : 1551 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37ed"), "dispatching_base_number" : "B02598", "date" : "1/22/2015", "active_vehicles" : 1071, "trips" : 9080 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37ee"), "dispatching_base_number" : "B02682", "date" : "1/22/2015", "active_vehicles" : 1295, "trips" : 10699 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37ef"), "dispatching_base_number" : "B02765", "date" : "1/22/2015", "active_vehicles" : 295, "trips" : 2038 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37f0"), "dispatching_base_number" : "B02598", "date" : "1/23/2015", "active_vehicles" : 1093, "trips" : 9343 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37f1"), "dispatching_base_number" : "B02512", "date" : "1/23/2015", "active_vehicles" : 246, "trips" : 1670 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37f2"), "dispatching_base_number" : "B02765", "date" : "1/23/2015", "active_vehicles" : 299, "trips" : 2162 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37f3"), "dispatching_base_number" : "B02764", "date" : "1/23/2015", "active_vehicles" : 4040, "trips" : 33756 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37f4"), "dispatching_base_number" : "B02617", "date" : "1/23/2015", "active_vehicles" : 1482, "trips" : 13121 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37f5"), "dispatching_base_number" : "B02682", "date" : "1/23/2015", "active_vehicles" : 1330, "trips" : 11767 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37f6"), "dispatching_base_number" : "B02598", "date" : "1/24/2015", "active_vehicles" : 945, "trips" : 10040 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37f7"), "dispatching_base_number" : "B02764", "date" : "1/24/2015", "active_vehicles" : 3652, "trips" : 39187 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37f8"), "dispatching_base_number" : "B02512", "date" : "1/24/2015", "active_vehicles" : 211, "trips" : 1608 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37f9"), "dispatching_base_number" : "B02617", "date" : "1/24/2015", "active_vehicles" : 1367, "trips" : 14143 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37fa"), "dispatching_base_number" : "B02682", "date" : "1/24/2015", "active_vehicles" : 1223, "trips" : 13355 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37fb"), "dispatching_base_number" : "B02765", "date" : "1/24/2015", "active_vehicles" : 245, "trips" : 2376 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37fc"), "dispatching_base_number" : "B02512", "date" : "1/25/2015", "active_vehicles" : 183, "trips" : 1190 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37fd"), "dispatching_base_number" : "B02764", "date" : "1/25/2015", "active_vehicles" : 3300, "trips" : 28066 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37fe"), "dispatching_base_number" : "B02765", "date" : "1/25/2015", "active_vehicles" : 226, "trips" : 1755 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe37ff"), "dispatching_base_number" : "B02598", "date" : "1/25/2015", "active_vehicles" : 829, "trips" : 7219 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3800"), "dispatching_base_number" : "B02682", "date" : "1/25/2015", "active_vehicles" : 1046, "trips" : 9303 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3801"), "dispatching_base_number" : "B02617", "date" : "1/25/2015", "active_vehicles" : 1203, "trips" : 10362 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3802"), "dispatching_base_number" : "B02617", "date" : "1/26/2015", "active_vehicles" : 1150, "trips" : 7608 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3803"), "dispatching_base_number" : "B02598", "date" : "1/26/2015", "active_vehicles" : 860, "trips" : 5919 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3804"), "dispatching_base_number" : "B02765", "date" : "1/26/2015", "active_vehicles" : 230, "trips" : 1363 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3805"), "dispatching_base_number" : "B02764", "date" : "1/26/2015", "active_vehicles" : 3012, "trips" : 19940 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3806"), "dispatching_base_number" : "B02682", "date" : "1/26/2015", "active_vehicles" : 1084, "trips" : 7565 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3807"), "dispatching_base_number" : "B02512", "date" : "1/26/2015", "active_vehicles" : 197, "trips" : 1000 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3808"), "dispatching_base_number" : "B02682", "date" : "1/27/2015", "active_vehicles" : 600, "trips" : 4414 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3809"), "dispatching_base_number" : "B02765", "date" : "1/27/2015", "active_vehicles" : 135, "trips" : 921 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe380a"), "dispatching_base_number" : "B02617", "date" : "1/27/2015", "active_vehicles" : 596, "trips" : 4325 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe380b"), "dispatching_base_number" : "B02598", "date" : "1/27/2015", "active_vehicles" : 434, "trips" : 2957 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe380c"), "dispatching_base_number" : "B02512", "date" : "1/27/2015", "active_vehicles" : 112, "trips" : 629 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe380d"), "dispatching_base_number" : "B02764", "date" : "1/27/2015", "active_vehicles" : 1619, "trips" : 11998 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe380e"), "dispatching_base_number" : "B02764", "date" : "1/28/2015", "active_vehicles" : 3692, "trips" : 28137 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe380f"), "dispatching_base_number" : "B02682", "date" : "1/28/2015", "active_vehicles" : 1235, "trips" : 10025 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3810"), "dispatching_base_number" : "B02765", "date" : "1/28/2015", "active_vehicles" : 286, "trips" : 1913 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3811"), "dispatching_base_number" : "B02617", "date" : "1/28/2015", "active_vehicles" : 1356, "trips" : 10862 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3812"), "dispatching_base_number" : "B02598", "date" : "1/28/2015", "active_vehicles" : 1011, "trips" : 8071 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3813"), "dispatching_base_number" : "B02512", "date" : "1/28/2015", "active_vehicles" : 235, "trips" : 1438 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3814"), "dispatching_base_number" : "B02617", "date" : "1/29/2015", "active_vehicles" : 1474, "trips" : 12600 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3815"), "dispatching_base_number" : "B02764", "date" : "1/29/2015", "active_vehicles" : 3959, "trips" : 31637 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3816"), "dispatching_base_number" : "B02682", "date" : "1/29/2015", "active_vehicles" : 1316, "trips" : 11485 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3817"), "dispatching_base_number" : "B02765", "date" : "1/29/2015", "active_vehicles" : 295, "trips" : 2086 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3818"), "dispatching_base_number" : "B02512", "date" : "1/29/2015", "active_vehicles" : 250, "trips" : 1687 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3819"), "dispatching_base_number" : "B02598", "date" : "1/29/2015", "active_vehicles" : 1082, "trips" : 9499 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe381a"), "dispatching_base_number" : "B02512", "date" : "1/30/2015", "active_vehicles" : 256, "trips" : 2016 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe381b"), "dispatching_base_number" : "B02617", "date" : "1/30/2015", "active_vehicles" : 1501, "trips" : 14793 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe381c"), "dispatching_base_number" : "B02682", "date" : "1/30/2015", "active_vehicles" : 1384, "trips" : 13852 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe381d"), "dispatching_base_number" : "B02764", "date" : "1/30/2015", "active_vehicles" : 4124, "trips" : 39110 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe381e"), "dispatching_base_number" : "B02765", "date" : "1/30/2015", "active_vehicles" : 322, "trips" : 2785 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe381f"), "dispatching_base_number" : "B02598", "date" : "1/30/2015", "active_vehicles" : 1106, "trips" : 11167 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3820"), "dispatching_base_number" : "B02765", "date" : "1/31/2015", "active_vehicles" : 309, "trips" : 3282 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3821"), "dispatching_base_number" : "B02512", "date" : "1/31/2015", "active_vehicles" : 225, "trips" : 1892 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3822"), "dispatching_base_number" : "B02617", "date" : "1/31/2015", "active_vehicles" : 1394, "trips" : 15756 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3823"), "dispatching_base_number" : "B02682", "date" : "1/31/2015", "active_vehicles" : 1321, "trips" : 15388 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3824"), "dispatching_base_number" : "B02764", "date" : "1/31/2015", "active_vehicles" : 3947, "trips" : 44297 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3825"), "dispatching_base_number" : "B02598", "date" : "1/31/2015", "active_vehicles" : 1027, "trips" : 11642 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3826"), "dispatching_base_number" : "B02598", "date" : "2/1/2015", "active_vehicles" : 961, "trips" : 9499 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3827"), "dispatching_base_number" : "B02682", "date" : "2/1/2015", "active_vehicles" : 1214, "trips" : 12436 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3828"), "dispatching_base_number" : "B02512", "date" : "2/1/2015", "active_vehicles" : 193, "trips" : 1377 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3829"), "dispatching_base_number" : "B02765", "date" : "2/1/2015", "active_vehicles" : 289, "trips" : 2672 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe382a"), "dispatching_base_number" : "B02617", "date" : "2/1/2015", "active_vehicles" : 1355, "trips" : 13458 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe382b"), "dispatching_base_number" : "B02764", "date" : "2/1/2015", "active_vehicles" : 3740, "trips" : 37468 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe382c"), "dispatching_base_number" : "B02617", "date" : "2/2/2015", "active_vehicles" : 1217, "trips" : 12216 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe382d"), "dispatching_base_number" : "B02682", "date" : "2/2/2015", "active_vehicles" : 1152, "trips" : 11981 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe382e"), "dispatching_base_number" : "B02765", "date" : "2/2/2015", "active_vehicles" : 275, "trips" : 2607 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe382f"), "dispatching_base_number" : "B02598", "date" : "2/2/2015", "active_vehicles" : 939, "trips" : 9511 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3830"), "dispatching_base_number" : "B02764", "date" : "2/2/2015", "active_vehicles" : 3270, "trips" : 30761 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3831"), "dispatching_base_number" : "B02512", "date" : "2/2/2015", "active_vehicles" : 227, "trips" : 1904 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3832"), "dispatching_base_number" : "B02765", "date" : "2/3/2015", "active_vehicles" : 299, "trips" : 2410 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3833"), "dispatching_base_number" : "B02598", "date" : "2/3/2015", "active_vehicles" : 991, "trips" : 9602 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3834"), "dispatching_base_number" : "B02512", "date" : "2/3/2015", "active_vehicles" : 257, "trips" : 1915 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3835"), "dispatching_base_number" : "B02764", "date" : "2/3/2015", "active_vehicles" : 3674, "trips" : 31641 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3836"), "dispatching_base_number" : "B02617", "date" : "2/3/2015", "active_vehicles" : 1350, "trips" : 12665 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3837"), "dispatching_base_number" : "B02682", "date" : "2/3/2015", "active_vehicles" : 1269, "trips" : 11955 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3838"), "dispatching_base_number" : "B02764", "date" : "2/4/2015", "active_vehicles" : 3856, "trips" : 29994 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3839"), "dispatching_base_number" : "B02765", "date" : "2/4/2015", "active_vehicles" : 309, "trips" : 2334 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe383a"), "dispatching_base_number" : "B02512", "date" : "2/4/2015", "active_vehicles" : 244, "trips" : 1639 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe383b"), "dispatching_base_number" : "B02682", "date" : "2/4/2015", "active_vehicles" : 1311, "trips" : 11309 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe383c"), "dispatching_base_number" : "B02617", "date" : "2/4/2015", "active_vehicles" : 1393, "trips" : 11959 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe383d"), "dispatching_base_number" : "B02598", "date" : "2/4/2015", "active_vehicles" : 1072, "trips" : 9600 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe383e"), "dispatching_base_number" : "B02617", "date" : "2/5/2015", "active_vehicles" : 1524, "trips" : 14499 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe383f"), "dispatching_base_number" : "B02682", "date" : "2/5/2015", "active_vehicles" : 1418, "trips" : 13782 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3840"), "dispatching_base_number" : "B02598", "date" : "2/5/2015", "active_vehicles" : 1179, "trips" : 11609 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3841"), "dispatching_base_number" : "B02512", "date" : "2/5/2015", "active_vehicles" : 264, "trips" : 2022 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3842"), "dispatching_base_number" : "B02765", "date" : "2/5/2015", "active_vehicles" : 355, "trips" : 3011 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3843"), "dispatching_base_number" : "B02764", "date" : "2/5/2015", "active_vehicles" : 4093, "trips" : 35990 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3844"), "dispatching_base_number" : "B02617", "date" : "2/6/2015", "active_vehicles" : 1526, "trips" : 15417 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3845"), "dispatching_base_number" : "B02765", "date" : "2/6/2015", "active_vehicles" : 385, "trips" : 3569 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3846"), "dispatching_base_number" : "B02598", "date" : "2/6/2015", "active_vehicles" : 1181, "trips" : 11897 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3847"), "dispatching_base_number" : "B02512", "date" : "2/6/2015", "active_vehicles" : 261, "trips" : 1989 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3848"), "dispatching_base_number" : "B02764", "date" : "2/6/2015", "active_vehicles" : 4170, "trips" : 38693 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3849"), "dispatching_base_number" : "B02682", "date" : "2/6/2015", "active_vehicles" : 1414, "trips" : 14375 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe384a"), "dispatching_base_number" : "B02598", "date" : "2/7/2015", "active_vehicles" : 1031, "trips" : 10512 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe384b"), "dispatching_base_number" : "B02512", "date" : "2/7/2015", "active_vehicles" : 211, "trips" : 1504 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe384c"), "dispatching_base_number" : "B02617", "date" : "2/7/2015", "active_vehicles" : 1383, "trips" : 13688 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe384d"), "dispatching_base_number" : "B02682", "date" : "2/7/2015", "active_vehicles" : 1300, "trips" : 13450 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe384e"), "dispatching_base_number" : "B02764", "date" : "2/7/2015", "active_vehicles" : 3849, "trips" : 38530 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe384f"), "dispatching_base_number" : "B02765", "date" : "2/7/2015", "active_vehicles" : 345, "trips" : 3473 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3850"), "dispatching_base_number" : "B02764", "date" : "2/8/2015", "active_vehicles" : 3422, "trips" : 29692 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3851"), "dispatching_base_number" : "B02765", "date" : "2/8/2015", "active_vehicles" : 313, "trips" : 2623 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3852"), "dispatching_base_number" : "B02598", "date" : "2/8/2015", "active_vehicles" : 923, "trips" : 8129 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3853"), "dispatching_base_number" : "B02617", "date" : "2/8/2015", "active_vehicles" : 1256, "trips" : 11004 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3854"), "dispatching_base_number" : "B02682", "date" : "2/8/2015", "active_vehicles" : 1136, "trips" : 10356 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3855"), "dispatching_base_number" : "B02512", "date" : "2/8/2015", "active_vehicles" : 176, "trips" : 1196 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3856"), "dispatching_base_number" : "B02617", "date" : "2/9/2015", "active_vehicles" : 1312, "trips" : 10887 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3857"), "dispatching_base_number" : "B02682", "date" : "2/9/2015", "active_vehicles" : 1241, "trips" : 10209 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3858"), "dispatching_base_number" : "B02598", "date" : "2/9/2015", "active_vehicles" : 976, "trips" : 8135 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3859"), "dispatching_base_number" : "B02764", "date" : "2/9/2015", "active_vehicles" : 3543, "trips" : 28266 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe385a"), "dispatching_base_number" : "B02512", "date" : "2/9/2015", "active_vehicles" : 228, "trips" : 1565 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe385b"), "dispatching_base_number" : "B02765", "date" : "2/9/2015", "active_vehicles" : 388, "trips" : 2894 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe385c"), "dispatching_base_number" : "B02764", "date" : "2/10/2015", "active_vehicles" : 3700, "trips" : 29124 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe385d"), "dispatching_base_number" : "B02512", "date" : "2/10/2015", "active_vehicles" : 233, "trips" : 1555 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe385e"), "dispatching_base_number" : "B02617", "date" : "2/10/2015", "active_vehicles" : 1364, "trips" : 11401 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe385f"), "dispatching_base_number" : "B02765", "date" : "2/10/2015", "active_vehicles" : 422, "trips" : 3432 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3860"), "dispatching_base_number" : "B02682", "date" : "2/10/2015", "active_vehicles" : 1281, "trips" : 10536 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3861"), "dispatching_base_number" : "B02598", "date" : "2/10/2015", "active_vehicles" : 1029, "trips" : 8718 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3862"), "dispatching_base_number" : "B02617", "date" : "2/11/2015", "active_vehicles" : 1450, "trips" : 12749 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3863"), "dispatching_base_number" : "B02764", "date" : "2/11/2015", "active_vehicles" : 3849, "trips" : 31889 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3864"), "dispatching_base_number" : "B02512", "date" : "2/11/2015", "active_vehicles" : 255, "trips" : 1831 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3865"), "dispatching_base_number" : "B02598", "date" : "2/11/2015", "active_vehicles" : 1115, "trips" : 10034 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3866"), "dispatching_base_number" : "B02765", "date" : "2/11/2015", "active_vehicles" : 450, "trips" : 3778 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3867"), "dispatching_base_number" : "B02682", "date" : "2/11/2015", "active_vehicles" : 1396, "trips" : 12189 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3868"), "dispatching_base_number" : "B02617", "date" : "2/12/2015", "active_vehicles" : 1532, "trips" : 14263 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3869"), "dispatching_base_number" : "B02512", "date" : "2/12/2015", "active_vehicles" : 269, "trips" : 2092 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe386a"), "dispatching_base_number" : "B02682", "date" : "2/12/2015", "active_vehicles" : 1468, "trips" : 13786 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe386b"), "dispatching_base_number" : "B02765", "date" : "2/12/2015", "active_vehicles" : 536, "trips" : 4609 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe386c"), "dispatching_base_number" : "B02598", "date" : "2/12/2015", "active_vehicles" : 1181, "trips" : 11640 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe386d"), "dispatching_base_number" : "B02764", "date" : "2/12/2015", "active_vehicles" : 4137, "trips" : 36844 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe386e"), "dispatching_base_number" : "B02617", "date" : "2/13/2015", "active_vehicles" : 1590, "trips" : 16996 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe386f"), "dispatching_base_number" : "B02682", "date" : "2/13/2015", "active_vehicles" : 1523, "trips" : 16088 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3870"), "dispatching_base_number" : "B02764", "date" : "2/13/2015", "active_vehicles" : 4395, "trips" : 43561 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3871"), "dispatching_base_number" : "B02765", "date" : "2/13/2015", "active_vehicles" : 599, "trips" : 5909 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3872"), "dispatching_base_number" : "B02512", "date" : "2/13/2015", "active_vehicles" : 281, "trips" : 2408 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3873"), "dispatching_base_number" : "B02598", "date" : "2/13/2015", "active_vehicles" : 1216, "trips" : 13062 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3874"), "dispatching_base_number" : "B02764", "date" : "2/14/2015", "active_vehicles" : 4129, "trips" : 45858 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3875"), "dispatching_base_number" : "B02512", "date" : "2/14/2015", "active_vehicles" : 236, "trips" : 2055 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3876"), "dispatching_base_number" : "B02598", "date" : "2/14/2015", "active_vehicles" : 1111, "trips" : 12678 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3877"), "dispatching_base_number" : "B02765", "date" : "2/14/2015", "active_vehicles" : 583, "trips" : 6307 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3878"), "dispatching_base_number" : "B02617", "date" : "2/14/2015", "active_vehicles" : 1486, "trips" : 16999 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3879"), "dispatching_base_number" : "B02682", "date" : "2/14/2015", "active_vehicles" : 1428, "trips" : 16448 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe387a"), "dispatching_base_number" : "B02682", "date" : "2/15/2015", "active_vehicles" : 1261, "trips" : 14517 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe387b"), "dispatching_base_number" : "B02764", "date" : "2/15/2015", "active_vehicles" : 3651, "trips" : 41209 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe387c"), "dispatching_base_number" : "B02617", "date" : "2/15/2015", "active_vehicles" : 1293, "trips" : 14662 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe387d"), "dispatching_base_number" : "B02765", "date" : "2/15/2015", "active_vehicles" : 521, "trips" : 5500 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe387e"), "dispatching_base_number" : "B02512", "date" : "2/15/2015", "active_vehicles" : 210, "trips" : 1996 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe387f"), "dispatching_base_number" : "B02598", "date" : "2/15/2015", "active_vehicles" : 1003, "trips" : 11517 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3880"), "dispatching_base_number" : "B02598", "date" : "2/16/2015", "active_vehicles" : 934, "trips" : 9052 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3881"), "dispatching_base_number" : "B02512", "date" : "2/16/2015", "active_vehicles" : 207, "trips" : 1576 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3882"), "dispatching_base_number" : "B02617", "date" : "2/16/2015", "active_vehicles" : 1214, "trips" : 11824 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3883"), "dispatching_base_number" : "B02764", "date" : "2/16/2015", "active_vehicles" : 3524, "trips" : 33448 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3884"), "dispatching_base_number" : "B02682", "date" : "2/16/2015", "active_vehicles" : 1164, "trips" : 11323 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3885"), "dispatching_base_number" : "B02765", "date" : "2/16/2015", "active_vehicles" : 508, "trips" : 4875 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3886"), "dispatching_base_number" : "B02764", "date" : "2/17/2015", "active_vehicles" : 3826, "trips" : 32473 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3887"), "dispatching_base_number" : "B02512", "date" : "2/17/2015", "active_vehicles" : 241, "trips" : 1797 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3888"), "dispatching_base_number" : "B02682", "date" : "2/17/2015", "active_vehicles" : 1314, "trips" : 11887 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3889"), "dispatching_base_number" : "B02617", "date" : "2/17/2015", "active_vehicles" : 1378, "trips" : 12524 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe388a"), "dispatching_base_number" : "B02598", "date" : "2/17/2015", "active_vehicles" : 1066, "trips" : 9463 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe388b"), "dispatching_base_number" : "B02765", "date" : "2/17/2015", "active_vehicles" : 578, "trips" : 4907 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe388c"), "dispatching_base_number" : "B02598", "date" : "2/18/2015", "active_vehicles" : 1078, "trips" : 9538 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe388d"), "dispatching_base_number" : "B02682", "date" : "2/18/2015", "active_vehicles" : 1314, "trips" : 11724 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe388e"), "dispatching_base_number" : "B02617", "date" : "2/18/2015", "active_vehicles" : 1394, "trips" : 12016 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe388f"), "dispatching_base_number" : "B02765", "date" : "2/18/2015", "active_vehicles" : 586, "trips" : 5059 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3890"), "dispatching_base_number" : "B02764", "date" : "2/18/2015", "active_vehicles" : 3842, "trips" : 32317 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3891"), "dispatching_base_number" : "B02512", "date" : "2/18/2015", "active_vehicles" : 228, "trips" : 1589 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3892"), "dispatching_base_number" : "B02598", "date" : "2/19/2015", "active_vehicles" : 1127, "trips" : 11739 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3893"), "dispatching_base_number" : "B02512", "date" : "2/19/2015", "active_vehicles" : 250, "trips" : 2120 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3894"), "dispatching_base_number" : "B02682", "date" : "2/19/2015", "active_vehicles" : 1428, "trips" : 14591 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3895"), "dispatching_base_number" : "B02764", "date" : "2/19/2015", "active_vehicles" : 4110, "trips" : 39110 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3896"), "dispatching_base_number" : "B02765", "date" : "2/19/2015", "active_vehicles" : 663, "trips" : 6447 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3897"), "dispatching_base_number" : "B02617", "date" : "2/19/2015", "active_vehicles" : 1452, "trips" : 14750 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3898"), "dispatching_base_number" : "B02764", "date" : "2/20/2015", "active_vehicles" : 4384, "trips" : 44755 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe3899"), "dispatching_base_number" : "B02617", "date" : "2/20/2015", "active_vehicles" : 1574, "trips" : 16856 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe389a"), "dispatching_base_number" : "B02598", "date" : "2/20/2015", "active_vehicles" : 1186, "trips" : 12758 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe389b"), "dispatching_base_number" : "B02682", "date" : "2/20/2015", "active_vehicles" : 1497, "trips" : 16342 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe389c"), "dispatching_base_number" : "B02765", "date" : "2/20/2015", "active_vehicles" : 736, "trips" : 7824 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe389d"), "dispatching_base_number" : "B02512", "date" : "2/20/2015", "active_vehicles" : 272, "trips" : 2380 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe389e"), "dispatching_base_number" : "B02598", "date" : "2/21/2015", "active_vehicles" : 1044, "trips" : 12132 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe389f"), "dispatching_base_number" : "B02682", "date" : "2/21/2015", "active_vehicles" : 1374, "trips" : 16149 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38a0"), "dispatching_base_number" : "B02765", "date" : "2/21/2015", "active_vehicles" : 685, "trips" : 7658 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38a1"), "dispatching_base_number" : "B02617", "date" : "2/21/2015", "active_vehicles" : 1443, "trips" : 16098 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38a2"), "dispatching_base_number" : "B02512", "date" : "2/21/2015", "active_vehicles" : 238, "trips" : 2149 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38a3"), "dispatching_base_number" : "B02764", "date" : "2/21/2015", "active_vehicles" : 3981, "trips" : 44194 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38a4"), "dispatching_base_number" : "B02512", "date" : "2/22/2015", "active_vehicles" : 199, "trips" : 1312 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38a5"), "dispatching_base_number" : "B02617", "date" : "2/22/2015", "active_vehicles" : 1248, "trips" : 10696 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38a6"), "dispatching_base_number" : "B02682", "date" : "2/22/2015", "active_vehicles" : 1220, "trips" : 10970 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38a7"), "dispatching_base_number" : "B02764", "date" : "2/22/2015", "active_vehicles" : 3478, "trips" : 30157 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38a8"), "dispatching_base_number" : "B02598", "date" : "2/22/2015", "active_vehicles" : 909, "trips" : 8271 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38a9"), "dispatching_base_number" : "B02765", "date" : "2/22/2015", "active_vehicles" : 566, "trips" : 5034 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38aa"), "dispatching_base_number" : "B02598", "date" : "2/23/2015", "active_vehicles" : 966, "trips" : 8943 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38ab"), "dispatching_base_number" : "B02617", "date" : "2/23/2015", "active_vehicles" : 1332, "trips" : 11720 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38ac"), "dispatching_base_number" : "B02764", "date" : "2/23/2015", "active_vehicles" : 3734, "trips" : 31173 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38ad"), "dispatching_base_number" : "B02682", "date" : "2/23/2015", "active_vehicles" : 1262, "trips" : 11714 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38ae"), "dispatching_base_number" : "B02765", "date" : "2/23/2015", "active_vehicles" : 665, "trips" : 5823 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38af"), "dispatching_base_number" : "B02512", "date" : "2/23/2015", "active_vehicles" : 238, "trips" : 1844 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38b0"), "dispatching_base_number" : "B02764", "date" : "2/24/2015", "active_vehicles" : 3965, "trips" : 34686 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38b1"), "dispatching_base_number" : "B02512", "date" : "2/24/2015", "active_vehicles" : 247, "trips" : 1869 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38b2"), "dispatching_base_number" : "B02598", "date" : "2/24/2015", "active_vehicles" : 1061, "trips" : 9954 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38b3"), "dispatching_base_number" : "B02682", "date" : "2/24/2015", "active_vehicles" : 1346, "trips" : 12497 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38b4"), "dispatching_base_number" : "B02617", "date" : "2/24/2015", "active_vehicles" : 1456, "trips" : 13719 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38b5"), "dispatching_base_number" : "B02765", "date" : "2/24/2015", "active_vehicles" : 698, "trips" : 6390 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38b6"), "dispatching_base_number" : "B02512", "date" : "2/25/2015", "active_vehicles" : 246, "trips" : 1647 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38b7"), "dispatching_base_number" : "B02598", "date" : "2/25/2015", "active_vehicles" : 1076, "trips" : 9405 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38b8"), "dispatching_base_number" : "B02765", "date" : "2/25/2015", "active_vehicles" : 706, "trips" : 6178 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38b9"), "dispatching_base_number" : "B02682", "date" : "2/25/2015", "active_vehicles" : 1395, "trips" : 12693 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38ba"), "dispatching_base_number" : "B02617", "date" : "2/25/2015", "active_vehicles" : 1473, "trips" : 12811 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38bb"), "dispatching_base_number" : "B02764", "date" : "2/25/2015", "active_vehicles" : 3934, "trips" : 31957 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38bc"), "dispatching_base_number" : "B02598", "date" : "2/26/2015", "active_vehicles" : 1134, "trips" : 10661 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38bd"), "dispatching_base_number" : "B02617", "date" : "2/26/2015", "active_vehicles" : 1539, "trips" : 14461 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38be"), "dispatching_base_number" : "B02682", "date" : "2/26/2015", "active_vehicles" : 1465, "trips" : 13814 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38bf"), "dispatching_base_number" : "B02512", "date" : "2/26/2015", "active_vehicles" : 243, "trips" : 1797 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38c0"), "dispatching_base_number" : "B02765", "date" : "2/26/2015", "active_vehicles" : 745, "trips" : 6744 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38c1"), "dispatching_base_number" : "B02764", "date" : "2/26/2015", "active_vehicles" : 4101, "trips" : 36091 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38c2"), "dispatching_base_number" : "B02765", "date" : "2/27/2015", "active_vehicles" : 786, "trips" : 7563 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38c3"), "dispatching_base_number" : "B02617", "date" : "2/27/2015", "active_vehicles" : 1551, "trips" : 14677 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38c4"), "dispatching_base_number" : "B02598", "date" : "2/27/2015", "active_vehicles" : 1114, "trips" : 10755 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38c5"), "dispatching_base_number" : "B02512", "date" : "2/27/2015", "active_vehicles" : 272, "trips" : 2056 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38c6"), "dispatching_base_number" : "B02764", "date" : "2/27/2015", "active_vehicles" : 4253, "trips" : 38780 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38c7"), "dispatching_base_number" : "B02682", "date" : "2/27/2015", "active_vehicles" : 1510, "trips" : 14975 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38c8"), "dispatching_base_number" : "B02598", "date" : "2/28/2015", "active_vehicles" : 994, "trips" : 10319 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38c9"), "dispatching_base_number" : "B02764", "date" : "2/28/2015", "active_vehicles" : 3952, "trips" : 39812 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38ca"), "dispatching_base_number" : "B02617", "date" : "2/28/2015", "active_vehicles" : 1372, "trips" : 14022 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38cb"), "dispatching_base_number" : "B02682", "date" : "2/28/2015", "active_vehicles" : 1386, "trips" : 14472 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38cc"), "dispatching_base_number" : "B02512", "date" : "2/28/2015", "active_vehicles" : 230, "trips" : 1803 }</br>
{ "_id" : ObjectId("6284915b0fbdf92118fe38cd"), "dispatching_base_number" : "B02765", "date" : "2/28/2015", "active_vehicles" : 747, "trips" : 7753 }</br>
```

> db.pickups.insert({"dispatching_base_number" : "B02765", "date" : "3/1/2015", "active_vehicles" : 777, "trips" : 7000});</br>
```
WriteResult({ "nInserted" : 1 })
```
> db.pickups.insert([{"dispatching_base_number" : "B02598", "date" : "3/1/2015", "active_vehicles" : 500, "trips" : 5000},</br>
>   {"dispatching_base_number" : "B02764", "date" : "3/1/2015", "active_vehicles" : 600, "trips" : 6000},</br>
>   {"dispatching_base_number" : "B02617", "date" : "3/1/2015", "active_vehicles" : 700, "trips" : 7000},</br>
>   {"dispatching_base_number" : "B02682", "date" : "3/1/2015", "active_vehicles" : 800, "trips" : 8000},</br>
>   {"dispatching_base_number" : "B02512", "date" : "3/1/2015", "active_vehicles" : 900, "trips" : 9000}]);</br>

```
BulkWriteResult({
        "writeErrors" : [ ],
        "writeConcernErrors" : [ ],
        "nInserted" : 5,
        "nUpserted" : 0,
        "nMatched" : 0,
        "nModified" : 0,
        "nRemoved" : 0,
        "upserted" : [ ]
})
```

> db.pickups.find({"date" : "3/1/2015"});</br>

```
{ "_id" : ObjectId("6284954bce4f4b7b920ca1e3"), "dispatching_base_number" : "B02765", "date" : "3/1/2015", "active_vehicles" : 777, "trips" : 7000 }</br>
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e4"), "dispatching_base_number" : "B02598", "date" : "3/1/2015", "active_vehicles" : 500, "trips" : 5000 }</br>
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e5"), "dispatching_base_number" : "B02764", "date" : "3/1/2015", "active_vehicles" : 600, "trips" : 6000 }</br>
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e6"), "dispatching_base_number" : "B02617", "date" : "3/1/2015", "active_vehicles" : 700, "trips" : 7000 }</br>
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e7"), "dispatching_base_number" : "B02682", "date" : "3/1/2015", "active_vehicles" : 800, "trips" : 8000 }</br>
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e8"), "dispatching_base_number" : "B02512", "date" : "3/1/2015", "active_vehicles" : 900, "trips" : 9000 }</br>
```

> db.pickups.update({"dispatching_base_number" : "B02765", "date" : "3/1/2015"},{$set:{"active_vehicles" : 400, "trips" : 4000}});</br>
```
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })</br>
```
> db.pickups.find({"date" : "3/1/2015"});</br>

```
{ "_id" : ObjectId("6284954bce4f4b7b920ca1e3"), "dispatching_base_number" : "B02765", "date" : "3/1/2015", "active_vehicles" : 400, "trips" : 4000 }</br>
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e4"), "dispatching_base_number" : "B02598", "date" : "3/1/2015", "active_vehicles" : 500, "trips" : 5000 }</br>
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e5"), "dispatching_base_number" : "B02764", "date" : "3/1/2015", "active_vehicles" : 600, "trips" : 6000 }</br>
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e6"), "dispatching_base_number" : "B02617", "date" : "3/1/2015", "active_vehicles" : 700, "trips" : 7000 }</br>
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e7"), "dispatching_base_number" : "B02682", "date" : "3/1/2015", "active_vehicles" : 800, "trips" : 8000 }</br>
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e8"), "dispatching_base_number" : "B02512", "date" : "3/1/2015", "active_vehicles" : 900, "trips" : 9000 }</br>
```

#### Total trips in February
> db.pickups.aggregate([{$match: {"date":{$gte:"2/1/2015", $lt:"3/1/2015"}}}, {$group: {_id:"$dispatching_base_number", totalTrips: {$sum:"$trips"}}}]);</br>

```
{ "_id" : "B02682", "totalTrips" : 366568 }</br>
{ "_id" : "B02617", "totalTrips" : 379037 }</br>
{ "_id" : "B02512", "totalTrips" : 50987 }</br>
{ "_id" : "B02765", "totalTrips" : 137383 }</br>
{ "_id" : "B02764", "totalTrips" : 998473 }</br>
{ "_id" : "B02598", "totalTrips" : 289133 }</br>
```

## Indexes
### Before
> db.pickups.explain().aggregate([{$match: {"date":{$gte:"2/1/2015", $lt:"3/1/2015"}}}, {$group: {_id:"$dispatching_base_number", totalTrips: {$sum:"$trips"}}}]);</br>

        "explainVersion" : "1",
        "stages" : [
                {
                        "$cursor" : {
                                "queryPlanner" : {
                                        "namespace" : "uber.pickups",
                                        "indexFilterSet" : false,
                                        "parsedQuery" : {
                                                "$and" : [
                                                        {
                                                                "date" : {
                                                                        "$lt" : "3/1/2015"
                                                                }
                                                        },
                                                        {
                                                                "date" : {
                                                                        "$gte" : "2/1/2015"
                                                                }
                                                        }
                                                ]
                                        },
                                        "queryHash" : "EC006CAD",
                                        "planCacheKey" : "BB4FB5E3",
                                        "maxIndexedOrSolutionsReached" : false,
                                        "maxIndexedAndSolutionsReached" : false,
                                        "maxScansToExplodeReached" : false,
                                        "winningPlan" : {
                                                "stage" : "PROJECTION_SIMPLE",
                                                "transformBy" : {
                                                        "dispatching_base_number" : 1,
                                                        "trips" : 1,
                                                        "_id" : 0
                                                },
                                                "inputStage" : {
                                                        "stage" : "COLLSCAN",
                                                        "filter" : {
                                                                "$and" : [
                                                                        {
                                                                                "date" : {
                                                                                        "$lt" : "3/1/2015"
                                                                                }
                                                                        },
                                                                        {
                                                                                "date" : {
                                                                                        "$gte" : "2/1/2015"
                                                                                }
                                                                        }
                                                                ]
                                                        },
                                                        "direction" : "forward"
                                                }
                                        },
                                        "rejectedPlans" : [ ]
                                }
                        }
                },
                {
                        "$group" : {
                                "_id" : "$dispatching_base_number",
                                "totalTrips" : {
                                        "$sum" : "$trips"
                                }
                        }
                }
        ],
        "serverInfo" : {
                "host" : "mongodb1",
                "port" : 27017,
                "version" : "5.0.8",
                "gitVersion" : "c87e1c23421bf79614baf500fda6622bd90f674e"
        },
        "serverParameters" : {
                "internalQueryFacetBufferSizeBytes" : 104857600,
                "internalQueryFacetMaxOutputDocSizeBytes" : 104857600,
                "internalLookupStageIntermediateDocumentMaxSizeBytes" : 104857600,
                "internalDocumentSourceGroupMaxMemoryBytes" : 104857600,
                "internalQueryMaxBlockingSortMemoryUsageBytes" : 104857600,
                "internalQueryProhibitBlockingMergeOnMongoS" : 0,
                "internalQueryMaxAddToSetBytes" : 104857600,
                "internalDocumentSourceSetWindowFieldsMaxMemoryBytes" : 104857600
        },
        "command" : {
                "aggregate" : "pickups",
                "pipeline" : [
                        {
                                "$match" : {
                                        "date" : {
                                                "$gte" : "2/1/2015",
                                                "$lt" : "3/1/2015"
                                        }
                                }
                        },
                        {
                                "$group" : {
                                        "_id" : "$dispatching_base_number",
                                        "totalTrips" : {
                                                "$sum" : "$trips"
                                        }
                                }
                        }
                ],
                "explain" : true,
                "cursor" : {

                },
                "lsid" : {
                        "id" : UUID("d2162d37-9f6e-4c40-8973-72769e6dc321")
                },
                "$db" : "uber"
        },
        "ok" : 1
}

### After
> db.pickups.createIndex({date: 1});
```
{
        "numIndexesBefore" : 1,
        "numIndexesAfter" : 2,
        "createdCollectionAutomatically" : false,
        "ok" : 1
```

> db.pickups.explain().aggregate([{$match: {"date":{$gte:"2/1/2015", $lt:"3/1/2015"}}}, {$group: {_id:"$dispatching_base_number", totalTrips: {$sum:"$trips"}}}]);

        "explainVersion" : "1",
        "stages" : [
                {
                        "$cursor" : {
                                "queryPlanner" : {
                                        "namespace" : "uber.pickups",
                                        "indexFilterSet" : false,
                                        "parsedQuery" : {
                                                "$and" : [
                                                        {
                                                                "date" : {
                                                                        "$lt" : "3/1/2015"
                                                                }
                                                        },
                                                        {
                                                                "date" : {
                                                                        "$gte" : "2/1/2015"
                                                                }
                                                        }
                                                ]
                                        },
                                        "queryHash" : "EC006CAD",
                                        "planCacheKey" : "C6F40395",
                                        "maxIndexedOrSolutionsReached" : false,
                                        "maxIndexedAndSolutionsReached" : false,
                                        "maxScansToExplodeReached" : false,
                                        "winningPlan" : {
                                                "stage" : "PROJECTION_SIMPLE",
                                                "transformBy" : {
                                                        "dispatching_base_number" : 1,
                                                        "trips" : 1,
                                                        "_id" : 0
                                                },
                                                "inputStage" : {
                                                        "stage" : "FETCH",
                                                        "inputStage" : {
                                                                "stage" : "IXSCAN",
                                                                "keyPattern" : {
                                                                        "date" : 1
                                                                },
                                                                "indexName" : "date_1",
                                                                "isMultiKey" : false,
                                                                "multiKeyPaths" : {
                                                                        "date" : [ ]
                                                                },
                                                                "isUnique" : false,
                                                                "isSparse" : false,
                                                                "isPartial" : false,
                                                                "indexVersion" : 2,
                                                                "direction" : "forward",
                                                                "indexBounds" : {
                                                                        "date" : [
                                                                                "[\"2/1/2015\", \"3/1/2015\")"
                                                                        ]
                                                                }
                                                        }
                                                }
                                        },
                                        "rejectedPlans" : [ ]
                                }
                        }
                },
                {
                        "$group" : {
                                "_id" : "$dispatching_base_number",
                                "totalTrips" : {
                                        "$sum" : "$trips"
                                }
                        }
                }
        ],
        "serverInfo" : {
                "host" : "mongodb1",
                "port" : 27017,
                "version" : "5.0.8",
                "gitVersion" : "c87e1c23421bf79614baf500fda6622bd90f674e"
        },
        "serverParameters" : {
                "internalQueryFacetBufferSizeBytes" : 104857600,
                "internalQueryFacetMaxOutputDocSizeBytes" : 104857600,
                "internalLookupStageIntermediateDocumentMaxSizeBytes" : 104857600,
                "internalDocumentSourceGroupMaxMemoryBytes" : 104857600,
                "internalQueryMaxBlockingSortMemoryUsageBytes" : 104857600,
                "internalQueryProhibitBlockingMergeOnMongoS" : 0,
                "internalQueryMaxAddToSetBytes" : 104857600,
                "internalDocumentSourceSetWindowFieldsMaxMemoryBytes" : 104857600
        },
        "command" : {
                "aggregate" : "pickups",
                "pipeline" : [
                        {
                                "$match" : {
                                        "date" : {
                                                "$gte" : "2/1/2015",
                                                "$lt" : "3/1/2015"
                                        }
                                }
                        },
                        {
                                "$group" : {
                                        "_id" : "$dispatching_base_number",
                                        "totalTrips" : {
                                                "$sum" : "$trips"
                                        }
                                }
                        }
                ],
                "explain" : true,
                "cursor" : {
                },
                "lsid" : {
                        "id" : UUID("d2162d37-9f6e-4c40-8973-72769e6dc321")
                },
                "$db" : "uber"
        },
        "ok" : 1
