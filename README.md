# 執行 mongodb 與 express

```
    docker compose up -d
```

# 刪除容器

```
    docker compose down
```

# 停止容器

```
    docker compose down
```

# 進入 mongodb 容器

```
    docker exec -it mongo bash
```

# 進入 mongo 且登入設定的權限

```
    mongosh -u admin -p admin --authenticationDatabase admin
```

# 新增 db 與 collection 指令

```
    # 新增db
    use school

    # 查看db
    sohw dbs

    # 新增集合
    db.createCollection("students")

    # 查看集合
    show collections

    # 刪除db
    db.dropDatabase()

```

# 新增資料
```
    # 新增單筆資料
    db.students.insertOne({name:"Spongebob", age:30, gpa:3.2})

    # 新增多筆資料
    db.students.insertMany([{name:"Patrick", age:38, gpa:1.5},{name:"Edward", age:32, gpa:4.2},
    {name:"Sandy", age:18, gpa:2.2}])

    # 查詢集合的所有資料
    db.students.find()

    # 新增其他相關型態: 日期、陣列、物件...
    db.students.insertOne({
        name:"Larry", 
        age:32, 
        gpa:2.8, 
        fullTime: false, 
        registerDate:new Date(), 
        gradutionDate: null, 
        courses:["Biology", "Chemistry", "Calculus"], 
        address:{street:"123 Fake St.", city:"Bikini Bottom:, zip: 12345"}
    })
```

# 排序與限制
```
    # 排序:1升序，-1降序
    db.students.find().sort({gpa:1})
    db.students.find().sort({gpa:-1})

    # 限制:取1筆，取3筆
    db.students.find().sort({gpa:1}).limit(1)
    db.students.find().sort({gpa:-1}).limit(3)

```

# where 搜尋條件 .find({query}, {projection})
```
    # 使用條件
    db.students.find({ name: 'Larry'})

    # 只顯示想要印出的欄位
    db.students.find({}, {_id:false, name:true})

    # 大於、小於、等於
    db.students.find({ gpa: { $gt: 3 } })
    db.students.find({ gpa: { $lt: 2 } })
    db.students.find({ gpa: { $eq: 4.2 } })

    # OR、AND用法
    db.collection.find({
    $or: [
        { name: 'Larry' },
        { age: { $gt: 30 } }
        ]
    })
    db.collection.find({
    $and: [
        { name: 'Larry' },
        { age: { $gt: 30 } }
        ]
    })
```