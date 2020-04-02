## pymongo

 ### 连接数据库

```python
import pymongo

client = pymongo.MongoClient(host='localhost',port=27017)

db = client.test
collection = db.students
```

### 插入数据

![img](https://s0.lgstatic.com/i/image3/M01/77/43/Cgq2xl5x2QeASAC7AADAk5bdEIY371.png)

运行结果:![img](https://s0.lgstatic.com/i/image3/M01/77/42/CgpOIF5x2QeAA052AACEfhuBIa0700.png)

### 查询

插入数据后，我们可以利用 find_one 或 find 方法进行查询，其中 find_one 查询得到的是单个结果，find 则返回一个生成器对象。

![img](https://s0.lgstatic.com/i/image3/M01/77/43/Cgq2xl5x2QiAaDGCAABzgeApOuM757.png)

运行结果:

我们也可以根据 ObjectId 来查询，此时需要调用 bson 库里面的 objectid：

![img](https://s0.lgstatic.com/i/image3/M01/77/43/Cgq2xl5x2QmAQ_T5AACyW1Bb18A763.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/77/42/CgpOIF5x2QmAAl5iAADX1DQdoSk170.png)

对于多条数据的查询，我们可以使用 find 方法。例如，这里查找年龄为 20 的数据

![img](https://s0.lgstatic.com/i/image3/M01/77/43/Cgq2xl5x2QmASS8uAAB_goSj87U859.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/77/42/CgpOIF5x2QqAAmNFAAKL7FcbguU871.png)

查询年龄大于20:

![img](https://s0.lgstatic.com/i/image3/M01/77/43/Cgq2xl5x2QqAB9C7AABSLRyrOzQ371.png)

### 比较符号

![img](https://s0.lgstatic.com/i/image3/M01/77/5E/Cgq2xl5x83iAAn4RAAEsbDKOSTc291.png)

### 计数

![img](https://s0.lgstatic.com/i/image3/M01/77/43/Cgq2xl5x2QqAMo5tAABMqUJTb28040.png)

![img](https://s0.lgstatic.com/i/image3/M01/77/42/CgpOIF5x2QqAJ94tAABgKYUiBcE785.png)

### 排序

![img](https://s0.lgstatic.com/i/image3/M01/77/43/Cgq2xl5x2QuAAtTnAACHNz2Q7wU394.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/77/43/Cgq2xl5x2QuAUR6iAABCR5Cfaf4375.png)

### 偏移

在某些情况下，我们可能只需要取某几个元素，这时可以利用 skip 方法偏移几个位置，比如偏移 2，就代表忽略前两个元素，得到第 3 个及以后的元素：

![img](https://s0.lgstatic.com/i/image3/M01/77/43/CgpOIF5x2QuAShiQAACTgqHdpd4390.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/77/43/CgpOIF5x2QuAQT5EAAAvCcNmuGI295.png)

我们还可以用 limit 方法指定要取的结果个数

![img](https://s0.lgstatic.com/i/image3/M01/77/43/Cgq2xl5x2QuAGic_AACb-bARyMA665.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/77/43/CgpOIF5x2QyAAfY8AAAoKiLgiP0381.png)

### 更新

![img](https://s0.lgstatic.com/i/image3/M01/77/43/CgpOIF5x2QyAWgSaAACvZHpygwU295.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/77/43/Cgq2xl5x2QyAIywJAABRYXL2h4o272.png)

返回结果是字典形式，ok 代表执行成功，nModified 代表影响的数据条数。

另外，我们也可以使用 $set 操作符对数据进行更新，

![img](https://s0.lgstatic.com/i/image3/M01/77/43/CgpOIF5x2QyAB0kIAABWjJCLkgM205.png)

![img](https://s0.lgstatic.com/i/image3/M01/77/43/Cgq2xl5x2Q2Ac-DYAADAONA6aCs205.png)

这里指定查询条件为年龄大于 20，然后更新条件为 {'$inc': {'age': 1}}，表示年龄加 1，执行之后会将第一条符合条件的数据年龄加 1。

运行结果如下：

![img](https://s0.lgstatic.com/i/image3/M01/77/43/Cgq2xl5x2Q2AO3oHAABh46obF64598.png)

可以看到匹配条数为 1 条，影响条数也为 1 条。

如果调用 update_many 方法，则会将所有符合条件的数据都更新

![img](https://s0.lgstatic.com/i/image3/M01/77/43/CgpOIF5x2Q2AV04wAADDq1iOQXI112.png)

![img](https://s0.lgstatic.com/i/image3/M01/77/43/Cgq2xl5x2Q2AcfgEAABlqM7BsrU731.png)

### 删除

![img](https://s0.lgstatic.com/i/image3/M01/77/43/Cgq2xl5x2Q6AFExLAABdakOVIRc981.png)

![img](https://s0.lgstatic.com/i/image3/M01/77/43/CgpOIF5x2Q6AObujAAAkXjolx0s454.png)

