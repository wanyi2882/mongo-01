## create database

1. Create Database
```
use fake_school
```
2. The new database is not permanent until we add a document to it.
3. To add a document to a new collection - just assume the collection exists and try to add to it
```
db.students.insertMany([
    {
    "name": "Jane Doe",
    "age": 13,
    "subjects": ["Defense Against the Dark Arts", "Charms", "History of Magic"],
    "date_enrolled": ISODate("2016-05-13")
},
    {
    "name": "James Verses",
    "age": 14,
    "subjects": ["Transfiguration", "Alchemy"],
    "date_enrolled": ISODate("2015-06-15")
},
    {
    "name": "Jonathan Goh",
    "age": 12,
    "subjects": ["Divination", "Study of Ancient Runes"],
    "date_enrolled": ISODate("2017-04-16")
}
])
```
## Hands on for update documents
* Increase the age of all the students by 1
```
db.students.updateMany({
},{
    "$inc": {
        "age": 1
        }
    }
)
```

* Change the date enrolled of Jonathan Goh to 2018 13th May
```
db.students.update({
    "_id": ObjectId("6144446f540ffeac25fc808e")
},{
    "$set":{
        "date_enrolled": ISODate("2018-05-13")
    }
})
```
* Change the age of James Verses to 13
```
db.students.update({
    "_id": ObjectId("6144446f540ffeac25fc808d")
},{
    "$set":{
        "age": 13
    }
})

```
* Change the student with the name of "Jane Doe" to "Jane Doe Jr" and her age to 11.

```
db.students.update({
    "name": "Jane Doe"
},{
    "$set":{
        "name": "Jane Doe Jr",
        "age": 11
    }
})
```
