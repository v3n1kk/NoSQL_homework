##### Virtual machine: 2x CPU, 4Gb RAM, 8Gb SSD
##### OS: debian 10

### Установка и настройка пакетов

```
sudo apt-get install -y apt-transport-https ca-certificates dirmngr
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 8919F6BD2B48D754
echo "deb https://packages.clickhouse.com/deb stable main" | sudo tee \
    /etc/apt/sources.list.d/clickhouse.list
sudo apt-get update
sudo apt-get install -y clickhouse-server clickhouse-client
sudo service clickhouse-server start
```

### Практическая часть

Попробуем подключиться к clickhouse
```
clickhouse-client --password <password>

ClickHouse client version 22.5.1.2079 (official build).
Connecting to localhost:9000 as user default.
Connected to ClickHouse server version 22.5.1 revision 54455.

Warnings:
 * Linux is not using a fast TSC clock source. Performance can be degraded.
 * Linux transparent hugepages are set to "always".
 * Maximum number of threads is lower than 30000. There could be problems with handling a lot of simultaneous queries.
```

Clickhouse доступен. Сразу создадим тестовую БД и таблицу в ней
```
CREATE DATABASE tutorial
USE tutorial
CREATE TABLE tutorial.visits_v1
(
    `CounterID` UInt32,
    `StartDate` Date,
    `Sign` Int8,
    `IsNew` UInt8,
    `VisitID` UInt64,
    `UserID` UInt64,
    `StartTime` DateTime,
    `Duration` UInt32,
    `UTCStartTime` DateTime,
    `PageViews` Int32,
    `Hits` Int32,
    `IsBounce` UInt8,
    `Referer` String,
    `StartURL` String,
    `RefererDomain` String,
    `StartURLDomain` String,
    `EndURL` String,
    `LinkURL` String,
    `IsDownload` UInt8,
    `TraficSourceID` Int8,
    `SearchEngineID` UInt16,
    `SearchPhrase` String,
    `AdvEngineID` UInt8,
    `PlaceID` Int32,
    `RefererCategories` Array(UInt16),
    `URLCategories` Array(UInt16),
    `URLRegions` Array(UInt32),
    `RefererRegions` Array(UInt32),
    `IsYandex` UInt8,
    `GoalReachesDepth` Int32,
    `GoalReachesURL` Int32,
    `GoalReachesAny` Int32,
    `SocialSourceNetworkID` UInt8,
    `SocialSourcePage` String,
    `MobilePhoneModel` String,
    `ClientEventTime` DateTime,
    `RegionID` UInt32,
    `ClientIP` UInt32,
    `ClientIP6` FixedString(16),
    `RemoteIP` UInt32,
    `RemoteIP6` FixedString(16),
    `IPNetworkID` UInt32,
    `SilverlightVersion3` UInt32,
    `CodeVersion` UInt32,
    `ResolutionWidth` UInt16,
    `ResolutionHeight` UInt16,
    `UserAgentMajor` UInt16,
    `UserAgentMinor` UInt16,
    `WindowClientWidth` UInt16,
    `WindowClientHeight` UInt16,
    `SilverlightVersion2` UInt8,
    `SilverlightVersion4` UInt16,
    `FlashVersion3` UInt16,
    `FlashVersion4` UInt16,
    `ClientTimeZone` Int16,
    `OS` UInt8,
    `UserAgent` UInt8,
    `ResolutionDepth` UInt8,
    `FlashMajor` UInt8,
    `FlashMinor` UInt8,
    `NetMajor` UInt8,
    `NetMinor` UInt8,
    `MobilePhone` UInt8,
    `SilverlightVersion1` UInt8,
    `Age` UInt8,
    `Sex` UInt8,
    `Income` UInt8,
    `JavaEnable` UInt8,
    `CookieEnable` UInt8,
    `JavascriptEnable` UInt8,
    `IsMobile` UInt8,
    `BrowserLanguage` UInt16,
    `BrowserCountry` UInt16,
    `Interests` UInt16,
    `Robotness` UInt8,
    `GeneralInterests` Array(UInt16),
    `Params` Array(String),
    `Goals` Nested(
        ID UInt32,
        Serial UInt32,
        EventTime DateTime,
        Price Int64,
        OrderID String,
        CurrencyID UInt32),
    `WatchIDs` Array(UInt64),
    `ParamSumPrice` Int64,
    `ParamCurrency` FixedString(3),
    `ParamCurrencyID` UInt16,
    `ClickLogID` UInt64,
    `ClickEventID` Int32,
    `ClickGoodEvent` Int32,
    `ClickEventTime` DateTime,
    `ClickPriorityID` Int32,
    `ClickPhraseID` Int32,
    `ClickPageID` Int32,
    `ClickPlaceID` Int32,
    `ClickTypeID` Int32,
    `ClickResourceID` Int32,
    `ClickCost` UInt32,
    `ClickClientIP` UInt32,
    `ClickDomainID` UInt32,
    `ClickURL` String,
    `ClickAttempt` UInt8,
    `ClickOrderID` UInt32,
    `ClickBannerID` UInt32,
    `ClickMarketCategoryID` UInt32,
    `ClickMarketPP` UInt32,
    `ClickMarketCategoryName` String,
    `ClickMarketPPName` String,
    `ClickAWAPSCampaignName` String,
    `ClickPageName` String,
    `ClickTargetType` UInt16,
    `ClickTargetPhraseID` UInt64,
    `ClickContextType` UInt8,
    `ClickSelectType` Int8,
    `ClickOptions` String,
    `ClickGroupBannerID` Int32,
    `OpenstatServiceName` String,
    `OpenstatCampaignID` String,
    `OpenstatAdID` String,
    `OpenstatSourceID` String,
    `UTMSource` String,
    `UTMMedium` String,
    `UTMCampaign` String,
    `UTMContent` String,
    `UTMTerm` String,
    `FromTag` String,
    `HasGCLID` UInt8,
    `FirstVisit` DateTime,
    `PredLastVisit` Date,
    `LastVisit` Date,
    `TotalVisits` UInt32,
    `TraficSource` Nested(
        ID Int8,
        SearchEngineID UInt16,
        AdvEngineID UInt8,
        PlaceID UInt16,
        SocialSourceNetworkID UInt8,
        Domain String,
        SearchPhrase String,
        SocialSourcePage String),
    `Attendance` FixedString(16),
    `CLID` UInt32,
    `YCLID` UInt64,
    `NormalizedRefererHash` UInt64,
    `SearchPhraseHash` UInt64,
    `RefererDomainHash` UInt64,
    `NormalizedStartURLHash` UInt64,
    `StartURLDomainHash` UInt64,
    `NormalizedEndURLHash` UInt64,
    `TopLevelDomain` UInt64,
    `URLScheme` UInt64,
    `OpenstatServiceNameHash` UInt64,
    `OpenstatCampaignIDHash` UInt64,
    `OpenstatAdIDHash` UInt64,
    `OpenstatSourceIDHash` UInt64,
    `UTMSourceHash` UInt64,
    `UTMMediumHash` UInt64,
    `UTMCampaignHash` UInt64,
    `UTMContentHash` UInt64,
    `UTMTermHash` UInt64,
    `FromHash` UInt64,
    `WebVisorEnabled` UInt8,
    `WebVisorActivity` UInt32,
    `ParsedParams` Nested(
        Key1 String,
        Key2 String,
        Key3 String,
        Key4 String,
        Key5 String,
        ValueDouble Float64),
    `Market` Nested(
        Type UInt8,
        GoalID UInt32,
        OrderID String,
        OrderPrice Int64,
        PP UInt32,
        DirectPlaceID UInt32,
        DirectOrderID UInt32,
        DirectBannerID UInt32,
        GoodID String,
        GoodName String,
        GoodQuantity Int32,
        GoodPrice Int64),
    `IslandID` FixedString(16)
)
ENGINE = CollapsingMergeTree(Sign)
PARTITION BY toYYYYMM(StartDate)
ORDER BY (CounterID, StartDate, intHash32(UserID), VisitID)
SAMPLE BY intHash32(UserID)

```

Далее выйдем из cli и перейдем к наполнению БД тестовыми данными.
Для начала скачаем тестовый набор:
```
curl https://datasets.clickhouse.com/visits/tsv/visits_v1.tsv.xz | unxz --threads=`nproc` > visits_v1.tsv
```

И выполним вставку данных:
```
clickhouse-client --query "INSERT INTO tutorial.visits_v1 FORMAT TSV" --max_insert_block_size=30000 < visits_v1.tsv
```

Если не появилось никаких ошибок, значит данные были успешно загружены. Попробуем выполнить несколько запросов:
```
clickhouse-client --password <password>

ClickHouse client version 22.5.1.2079 (official build).
Connecting to localhost:9000 as user default.
Connected to ClickHouse server version 22.5.1 revision 54455.

Warnings:
 * Linux is not using a fast TSC clock source. Performance can be degraded.
 * Linux transparent hugepages are set to "always".
 * Maximum number of threads is lower than 30000. There could be problems with handling a lot of simultaneous queries.
 clickhouse1 :) SELECT COUNT(*) FROM tutorial.visits_v1

SELECT COUNT(*)
FROM tutorial.visits_v1

Query id: 65986304-c2ab-4b1c-9436-21ee9bc39294

┌─count()─┐
│ 1680437 │
└─────────┘

1 row in set. Elapsed: 0.105 sec.
```

Запрос по подсчет общего количества строк выполнялся 0.105с. Это при учете "холодного" кэша и без оптимизации таблицы после загрузки.
Проведем оптимизацию таблицы и выполним этот же запрос:
```
clickhouse1 :) OPTIMIZE TABLE tutorial.visits_v1 FINAL

OPTIMIZE TABLE tutorial.visits_v1 FINAL

Query id: 331eeeb9-8812-46e6-a3ab-8862eeb220b4

Ok.

0 rows in set. Elapsed: 34.634 sec.

clickhouse1 :) SELECT COUNT(*) FROM tutorial.visits_v1

SELECT COUNT(*)
FROM tutorial.visits_v1

Query id: 246e6ab3-ce38-4b3f-b533-06a40e069d56

┌─count()─┐
│ 1676861 │
└─────────┘

1 row in set. Elapsed: 0.006 sec.
```

Запрос отработал значительно быстрее. Вполне вероятно, что повлияла не только оптимизация таблицы, но и также прогретый кэш.
Выполним еще несколько аналитических запросов:

```
SELECT
    sum(Sign) AS visits,
    sumIf(Sign, has(Goals.ID, 1105530)) AS goal_visits,
    (100. * goal_visits) / visits AS goal_percent
FROM tutorial.visits_v1
WHERE (CounterID = 912887) AND (toYYYYMM(StartDate) = 201403) AND (domain(StartURL) = 'yandex.ru')

Query id: 2db6c68c-ea7a-4a39-8f05-dfb024be6518

┌─visits─┬─goal_visits─┬──────goal_percent─┐
│  10543 │        8553 │ 81.12491700654462 │
└────────┴─────────────┴───────────────────┘

1 row in set. Elapsed: 0.299 sec. Processed 19.95 thousand rows, 3.38 MB (66.67 thousand rows/s., 11.30 MB/s.)

SELECT
    StartURL AS URL,
    AVG(Duration) AS AvgDuration
FROM tutorial.visits_v1
WHERE (StartDate >= '2014-03-23') AND (StartDate <= '2014-03-30')
GROUP BY URL
ORDER BY AvgDuration DESC
LIMIT 10

Query id: 43aff231-5914-4cdb-968f-c0ea8e3bcb80

Connecting to database recipes at localhost:9000 as user default.
Connected to ClickHouse server version 22.5.1 revision 54455.

┌─URL─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┬─AvgDuration─┐
│ http://itpalanija-pri-patrivative=0&ads_app_user                                                                                                                                                │       60127 │
│ http://renaul-myd-ukraine                                                                                                                                                                       │       58938 │
│ http://karta/Futbol/dynamo.kiev.ua/kawaica.su/648                                                                                                                                               │       56538 │
│ https://moda/vyikroforum1/top.ru/moscow/delo-product/trend_sms/multitryaset/news/2014/03/201000                                                                                                 │       55218 │
│ http://e.mail=on&default?abid=2061&scd=yes&option?r=city_inter.com/menu&site-zaferio.ru/c/m.ensor.net/ru/login=false&orderStage.php?Brandidatamalystyle/20Mar2014%2F007%2F94dc8d2e06e56ed56bbdd │       51378 │
│ http://karta/Futbol/dynas.com/haberler.ru/messages.yandsearchives/494503_lte_13800200319                                                                                                        │       49078 │
│ http://xmusic/vstreatings of speeds                                                                                                                                                             │       36925 │
│ http://news.ru/yandex.ru/api.php&api=http://toberria.ru/aphorizana                                                                                                                              │       36902 │
│ http://bashmelnykh-metode.net/video/#!/video/emberkas.ru/detskij-yazi.com/iframe/default.aspx?id=760928&noreask=1&source                                                                        │       34323 │
│ http://censonhaber/547-popalientLog=0&strizhki-petro%3D&comeback=search?lr=213&text                                                                                                             │       31773 │
└─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┴─────────────┘

10 rows in set. Elapsed: 0.977 sec. Processed 1.44 million rows, 113.09 MB (1.47 million rows/s., 115.73 MB/s.)
```

Развернем дополнительно еще одну тестовую БД recipes
https://recipenlg.cs.put.poznan.pl/dataset



