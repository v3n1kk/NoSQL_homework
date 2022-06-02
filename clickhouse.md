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
И выполним загрузку данных в clickhouse
```
clickhouse-client --password <password> --query "
    INSERT INTO recipes.recipes
    SELECT
        title,
        JSONExtract(ingredients, 'Array(String)'),
        JSONExtract(directions, 'Array(String)'),
        link,
        source,
        JSONExtract(NER, 'Array(String)')
    FROM input('num UInt32, title String, ingredients String, directions String, link String, source LowCardinality(String), NER String')
    FORMAT CSVWithNames
" --input_format_with_names_use_header 0 --format_csv_allow_single_quote 0 --input_format_allow_errors_num 10 --max_insert_block_size=50000 < full_dataset.csv
```

Подключимся и выполним несколько аналитических запросов:
```
clickhouse-client --password user
ClickHouse client version 22.5.1.2079 (official build).
Connecting to localhost:9000 as user default.
Connected to ClickHouse server version 22.5.1 revision 54455.

Warnings:
 * Linux is not using a fast TSC clock source. Performance can be degraded.
 * Linux transparent hugepages are set to "always".
 * Maximum number of threads is lower than 30000. There could be problems with handling a lot of simultaneous queries.

clickhouse1 :) use re
Display all 159 possibilities? (y or n)
clickhouse1 :) use recipes;

USE recipes

Query id: 752226aa-7bb3-4a76-9e0e-47013ca896b3

Ok.

0 rows in set. Elapsed: 0.001 sec.

clickhouse1 :) SELECT count() FROM recipes;

SELECT count()
FROM recipes

Query id: 45476d2c-be0d-4b40-b95f-a68d96b07aa6

┌─count()─┐
│ 2231142 │
└─────────┘

1 row in set. Elapsed: 0.105 sec.

clickhouse1 :) SELECT
                   arrayJoin(NER) AS k,
                   count() AS c
               FROM recipes
               GROUP BY k
               ORDER BY c DESC
               LIMIT 50

SELECT
    arrayJoin(NER) AS k,
    count() AS c
FROM recipes
GROUP BY k
ORDER BY c DESC
LIMIT 50

Query id: b54472cf-8e84-4061-8a72-bef05b06b1c6

┌─k────────────────────┬──────c─┐
│ salt                 │ 890741 │
│ sugar                │ 620027 │
│ butter               │ 493823 │
│ flour                │ 466110 │
│ eggs                 │ 401276 │
│ onion                │ 372469 │
│ garlic               │ 358364 │
│ milk                 │ 346769 │
│ water                │ 326092 │
│ vanilla              │ 270381 │
│ olive oil            │ 197877 │
│ pepper               │ 179305 │
│ brown sugar          │ 174447 │
│ tomatoes             │ 163933 │
│ egg                  │ 160507 │
│ baking powder        │ 148277 │
│ lemon juice          │ 146414 │
│ Salt                 │ 122558 │
│ cinnamon             │ 117927 │
│ sour cream           │ 116682 │
│ cream cheese         │ 114423 │
│ margarine            │ 112742 │
│ celery               │ 112676 │
│ baking soda          │ 110690 │
│ parsley              │ 102151 │
│ chicken              │ 101505 │
│ onions               │  98903 │
│ vegetable oil        │  91395 │
│ oil                  │  85600 │
│ mayonnaise           │  84822 │
│ pecans               │  79741 │
│ nuts                 │  78471 │
│ potatoes             │  75820 │
│ carrots              │  75458 │
│ pineapple            │  74345 │
│ soy sauce            │  70355 │
│ black pepper         │  69064 │
│ thyme                │  68429 │
│ mustard              │  65948 │
│ chicken broth        │  65112 │
│ bacon                │  64956 │
│ honey                │  64626 │
│ oregano              │  64077 │
│ ground beef          │  64068 │
│ unsalted butter      │  63848 │
│ mushrooms            │  61465 │
│ Worcestershire sauce │  59328 │
│ cornstarch           │  58476 │
│ green pepper         │  58388 │
│ Cheddar cheese       │  58354 │
└──────────────────────┴────────┘

clickhouse1 :) SELECT
                   title,
                   length(NER),
                   length(directions)
               FROM recipes.recipes
               WHERE has(NER, 'strawberry')
               ORDER BY length(directions) DESC
               LIMIT 10

SELECT
    title,
    length(NER),
    length(directions)
FROM recipes.recipes
WHERE has(NER, 'strawberry')
ORDER BY length(directions) DESC
LIMIT 10

Query id: 9053f7e5-f245-460a-93d7-01e182f22728

┌─title────────────────────────────────────────────────────────────┬─length(NER)─┬─length(directions)─┐
│ Chocolate-Strawberry-Orange Wedding Cake                         │          24 │                126 │
│ Strawberry Cream Cheese Crumble Tart                             │          19 │                 47 │
│ Charlotte-Style Ice Cream                                        │          11 │                 45 │
│ Sinfully Good a Million Layers Chocolate Layer Cake, With Strawb │          31 │                 45 │
│ Sweetened Berries With Elderflower Sherbet                       │          24 │                 44 │
│ Chocolate-Strawberry Mousse Cake                                 │          15 │                 42 │
│ Rhubarb Charlotte with Strawberries and Rum                      │          20 │                 42 │
│ Old-Fashioned Ice Cream Sundae Cake                              │          17 │                 37 │
│ Chef Joey's Strawberry Vanilla Tart                              │           7 │                 37 │
│ Watermelon Cake                                                  │          16 │                 36 │
└──────────────────────────────────────────────────────────────────┴─────────────┴────────────────────┘

10 rows in set. Elapsed: 1.334 sec. Processed 2.23 million rows, 1.54 GB (1.67 million rows/s., 1.16 GB/s.)

clickhouse1 :) SELECT arrayJoin(directions)
               FROM recipes.recipes
               WHERE title = 'Watermelon Cake'

SELECT arrayJoin(directions)
FROM recipes.recipes
WHERE title = 'Watermelon Cake'

Query id: b24d6be8-6b0c-4bb3-9743-3b56a5144df1

┌─arrayJoin(directions)──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ This historic recipe has been transcribed from the original text in the 1883 version of the First Texas Cookbook.                                                                                                                                          │
│ Sprinkle flour over cake mix.                                                                                                                                                                                                                              │
│ Add gelatin, oil and melon. Mix thoroughly with electric mixer, adding one egg at a time. Bake in 2 greased 8-inch pans at 325°.                                                                                                                           │
│ Ice when cool.                                                                                                                                                                                                                                             │
│ Sift flour, baking powder and salt together. Cream margarine; add sugar gradually and cream thoroughly. Add flour alternately with milk. Beat egg whites and add to batter. Divide batter into 2 parts. To one part, add red food coloring and well floured raisins. Grease melon mold or Bundt pan. Put a layer of white batter in the bottom, the red in the center and a layer of white on top. Bake in a 350° oven for 45 to 55 minutes. Frost with green icing. │
└────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
┌─arrayJoin(directions)──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ To make the coconut whipped cream, scrape the coconut cream from the top of the can into a large mixing bowl. The cream should have separated from the coconut juice after being refrigerated. │
│ Whip the coconut cream with a hand mixer until fluffy, about 5-10 minutes. Note: it will not be a stiff and fluffy as dairy whipped cream. Place in fridge until ready to use.                 │
│ To prepare the watermelon, slice off the top and bottom first, then slice the middle sections of the rind. Trim the watermelon to resemble a round or square cake shape as much as possible.   │
│ Pre-slice your watermelon cake into 6-8 servings.                                                                                                                                              │
│ Use paper towel to pat your watermelon as dry as possible to help the cream adhere.                                                                                                            │
│ Spread the whipped coconut cream evenly over watermelon cake and top with strawberry slices and crushed almonds. Serve immediately or refrigerate up to 3 days.                                │
└────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
┌─arrayJoin(directions)────────────────────────────────────────────────────────────────────────────┐
│ In a mixing bowl, combine dry cake mix, gelatin, eggs, water and oil.                            │
│ Beat on low speed just until moistened.                                                          │
│ Beat on high for 2 minutes or until well blended.                                                │
│ Pour into two greased and floured 9-inch round baking pans.                                      │
│ Bake at 350° for 30 to 35 minutes or until a toothpick inserted near the center comes out clean. │
│ Cool 10 minutes.                                                                                 │
│ Remove from pans to wire racks to cool completely.                                               │
│ Mix angel food cake mix, using directions on box.                                                │
│ Put a small amount of white cake around sides and bottom of angel food cake pan.                 │
│ Mix red food coloring with rest of mixture.                                                      │
│ Pour rest in pan.                                                                                │
│ Add chocolate chips to make seeds.                                                               │
│ Bake.                                                                                            │
│ Frost with green frosting when cool.                                                             │
│ Cream butter.                                                                                    │
│ Add sugar gradually and beat thoroughly.                                                         │
│ Sift flour; measure and add salt and baking powder.                                              │
│ Sift again.                                                                                      │
│ Add sifted dry ingredients alternately with milk and flavoring.                                  │
│ Beat thoroughly after each addition.                                                             │
│ Fold in stiffly beaten egg whites.                                                               │
│ Grease and flour 2 (9-inch) cake pans.                                                           │
│ Take a spoon and put a white ring of batter along outside edge of cake pans.                     │
│ To the remaining batter, add chocolate chips and red food coloring. Stir with spoon              │
│ to mix.                                                                                          │
│ Pour red mixture into middle of cake pan.                                                        │
│ Spread with spoon to touch white ring.                                                           │
│ Bake at 350° for 30 to 35 minutes.                                                               │
│ Cool.                                                                                            │
│ Frost with favorite white icing with green food coloring added.                                  │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘
┌─arrayJoin(directions)───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ In a large bowl, combine the cake mix, gelatin, water, eggs and oil; beat on low speed for 30 seconds. Beat on medium for 2 minutes.                                                                                                                │
│ Pour into two greased and floured 9-in. round baking pans. Bake at 350° for 30-35 minutes or until a toothpick inserted in the center comes out clean. Cool for 10 minutes before removing from pans to wire racks to cool completely.              │
│ Set aside 2 tablespoons frosting for decorating. Place 1-1/4 cups frosting in a bowl; tint red. Tint remaining frosting green.                                                                                                                      │
│ Place one cake layer on a serving plate; spread with 1/2 cup red frosting to within 1/4 in. of edges. Top with second cake. Frost top with remaining red frosting to within 3/4 in. of edges. Frost sides and top edge of cake with green frosting. │
│ Cut a 1/4-in. hole in the corner of pastry or plastic bag. Fill the bag with reserved white frosting. Pipe around top edge of cake where green and pink frostings meet. For seeds, insert chocolate chips upside down into cake top.                │
│ Cut 2-inch-thick slice from both ends of watermelon; discard trimmed slices.                                                                                                                                                                        │
│ Stand watermelon on cutting board. Starting at top of melon, use long thin sharp knife to carefully cut between rind and fruit all around watermelon to separate rind from fruit. Remove and discard rind.                                          │
│ Pat melon with paper towels to dry; place on platter. Frost with Cool Whip.                                                                                                                                                                         │
│ Decorate with fruit and serve.                                                                                                                                                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
┌─arrayJoin(directions)──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ -Make Your Batter-.                                                                                                                                                                                                                                        │
│ Preheat your oven to 350°C Prepare 4 six-inch-round, three-inch-deep (6"x3") cake pans by spraying the bottom and halfway up the sides with baking spray and placing a baking paper round in the bottom.                                                   │
│ In a medium-sized bowl, combine your eggs, 1/2 cup of your milk, and vanilla and whisk to combine. Set aside.                                                                                                                                              │
│ In the bowl of a stand mixer fitted with the paddle attachment, combine your flour, powdered sugar, baking powder, and salt and mix on low speed for a few minutes until combined. Low speed is important here so as to avoid creating a burst of flour that will get all over your hair and maybe in your eyes, it is the worst. │
│ All at once, add in your butter and keep mixing to moisten your dry ingredients creating a crumb-like consistency, about 20 seconds. Begin streaming in your remaining 1 1/2 cups milk, half a cup at a time, continuing to beat on the lowest speed. When all the milk is added, raise the mixer speed to medium and continue to beat the batter for about 30 seconds. This process is important because it incorporates air into your batter. │
│ Scrape your bowl with a spatula, and then return the batter to low speed. Add your egg mixture in three batches, allowing each to incorporate fully before adding the next. Add 1 teaspoon of Watermelon food gel and beat again on medium for about 20 seconds. If you'd like to achieve a deeper color, add another 1/2-1 teaspoon of gel coloring and beat on medium to combine. │
│ Divide your batter between your four prepped pans and smooth the batter to level it. Bake for 40 minutes, then keep a close eye on your cakes for the next 5-7-you'll want them to bounce back when you press on the middle of the top of the cakes. You can also insert a cake tester, and it should come out clean with at most a few crumbs clinging to it. │
│ Remove your cakes from the oven and allow them to come to room temperature on a rack. Then, I like to wrap them up in plastic and put them in the fridge for at least half an hour, preferably overnight before I remove them from the pans. These cakes should rest in the fridge for at least 8 hours total before stacking. │
│ -Make Your Watermelon Simple Syrup-.                                                                                                                                                                                                                       │
│ Place your water in a medium saucepan and add your unwrapped jolly rancher candies. Bring the water to a boil, then reduce to a simmer, stirring occasionally until the candy dissolves completely. Simmer for an additional 10 minutes, then set aside to cool to room temperature. │
│ -Prepare Your Buttercream-.                                                                                                                                                                                                                                │
│ Whip up some Milkmoon Meringue Buttercream (recipe #536136), you'll need 2x the amount listed in the recipe. Reserve 5 cups of this buttercream for your filling, and set the rest aside.                                                                  │
│ Combine the 5 cups buttercream with your mascarpone, beating well to combine thoroughly. Add drops of Watermelon food coloring gel until you reach the same shade as the cakes you baked (cut a small amount off the top of one of your cakes to take a peek at the color inside). │
│ Take 1/2 of your reserved white buttercream and add Super Black food gel into it until you achieve a strong black. Hot tip: this color will deepen as it stands. Set aside.                                                                                │
│ -Prep Your Layers-.                                                                                                                                                                                                                                        │
│ Start by trimming the domes off your cakes. We want flat disks of cake so we can accomplish a tall build!                                                                                                                                                  │
│ Now torte your layers out. Torting is the process of cutting a large cake into smaller layers, and I like to torte my layers super thin. You can choose instead to just trim the domes and leave the cakes as-is for a four-layer cake, or torte each cake in half for eight layers. The more layers, the cooler the seed affect in the slice reveal, however! │
│ -Build Your Cakes-.                                                                                                                                                                                                                                        │
│ Prepare two disposable piping bags, one filled with your black buttercream and the other with your red. Cut off the tips of each to create a hole that is roughly 1/8 of an inch wide, fairly small.                                                       │
│ Using a turntable as a base, center your first layer on an 8" round cake drum with a small dab of buttercream in the middle to anchor the cake. Brush the layer with a small amount of jolly rancher syrup. Then, pipe a spiral of buttercream in the very middle of the layer, measuring about 1-1 1/2 inches wide. Smooth this buttercream, then pipe another spiral of buttercream starting about 1/8 inch away from the buttercream at the center, and extending all the way to the edges of the layer. │
│ Pipe your black buttercream into the opening left, creating a black ring in the middle of the layer. Smooth your red buttercream, being careful not to disturb the black ring. Place your next layer of cake on top, doing your best not to drag it around too much as you center it. Repeat until you reach your final layer of cake, at which point you can wrap the whole thing in plastic and refrigerate stack until firm, at least an hour. │
│ Remove from the refrigerator when the cake doesn't wiggle when you shake it, and place it on a turntable on the counter. Using a serrated knife, go around the cake trimming off those crusty sides. Wrap the nude cake in plastic, and put it back in the refrigerator. │
│ -Frost Your Cake-.                                                                                                                                                                                                                                         │
│ You can start by crumb-coating the sides of your cake with a small amount of your white buttercream and refrigerate 10-20 minutes to set, or skip the crumb coat if you're confident diving right inches Leave the top un-coated! This will help with the watermelon slice illusion. │
│ Begin frosting your cake by placing about a 1/2 cup dollop of buttercream on top of your cake, and smoothing it out to the edges, making sure the buttercream overhangs the edges of the cake by at least 1/2 inch all the way around. Refrigerate until the buttercream is firm. Using a paring knife, trim the buttercream back so it's perfectly flush with the sides. │
│ To create the white layer of rind, place about two cups of your white buttercream in a disposable piping bag and cut a 1/4 inch hole in the end. Pipe the buttercream in rings up the entire cake, making sure to over-pipe at the top so the white buttercream sticks up in a ring around the top. Use a straight-edge to smooth your buttercream on the sides-I use a 14" quilting ruler!-and refrigerate about 10-20 minutes. │
│ Take your remaining white buttercream and, using mostly Electric Green with a few squeezes of Leaf Green to deepen, create a bright green watermelon rind color.                                                                                           │
│ Repeat the piping process with the light green buttercream, working your way up the sides and then smoothing them down. Put the cake back in the refrigerator to firm up.                                                                                  │
│ -Paint Your Rind-.                                                                                                                                                                                                                                         │
│ Melt down your remaining green buttercream in the microwave until it's a paintable consistency. Stir in more green coloring, including a few drops of Forest Green to deepen the hue. Using a flat or fan brush, brush your buttercream up the sides of your cake, creating loose, imperfect stripes. You can go for perfection if you like! You'll get a more cartoonish, less realistic look to your watermelon cake, which can be fun too. When you're finished, put the cake in the fridge again. │
│ -Trim the Top-.                                                                                                                                                                                                                                            │
│ After 10-20 minutes when the buttercream is totally firm, use your paring knife to trim the white and green buttercream down from around the top of the cake, making it totally flush with the smooth watermelon red buttercream on the top. You'll reveal a perfectly smooth watermelon cross-section that will have your guests scratching their heads! │
│ Pipe about eight black seeds in a circle around the top using an Ateco 8" round tip, piping teardrop shapes by piping a small pearl and drawing it to the center while releasing pressure on your bag.                                                     │
│ -Drumroll, Please!-.                                                                                                                                                                                                                                       │
│ Create a picnic spread and get ready to blow your guests' minds-it's time to slice your watermelon! Using a non-serrated knife, line the point up with the middle of the cake and, holding the knife completely level, slice down in a clean, confident motion until you hit the board. Remove the knife, wipe with a paper towel, and repeat to cut a slice that is perhaps 1/4-1/5 of the entire cake if you want it to be able to stand freely. Then, push an offset spatula under the slice, and lift up, using your other hand to stabilize the top of the slice. Pop the slice out from the bottom up, and remove to reveal... a slice of watermelon, complete with seeds and a perfect rind! │
│ Enjoy!                                                                                                                                                                                                                                                     │
│ Set aside 2 tablespoons chocolate covered raisins.                                                                                                                                                                                                         │
│ Prepare cake batter according to the package directions.                                                                                                                                                                                                   │
│ Add 12 drops of red food coloring and the remaining chocolate covered raisins to the batter; stir to mix.                                                                                                                                                  │
│ Pour batter into two 8-inch cake pans that have been sprayed with non-stick cooking spray, lined with wax paper and sprayed again with non-stick cooking spray.                                                                                            │
│ Bake according to package directions.                                                                                                                                                                                                                      │
│ Let cool for 10 minutes, then turn out onto wire racks to cool completely.                                                                                                                                                                                 │
│ Divide the frosting equally between two bowls.                                                                                                                                                                                                             │
│ Add the green food coloring to one bowl; stir to combine.                                                                                                                                                                                                  │
│ Add the rest of the red food coloring (8 drops) to the other bowl; stir to combine.                                                                                                                                                                        │
│ Invert one cake layer onto a serving plate; frost the top of the cake layer with half of the red frosting.                                                                                                                                                 │
│ Place the second layer on top of the first layer; frost the top with the remaining red frosting.                                                                                                                                                           │
│ Frost the sides with the green frosting.                                                                                                                                                                                                                   │
│ Sprinkle the reserved chocolate-covered raisins over the top to look like seeds.                                                                                                                                                                           │
│ Serve.                                                                                                                                                                                                                                                     │
└────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
┌─arrayJoin(directions)───────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ Preheat oven to 350*.                                                                                                       │
│ Grease and flour two 9" round cake pans.                                                                                    │
│ Cut two aluminum foil pieces 24" long.                                                                                      │
│ Fold and refold each strip until each strip is 2" wide.                                                                     │
│ Mold strips around 7" round bowl to shape.                                                                                  │
│ Tape ends together to form 7" circles.                                                                                      │
│ Prepare cake following package directions for original recipe.                                                              │
│ Measure 1 1/2 cups batter into bowl.                                                                                        │
│ Add 12 drops green food coloring.                                                                                           │
│ Add 15 drops red food coloring to remaining batter.                                                                         │
│ Stir until thoroughly blended.                                                                                              │
│ Place foil circles in center of pans.                                                                                       │
│ Pour half the green batter outside each foil circle.                                                                        │
│ Pull out foil rings.                                                                                                        │
│ Bake and cool cake following package directions.                                                                            │
│ Tint 1/2 cup cream cheese frosting to desired pink color.                                                                   │
│ Tint remaining frosting to green color.                                                                                     │
│ To assemble, place one cake layer on serving plate.                                                                         │
│ Spread strawberry jam on pink layer of cake layer.                                                                          │
│ Spread green frosting on green part of cake layer.                                                                          │
│ Spread green frosting on green part of cake layer.                                                                          │
│ Top with second cake layer.                                                                                                 │
│ Frost sides and green area on top layer with green frosting.                                                                │
│ Spread pink frosting on center of cake top; sprinkle with miniature chocolate chips.                                        │
│ Remove all but lowest rack from oven.                                                                                       │
│ Turn on your oven's broiler.                                                                                                │
│ Cut a cylinder of watermelon about 6-inches high.                                                                           │
│ Removing the rind, carve the watermelon into the shape of a round cake 8-inches in diameter and 6-inches in height.         │
│ Set aside.                                                                                                                  │
│ In a large bowl, beat the egg whites while slowly adding the sugar.                                                         │
│ Continue adding sugar and beating until stiff peaks form.                                                                   │
│ Place watermelon "cake" flat on a heatproof platter and frost with the meringue.                                            │
│ (Make sure every bit of the watermelon is covered!                                                                          │
│ ).                                                                                                                          │
│ Place "cake" into oven as far from the broiler as possible - hence on the lowest rack - and broil until meringue is golden. │
│ Remove watermelon cake from oven.                                                                                           │
│ Meanwhile, heat the brandy in a small saucepan just until warm.                                                             │
│ Ignite and pour over the meringue.                                                                                          │
│ When the flames subside, cut into wedges as you would a cake.                                                               │
└─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
┌─arrayJoin(directions)──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ Heat oven to 350°F Grease bottoms only of two 8- or 9-inch round pans with shortening or cooking spray.                                                                                                                                                    │
│ In large bowl, stir into batter 1/2 cup of the chocolate chips. Add the drink mix, stir, and pour into pans.                                                                                                                                               │
│ Bake 27 to 32 minutes or until toothpick inserted in center comes out clean. Cool 10 minutes; remove from pans to wire racks. Cool completely, about 1 hour.                                                                                               │
│ In small bowl, stir 1 cup frosting with 10 to 12 drops green food coloring. Stir 10 to 12 drops red food color into remaining frosting.                                                                                                                    │
│ Cut cake rounds crosswise in half to make 4 halves. Frost uncut sides with green frosting; press green jelly beans into frosting. Frost top of cake with red frosting; press remaining 2 tablespoons chocolate chips into frosting for seeds.              │
│ To serve, cut into wedges.                                                                                                                                                                                                                                 │
│ Preheat oven to 350°F.                                                                                                                                                                                                                                     │
│ Prepare two 9-inch round cake pans by spraying with nonstick spray. Line bottoms with wax paper; coat with spray.                                                                                                                                          │
│ In large bowl combine cake mix, pudding mix, eggs, water and oil. Beat at medium speed with electric mixer for 2 minutes. Pour evenly into prepared pans. Bake 30 to 35 minutes until cake tester inserted in centers comes out clean.                     │
│ Cool in pans on wire rack 15 minutes; invert cakes onto rack, remove paper and allow to cool completely.                                                                                                                                                   │
│ Tint one of the cans of frosting red-orange. Using leaf green, yellow and a bit of black, tint one can frosting pale green. Place 1/2 cup pale green frosting in a pastry bag fitted with decorating tip. Add more leaf green and black food color to remaining pale green frosting until it turns dark green. │
│ Stack cake layers on a cutting board; cut crosswise in half. Set one piece aside.                                                                                                                                                                          │
│ For large melon slice: Sandwich 3 cake layer halves with 1/3 cup white frosting between each (invert top layer so flat side is up).                                                                                                                        │
│ For small melon wedges: Cut reserved piece of cake into 3 wedges. Frost large slice and wedges with a thin layer of remaining white frosting.                                                                                                              │
│ Frost rounded edges of cakes with dark green frosting. Using flat slide of decorating tip, pipe pale green frosting along edge of dark green frosting on sides and top. Pipe squiggly lines onto sides over dark green frosting. Using spatula, smear pale green lines to create the look of watermelon skin. │
│ Reserve 1/2 cup red-orange frosting. With remaining red-orange frosting, frost top and straight sides of cakes, leaving about 1/2-inch border of white frosting. Slice chocolate-covered raisins in half lengthwise to resemble seeds. Place cut-side up into red-orange frosting for pits. Chill several hours or overnight in refrigerator to set. │
│ Transfer large melon slice to serving tray, standing it on rounded edge. Frost back side of cake with reserved red-orange frosting; decorate with additional chocolate-covered raisins. Place small wedges on tray with large slice.                       │
│ To serve large cake, place it back onto a flat side before cutting into slices.                                                                                                                                                                            │
│ Combine cake mix, gelatin, eggs, water and oil.                                                                                                                                                                                                            │
│ Beat on low speed just until moistened.                                                                                                                                                                                                                    │
│ Beat on high for 2 minutes or until well blended.                                                                                                                                                                                                          │
│ Pour into two greased and floured 9 inch round pans.                                                                                                                                                                                                       │
│ Bake at 350 degrees for 30-35 minutes or until a toothpick inserted comes out clean.                                                                                                                                                                       │
│ Cool for 10 minutes;remove from pans and cool completely.                                                                                                                                                                                                  │
│ Set aside 2 tablespoons frosting for decorating.                                                                                                                                                                                                           │
│ Place 1 1/4 cup frosting in a bowl; tint red.                                                                                                                                                                                                              │
│ Tint remaining frosting green.                                                                                                                                                                                                                             │
│ Place one cake layer on a serving plate; spread with 1/2 cup red frosting to within 1/4 inch of edges.                                                                                                                                                     │
│ Top with second cake.                                                                                                                                                                                                                                      │
│ Frost top with remaining red frosting to within 3/4 inch of edges.                                                                                                                                                                                         │
│ Frost sides and top edge with green frosting.                                                                                                                                                                                                              │
│ Place reserved white frosting in a frosting bag or plastic bag with corner cut out.                                                                                                                                                                        │
│ Pipe around top edge of cake where green and red frosting meets.                                                                                                                                                                                           │
│ For seeds, insert chocolate chips upside down into cake top.                                                                                                                                                                                               │
└────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
┌─arrayJoin(directions)───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ For the frosting: With an electric mixer, beat the heavy cream, sugar and vanilla on medium-high speed until the cream reaches stiff peaks. │
│ Refrigerate until ready to use.                                                                                                             │
│ For the cake: Cut off the ends of the watermelon, leaving the middle section; remove the rind.                                              │
│ Pat the outside of the watermelon dry with paper towels.                                                                                    │
│ Set the "cake" on a serving plate.                                                                                                          │
│ Cover the watermelon cake with the frosting.                                                                                                │
│ Press the almonds into the sides of the cake.                                                                                               │
│ Top with the strawberry slices.                                                                                                             │
│ Cut into 6 to 8 wedges and serve immediately.                                                                                               │
│ Directions: The "cake" is watermelon.                                                                                                       │
│ Cut the ends off the watermelon to form the top & bottom of the cake; then cut away the rind from the sides of the cake.                    │
│ Use cookie cutters to cut cantaloupe flowers and honeydew leaves/ Use toothpicks to attach to cake.                                         │
│ Decorate with additional strawberries, blueberries, apples, grapes, and oranges.                                                            │
└─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘

186 rows in set. Elapsed: 0.146 sec. Processed 71.67 thousand rows, 44.22 MB (489.73 thousand rows/s., 302.17 MB/s.)
```

#### Выводы
OLAP-запросы, как и ожидалось, в clickhouse отрабатывают очень быстро благодаря своей колоночноориентированной структуре хранения. Такая скорость позволяет строить аналитические отчеты значительно эффективнее RDBMS решений. В то же время, clickhouse не очень хорошо работает с обновлением, удалением данных и вставкой данных малых объемов. Таким образом, можно сделать вывод, что clickhouse эффективен для определенных решений, такие как OLAP, либо системы логирования.
