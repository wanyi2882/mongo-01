## Add in the following pets:
Name: Jorden,
Age: 15
Breed: Golden Retriever
Species: dog

Name: Dash
Age: 3
Breed: Hamster
Species: Hamster

Name: Carrot
Age: 1.5
Breed: Australian Dwarf
Species: Rabbit

## Create database
use pet_database

## add collection and documents

```
db.pets.insertMany([
    {
    "name": "Jorden",
    "age": 15,
    "breed": "Golden Retriever",
    "species": "dog"
},
{
    "name": "Dash",
    "age": 3,
    "breed": "Hamster",
    "species": "Hamster"
},
{
    "name": "Carrot",
    "age": 1.5,
    "breed": "Australian Dwarf",
    "species": "Rabbit"
}
])
```

## Change Carrot's age to 2.5
```
db.pets.update({
    "_id": ObjectId("61445a1e540ffeac25fc8097")
},{
    "name": "Carrot",
    "age": 2.5,
    "breed": "Australian Dwarf",
    "species": "Rabbit"
})
```

## Replace Dash the hamster's information (using the PUT method) with the following:
Name: Dash
Age: 4.5
Breed: Winter White
Species: Hamster

```
db.pets.update({
    "_id": ObjectId("61445a1e540ffeac25fc8096")
},{
    "name": "Dash",
    "age": 4.5,
    "breed": "Winter White",
    "species": "Hamster"
})
```

## Delete Jorden, because it went to the rainbow bridge due to old age.
```
db.pets.remove({
    "_id": ObjectId("61445a1e540ffeac25fc8095")
})
```
