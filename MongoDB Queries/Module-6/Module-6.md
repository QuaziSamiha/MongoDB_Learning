# 14.05.24 and 24.05.24

- aggregation operations in mongodb — google it
  (https://studio3t.com/knowledge-base/articles/mongodb-aggregation-framework/)

# 6-0 Intro The Powerful Aggregation Framework

```
db.firstTest.find()
```

```
db.firstTest.aggregate([])
```

```
db.firstTest.aggregate(
    [
    // stage-1
    { $match: { gender: "Male" } }
    ]
)
```

```
db.firstTest.find(
    {
        gender: 'Male', age: { $lt: 30 }
    }
).project({ gender: 1, age: 1 })
```

```
db.firstTest.aggregate(
    [
        // stage-1
        { $match: { gender: "Male", age: { $lt: 30 } } }
    ]
)
```

```
db.firstTest.find(
    {
        gender: 'Male', age: { $lt: 30 }
    }
).project({ name: 1, gender: 1, age: 1 })
```

```
db.firstTest.aggregate(
    [
        // stage-1
        { $match: { gender: "Male", age: { $lt: 30 } } },
        // stage-2
        { $project: { name: 1, age: 1, gender: 1 } }
    ]
)
```

# 6-2 $AddFields , $Out , $Merge Aggregation Stage

```
db.firstTest.aggregate(
    [
        // stage-1
        { $match: { gender: "Male" } },
        // stage-2
        { $match: { age: { $lt: 30 } } },
        // stage-3
        { $project: { name: 1, age: 1, gender: 1 } }
    ]
)
```

```
db.firstTest.aggregate([
    // stage-1
    { $match: { gender: "Male" } },
    // stage-2
    { $addFields: { course: "level-2" } }
])
```

```
db.firstTest.aggregate([
    // stage-1
    { $match: { gender: "Male" } },
    // stage-2
    { $addFields: { course: "level-2" } },
    // stage-3
    { $project: { course: 1 } }
])
```

```
db.firstTest.find({}).project({ course: 1 })
```

- Does addFields change original documents? — google it

```
db.firstTest.aggregate(
    [
        // stage-1
        { $match: { gender: "Male" } },
        // stage-2
        { $addFields: { course: "level-5", eduTech: "PH" } },
        // stage-3
        { $project: { course: 1, eduTech: 1 } }
    ]
)
```

```
db.firstTest.aggregate(
    [
        // stage-1
        { $match: { gender: "Male" } },
        // stage-2
        { $addFields: { course: "level-2", eduTech: "PH", vondulField: 'yo yo' } },
        // stage-3
        { $project: { course: 1, eduTech: 1, vondulField: 1 } }
    ]
)
```

```
db.firstTest.aggregate(
    [
        // stage-1
        { $match: { gender: "Male" } },
        // stage-2
        { $addFields: { course: "level-2", eduTech: "PH", vondulField: 'yo yo' } },
        // stage-3
        { $project: { course: 1, eduTech: 1, vondulField: 1 } },
        // stage-4
        { $out: "course-students" }
    ]
)
```

```
db.firstTest.aggregate(
    [
        // stage-1
        { $match: { gender: "Male" } },
        // stage-2
        { $addFields: { course: "level-2", eduTech: "PH", vondulField: 'yo yo' } },
        // stage-3
        { $out: "course-students" }
    ]
)
```

```
db.firstTest.aggregate(
    [
        // stage-1
        { $match: { gender: "Male" } },
        // stage-2
        { $addFields: { course: "level-2", eduTech: "PH", vondulField: 'yo yo' } },
        // stage-3
        { $merge: "firstTest" }
    ]
)
```

```
db.firstTest.aggregate(
    [
        // stage-1
        { $addFields: { course: "level-2", eduTech: "PH", vondulField: 'yo yo' } },
        // stage-2
        { $merge: "firstTest" }
    ]
)
```

# 6-3 $Group , $Sum , $Push Aggregation Stage

[https://studio3t.com/knowledge-base/articles/mongodb-aggregation-framework/]

```
db.firstTest.aggregate(
    [
        { $group: { _id: "$gender" } }
    ]
)
```

```
db.firstTest.aggregate(
    [
        { $group: { _id: "$address.country" } }
    ]
)
```

```
db.firstTest.aggregate(
    [
        { $group: { _id: "$course" } }
    ]
)
```

```
db.firstTest.aggregate(
    [
        { $group: { _id: "$age" } }
    ]
)
```

```
db.firstTest.aggregate(
    [
        { $group: { _id: "$age", count: { $sum: 1 } } }
    ]
)
```

```
db.firstTest.aggregate(
    [
        { $group: { _id: "$gender", count: { $sum: 1 } } }
    ]
)
```

```
db.firstTest.aggregate(
    [
        { $group: { _id: "$address.country", count: { $sum: 1 } } }
    ]
)
```

```
db.firstTest.aggregate(
    [
        { $group: { _id: "$address.country", personName: { $push: "$name" } } }
    ]
)
```

```
db.firstTest.aggregate(
    [
        { $group: { _id: "$address.country", count: { $sum: 1 }, personName: { $push: "$name" } } }
    ]
)
```

```
db.firstTest.aggregate(
    [
        { $group: { _id: "$address.country", count: { $sum: 1 }, personName: { $push: "$$ROOT" } } }
    ]
)
```

```
db.firstTest.aggregate(
    [
        { $group: { _id: "$address.country", count: { $sum: 1 }, personName: { $push: "$$ROOT" } } }
    ]
)
```

```
db.firstTest.aggregate(
    [
        {
            // stage-1
            $group: {
                _id: "$address.country",
                count: { $sum: 1 },
                fullDoc: { $push: "$$ROOT" }
            }
        },
        // stage-2
        {
            $project: {
                "fullDoc.name": 1,
                "fullDoc.email": 1,
                "fullDoc.phone": 1
            }
        }
    ]
)
```

# 6-4 Explore More About $Group & $Project (15.05.24)

```
db.firstTest.aggregate(
    [
        {
            // stage-1
            $group: {
                _id: null,
            }
        }
    ]
)
```

```
db.firstTest.aggregate(
    [
        {
            // stage-1
            $group: {
                _id: null,
                totalSalary: { $sum: 1 }
            }
        }
    ]
)
```

```
db.firstTest.aggregate(
    [
        {
            // stage-1
            $group: {
                _id: null,
                totalSalary: { $sum: "$salary" }
            }
        },
    ]
)
```

```
db.firstTest.aggregate(
    [
        {
            // stage-1
            $group: {
                _id: null,
                totalSalary: { $sum: "$salary" },
                maxSalary: { $max: '$salary' }
            }
        }
    ]
)
```

```
db.firstTest.find({ salary: { $gt: 99 } })
```

```
db.firstTest.aggregate(
    [
        {
            // stage-1
            $group: {
                _id: null,
                totalSalary: { $sum: "$salary" },
                maxSalary: { $max: '$salary' },
                minSalaray: { $min: '$salary' }
            }
        },
    ]
)
```

```
db.firstTest.aggregate(
    [
        {
            // stage-1
            $group: {
                _id: null,
                totalSalary: { $sum: "$salary" },
                maxSalary: { $max: '$salary' },
                minSalaray: { $min: '$salary' },
                avgSalary: { $avg: "$salary" }
            }
        }
    ]
)
```

```
db.firstTest.aggregate(
    [
        {
            // stage-1
            $group: {
                _id: null,
                totalSalary: { $sum: "$salary" },
                maxSalary: { $max: '$salary' },
                minSalaray: { $min: '$salary' },
                avgSalary: { $avg: "$salary" }
            }
        },
        {
            $project: {
                totalSalary: 1,
                maxSalary: 1,
                minSalaray: 1,
                avgSalary: 1
            }
        }
    ]
)
```

- $subtract (aggregation)

```
db.firstTest.aggregate(
    [
        {
            // stage-1
            $group: {
                _id: null,
                totalSalary: { $sum: "$salary" },
                maxSalary: { $max: '$salary' },
                minSalaray: { $min: '$salary' },
                avgSalary: { $avg: "$salary" }
            }
        },
        {
            $project: {
                totalSalary: 1,
                maxSalary: 1,
                minSalaray: 1,
                averageSalary: "$avgSalary",
                rangeBetweenMaxMin: { $subtract: ["$maxSalary", "$minSalary"] }
            }
        }
    ]
)
```

# 6-5 Explore $Group With $Unwind Aggregation Stage

```
db.firstTest.aggregate(
    [
        // stage-2
        {
            $group: { _id: "$friends" }
        }
    ]
)
```

- MongoDB unwind

```
db.firstTest.aggregate([
    // stage-1
    {
        $unwind: "$friends"
    },
    // stage-2
    {
        $group: { _id: "$friends" }
    }
])
```

```
db.firstTest.aggregate([
    // stage-1
    {
        $unwind: "$friends"
    },
    // stage-2
    {
        $group: { _id: "$friends", count: { $sum: 1 } }
    }
])
```

```
db.firstTest.aggregate([
    // stage-1
    {
        $unwind: "$interests"
    }
])
```

```
db.firstTest.aggregate([
    // stage-1
    {
        $unwind: "$interests"
    },
    {
        $group: { _id: "$age" }
    }
])
```

```
db.firstTest.aggregate([
    // stage-1
    {
        $unwind: "$interests"
    },
    {
        $group: { _id: "$age", intersetsPerAge: { $push: '$interests' } }
    }
])
```

# 6-6 $Bucket, $Sort, And $Limit Aggregation Stage

- $bucket (aggregation)

```
db.firstTest.aggregate([
    // stage-1
    {
        $bucket: {
            groupBy: '$age',
            boundaries: [20, 40, 60, 80],
            default: 'upper than 80',
            output: {
                count: { $sum: 1 }
            }
        }
    }
])
```

```
db.firstTest.aggregate([
    // stage-1
    {
        $bucket: {
            groupBy: '$age',
            boundaries: [20, 40, 60, 80],
            default: 'upper than 80',
            output: {
                count: { $sum: 1 },
                who: { $push: '$name' }
            }
        }
    }
])
```

```
db.firstTest.aggregate([
    // stage-1
    {
        $bucket: {
            groupBy: '$age',
            boundaries: [20, 40, 60, 80],
            default: 'upper than 80',
            output: {
                count: { $sum: 1 },
                who: { $push: '$$ROOT' }
            }
        }
    }
])
```

```
db.firstTest.find({}).sort({ age: 1 }).project({ age: 1 })
```

```
db.firstTest.aggregate([
    // stage-1
    {
        $bucket: {
            groupBy: '$age',
            boundaries: [20, 40, 60, 80],
            default: 'upper than 80',
            output: {
                count: { $sum: 1 },
                who: { $push: '$$ROOT' }
            }
        }
    },
    // stage-2
    {
        $sort: { count: -1 } // descending
    }
])
```

```
db.firstTest.aggregate([
    // stage-1
    {
        $bucket: {
            groupBy: '$age',
            boundaries: [20, 40, 60, 80],
            default: 'upper than 80',
            output: {
                count: { $sum: 1 },
                who: { $push: '$$ROOT' }
            }
        }
    },
    // stage-2
    {
        $sort: { count: -1 } // descendingg
    },
    {
        $project: { count: 1 }
    }
])
```

```
db.firstTest.find({}).sort({ age: 1 }).project({ age: 1 }).limit(2)
```

```
db.firstTest.aggregate([
    // stage-1
    {
        $bucket: {
            groupBy: '$age',
            boundaries: [20, 40, 60, 80],
            default: 'upper than 80',
            output: {
                count: { $sum: 1 },
                who: { $push: '$$ROOT' }
            }
        }
    },
    // stage-2
    {
        $sort: { count: -1 } // descendingg
    },
    // stage-3
    {
        $limit: 2
    },
    // stage-4
    {
        $project: { count: 1 }
    }
])

```

# 6-7 $Facet, Multiple Pipeline Aggregation Stage

```
db.firstTest.aggregate([
    {
        $facet: {
            "friendsCount": [
                { $unwind: '$friends' }]
        }
    }
])
```

```
db.firstTest.aggregate([
    {
        $facet: {
            // pipeline 1
            "friendsCount": [
                // stage 1
                { $unwind: '$friends' },
                // stage 2
                { $group: { _id: '$friends', count: { $sum: 1 } } }
            ],
            // pipeline 2
            "educationCount": [
                // stage 1
                { $unwind: "$education" },
                // stage 2
                { $group: { _id: '$education', count: { $sum: 1 } } }
            ]
        }
    }
])
```

```
db.firstTest.aggregate([
    {
        $facet: {
            // pipeline 1
            "friendsCount": [
                // stage 1
                { $unwind: '$friends' },
                // stage 2
                { $group: { _id: '$friends', count: { $sum: 1 } } }
            ],
            // pipeline 2
            "educationCount": [
                // stage 1
                { $unwind: "$education" },
                // stage 2
                { $group: { _id: '$education', count: { $sum: 1 } } }
            ],
            // pipeline 3
            "skillsCount": [
                // stage 1
                { $unwind: "$skills" },
                // stage 2
                { $group: { _id: '$skills', count: { $sum: 1 } } }
            ]
        }
    }
])
db.firstTest.aggregate([
    {
        $facet: {
            // pipeline 1
            "friendsCount": [
                // stage 1
                { $unwind: '$friends' },
                // stage 2
                { $group: { _id: '$friends', count: { $sum: 1 } } }
            ],
            // pipeline 2
            "educationCount": [
                // stage 1
                { $unwind: "$education" },
                // stage 2
                { $group: { _id: '$education', count: { $sum: 1 } } }
            ],
            // pipeline 3
            "skillsCount": [
                // stage 1
                { $unwind: "$skills" },
                // stage 2
                { $group: { _id: '$skills', count: { $sum: 1 } } }
            ]
        }
    }
])
```

# 6-8 $Lookup Stage, Embedding Vs Referencing.Mp4

# referencing VS embedding

```
db.orders.aggregate([
    {
        $lookup: {
            from: "firstTest",
            localField: "userId",
            foreignField: "_id",
            as: "mezba>"
        }
    }
])
```

# 6-9 What Is Indexing, COLLSCAN Vs IXSCAN

```
db.firstTest.find({"_id" : ObjectId("6406ad63fc13ae5a40000065")}).explain()
```

```
db.firstTest.find({"_id" : ObjectId("6406ad63fc13ae5a40000065")}).explain("executionStats")
```

```
db.firstTest.find({	"email" : "mdangl1@odnoklassniki.ru"}).explain("executionStats")
```

// index scan & collscan

```
db.getCollection("massive-data").createIndex(
    { email: 1 },
)
```

- more indexing, more memory use -- since a data structure is created for indexing in memory

# 6-10 Explore Compound Index And Text Index

```
db.getCollection("massive-data").dropIndex(
    { email: 1 },
)
```

```
db.getCollection("massive-data").createIndex(
    { about: "text" })
```

```
db.getCollection("massive-data").find({ $text: { $search: "dolar" } })
```
