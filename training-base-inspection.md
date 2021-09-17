## Training Database Inspection Collections

* Find all businesses which has violations issued

```
db.inspections.find({
    "result": "Violation Issued"
},{
}).pretty()

```

* Find all business which has violations, and are in the city of New York.

```
db.inspections.find({
    "result": "Violation Issued",
    "address.city": "New York"
},{
}).pretty()

```
* Count how many businesses there in the city of New York

```
db.inspections.count({
    "address.city": "New York"
},{
})

```
* Count how many businesses there are in the city of Ridgewood and does not have violations (hint: google for "not equal" in Mongo)

```
db.inspections.count({
    "address.city": "Ridgewood",
    "result": {
        "$ne": "Violation Issued"
    }
},{
})

```