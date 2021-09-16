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