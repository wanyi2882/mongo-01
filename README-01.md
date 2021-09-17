## to show all the databases on the server
```
show databases
```

## set the active database
```
use name_ofdb
```
example:
```
use sample_airbnb
```
to show all collections:
```
show collections 
```
show the corrent active database:
```
db
```
## queries:
To find/retrieve all the documents of a collection:
```
db.<name of collection>.find()
```
For example, to get all the listings and reivews (return first 10 results), type it it will show next 10
```
db.listingsAndReviews.find()
```
To beautify (ie. format) output
```
db.listingsAndReviews.find().pretty()
```

## Projection
Display only the centain keys from the document
```
db.listingsAndReviews.find({},
{
    "name": 1
}).pretty()
```

How to project by a field inside a nested object 
The first {} inside find is the criteria, empty means all criteria

```
db.listingsAndReviews.find({},
{
    "name": 1,
    "address.country":1
}).pretty()
```
db.listingsAndReviews.find({},
{
    "name": 1,
    "address.country":1,
    "beds": 1
}).pretty()

```
Show only the first 5 results
```
db.listingsAndReviews.find({},
{
    "name": 1,
    "address.country":1,
    "beds": 1
}).pretty().limit(5)

## Filtering

Specify criteria in the first argument of 'find'

Find all documents wherea specific key has a specific value

Example find all the listings that has exactly 2 beds ({criteria},{projections})

```
db.listingsAndReviews.find({
    "beds":2
},
{
    "name": 1,
    "beds": 1
}).pretty()
```

Searching by multiple criteria - find all with 2 beds and 2 bedrooms
```
db.listingsAndReviews.find({
    "beds":2,
    "bedrooms": 2
},
{
    "name": 1,
    "beds": 1,
    "bedrooms": 1
}).pretty()
```

Search in embedded key
```
db.listingsAndReviews.find({
    "beds":2,
    "bedrooms": 2,
    "address.country": "Canada"
},
{
    "name": 1,
    "beds": 1,
    "bedrooms": 1,
    "address.country": 1
}).pretty()
```

## Finding by inequality

We have to use the sepcial operators `$gt` for greater than
```
db.listingsAndReviews.find({
    "beds":{
        '$gt': 3
    }
},{
    "name": 1,
    "beds": 1
})
```
`$gt` = greater than
`$lt` = lesser than
`$gte` = greater than equal
`$lte` = greater than equal
`$ne` = not equal

```
Find all listings that have between 3 to 6 beds and are in Brazil:

```
db.listingsAndReviews.find({
    'beds':{
        '$gte':3,
        '$lte':6
    },
    'address.country':'Brazil'
},{
    'beds':1,
    'bedrooms':1,
    'address.country':1
}).pretty()

## Filtering by a key that is a array

Find one of the required in array `$in` which is or
```
db.listingsAndReviews.find({
    "amenities": {
        '$in': ["Oven", "Microwave", "Stove"]
    }
},{
    "name": 1,
    "amenities": 1
}).pretty()
```

Find `$all` fit all criteria in array
```
db.listingsAndReviews.find({
    "amenities": {
        '$all': ["Oven", "Microwave", "Stove"]
    }
},{
    "name": 1,
    "amenities": 1
}).pretty()
```

## Search by regular expression

Look for substring

* Find all the listings that the word `spacious` in the name
We use the the `$regex` operator
```

db.listingsAndReviews.find({
    'name': {
        '$regex': "spacious",
        '$options': "i"
    }
},{ 'name': 1
})
```
*Find all the listings where the name includes the phrase 'apartment for x', where x is a number between 1 to 9

```
db.listingsAndReviews.find({
    'name': {
        '$regex': "apartment for \[1-9]",
        '$options': "i"
    }
},{ 'name': 1
})
```
## Select by ObjectID

**The examples below uses the `sample_mflix` database**

```
use sample_mflix;
```

To find a document by its ObjectId:
```
db.movies.find({
    '_id':ObjectId("573a1390f29313caabcd5b9a")
}).pretty()
```

## Logical operators
We want to find listings that are either in Brazil or Canada.

```
db.listingsAndReviews.find({
    "$or":[
        {
            'address.country':"Brazil"
        },
        {
            'address.country':"Canada"
        }
    ]
}, {
    'name':1,
    'address.country':1
})
```
Find all the listings that are from Brazil and has at least 2 bedrooms or listings that are from Canada.

```
db.listingsAndReviews.find({
    "$or":[
        {
            "address.country":"Brazil",
            "bedrooms":{
                "$gte":3
            }
        },
        {
            "address.country":"Canada",
        }
    ]
},{
    'name':1,
    'address.country':1,
    'bedrooms':1
})
```

Use `$not` to do the inverse. Example: Show all the listings that are not from Brazil.

```
db.reviewAndListings.find({
   'address.country':{
       '$not':{
           '$in':['Brazil', 'Canada']
       }
   }
},{
    'name':1,
    'address.country':1
})
```

## Find by dates

Dates in Mongo are stored using `ISODate` objects.  The parameter used to create a `ISODate` object is the date in the `YYYY-MM-DD` format.
```
db.listingsAndReviews.find({
    'first_review':{
        '$gte':ISODate('2018-01-01')
    }
},{
    'name':1,
    'first_review':1
})
```

## creating your own database

1. create database
```
Use tgc14_animal_shelter
```
2. The new database is not permanent until we add a document to it.
3. To add a document to a new collection - just assume the collection exists and try to add to it
```
db.animals.insert({
    "name": "Fluffy",
    "age": 3,
    "breed": "Golden retriever",
    "type": "dog"
})
```

4. insert many at one go
```
db.animals.insertMany([
    {
    "name": "Daisy",
    "age": 5,
    "breed": "Greyhound",
    "type": "dog"
},
{
    "name": "Timmy",
    "age": 1,
    "breed": "Border Collie",
    "type": "dog"
}
])
```

5. How to enter with date:
```
db.animals.insert(
    {
    "name": "Teacup",
    "age": 9,
    "breed": "Persian Cat",
    "type": "cat",
    "date_enrolled": ISODate()
})
```

6. Give fix date
```
db.animals.insert(
    {
    "name": "Miranda",
    "age": 2,
    "breed": "Long-tailed Monkey",
    "type": "monkey",
    "date_enrolled": ISODate("2021-02-28")
})
```