- **1 Find all the documents in the collection where age is greater than 30 and only returns name and email:**

```
db.practice1.find({
    age: { $gt: 30 }
}).project({ name: 1, email: 1 })
```

- **2 Find documents where the favourite color is either "Maroon" or "Blue":**

**Implicit OR:**

```
db.practice1.find({
    favoutiteColor: {
        $in: ['Maroon', 'Blue']
    }
}).project({ favoutiteColor: 1 })
```

**Implicit AND:**

```
db.practice1.find({
    $or: [
        {
            favoutiteColor: { $eq: "Maroon" }
        },
        {
            favoutiteColor: { $eq: "Blue" }
        }
    ]
}).project({ favoutiteColor: 1 })
```

- **3. Find all documents where skill is an empty array:**

```
db.practice1.find({
    skills: {$size: 0}
}).project({ skills: 1 })
```

- **4. Find documents where person has skills in both 'Java' and 'JavaScript':**

**Explicit AND**

```
db.practice1.find({
    $and: [
        { "skills.name": "JAVA" },
        { "skills.name": "JAVASCRIPT" }
    ]
}).project({ "skills.name": 1 })
```

**Implicit AND:**

```
db.practice1.find(
    {
        "skills.name": { $eq: 'JAVA' }
    },
    {
        'skills.name': { $eq: 'JAVASCRIPT' }
    }
).project({ "skills.name": 1 })
```

- **5. Add a new skill to the skills array for the document with the email : 'amccurry3@cnet.com'. The skill is {"name": "Python", "level": "Beginner", "isLearning": true}**

```
db.practice1.insertOne({email: "amccurry3@cnet.com"})
```

```
db.practice1.find({
    email: 'amccurry3@cnet.com'
})
```
