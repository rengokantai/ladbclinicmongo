# ladbclinicmongo
## 1. Data and MongoDB in Five Min
### 2 Strengths and weaknesses of MongoDB
|Advantages|Disadvantages|
|---|---|
|can change the data structure|Data integrity issues|
|Can store different data together|Client responsible for data|
|Easy to add new fields|Hard to impose restrictions|

## 2. Create a Database
### 3 Explore the data structure
download file
```
wget https://data.ca.gov/sites/default/files/CA_DRU_proj_2010-2060.csv
```
### 4 Create a database in MongoDB
```
mongoimport --collection population --file CA_DRU_proj_2010-2060.csv --type csv --headerline
mongo
```
command
```
db.population.count()
```

```
db.accidents.aggregate([
  {$lookup:{
    from:"vehicles",
    localField:"Index",
    foreignField:"Index",
    as:"Vehicles"}
  },
  {$unwind:"$Vehicles"},
  {$project:{Index:1,Severity:1,_id:0,Type:"$Vehicles.Vehicle_Type"}},
  {$out:"combined"}
])
```
```
db.combined.find()
```
