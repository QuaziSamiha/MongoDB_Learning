# Module 5 (10 May, 2024)

- 25 May, 2024

# 5-1-A Install MongoDB compass & No SQL Booster (windows)

- MongoDB Community Server Download:
  [https://www.mongodb.com/try/download/community]

* Commands for MongoDB compass:
  - show dbs
  - use practice

# Queries:

```
show dbs
```

```
db.createCollection(‘test’)
```

```
db.test.getCollection('test').insertOne({ name: 'pumpa', age: 2 })
```

```
db.test.getCollection('test').find()
```

- MongoDB Shell Download: https://www.mongodb.com/try/download/shell
- steps:

1. Path copied: C:\Program Files\MongoDB\Server\7.0\bin
2. Setting mongosh path
3. Edit environmental variable → users variable for hp
4. Commands for cmd:
   mongod –version
   mongosh

GUI :
Studio 3T
No SQL Booster — GUI for MongoDB – free for one month --> https://nosqlbooster.com/

# 5-2 Insert,InsertOne, Find, FindOne, Field Filtering, Project

- practice data:
  https://github.com/Apollo-Level2-Web-Dev/mongodb-practice

# Queries In NoSQLBooster:

```
db.test.insertOne({ name: 'pumpa', age: 2 })
```

```
db.test.insertOne({name: 'ATI'})
```

- Alt+shift+f —> to format

```
db.test.insertMany([{ name: 'vondul', age: 11 }, { name: 'akku', age: 3 }])
```

```
db.test.insertMany([{ name: 'Complete Web Development' }, { name: 'Next Level Web Development' }])
```

```
db.test.findOne({ age: 2 })
```

```
db.firstTest.findOne({age: 17})
```

```
db.firstTest.findOne({company: 'Demimbu'})
```

```
db.firstTest.find({company: 'Demimbu'})
```

```
db.firstTest.find({gender: 'Female'})
```

# Field filtering:

```
db.test.find()
```

```
db.firstTest.find({gender: 'Male'}, {gender: 1})
```

```
db.firstTest.find({ gender: 'Female' }, { gender: 1, age: 1 })
```

```
db.firstTest.find({gender: 'Male'}, {name: 1, gender: 1})
```

```
db.firstTest.find({gender: 'Male'}, {name: 1, phone: 1, email: 1, gender: 1})
```

```
db.firstTest.findOne({gender: 'Male'}, {name: 1, phone: 1, email: 1, gender: 1})
```

- project() only works with find(), it doesn't work with findOne()

```
db.firstTest.find({gender: 'Male'}).project({name: 1, phone: 1, email: 1, gender: 1})
```

# 5-3 $eq, $neq, $gt, $gte, $lt, $lte,

# MongoDB Operator

- Query and Projection Operators
- Comparison Query Operators

* $eq

```
db.firstTest.find({ gender: { $eq: "Male" } })
    .projection({ name: 1, gender: 1, age: 1 })
```

```
db.firstTest.find({gender: {$eq: 'Male'}})
```

```
db.firstTest.find({age: {$eq: 12}})
```

```
db.firstTest.find({ age: { $eq: 26 } }).project({ age: 1, name: 1 })
```

```
db.firstTest.find({age: {$ne: 12}})
```

```
db.firstTest.find({age: {$gt: 18}})
```

```
db.firstTest.find({age: {$gte: 18}})
```

```
db.firstTest.find({age: {$gte: 18}}).sort({age: 1})
```

```
db.firstTest.find({ age: { $gte: 18 } }).project({ age: 1 }).sort({ age: 1 })
```

```
db.firstTest.find({age: {$lt: 18}}).sort({age: 1})
```

```
db.firstTest.find().project({age: 1}).sort({age: 1})
```

# 5-4 $In, $Nin, Implicit And Condition

- age greater than 18 and less than 30

```
db.firstTest.find({age: {$gt: 18, $lt: 30}}, {age: 1})
```

```
db.firstTest.find(
    { age: { $gt: 18, $lt: 30 } },
    { age: 1 }
).sort({ age: 1 })
```

```
db.firstTest.find(
    {
        gender: 'Female',
        age: { $gt: 18, $lt: 30 }
    },
    { age: 1, gender: 1 }
).sort({ age: 1 })
```

```
db.firstTest.find(
    {
        gender: 'Female',
        age: { $in: [18, 24] }
    },
    { age: 1, gender: 1 }
).sort({ age: 1 })
```

```
db.firstTest.find(
    {
        gender: 'Female',
        age: { $nin: [18, 22, 24, 25] }
    },
    { age: 1, gender: 1 }
).sort({ age: 1 })
```

```
db.firstTest.find(
    {
        gender: 'Female',
        age: { $nin: [18, 22, 24, 25] },
        interests: 'Cooking'
    },
    { age: 1, gender: 1, interests: 1 }
).sort({ age: 1 })
```

```
db.firstTest.find(
    {
        gender: 'Female',
        age: { $nin: [18, 22, 24, 25] },
        interests: { $in: ['Cooking', 'Gaming'] }
    },
    { age: 1, gender: 1, interests: 1 }
).sort({ age: 1 })
```

# 5-5 $And, $Or, Implicit Vs Explicit (Logical Query Operator)

```
db.firstTest.find(
    {
        $and:
            [
                { age: { $ne: 15 } },
                { age: { $lt: 30 } }
            ]
    }
).project({ age: 1 })
```

```
db.firstTest.find(
    {
        $and:
            [
                { age: { $ne: 15 } },
                { age: { $lt: 30 } }
            ]
    }
).project({ age: 1 }).sort({ age: 1 })
```

```
db.firstTest.find(
    {
        $and:
            [
                { gender: 'Female' },
                { age: { $ne: 15 } },
                { age: { $lt: 30 } }
            ]
    }
).project({ age: 1, gender: 1 }).sort({ age: 1 })
```

- Explicit OR

```
db.firstTest.find(
    {
        $or:
        [
            { interests: "Traveling" },
            { interests: "Cooking" }
        ]
    }
).project({ interests: 1 })
```

```
db.firstTest.find(
    {
        $or:
            [
                { 'skills.name': "JAVASCRIPT" },
                { 'skills.name': "PYTHON" },
            ]
    }
).project({ skills: 1 })
```

- implicit OR

```
db.firstTest.find(
    {
        'skills.name': {
            $in: ["JAVASCRIPT", "PYTHON"]
        }
    }
).project({ skills: 1 })
```

# 5-6 $Exists, $Type, $Size (Element Query Operators)

```
db.firstTest.find(
    {
        age: { $exists: true }
    }
)
```

```
db.firstTest.find(
    {
        age: { $type: "string" }
    }
)
```

```
db.firstTest.find(
    {
        age: { $type: "string" }
    }
).project({ name: 1, age: 1 })
```

```
db.firstTest.find(
    {
        friends: { $type: "array" }
    }
)
```

```
db.firstTest.find(
    {
        friends: { $type: "array" }
    }
)
```

```
db.firstTest.find(
    {
        friends: { $type: "array" }
    }
).project({ friends: 1 })
```

- Array Query Operators

```
db.firstTest.find({ friends: { $size: 4 } })
```

```
db.firstTest.find(
    {
        friends: { $size: 4 }
    }
).project({ friends: 1 })
```

- Empty Array

```
db.firstTest.find(
    {
        friends: { $size: 0 }
    }
).project({ friends: 1 })
```

```
db.firstTest.find(
    {
        company:
            { $type: "null" }
    }
).project({ company: 1 })
```

# 5-7 $All , $ElemMatch

```
db.firstTest.find(
    { interests: "Cooking" }
).project({ interests: 1 })
```

- Position within array

```
db.firstTest.find(
    {
      "interests.2": "Cooking"
    }
).project({ interests: 1 })
```

- Exact Matching

```
db.firstTest.find(
    {
        interests: ["Travelling", "Reading", "Cooking"]
    }
).project({ interests: 1 })
```

- Only Matching

```
db.firstTest.find(
    {
        interests:
        {
            $all: ["Travelling", "Reading", "Cooking"]
        }
    }
).project({ interests: 1 })
```

```
db.firstTest.find(
    {
        "skills.name": "JAVASCRIPT"
    }
).project({ skills: 1 })
```

```
db.firstTest.find(
    {
        "skills.name": "JAVASCRIPT", "skills.level": "Intermidiate"
    }
).project({ skills: 1 })
```

```
db.firstTest.find(
    {
        skills: {
            name: 'JAVASCRIPT',
            level: 'Intermidiate',
            isLearning: false
        }
    }
).project({ skills: 1 })
```

```
db.firstTest.find(
    {
        skills: {
            name: 'JAVASCRIPT',
            level: 'Intermidiate'
        }
    }
).project({ skills: 1 })
```

```
db.firstTest.find(
    {
        skills: {
            $elemMatch: {
                name: 'JAVASCRIPT',
                level: 'Intermidiate'
            }
        }
    }
).project({ skills: 1 })
```

# 5-8 $Set, $AddToSet, $Push, (Field Update Operators)

```
db.firstTest.find(
    {
        _id: ObjectId("6406ad63fc13ae5a40000069")
    }
)
```

```
db.firstTest.updateOne(
    {
        _id: ObjectId("6406ad63fc13ae5a40000069")
    },
    { $set: { age: 80 } }
)
```

```
db.firstTest.updateOne(
    {
        _id: ObjectId("6406ad63fc13ae5a40000069")
    },
    { $set: { interests: "Gaming" } }
)
```

```
db.firstTest.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000069") },
    { $set: { interests: ["Gaming"] } }
)
```

- Array Update Operators

```
db.firstTest.updateOne(
    {
        _id: ObjectId("6406ad63fc13ae5a40000069")
    },
    {
        $addToSet: { interests: "Writting" }
    }
)
```

```
db.firstTest.updateOne(
    {
        _id: ObjectId("6406ad63fc13ae5a40000069")
    },
    {
        $addToSet: { interests: ["Writting", "Coding"] }
    }
)
```

```
db.firstTest.updateOne(
    {
        _id: ObjectId("6406ad63fc13ae5a40000069")
    },
    {
        $addToSet: {
            interests: { $each: ["Writting", "Driving"] }
        }
    }
)
```

```
db.firstTest.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000069") },
    {
        $push: {
            interests: { $each: ["Writting", "Driving"] }
        }
    }
)
```

# 5-9 $Unset, $Pop, $Pull, $PullAll (Field Update Operators)

```
db.firstTest.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000069") },
    {
        $unset: { birthday: "" }
    }
)
```

- Operators

* $pop

- remove last element from array

```
db.firstTest.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000069") },
    {
        $pop: { friends: 1 }
    }
)
```

```
db.firstTest.find({ _id: ObjectId("6406ad63fc13ae5a40000069") })
```

```
db.firstTest.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000069") },
    {
        $pop: { friends: -1 }
    }
)
```

```
db.firstTest.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000069") },
    {
        $pull: { friends: "Najmus Sakib" }
    }
)
```

```
db.firstTest.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000069") },
    {
        $pullAll: { friends: ["Abdur Rakib", "Mir Hussain"] }
    }
)
```

```
db.firstTest.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000069") },
    {
        $pullAll: {
            interests: ["Writting",
                "Driving",
                "Writting",]
        }
    }
)
```

# 5-10 More About $Set, How To Explore Documentation

```
db.firstTest.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000069") },
    { $set: { "address.city": "Dhaka" } }
)
```

- multiple value update

```
db.firstTest.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000069") },
    {
        $set: {
            "address.city": "Rajshahi",
            "address.country": "Bangladesh"
        }
    }
)
```

- Mongodb update a value in an array of object of array
- Field Names with Periods and Dollar Signs

- $(update)

- updating object property from an array of object:

```
db.firstTest.updateOne(
    {
        _id: ObjectId("6406ad63fc13ae5a40000069"),
        "education.major": "Education"
    },
    {
        $set: {
            "education.$.major": "CSE"
        }
    }
)
```

- How to increment in mongodb – google it

- $inc

```
db.firstTest.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000069") },
    {
        $inc: { age: 1 }
    }
)
```

# 5-11 Delete Documents, Drop Collection And How To Explore By Yourself

- How to delete a document from mongodb – google it
  Delete Documents

```
db.firstTest.deleteOne(
    {
        _id: ObjectId("6406ad63fc13ae5a40000069")
    }
)
```

- How to delete collection in mongodb – google it

```
db.collection.drop()
```

- How to create a collection in mongodb — google it

```
db.createCollection()
```

```
db.createCollection("secondTest")
```

```
db.secondTest.insertOne({test: "I am testing"})
```

PH Task
