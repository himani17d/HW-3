# Assignment-3-DSO-553

#### Question 1

#### A.

##### There are 2 stages in the pipeline
```
db.orders.aggregate( [
 { $group: { _id: "$productName", sumQuantity: { $sum: "$quantity" } } },
 { $sort : { product_name : 1 } }
] )
```

#### B.

##### There are 3 stages in the pipeline
```
db.orders.aggregate( [
 { $match: { status: "urgent" } },
 { $group: { _id: "$productName", sumQuantity: { $sum: "$quantity" } } }
] )
```

#### C.


##### There are 2 stages in the pipeline
```
db.orders.aggregate( [
 { $group: { _id: {
            "productName": "$productName",
            "status": "$status"}, 
            sumQuantity: { $sum: "$quantity" } } },
    { $sort : { product_name:1, status : 1 } }
    
    
] )
```

#### D.

##### There are 2 stages in the pipeline

```
db.orders.aggregate( [
 { $group: { _id: {
            "productName": "$productName",
            "status": "$status"
        }, sumQuantity: { $sum: "$quantity" } } },
    { "$match" : { 
        "sumQuantity" : { "$gte" : 15 } 
    } },
    { $sort : { status : -1,product_name:-1 } }
] )
```



#### Question 2


#### A.

###### There are 1,00,000 classes in the collection grades

```
db.grades.aggregate( [
   { $count: "myCount" }
])
```

#### B.

###### There are 10,000 unique students in the collection grades

```
db.grades.distinct("student_id").length
```

#### C.

##### The average of exam scores is 49.32031796981391

```
db.grades.aggregate( [{ $match: { class_id: 212} },
   {
     $unwind: { path: "$scores"}
    },
    {
     $group:
        {
          _id: ["$scores.type"],
          average: { $avg: "$scores.score" }
        }
    },
    {$match:{_id:"exam"}}
 ] )
```

#### D.

##### The standard deviation of exam scores is 29.280553806350333

```
db.grades.aggregate( [{ $match: { class_id: 212} },
   {
     $unwind: { path: "$scores"}
    },
    {
     $group:
        {
          _id: ["$scores.type"],
          Standard_deviation: { $stdDevPop: "$scores.score" }
        }
    },
    {$match:{_id:"exam"}}
 ] )
```





