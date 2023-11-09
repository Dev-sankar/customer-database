 
**01 Create a Database called customers**

```
test> use customers
switched to db customers

```

** 
02 Create a collection called customerdetails.
**
```
customers> db.createCollection("customerdetails")
{ ok: 1 }

```
**
3. Insert all documents into the collection named   customerdetails.

**

```
customers> db.customerdetails.insertMany([{name:"john",age:25,gender:"male",city:"new york"},{name:"emily",age:22,gender:"female",city:"london"},{name:"daniel",age:28,gender:"male",city:"sydney"},{name:"sophia",age:24,gender:"female",city:"paris"},{name:"wiliam",age:26,gender:"male",city:"chicago"},{name:"Olivia",age:23,gender:"female",city:"los angeles"},{name:"benjamin",age:27,gender:"male",city:"toronto"},{name:"mila",age:29,gender:"female",city:"berlin"},{name:"james",age:30,gender:"male",city:"tokyo"}])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("654ca4b30da73a2f96d37eec"),
    '1': ObjectId("654ca4b30da73a2f96d37eed"),
    '2': ObjectId("654ca4b30da73a2f96d37eee"),
    '3': ObjectId("654ca4b30da73a2f96d37eef"),
    '4': ObjectId("654ca4b30da73a2f96d37ef0"),
    '5': ObjectId("654ca4b30da73a2f96d37ef1"),
    '6': ObjectId("654ca4b30da73a2f96d37ef2"),
    '7': ObjectId("654ca4b30da73a2f96d37ef3"),
    '8': ObjectId("654ca4b30da73a2f96d37ef4")
  }
}


```
**
4. Retrieve all documents from the collection and sort the results by the “age” field    in ascending order

**

```
customers> db.customerdetails.find().sort({ age: 1 }).pretty()
[
  {
    _id: ObjectId("654ca4b30da73a2f96d37eed"),
    name: 'emily',
    age: 22,
    gender: 'female',
    city: 'london'
  },
  {
    _id: ObjectId("654ca4b30da73a2f96d37ef1"),
    name: 'Olivia',
    age: 23,
    gender: 'female',
    city: 'los angeles'
  },
  {
    _id: ObjectId("654ca4b30da73a2f96d37eef"),
    name: 'sophia',
    age: 24,
    gender: 'female',
    city: 'paris'
  },
  {
    _id: ObjectId("654ca4b30da73a2f96d37eec"),
    name: 'john',
    age: 25,
    gender: 'male',
    city: 'new york'
  },
  {
    _id: ObjectId("654ca4b30da73a2f96d37ef0"),
    name: 'wiliam',
    age: 26,
    gender: 'male',
    city: 'chicago'
  },
  {
    _id: ObjectId("654ca4b30da73a2f96d37ef2"),
    name: 'benjamin',
    age: 27,
    gender: 'male',
    city: 'toronto'
  },
  {
    _id: ObjectId("654ca4b30da73a2f96d37eee"),
    name: 'daniel',
    age: 28,
    gender: 'male',
    city: 'sydney'
  },
  {
    _id: ObjectId("654ca4b30da73a2f96d37ef3"),
    name: 'mila',
    age: 29,
    gender: 'female',
    city: 'berlin'
  },
  {
    _id: ObjectId("654ca4b30da73a2f96d37ef4"),
    name: 'james',
    age: 30,
    gender: 'male',
    city: 'tokyo'
  }
]

```

**
5. Count the number of females. 

**

```
customers> db.customerdetails.countDocuments({gender:"female"})
4
```

**
6.Insert one document into the customerdetails collection
**
```
customers> db.customerdetails.insertOne({name:"nilax",age:23,gender:"male",city:"jaffna" })
{
  acknowledged: true,
  insertedId: ObjectId("654cacc80da73a2f96d37ef5")
}

```
**
7. Update city=SriLanka to John.
**
```
customers> db.customerdetails.update({name:"john",age:25,gender:"male"},{$set:{city:"jaffna"}},{upsert:true})
DeprecationWarning: Collection.update() is deprecated. Use updateOne, updateMany, or bulkWrite.
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

```

**
8. Remove the customer from Tokyo.
**

```
customers> db.customerdetails.remove({city:"tokyo"})
DeprecationWarning: Collection.remove() is deprecated. Use deleteOne, deleteMany, findOneAndDelete, or bulkWrite.
{ acknowledged: true, deletedCount: 1 }

```

**
9.  Find customers not from Los Angeles.

**

```
customers> db.customerdetails.find({city:{$ne:"los angeles"}})
[
  {
    _id: ObjectId("654ca4b30da73a2f96d37eec"),
    name: 'john',
    age: 25,
    gender: 'male',
    city: 'jaffna'
  },
  {
    _id: ObjectId("654ca4b30da73a2f96d37eed"),
    name: 'emily',
    age: 22,
    gender: 'female',
    city: 'london'
  },
  {
    _id: ObjectId("654ca4b30da73a2f96d37eee"),
    name: 'daniel',
    age: 28,
    gender: 'male',
    city: 'sydney'
  },
  {
    _id: ObjectId("654ca4b30da73a2f96d37eef"),
    name: 'sophia',
    age: 24,
    gender: 'female',
    city: 'paris'
  },
  {
    _id: ObjectId("654ca4b30da73a2f96d37ef0"),
    name: 'wiliam',
    age: 26,
    gender: 'male',
    city: 'chicago'
  },
  {
    _id: ObjectId("654ca4b30da73a2f96d37ef2"),
    name: 'benjamin',
    age: 27,
    gender: 'male',
    city: 'toronto'
  },
  {
    _id: ObjectId("654ca4b30da73a2f96d37ef3"),
    name: 'mila',
    age: 29,
    gender: 'female',
    city: 'berlin'
  },
  {
    _id: ObjectId("654cacc80da73a2f96d37ef5"),
    name: 'nilax',
    age: 23,
    gender: 'male',
    city: 'jaffna'
  }
]

```
**
10.Find the customers who are older than age 25.

**
```
customers> db.customerdetails.find({age:{$gt:25}})
[
  {
    _id: ObjectId("654ca4b30da73a2f96d37eee"),
    name: 'daniel',
    age: 28,
    gender: 'male',
    city: 'sydney'
  },
  {
    _id: ObjectId("654ca4b30da73a2f96d37ef0"),
    name: 'wiliam',
    age: 26,
    gender: 'male',
    city: 'chicago'
  },
  {
    _id: ObjectId("654ca4b30da73a2f96d37ef2"),
    name: 'benjamin',
    age: 27,
    gender: 'male',
    city: 'toronto'
  },
  {
    _id: ObjectId("654ca4b30da73a2f96d37ef3"),
    name: 'mila',
    age: 29,
    gender: 'female',
    city: 'berlin'
  }
]

```

**
11.Retrieve the males who are less than 25.

**
```
customer> db.customerdetails.find({$and:[{age:{$lt:25}},{gender:"male"}]})
[
  {
    _id: ObjectId("654d59299c7462baa06abdf3"),
    name: 'nilax',
    age: 23,
    gender: 'male',
    city: 'jaffna'
  }
]

```

** 12.Update Francis age to 35, if Francis is not available upsert. **
```

customer> db.customerdetails.update({name:"franics"},{$set:{age:30}},{uupsert:true})
{
  acknowledged: true,
  insertedId: ObjectId("654d69864ac3fbc6979cd606"),
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 1
}
customer> 

```

** 13.Retrieve males who are younger than 30 and older than25. **
```
customer> db.customerdetails.find({$and:[{gender:"male"},{age:{$gt:25,$lt:30}}]})
[
  {
    _id: ObjectId("654d58e09c7462baa06abdec"),
    name: 'daniel',
    age: 28,
    gender: 'male',
    city: 'sydney'
  },
  {
    _id: ObjectId("654d58e09c7462baa06abdee"),
    name: 'wiliam',
    age: 26,
    gender: 'male',
    city: 'chicago'
  },
  {
    _id: ObjectId("654d58e09c7462baa06abdf0"),
    name: 'benjamin',
    age: 27,
    gender: 'male',
    city: 'toronto'
  }
]
```

** 
14.Find a customer who is lesser than or equal to 23.
**
```
customer> db.customerdetails.find({age:{$lte:23}})
[
  {
    _id: ObjectId("654d58e09c7462baa06abdeb"),
    name: 'emily',
    age: 22,
    gender: 'female',
    city: 'london'
  },
  {
    _id: ObjectId("654d58e09c7462baa06abdef"),
    name: 'Olivia',
    age: 23,
    gender: 'female',
    city: 'los angeles'
  },
  {
    _id: ObjectId("654d59299c7462baa06abdf3"),
    name: 'nilax',
    age: 23,
    gender: 'male',
    city: 'jaffna'
  }
]
customer> db.customerdetails.find({age:{$lte:23}})
[
  {
    _id: ObjectId("654d58e09c7462baa06abdeb"),
    name: 'emily',
    age: 22,
    gender: 'female',
    city: 'london'
  },
  {
    _id: ObjectId("654d58e09c7462baa06abdef"),
    name: 'Olivia',
    age: 23,
    gender: 'female',
    city: 'los angeles'
  },
  {
    _id: ObjectId("654d59299c7462baa06abdf3"),
    name: 'nilax',
    age: 23,
    gender: 'male',
    city: 'jaffna'
  }
]
```
** 15.Remove the customer from Tokyo.**
```
customer> db.customerdetails.remove({name:"james",age:30,gender:"male",city:"tokyo"})
{ acknowledged: true, deletedCount: 0 }
```
