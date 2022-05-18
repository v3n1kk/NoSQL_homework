##### Virtual machine: 1x CPU, 1Gb RAM, 8Gb SSD
##### OS: debian 10

### Install:
```
apt-get install gnupg 
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add - 
echo "deb http://repo.mongodb.org/apt/debian buster/mongodb-org/5.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list 
apt-get update 
apt-get install -y mongodb-org 
systemctl start mongod 
```
### Import data (Taxi trips in January-February 2015)
```
mongoimport -d uber -c pickups --type csv --file /tmp/Uber-Jan-Feb-FOIL.csv --headerline 

2022-05-18T02:25:31.812-0400    connected to: mongodb://localhost/ 
2022-05-18T02:25:31.841-0400    354 document(s) imported successfully. 0 document(s) failed to import. 
```
### Usage
```
mongo 
```
```
show dbs; 

admin   0.000GB 
config  0.000GB 
local   0.000GB 
uber    0.000GB 
```
```
use uber; 

switched to db uber
```
#### Select all
```
db.pickups.find(); 

{ "_id" : ObjectId("6284915b0fbdf92118fe376c"), "dispatching_base_number" : "B02512", "date" : "1/1/2015", "active_vehicles" : 190, "trips" : 1132 }
{ "_id" : ObjectId("6284915b0fbdf92118fe376d"), "dispatching_base_number" : "B02765", "date" : "1/1/2015", "active_vehicles" : 225, "trips" : 1765 }
{ "_id" : ObjectId("6284915b0fbdf92118fe376e"), "dispatching_base_number" : "B02764", "date" : "1/1/2015", "active_vehicles" : 3427, "trips" : 29421 }
{ "_id" : ObjectId("6284915b0fbdf92118fe376f"), "dispatching_base_number" : "B02682", "date" : "1/1/2015", "active_vehicles" : 945, "trips" : 7679 }
{ "_id" : ObjectId("6284915b0fbdf92118fe3770"), "dispatching_base_number" : "B02617", "date" : "1/1/2015", "active_vehicles" : 1228, "trips" : 9537 }
{ "_id" : ObjectId("6284915b0fbdf92118fe3771"), "dispatching_base_number" : "B02598", "date" : "1/1/2015", "active_vehicles" : 870, "trips" : 6903 }
{ "_id" : ObjectId("6284915b0fbdf92118fe3772"), "dispatching_base_number" : "B02598", "date" : "1/2/2015", "active_vehicles" : 785, "trips" : 4768 }
{ "_id" : ObjectId("6284915b0fbdf92118fe3773"), "dispatching_base_number" : "B02617", "date" : "1/2/2015", "active_vehicles" : 1137, "trips" : 7065 }
{ "_id" : ObjectId("6284915b0fbdf92118fe3774"), "dispatching_base_number" : "B02512", "date" : "1/2/2015", "active_vehicles" : 175, "trips" : 875 }
{ "_id" : ObjectId("6284915b0fbdf92118fe3775"), "dispatching_base_number" : "B02682", "date" : "1/2/2015", "active_vehicles" : 890, "trips" : 5506 }
{ "_id" : ObjectId("6284915b0fbdf92118fe3776"), "dispatching_base_number" : "B02765", "date" : "1/2/2015", "active_vehicles" : 196, "trips" : 1001 }
{ "_id" : ObjectId("6284915b0fbdf92118fe3777"), "dispatching_base_number" : "B02764", "date" : "1/2/2015", "active_vehicles" : 3147, "trips" : 19974 }
{ "_id" : ObjectId("6284915b0fbdf92118fe3778"), "dispatching_base_number" : "B02765", "date" : "1/3/2015", "active_vehicles" : 201, "trips" : 1526 }
{ "_id" : ObjectId("6284915b0fbdf92118fe3779"), "dispatching_base_number" : "B02617", "date" : "1/3/2015", "active_vehicles" : 1188, "trips" : 10664 }
{ "_id" : ObjectId("6284915b0fbdf92118fe377a"), "dispatching_base_number" : "B02598", "date" : "1/3/2015", "active_vehicles" : 818, "trips" : 7432 }
...
{ "_id" : ObjectId("6284915b0fbdf92118fe38cd"), "dispatching_base_number" : "B02765", "date" : "2/28/2015", "active_vehicles" : 747, "trips" : 7753 }
```
#### Insert some trips in March 2015
##### InsertOne
```
db.pickups.insert({"dispatching_base_number" : "B02765", "date" : "3/1/2015", "active_vehicles" : 777, "trips" : 7000});

WriteResult({ "nInserted" : 1 })
```
##### InsertMany
```
db.pickups.insert([{"dispatching_base_number" : "B02598", "date" : "3/1/2015", "active_vehicles" : 500, "trips" : 5000},
   {"dispatching_base_number" : "B02764", "date" : "3/1/2015", "active_vehicles" : 600, "trips" : 6000},
   {"dispatching_base_number" : "B02617", "date" : "3/1/2015", "active_vehicles" : 700, "trips" : 7000},
   {"dispatching_base_number" : "B02682", "date" : "3/1/2015", "active_vehicles" : 800, "trips" : 8000},
   {"dispatching_base_number" : "B02512", "date" : "3/1/2015", "active_vehicles" : 900, "trips" : 9000}]);

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
#### Check data inserted
```
db.pickups.find({"date" : "3/1/2015"});

{ "_id" : ObjectId("6284954bce4f4b7b920ca1e3"), "dispatching_base_number" : "B02765", "date" : "3/1/2015", "active_vehicles" : 777, "trips" : 7000 }
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e4"), "dispatching_base_number" : "B02598", "date" : "3/1/2015", "active_vehicles" : 500, "trips" : 5000 }
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e5"), "dispatching_base_number" : "B02764", "date" : "3/1/2015", "active_vehicles" : 600, "trips" : 6000 }
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e6"), "dispatching_base_number" : "B02617", "date" : "3/1/2015", "active_vehicles" : 700, "trips" : 7000 }
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e7"), "dispatching_base_number" : "B02682", "date" : "3/1/2015", "active_vehicles" : 800, "trips" : 8000 }
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e8"), "dispatching_base_number" : "B02512", "date" : "3/1/2015", "active_vehicles" : 900, "trips" : 9000 }
```
#### Update number of trips for B02765 on 3/1/2015
```
db.pickups.update({"dispatching_base_number" : "B02765", "date" : "3/1/2015"},{$set:{"active_vehicles" : 400, "trips" : 4000}});

WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
```

#### Check fixed data
```
db.pickups.find({"date" : "3/1/2015"});

{ "_id" : ObjectId("6284954bce4f4b7b920ca1e3"), "dispatching_base_number" : "B02765", "date" : "3/1/2015", "active_vehicles" : 400, "trips" : 4000 }
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e4"), "dispatching_base_number" : "B02598", "date" : "3/1/2015", "active_vehicles" : 500, "trips" : 5000 }
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e5"), "dispatching_base_number" : "B02764", "date" : "3/1/2015", "active_vehicles" : 600, "trips" : 6000 }
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e6"), "dispatching_base_number" : "B02617", "date" : "3/1/2015", "active_vehicles" : 700, "trips" : 7000 }
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e7"), "dispatching_base_number" : "B02682", "date" : "3/1/2015", "active_vehicles" : 800, "trips" : 8000 }
{ "_id" : ObjectId("62849660ce4f4b7b920ca1e8"), "dispatching_base_number" : "B02512", "date" : "3/1/2015", "active_vehicles" : 900, "trips" : 9000 }
```

#### Total trips in February (aggregation)
```
db.pickups.aggregate([{$match: {"date":{$gte:"2/1/2015", $lt:"3/1/2015"}}}, {$group: {_id:"$dispatching_base_number", totalTrips: {$sum:"$trips"}}}]);

{ "_id" : "B02682", "totalTrips" : 366568 }
{ "_id" : "B02617", "totalTrips" : 379037 }
{ "_id" : "B02512", "totalTrips" : 50987 }
{ "_id" : "B02765", "totalTrips" : 137383 }
{ "_id" : "B02764", "totalTrips" : 998473 }
{ "_id" : "B02598", "totalTrips" : 289133 }
```

## Indexes
#### Execution plan without index
```
db.pickups.explain().aggregate([{$match: {"date":{$gte:"2/1/2015", $lt:"3/1/2015"}}}, {$group: {_id:"$dispatching_base_number", totalTrips: {$sum:"$trips"}}}]);

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
```

#### Create index
```
db.pickups.createIndex({date: 1});

{
        "numIndexesBefore" : 1,
        "numIndexesAfter" : 2,
        "createdCollectionAutomatically" : false,
        "ok" : 1
```

#### Check index usage
```
db.pickups.explain().aggregate([{$match: {"date":{$gte:"2/1/2015", $lt:"3/1/2015"}}}, {$group: {_id:"$dispatching_base_number", totalTrips: {$sum:"$trips"}}}]);

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
```
