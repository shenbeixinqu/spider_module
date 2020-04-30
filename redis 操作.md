## redis 操作

### redis 设置和查看密码

#### 初始化redis密码

```markdown
在配置文件中有个参数： requirepass  这个就是配置redis访问密码的参数；
比如 requirepass test123；
（Ps:需重启Redis才能生效）
redis的查询速度是非常快的，外部用户一秒内可以尝试多大150K个密码；所以密码要尽量长（对于DBA 没有必要必须记住密码）
```

#### 不重启redis设置密码

```markdown
redis 127.0.0.1:6379> config set requirepass 1234567
查询密码：
   redis 127.0.0.1:6379> config get requirepass
   (error) ERR operation not permitted
密码验证：
   redis 127.0.0.1:6379> auth 123456
再次查询：
   redis 127.0.0.1:6379> config get requirepass
   1) "requirepass"
   2) "test123"
```

### 登录redis

```markdown
redis-cli -p 6379 -a 123456
```

### 对string的操作

```shell
127.0.0.1:6379> exists hello // 查看key是否存在
(integer) 0
127.0.0.1:6379> set hello world // 设置hello-world
ok
127.0.0.1:6379> get hello // 获取hello的值
"world" 
127.0.0.1:6379> type hello // 值类型
string 
127.0.0.1:6379[2]> substr hello 1 2 // 获取substring
"or"
127.0.0.1:6379[2]> append hello ! // 字符串连接
(integer) 6
127.0.0.1:6379[2]> get hello
"world!"
127.0.0.1:6379> set haha heihei
OK
127.0.0.1:6379> keys h* // 返回满足条件的所有key
1) "hello"
3) "haha"
127.0.0.1:6379> randomkey // 随机返回一个key
"haha"
127.0.0.1:6379> rename hello hehe // 重命名key
OK
127.0.0.1:6379> expire haha 10
(integer) 1 // 设置haha的活动时间(s)
127.0.0.1:6379> ttl haha
(integer) 7 // 获取haha的活动时间
127.0.0.1:6379> get haha
(nil) // expire 时间到期后,该haha-heihei会删除
127.0.0.1:6379[2]> del hello
(integer) 0

```

### 对列表的操作

```shell
# redis在底层的实现实链表,因此, 无论list的空间复杂度是多少, 其时间复杂度是常数级别的. 即使用lpush在10个元素的list头部插入新元素, 和在上万个元素的lists头部插入新元素的速度相当. 但lists中的元素定位会比较慢.
# 常见操作有lpush, rpush, lrange等.
127.0.0.1:6379[2]> lpush list1 1 // 头部插入数据
(integer) 1
127.0.0.1:6379[2]> lpush list1 2 
(integer) 2
127.0.0.1:6379[2]> rpush list1 0 // 尾部插入数据
(integer) 3
127.0.0.1:6379[2]> lrange list1 0 1 // 列出编号0~1的元素
1) "2"
2) "1"
127.0.0.1:6379[2]> lrange list1 0 -1 // 列出编号0到倒数第一个的元素
1) "2"
2) "1"
3) "0"
127.0.0.1:6379[2]> llen list1 // lists长度
(integer) 3
127.0.0.1:6379[2]> lindex list1 1 // 根据index获取元素
"1"
127.0.0.1:6379[2]> ltrim list1 1 2 // 截取,仅保留编号1~2之间的元素
OK
127.0.0.1:6379[2]> lrange list1 0 10
1) "1"
2) "0"
127.0.0.1:6379[2]> lset list1 1 haha // 给1位置的元素赋值为haha
OK
127.0.0.1:6379[2]> lset list1 2 haha // 赋值,不能超出lists范围
(error) ERR index out of range
127.0.0.1:6379[2]> lrange list1 0 10
1) "1"
2) "haha"
127.0.0.1:6379[2]> rpush list1 haha
(integer) 3
127.0.0.1:6379[2]> rpush list1 haha
(integer) 4
127.0.0.1:6379[2]> lrange list1 0 10
1) "1"
2) "haha"
3) "haha"
4) "haha"
127.0.0.1:6379[2]> lrem list1 2 haha 删除2个值为haha的元素
(integer) 2
127.0.0.1:6379[2]> lrange list1 0 10
1) "1"
2) "haha"
127.0.0.1:6379[2]> lpop list1
"1"
127.0.0.1:6379[2]> lrange list1 0 10
1) "haha"
#  可以使用list来实现一个消息队列(如博客的评论内容),确保先后顺序
# 使用lrange还可以方便的实现分页功能
```

### 对set的操作

```shell
127.0.0.1:6379[2]> sadd set1 0 // 像set1中添加元素0
(integer) 1
127.0.0.1:6379[2]> sadd set1 1
(integer) 1
127.0.0.1:6379[2]> smembers set1 // 返回set1中的所有元素
1) "0"
2) "1"
127.0.0.1:6379[2]> scard set1 // 返回set的基数
(integer) 2
127.0.0.1:6379[2]> sismember set1 0 // 测试set1中是否包含元素0
(integer) 1
127.0.0.1:6379[2]> srandmember set1 // 随机返回一个元素
"0"
127.0.0.1:6379[2]> sadd set2 0
(integer) 1
127.0.0.1:6379[2]> sadd set2 2
(integer) 1
127.0.0.1:6379[2]> sinter set1 set2 // 求交集
1) "0"
127.0.0.1:6379[2]> sinterstore set3 set1 set2 // 保存交集到set3
(integer) 1
127.0.0.1:6379[2]> smembers set3
1) "0"
127.0.0.1:6379[2]> sunion set1 set2 // 求并集
1) "0"
2) "1"
3) "2"
127.0.0.1:6379[2]> sdiff set1 set2 // 求差集
1) "1"
127.0.0.1:6379[2]> sdiff set2 set1
1) "2"
```

### 对zset的操作

```shell
# zset是一种有序集合,其中每个元素都关联一个序号score
# 常见操作有 zrange zadd zrevrange
127.0.0.1:6379[2]> zadd zset1 1 dianping.com // 添加元素, score为1
(integer) 1
127.0.0.1:6379[2]> zadd zset1 2 baidu.com
(integer) 1
127.0.0.1:6379[2]> zadd zset1 3 qq.com
(integer) 1
127.0.0.1:6379[2]> zcard zset1 // 返回zset的基数
(integer) 3
127.0.0.1:6379[2]> zscore zset1 dianping.com // 返回元素的score
"1"
127.0.0.1:6379[2]> zrank zset1 dianping.com // 返回元素的rank
(integer) 0
127.0.0.1:6379[2]> zrange zset1 0 1 // 选取元素, score
从小到大
1) "dianping.com"
2) "baidu.com"
127.0.0.1:6379[2]> zrevrange zset1 0 1 // score从大到小
1) "qq.com"
2) "baidu.com"
127.0.0.1:6379[2]> zrem zset1 qq.com // 删除元素
(integer) 0

127.0.0.1:6379[2]> zincrby zset1 5 taobao.com // 如果元素不存在, 则添加该元素, 设置score为5
"5"
127.0.0.1:6379[2]> zcard zset1
(integer) 3
127.0.0.1:6379[2]> zincrby zset1 10 dianping.com // 如果元素存在, 则其score增加10
"11"
127.0.0.1:6379[2]> zrange zset1 0 10 withscores
1) "taobao.com"
2) "5"
3) "dianping.com"
4) "11"
# 此外, 还有zrevrank, zrevrange, zrangebyscore, zremrangebyrank, zramrangebyscore, zinterstore/zunionstore等操作.
```

### hash的操作

```shell
127.0.0.1:6379[2]> hset hash1 key1 value1 // 添加元素
(integer) 1
127.0.0.1:6379[2]> hget hash1 key1 // 获取元素的value
"value1"
127.0.0.1:6379[2]> hexists hash1 key1
(integer) 1
127.0.0.1:6379[2]> hset hash1 key2 value2
(integer) 1
127.0.0.1:6379[2]> hlen hash1
(integer) 2
127.0.0.1:6379[2]> hkeys hash1 // 获取hash1的所有key
1) "key1"
2) "key2"
127.0.0.1:6379[2]> hvals hash1 // 获取hash1的所有value
1) "value1"
2) "value2"
127.0.0.1:6379[2]> hmget hash1 key1 key2 // 获取元素
1) "value1"
2) "value2"
127.0.0.1:6379[2]> hgetall hash1 // 获取key/value
1) "key1"
2) "value1"
3) "key2"
4) "value2"
127.0.0.1:6379[2]> hset hash1 key3 10
(integer) 1
127.0.0.1:6379[2]> hincrby hash1 key3 5 // 将key3的value增加15(仅限整数)
(integer) 15
127.0.0.1:6379[2]> hmset hash1 key4 value4 key5 value5 // 批量添加元素
OK

```

### 其他操作

```shell
dbsize 查看所有key的数目
flushdb 删除当前选择数据库中的所有key
flushall 删除所有数据库中的所有key
save: 将数据同步保存到磁盘
bgsave: 异步保存
lastsave: 上次成功保存到磁盘的Unix时间戳
info: 查询server信息
config: 配置server
slaveof: 改变复制策略设置
```

### 参考

https://blog.csdn.net/icetime17/article/details/45767559