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