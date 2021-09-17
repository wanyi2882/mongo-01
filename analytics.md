## Use the accounts document from the sample_analytics database and answer the following questions:

* Find all accounts that have the InvestmentStock product
```
db.accounts.find({
    "products":{
        "$in": ["InvestmentStock"]
    }
},{
}).pretty()

```
* Find all accounts that have both the Commodity and InvestmentStock product
```
db.accounts.find({
    "products":{
        "$all": ["InvestmentStock", "Commodity"]
    }
},{
}).pretty()
```

* Find all accounts that have either Commodity OR CurrencyService product
```
db.accounts.find({
    "products":{
        "$in": ["Commodity", "CurrencyService"]
    }
},{
}).pretty()
```

* Find all accounts that does not have CurrencyService product
```
db.accounts.find({
    "products":{
        "$not":{
            "$in": ["CurrencyService"]
        }
    }
},{
}).pretty()
```

* Find all products have a limit of more than 1000, and offer both InvestmentStock and InvestmentFund products
```
db.accounts.find({
    "limit":{
        "$gt": 1000
    },
    "products":{
            "$all": ["InvestmentStock", "InvestmentFund"]
    }
},{
}).pretty()
```