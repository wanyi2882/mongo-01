## Use the sample_training database

```
Project the company name and year founded and find by the criteria below:
```

* All companies founded in the year 2006,
```
db.companies.find({
    "founded_year": 2006
},{
    "name": 1,
    "founded_year": 1
})
```

* All companies founded after the year 2000
```
db.companies.find({
    "founded_year": {
        '$gt': 2000
    }
},{
    "name": 1,
    "founded_year": 1
})
```

* All companies founded between the year 1900 and 2010
```
db.companies.find({
    "founded_year": {
        '$gt': 1900,
        '$lt': 2010
    }
},{
    "name": 1,
    "founded_year": 1
})
```

Project the company name, the valuation amount and the valuation currency of its IPO, and find by the criteria below
```
* All companies with valuation amount higher than 100 million
```
db.companies.find({
    "ipo.valuation_amount": {
        "$gt": 100000000
    }
},{
    "name": 1,
    "ipo.valuation_amount": 1,
    "ipo.valuation_currency_code": 1
}).pretty()

```
* All companies with valuation amount higher than 100 million and with the currency being 'USD'

```
db.companies.find({
    "ipo.valuation_amount": {
        "$gt": 100000000
    },
    "ipo.valuation_currency_code": "USD"
},{
    "name": 1,
    "ipo.valuation_amount": 1,
    "ipo.valuation_currency_code": 1
}).pretty()
```


