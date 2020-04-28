	## mongodb操作

### mongodb数据库的创建与删除

#### 创建使用数据库

```shell
use student
# 如果之前没有这个数据库，当前为创建一个新的数据库，那么必须插入一条数据，才能保证数据库创建成功。
# 数据库中不能直接插入数据，只能往集合(collections)中插入数据。
# 不需要专门创建集合，只需要声明集合并插入数据就会创建成功(以下示例均已user集合为例)
db.user.insert({"name":"augus"});
```

#### 显示当前数据库中的数据集合

```shell
show collections
```

#### 删除当前所在的数据库

```shell
db.dropDatabase()
db.user.drop()
```

### 向数据库中插入数据

```shell
db.user.insert({"name":"augus"})
```

### 数据库查找数据

#### 查询所有记录

```shell
db.user.find()
# 美化查询出的所有记录
db.user.find().pretty()
```

#### 查询当前集合中的某列去重后的数据

```shell
db.user.insert({"name":"augus","age":21})
db.user.insert({"name":"augus","age":23})
db.user.insert({"name":"kivi","age":22})

db.user.distinct("name")
[ "augus", "kivi" ]
```

####  查询age=22的记录

```shell
db.user.find({"age":22})
```

#### 查询年龄大于22的记录

```shell
db.user.find({age:{$gt:21}})
```

#### 查询age>=25的记录

```shell
db.user.find({age:{$gte:25}})
```

#### 查询age>=23并且age<=26

```shell
db.user.find({age:{"$gte":21,"$lte":23}})
```

#### 查询name中包含mongo的数据,多用于模糊查询搜索

```shell
db.user.find({name:/mongo/})
```

#### 查询 name 中以 mongo 开头的数据

```shell
db.user.find({name:/^mongo/})
```

查询指定列 name、age 数据， 并且age > 25

```shell
# name 也可以用 true 或 false，ture 的情况下与name:1 效果一样，如果用 false 就 是排除 name，显示其它列的信息。db.user.find({age: {$gt: 25}}, {name: 1});
db.user.find({age: {$gt: 25}}, {name: 1});
# 这样只会显示name的查询结果
{ "_id" : ObjectId("5ea78ecc6c68fa2f46774c18"), "name" : "augus" }
{ "_id" : ObjectId("5ea78eea6c68fa2f46774c19"), "name" : "kivi" }
```

#### 按照列排序 1 升序 -1 降序

```shell
db.user.find().sort({age:1})
```

#### 查询 name = kivi, age = 22 的数据

```shell
 db.user.find({"name":"kivi","age":22})
```

####  查询前 3条数据

```shell
db.user.find().limit(3)
```

####  查询 4条以后的数据

```shell
db.user.find().skip(4)
```

#### 查询3-6之间的数据

```shell
db.user.find().limit(6).skip(3)
```

#### OR 查询

```shell
db.user.find({$or:[{age:21},{age:22}]})
```

#### findOne 查询第一条数据

```shell
db.user.findOne()
```

### 查询某个结果集的记录条数，用于统计数量

```shell
db.user.find({age:{$gt:21}}).count()
```

### 更新数据

#### 查找名字为kivi的，把年龄更改为 30 岁

```shell
db.user.update({"name":"kivi"},{$set:{age:30}})
```

#### 查找所有性别为男的用户把年龄都改为 33 岁

```shell
db.user.update({"sex":"男"},{$set:{"age":32}},{multi:true})
```

####  查找name为kivi的用户,将其年龄增加50岁

```shell
db.user.update({"name":"kivi"},{$inc:{"age":50}})
```

#### 查找name为kivi的用户,将其年龄增加20岁,姓名改为kiviss

```shell
db.user.update({"name":"kivi"},{$inc:{"age":20},$set:{"name":"kiviss"}})
```

### 数据库删除数据

####  删除年龄为32的所有用户

```shell
db.user.remove({"name":21})
```

#### 删除年龄为32的一个用户

```shell
db.user.remove( { "age": "32" }, { justOne: true } )
```

