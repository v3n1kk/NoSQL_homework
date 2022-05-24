##### Virtual machine: 2x CPU, 4Gb RAM, 8Gb SSD
##### OS: debian 10

### Установка и настройка пакетов

Установка и сборка кластера couchbase будет производиться в docker. Для этого выполним установку необходимых пакетов
```
apt install docker-compose docker
```

После создадим каталоги для каждой ноды:
```
mkdir /var/lib/couchbase
mkdir /var/lib/couchbase/node1
mkdir /var/lib/couchbase/node2
mkdir /var/lib/couchbase/node3
```
Создадим каталог и подготовим файл образа. Инстансы couchbase будут подняты на портах 8091, 8092 и 8093.
```
mkdir /app
nano /app/docker-compose.yml

couchbase1:
  image: couchbase/server
  volumes:
    - /var/lib/couchbase/node1:/opt/couchbase/var
couchbase2:
  image: couchbase/server
  volumes:
    - /var/lib/couchbase/node2:/opt/couchbase/var
couchbase3:
  image: couchbase/server
  volumes:
    - /var/lib/couchbase/node3:/opt/couchbase/var
  ports:
    - 8091:8091
    - 8092:8092
    - 8093:8093
    - 11210:11210
```

Перейдем в каталог и выполним запуск образа
```
cd /app/
docker-compose up -d

Pulling couchbase1 (couchbase/server:)...
latest: Pulling from couchbase/server
d5fd17ec1767: Pull complete
0ec4614b2a11: Pull complete
fad73e729d3e: Pull complete
5de446c843e8: Pull complete
fb61c5eb7042: Pull complete
4cd9a77acd6b: Pull complete
6fc3779a93cc: Pull complete
c263783ee802: Pull complete
c5c6f0f5243f: Pull complete
4f4fb700ef54: Pull complete
c7fc78a311a0: Pull complete
Digest: sha256:735f304cb1ae94314e8a34aed46b4b0da74de223ab765b57745c42ad3d14b119
Status: Downloaded newer image for couchbase/server:latest
Creating app_couchbase3_1 ... done
Creating app_couchbase1_1 ... done
Creating app_couchbase2_1 ... done
```

Проверим что контейнеры запустились
```
docker-compose ps

      Name                    Command               State                                                                    Ports
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
app_couchbase1_1   /entrypoint.sh couchbase-s ...   Up      11207/tcp, 11210/tcp, 11211/tcp, 18091/tcp, 18092/tcp, 18093/tcp, 18094/tcp, 18095/tcp, 18096/tcp, 8091/tcp, 8092/tcp, 8093/tcp,
                                                            8094/tcp, 8095/tcp, 8096/tcp
app_couchbase2_1   /entrypoint.sh couchbase-s ...   Up      11207/tcp, 11210/tcp, 11211/tcp, 18091/tcp, 18092/tcp, 18093/tcp, 18094/tcp, 18095/tcp, 18096/tcp, 8091/tcp, 8092/tcp, 8093/tcp,
                                                            8094/tcp, 8095/tcp, 8096/tcp
app_couchbase3_1   /entrypoint.sh couchbase-s ...   Up      11207/tcp, 0.0.0.0:11210->11210/tcp, 11211/tcp, 18091/tcp, 18092/tcp, 18093/tcp, 18094/tcp, 18095/tcp, 18096/tcp,
                                                            0.0.0.0:8091->8091/tcp, 0.0.0.0:8092->8092/tcp, 0.0.0.0:8093->8093/tcp, 8094/tcp, 8095/tcp, 8096/tcp
```
Для сборки кластера нам понадобятся внутренние ip контейнеров docker. Их можно узнать следюущей командой:
```
docker inspect --format '{{ .NetworkSettings.IPAddress }}' app_couchbase1_1
172.17.0.4
docker inspect --format '{{ .NetworkSettings.IPAddress }}' app_couchbase2_1
172.17.0.3
docker inspect --format '{{ .NetworkSettings.IPAddress }}' app_couchbase3_1
172.17.0.2
```

### Сборка и настройка кластера 

Далее переходим к настройке кластера в браузер. Для этого необходимо перейти по адресу <host_ip>:8091. Будет открыта стартовая страница конфигуратора. Нажимаем "Setup New Cluster"
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/1.png)

Указываем имя кластера и имя пользователя/пароль для административной учетной записи
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/2.png)

Принимаем условия пользовательского соглашения и нажимаем "Configure Disk, Memory, Services"
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/3.png)

В открывшемся окне указываем адрес (желательно FQDN, но т.к. в данном примере используется docker то будем использовать ip-адрес) и квоты. На двух нодах будут располагаться только данные, но одной - сервисы аналитики, бекапы и проч
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/4.png)

Кластер создан и состоит на данный момент из 1-го узла. Добавим ноду нажав "Add Server"
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/6.png)

Указываем ip контейнера и выбираем сервис Data
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/7.png)

Далее нажимаем "Add Server" и указываем ip адрес последнего контейнера. Сервисы выбираем все из списка.
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/8.png)

Проставляем для сервисов квоты по использованию RAM
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/9.png)

После чего нажимаем "Rebalance" и ждем балансировки нод в кластере
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/10.png)

### Работа с тестовыми данными

Добавим тестовый набор данных. Для этого нужно перейти во вкладку "Buckets" и нажать на ссылку "sample bucket"
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/11.png)

В качестве тестового набора данных выберем "travel-sample" и нажмем "Load Sample Data"
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/12.png)

Снова перейдем на вкладку "Buckets" и проверим что данные появились. Также через GUI можно посмотреть какие документы и коллекции содержатся в данном bucket. 
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/13.png)

Выбрав "Scopes & Collections" посмотрим содержимое 
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/14.png)

Попробуем получить данные с помощью запроса. Для этого перейдем во вкладку "Query" и выполним простой select по scope inventory и коллекции hotel
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/15.png)

Данные также могут выводиться как в формате JSON, так и в табличном виде
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/16.png)

### Настройка autofailover

Для настройки autofailover перейдем во вкладку "Settings" и установим период автоматического переключения в 10 секунд. После чего нажмем "Save"
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/17.png)

Для проверки отказоустойчивости остановим один из контейнеров
```
docker stop app_couchbase2_1
```

По прошествию 10 секунд будет произведено автоматическое переключение о чем в GUI будет отображаться соответствующее сообщение
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/18.png)

Вышедшую из строя ноду выведем из кластера нажав "Rebalance". Кластер успешно перебалансирован.
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/19.png)

Снова запустим контейнер со второй нодой и вернем его в кластер:
```
docker start app_couchbase2_1
```

Для этого необходимо в GUI снова нажать "Add Server", указать ip-адрес ноды и выбрать необходимые сервисы
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/20.png)

Нода успешно добавлена. Для ввода в рабочее состояние необходима балансировка
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/21.png)

Нажав "Rebalance" данные на кластере были перераспределены и нода снова стала активна
![](https://github.com/v3n1kk/NoSQL_homework/blob/main/couchbase_pics/22.png)
