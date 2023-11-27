# 安装配置redis

`set nu`显示行号

```shell
tar -zxvf redis.7.2.1.tar.gz
#解压文件

cd redis-7.2.1
#进入目录

sudo apt-get install pkg-config
make && make install
#安装相应的配置

cd /usr/local/bin
#进入默认安装的位置
```

redis文件内容：

- redis-benchmark：性能测试工具
- redis-check-aof：修复有问题的AOF
- redis-check-dump：修复有问题的dump-rdb
- :star:redis-cli：客户端，操作入口
- redis-sentinel：redis集群使用
- :star:redis-server：服务器启动命令

```shell
mkdir /myredis
#在根目录下创建目录myredis

cd 桌面/opt/redis-7.2.1
cp redis.conf /myredis/redis7.conf
#将redis的配置文件复制到myredis中
```

```shell
chmod 666 /myredis/redis7.conf
#将文件改为可修改
```

**修改配置文件**

- daemonize no改为daemonize yes
- protected-mode yes改为protected-mode no

-  删除bind 127.0.0.1 -1::1

- 设置密码requirepass 123456

**启动服务**

```shell
redis-server /myredis/redis7.conf
ps -ef|grep redis|grep -v grep
#启动服务器

redis-cli -a 123456 -p 6379
#连接服务
```

**设置键值对**

```shell
set k v
#设置键值对

get k
#获取键所对应的值
```

**关闭服务**

```shell
redis-cli -a 123456 shutdown
#单实例关闭

redis-cli -p 6379 shutdown
#多实例关闭，指定端口关闭
```

# 数据类型

## String

- string 类型是二进制安全的。意思是 redis 的 string 可以包含任何数据。比如jpg图片或者序列化的对象。
- string 类型是 Redis 最基本的数据类型，string 类型的值最大能存储 512MB。

```shell
#nx 当key不存在时设置v1
127.0.0.1:6379[1]> set k1 v1 nx
OK
127.0.0.1:6379[1]> get k1
"v1"
#xx 当key存在时覆盖val
127.0.0.1:6379[1]> set k1 v1v1 xx
OK
127.0.0.1:6379[1]> get k1
"v1v1"

#ex time 设置过期时间
127.0.0.1:6379[1]> set k1 v1 ex 12
OK
127.0.0.1:6379[1]> ttl k1
(integer) 9
127.0.0.1:6379[1]> set k2 v2 px 8000
OK
127.0.0.1:6379[1]> ttl k2
(integer) 4
127.0.0.1:6379[1]> ttl k2
(integer) 1
127.0.0.1:6379[1]> ttl k2
(integer) -2

#keepttl 设置新值覆盖时，将原有的过期时间保留
127.0.0.1:6379> set k1 v1 ex 60
OK
127.0.0.1:6379> set k1 v2 keepttl
OK
127.0.0.1:6379> get k1
"v2"
127.0.0.1:6379> ttl k1
(integer) 34
```

```shell
#mset mget 同时设置多个键值对和获取多个值
127.0.0.1:6379> mset k1 v1 k2 v2 k3 v3 k4 v4
OK
127.0.0.1:6379> mget k1 k2 k3 k4 k5
1) "v1"
2) "v2"
3) "v3"
4) "v4"
5) (nil)

#getrange 获取一定范围内的值
#0 -1表示整个字符串
#setrange 在某个下标处替换值
127.0.0.1:6379> set k1 abcdefg
OK
127.0.0.1:6379> getrange k1 0 -1
"abcdefg"
127.0.0.1:6379> getrange k1 0 3
"abcd"
127.0.0.1:6379> setrange k1 0 123
(integer) 6
127.0.0.1:6379> get k1
"123bcd"

#strlen key获取值的长度
#append key val在末尾添加内容
127.0.0.1:6379> set k1 azxcv
OK
127.0.0.1:6379> strlen k1
(integer) 5
127.0.0.1:6379> append k1 qwert
(integer) 10
127.0.0.1:6379> get k1
"azxcvqwert"
```

## List

- 简单的字符串列表，按照插入顺序排序。可以添加一个元素到列表的头部（左边）或者尾部（右边）

```shell
#lpush list key从左侧依次压入元素
#rpush list key从右侧依次压入元素
127.0.0.1:6379> lpush list1 1 2 3 4 5
(integer) 5
127.0.0.1:6379> rpush list1 6 7 8 9 10
(integer) 10
#lrange 从左侧依次遍历
127.0.0.1:6379> lrange list1 0 -1
 1) "5"
 2) "4"
 3) "3"
 4) "2"
 5) "1"
 6) "6"
 7) "7"
 8) "8"
 9) "9"
10) "10"

#lpop list 左侧弹出一个元素
#rpop list 右侧弹出一个元素
127.0.0.1:6379> lpop list1 
"5"
127.0.0.1:6379> lrange list1 0 -1
1) "4"
2) "3"
3) "2"
4) "1"
5) "6"
6) "7"
7) "8"
8) "9"
9) "10"

#lindex key index 根据下标获取值
127.0.0.1:6379> lindex list1 1
"3"
```

```shell
#lrem list n val 删除n个val
127.0.0.1:6379> lpush list1 1 2 3 4 5 6 7 6 5 4 3 2 1
(integer) 13
127.0.0.1:6379> lrange list1 0 -1
 1) "1"
 2) "2"
 3) "3"
 4) "4"
 5) "5"
 6) "6"
 7) "7"
 8) "6"
 9) "5"
10) "4"
11) "3"
12) "2"
13) "1"
127.0.0.1:6379> lrem list1 2 1
(integer) 2
127.0.0.1:6379> lrange list1 0 -1
 1) "2"
 2) "3"
 3) "4"
 4) "5"
 5) "6"
 6) "7"
 7) "6"
 8) "5"
 9) "4"
10) "3"
11) "2"

#ltrim list start end
#根据下标截取元素，重新赋值给list
127.0.0.1:6379> ltrim list1 3 5
OK
127.0.0.1:6379> lrange list1 0 -1
1) "5"
2) "6"
3) "7"

#rpoplpush list1 list2
#将list1最后一个元素添加给list2
127.0.0.1:6379> lrange list1 0 -1
1) "1"
2) "2"
3) "3"
127.0.0.1:6379> lrange list2 0 -1
1) "4"
2) "5"
3) "6"
127.0.0.1:6379> rpoplpush list1 list2
"3"
127.0.0.1:6379> lrange list1 0 -1
1) "1"
2) "2"
127.0.0.1:6379> lrange list2 0 -1
1) "3"
2) "4"
3) "5"
4) "6"

#lset list index val
#给list特定下标设置值
127.0.0.1:6379> lset list1 0 a
OK
127.0.0.1:6379> lrange list1 0 -1
1) "a"
2) "2"

```



## Hash

- Redis hash 是一个键值(key=>value)对集合。

- Redis hash 是一个 string 类型的 field 和 value 的映射表，hash 特别适合用于存储对象。

**kv键值对，但v也是键值对**

```shell
#hset与hget
127.0.0.1:6379> hset user id 1 name aw age 20
(integer) 3
127.0.0.1:6379> hget user id
"1"
127.0.0.1:6379> hget user name
"aw"
127.0.0.1:6379> hget user age
"20"

#hexists key key1 判断key是否存在
127.0.0.1:6379> hexists user name
(integer) 1
127.0.0.1:6379> hexists user score
(integer) 0

#hkeys key 输出key
#hvals key 输出val
127.0.0.1:6379> hkeys user
1) "id"
2) "name"
3) "age"
127.0.0.1:6379> hvals user
1) "1"
2) "aw"
3) "20"

```



## Set

- Redis 的 Set 是 string 类型的无序集合。

- 集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是 O(1)

```shell
#sadd key val 添加多个val
127.0.0.1:6379> sadd set1 1 2 3 3 5 4
(integer) 5

#smembers key 显示所有val
127.0.0.1:6379> smembers set1
1) "1"
2) "2"
3) "3"
4) "4"
5) "5"

#sismember key val 判断val是否在key中
127.0.0.1:6379> sismember set1 6
(integer) 0
127.0.0.1:6379> sismember set1 1
(integer) 1

#scard key 统计key中的元素数量
127.0.0.1:6379> scard set1
(integer) 5

#srem key val 删除指定元素
127.0.0.1:6379> srem set1 5
(integer) 1
127.0.0.1:6379> smembers set1
1) "1"
2) "2"
3) "3"
4) "4"

#srandmember key n 随机展示n个val
127.0.0.1:6379> srandmember set1 3
1) "4"
2) "3"
3) "1"

#spop key n 随机弹出n个元素
127.0.0.1:6379> spop set1 2
1) "1"
2) "2"
127.0.0.1:6379> smembers set1
1) "3"
2) "4"

#smove key1 key2 num
#将key1中的num转移到key2中
127.0.0.1:6379> sadd set2 a b
(integer) 2
127.0.0.1:6379> smove set1 set2 4
(integer) 1
127.0.0.1:6379> smembers set1
1) "3"
127.0.0.1:6379> smembers set2
1) "b"
2) "a"
3) "4"
```

**集合的运算**

不改变原集合

```shell
127.0.0.1:6379> sadd set1 a b c 1 2
(integer) 5
127.0.0.1:6379> sadd set2 1 2 3 a d
(integer) 5

#sdiff key1 key2 删除key1中key2的元素
#差集
127.0.0.1:6379> sdiff set1 set2
1) "b"
2) "c"
127.0.0.1:6379> sdiff set2 set1
1) "d"
2) "3"

#sunion key1 key2 将两个key合并
#并集
127.0.0.1:6379> sunion set1 set2
1) "c"
2) "2"
3) "d"
4) "a"
5) "b"
6) "3"
7) "1"

#sinter key1 key2
#交集
127.0.0.1:6379> sinter set1 set2
1) "2"
2) "a"
3) "1"

```

## ZSet

- Redis zset 和 set 一样也是string类型元素的集合,且不允许重复的成员。

- 不同的是每个元素都会关联一个double类型的分数。redis正是通过分数来为集合中的成员进行从小到大的排序。

- zset的成员是唯一的,但分数(score)却可以重复。

相当于原来的v变成了k-v键值对

```bash
#zadd key score1 val1 score2 val2
#添加元素
127.0.0.1:6379> zadd z1 60 v1 70 v2 80 v3 10 v4
(integer) 4

#zrange key 展示元素、
#zrange key withscores展示元素和分数
127.0.0.1:6379> zrange z1 0 -1
1) "v4"
2) "v1"
3) "v2"
4) "v3"
127.0.0.1:6379> zrange z1 0 -1 withscores
1) "v4"
2) "10"
3) "v1"
4) "60"
5) "v2"
6) "70"
7) "v3"
8) "80"

#zrevrange key 逆序展示元素
127.0.0.1:6379> zrevrange z1 0 -1 withscores
1) "v3"
2) "80"
3) "v2"
4) "70"
5) "v1"
6) "60"
7) "v4"
8) "10"

#zrangebyscore key score1 score2
#展示[score1，score2]区间内的元素
127.0.0.1:6379> zrangebyscore z1 60 90 withscores
1) "v1"
2) "60"
3) "v2"
4) "70"
5) "v3"
6) "80"
#zrangebyscore key (score1 score2
#展示(score1，score2]区间内的元素
127.0.0.1:6379> zrangebyscore z1 (60 90 withscores
1) "v2"
2) "70"
3) "v3"
4) "80"
127.0.0.1:6379> zrangebyscore z1 60 (90 withscores
1) "v1"
2) "60"
3) "v2"
4) "70"
5) "v3"
6) "80"


#zscore key val 获取val对应的score
127.0.0.1:6379> zscore z1 v2
"70"

#zrem key val 删除val
127.0.0.1:6379> zrem z1 v2
(integer) 1
127.0.0.1:6379> zscore z1 v2
(nil)

#zcount key score1 score2
#统计[score1,score2]内的元素个数
127.0.0.1:6379> zrange z1 0 -1 withscores
1) "v4"
2) "10"
3) "v1"
4) "60"
5) "v2"
6) "60"
7) "v3"
8) "80"
127.0.0.1:6379> zcount z1 60 80
(integer) 3
```

## GEO

- 添加，获取地理位置的坐标
- 计算两个位置之间的距离
- 根据经纬度获取指定范围的地理位置集合

****

出现中文乱码解决方法

```shell
redis-cli -a 123456 --raw
```

****

```shell
# geoadd key longitude latitude location
# 给key添加经度纬度的地址
127.0.0.1:6379> geoadd city 16.403963 39.915119 "天安门"
0
127.0.0.1:6379> zrange city 0 -1
天安门

#geopos key location 返回经纬度
127.0.0.1:6379> geopos city 天安门
16.40396386384963989
39.91511970338637383

#geohash key location 哈希值编码
127.0.0.1:6379> geohash city 天安门
sr5ej6342j0
127.0.0.1:6379> geoadd city 116.403414 39.924091 "故宫"
1
#geodist key location1 lopcation2 
#返回两地之间的距离
127.0.0.1:6379> geodist city 天安门 故宫 m
8003990.4186

```





## HyperLogLog

- 基数统计算法，智慧根据输入的元素计算基数，而不会存储输入元素的本身。常用于统计网站的uv

**基数**：是一种数据集，去重复后的真实个数

```shell
#pfadd key val 添加数据
127.0.0.1:6379> pfadd hll01 1 3 5 5 7
(integer) 1

#pfcount key 返回基数值
127.0.0.1:6379> pfcount hll01
(integer) 5
127.0.0.1:6379> pfadd hll02 2 3 4 5 5 6
(integer) 1
127.0.0.1:6379> pfcount hll02
(integer) 5

#pfmerge key key1 key2 将key1和key2合并赋给key
127.0.0.1:6379> pfmerge dist hll01 hll02
OK
127.0.0.1:6379> pfcount dist
(integer) 7
```



## bitmap

- 由0和1状态表现的二进制bit数组

```shell
#setbit key index 0/1
#在index上设置0或1
127.0.0.1:6379> setbit k1 1 1
(integer) 1
127.0.0.1:6379> setbit k1 7 1
(integer) 1
127.0.0.1:6379> get k1
"A"

#getbit key index 获取下标index的val
127.0.0.1:6379> getbit k1 1
(integer) 1
127.0.0.1:6379> getbit k1 0
(integer) 0

#strlen key 返回key的大小，单位字节
127.0.0.1:6379> strlen k1
(integer) 1
127.0.0.1:6379> setbit k1 8 0
(integer) 0
127.0.0.1:6379> strlen k1
(integer) 2

```



## bitfield

- 一次性操作多个比特位域，执行一系列操作并返回一个响应数组

## Stream

- 发布订阅（pub/sub）可以分发消息，但无法记录历史消息。
- Redis Stream 提供了消息的持久化和主备复制功能，可以让任何客户端访问任何时刻的数据，并且能记住每一个客户端的访问位置，还能保证消息不丢失。

### 消息队列

```shell
# xadd stream *|id key val
#生成一个消息队列，并添加kv键值对
#*表示自动生成序号，或者可以使用id指定
#返回值前一部分是毫秒级的时间戳，后一部分是该时间戳下的第几条消息
#且序号必须是递增的
127.0.0.1:6379> xadd mystream * id 11 name za
1697628084816-0
127.0.0.1:6379> xadd mystream * id 12 name li4
1697628112850-0

#xrange stream - +
#从大到小返回消息队列
127.0.0.1:6379> xrange mystream - +
1) 1) "1697628084816-0"
   2) 1) "id"
      2) "11"
      3) "name"
      4) "za"
2) 1) "1697628112850-0"
   2) 1) "id"
      2) "12"
      3) "name"
      4) "li4"

#xrevrange stream - +
#从小到大返回消息队列
127.0.0.1:6379> xrevrange mystream + -
1) 1) "1697628112850-0"
   2) 1) "id"
      2) "12"
      3) "name"
      4) "li4"
2) 1) "1697628084816-0"
   2) 1) "id"
      2) "11"
      3) "name"
      4) "za"

#xdel stream id
127.0.0.1:6379> xdel mystream 1697628112850-0
(integer) 1
127.0.0.1:6379> xrange mystream - +
1) 1) "1697628084816-0"
   2) 1) "id"
      2) "11"
      3) "name"
      4) "za"

#xtrim stream maxlen n
#保留最大的n个消息
127.0.0.1:6379> xrange mystream - +
1) 1) "1697630165186-0"
   2) 1) "k1"
      2) "v1"
2) 1) "1697630193695-0"
   2) 1) "k2"
      2) "v2"
3) 1) "1697630201536-0"
   2) 1) "k3"
      2) "v3"
4) 1) "1697630215681-0"
   2) 1) "k4"
      2) "v4"
127.0.0.1:6379> xtrim mystream maxlen 2
(integer) 2
127.0.0.1:6379> xrange mystream - +
1) 1) "1697630201536-0"
   2) 1) "k3"
      2) "v3"
2) 1) "1697630215681-0"
   2) 1) "k4"
      2) "v4"

```



### 消费者组

```shell
```





# key操作命令

```shell
127.0.0.1:6379> set k1 v1
OK
127.0.0.1:6379> set k2 v2
OK
127.0.0.1:6379> set k3 v3
OK

#显示所有的键 keys *
127.0.0.1:6379> keys *
1) "k3"
2) "k1"
3) "k2"

#显示后面跟着的键存在的个数 exists key1,key2....
127.0.0.1:6379> exists k1
(integer) 1
127.0.0.1:6379> exists k1 k2 k3 k4
(integer) 3

#返回键的类型 type key
127.0.0.1:6379> type k1
string

#删除键，成功删除返回1，不成功返回0 del key
127.0.0.1:6379> del k3
(integer) 1
127.0.0.1:6379> del k4
(integer) 0

#非阻塞删除 unlink key
127.0.0.1:6379> unlink k2
(integer) 1

#查看键还有多少秒过期 ttl key
#-1表示永不过期
#-2表示已经过期
127.0.0.1:6379> ttl k2
(integer) -1

#为键设置过期时间 expire key time
127.0.0.1:6379> expire k1 20
(integer) 1
127.0.0.1:6379> ttl k1
(integer) 18
127.0.0.1:6379> ttl k1
(integer) -2

#每个redis都由16个数据库，编号0-15，默认使用的是0号数据库
127.0.0.1:6379> keys *
1) "list"
2) "k1"
3) "k2"
#将k1键移动到1号数据库 move key dbname
127.0.0.1:6379> move k1 1
(integer) 1
#使用1号数据库 select dbname
127.0.0.1:6379> select 1
OK
127.0.0.1:6379[1]> keys *
1) "k1"

#显示当前库的键的数量 dbsize
127.0.0.1:6379> dbsize
(integer) 2

#删除当前库 flushdb
127.0.0.1:6379> flushdb
OK
127.0.0.1:6379> keys *
(empty array)

#删除所有库 flushall
127.0.0.1:6379> flushall
OK
127.0.0.1:6379> select 1
OK
127.0.0.1:6379[1]> keys *
(empty array)
```

# 持久化

使用快照形式将数据和状态以文件的形式写到磁盘上，实现数据的保存。快照文件被称为RDB（dump.rdb)，RDB就是Redis DataBase的简称

## RDB配置

在redis7.conf修改

- 添加`save 5 2`          表示五秒钟修改两次则自动保存
- `dir ./dump`修改为`dir /myredis/dumpfiles`   修改自动保存路径

****

需要线创建文件夹`mkdir myredis/dumpfiles`

****

-  `dbfilename dump.rdb`修改为`dbfilename dump6379.rdb`     修改默认的文件名

## 保存文件

- 自动触发

```shell
#在redis.conf中添加配置
save seconds changes
# 多少秒触发多少次修改会自动保存
```

- 手动触发

```shell
#在命令行
bgsave
```

<font color='red'>只能使用bgsave，save会阻塞服务器直到完成持久化</font>

**修复文件**

```shell
redis-check-rdb /myredis/dumipfiles/dump6379.rdb
```

## RDB优化参数



## AOF

全称`append only file`以日志的形式记录每个写操作，只允许追加文件但不可以改写。再次启动redis时，会根据日志文件内容将所有指令再执行一边重新构建数据

默认情况下AOF时处于关闭状态

```shell
#开启AOF
appendonly yes
```

保存的文件名`appendonly.aof`

![5bbc6160e66a1a1acdf6cab89e391743](https://gitee.com/qiqibaba43/image/raw/master/202310221125993.png)

1. 客户端不断向服务器发送请求命令
2. 命令再到达Redis Server要先送入缓冲区，避免频繁的磁盘IO操作
3. 根据写回策略将命令写入磁盘
4. 为了避免文件膨胀，根据规则进行命令的合并（AOF的重写）
5. Redis Server重启后，从AOF载入数据

三种写回策略：默认everysec

- always：每个命令执行完，立即将日志写进磁盘
- everysec：每隔一秒将日志写入磁盘
- no：由操作系统决定

AOF产生的文件一共有三个

- base基本文件
- incr增量文件
- manifest清单文件

**修复文件**

```shell
redis-check-aof --fix appendonly.1.aof.incr
```

## 保存文件

**自动保存**

文件大小超过64mb，并且文件的大小较上次重写增长一倍

只保留可以恢复数据的最小指令集

比如

```shell
set k1 v1
set k1 v2
#最后有k1 v2 没有k1 v1
```

****

如果有aof则优先使用aof。不存在则使用rdb

****

# Redis事务

可以一次执行多个命令，本质是一组命令的集合。一个事务中的所有命令都会序列化，按顺序串行之执行不会被其他命令插入（放在一共队列中）

## 正常执行

```shell
#multi 开始，并将后续操作添加到队列中
127.0.0.1:6379> multi
OK
127.0.0.1:6379(TX)> set k1 v1
QUEUED
127.0.0.1:6379(TX)> set k2 v2
QUEUED
127.0.0.1:6379(TX)> set k3 v3
QUEUED
127.0.0.1:6379(TX)> incr count
QUEUED
#exec 结束，依次执行队列中的操作
127.0.0.1:6379(TX)> exec
1) OK
2) OK
3) OK
4) (integer) 1
```

## 放弃执行

语法错误，编译错误

```shell
127.0.0.1:6379> multi
OK
127.0.0.1:6379(TX)> set k1 v11
QUEUED
127.0.0.1:6379(TX)> set k2 v22
QUEUED
#discard 取消队列中的所有操作
127.0.0.1:6379(TX)> discard
OK
127.0.0.1:6379> get k1
"v1"
```

## 全体连坐

执行错误

```shell
127.0.0.1:6379> multi
OK
127.0.0.1:6379(TX)> set k1 v11
QUEUED
127.0.0.1:6379(TX)> set k2 v22
QUEUED
127.0.0.1:6379(TX)> set k3
(error) ERR wrong number of arguments for 'set' command
127.0.0.1:6379(TX)> exec
(error) EXECABORT Transaction discarded because of previous errors.
```

## 怨头债主

```shell
127.0.0.1:6379> multi
OK
127.0.0.1:6379(TX)> set k1 v11
QUEUED
127.0.0.1:6379(TX)> set k2 v22
QUEUED
127.0.0.1:6379(TX)> incr email
QUEUED
127.0.0.1:6379(TX)> exec
1) OK
2) OK
3) (error) ERR value is not an integer or out of range
127.0.0.1:6379> get k1
"v11"
```

## watch监控

Redis采用的是乐观锁。每次读取数据时不会上锁，但在更新的时候回判断其他用户是否更新该数据

```shell
127.0.0.1:6379> set k0 v0
OK
127.0.0.1:6379> set k1 v1
OK
127.0.0.1:6379> watch k0
OK
127.0.0.1:6379> multi
OK
127.0.0.1:6379> set k1 v11
QUEUED
127.0.0.1:6379(TX)> set k0 2
QUEUED
127.0.0.1:6379(TX)> exec
(nil)
127.0.0.1:6379> get k0
"1"
127.0.0.1:6379> get k1
"v1"
```

```shell
127.0.0.1:6379> set k0 1
OK
```

监控k0，执行`set k0 2`但未执行`exec`的时候，其他客户端修改了k0，就会导致队列中所有的操作失败

**执行完exec，之前添加的监控锁都会被取消**

# 管道

![a168bcf5b6972b4a15a85b4157fb6c74](https://gitee.com/qiqibaba43/image/raw/master/202310232006131.png)

只有Redis Server返回结果后，客户端才能发出下一个命令。中间多了RRT（Round Trip Time），频繁调用系统IO，Redis多次调用读写方法，性能差

![83f7f71bc8509418df8ea05087cf3622](C:\Users\任侠\Documents\Tencent Files\2962298936\nt_qq\nt_data\Pic\2023-10\Ori\83f7f71bc8509418df8ea05087cf3622.png)

管道可以一次性发送多条命令给服务器，服务器处理完毕后，通过一条响应将结果一次性返回，通过减少客户端与Redis之间的通信次数来降低往返延时事件

先创建文件`cmd.txt`，文件内容：

```shell
set k1 v1
set k2 v2
hset k33 name aw
hset k33 age 20
hset k33 gender male
lpush list 1 2 3 4 5
```

```shell
renxia@renxia-virtual-machine:~$ cat cmd.txt
set k1 v1
set k2 v2
hset k33 name aw
hset k33 age 20
hset k33 gender male
lpush list 1 2 3 4 5
renxia@renxia-virtual-machine:~$ cat cmd.txt|redis-cli -a 123456 ---pipe
renxia@renxia-virtual-machine:~$ cat cmd.txt|redis-cli -a 123456 --pipe
All data transferred. Waiting for the last reply...
Last reply received from server.
errors: 0, replies: 6

127.0.0.1:6379> get k1
"v1"
127.0.0.1:6379> get k2
"v2"
127.0.0.1:6379> hgetall k33
1) "name"
2) "aw"
3) "age"
4) "20"
5) "gender"
6) "male"
127.0.0.1:6379> lrange list 0 -1
 1) "5`"
 2) "4"
 3) "3"
 4) "2"
 5) "1"
```

# 复制

配置文件`redis.conf`

主机6379

```shell
daemonize yes
#bind 127.0.0.1 -::1
protected-mode no
port 6379
dir /myredis
pidfile /var/run/redis_6379.pid
logfile "/myredis/6379.log"
requirepass 123456
dbfilename dump6379.rdb
```

从机6380，6381

<font color="red">从机访问主机的密码</font>

```shell
replicaof 192.168.111.185 6379
#指定主机的ip地址和端口号
masterauth "123456"
#设置从机访问主机的同行密码
```

`info replication`查看配置信息

- 写操作只能在主机中进行，从机只能读操作
- 从机没有启动一样可以获得主机写入的数据
- 主机shutdown后，重启后还是主机

```shell
slaveof 主机号 端口号
```

命令行设置与配置文件设置的区别
命令行是一次性的，重启之后就恢复原样。配置文件是永久的

 当一台redis服务器既是master，又是slave。但他不能进行写操作

三种常见的关系：

- 一主多从
- 一脉相承
- 反客为主

# 哨兵

哨兵作用：

- 主从监控：监控主从redis库运行是否正常
- 故障转移：当master发生shutdown，根据投票数将slave变成新的master
- 消息通知：将故障转移结果发送给客户端
- 配置中心：客户端通过哨兵获取redis主节点

## 配置文件

哨兵sentinel

```shell
sentinel monitor <master-name> <ip> <redis-port> <quorum>
# 设置需要监控的master主机
# quorum表示最少有几个哨兵认可客观下线，同意故障迁移的法定票数。哨兵可能因为网络阻塞误认为主机下线。需要多个哨兵一起确定主机是否已经下线

sentinel auth-pass <master-name> <password>
# 连接master的密码
```

## 运行哨兵

```
redis-sentinel sentinel26379,conf -sentinel
```

当原master下线后恢复，不会重新称为master而是变成slave

## 故障处理

当达到投票数后，再由哨兵根据raft算法选出一个主哨兵。主哨兵指定新的master

指定master的标准：

- 权限
- 赋值偏移量
- Run ID

# 集群

由于数据量过大，单个master复制集难以承担，需要对多个复制集进行集群，形成只负责存储数据的一部分。提供在多个redis节点之间共享数据的程序结

## 作用

- Redis集群支持多个master，每个master又可以挂载多个slave
- 集群自带哨兵的故障转移机制，不需要再使用哨兵
- 客户端与redis的节点连接，不再需要连接集群中的所有节点，只需要任意连接集群中的任一可用节点即可
- 槽位slot负责分配到各个物理服务节点，由对应的集群负责维护节点，插槽和数据之间的关系

## 槽位

没有使用哈希算法，使用了一种叫做哈希槽的概念。

Redis集群由16384个哈希槽，每个key通过CRC16校验，对16384取模来决定放置在哪个槽中，集群的每个节点负责一部分的哈希槽

一般槽位最多设置一千个

## 分片

将存储的数据分布到多个Redis机器上，这称为数据集合分片。每次数据增加减少，或者增加节点。只需要改变分片即可

**哈希取余**

对节点的个数取模

缺点：增加或减少节点数时，所有键值对对应的节点都需要重新计算

**哈希一致性算法**

将线性区间$[0,2^{32}-1]$抽象为逻辑上的闭环，使得$0=2^{32}$，将redis节点均匀分布在闭环上，计算键值对的哈希值，找到在闭环上的位置，然后顺时针遇到的第一个节点服务器就是该键值对所存储的服务器

优点：

- 容错性高，当某节点服务器不可用，直接将该节点对应的分片转移到下一台服务器中
- 扩展性高，当新增节点，只需要将一部分数据重新添加进新的服务器

缺点：当节点分布不均匀，会导致数据倾斜

**哈希槽算法**

使用16384个槽位作为中间件，将数据存储到槽位中，槽位平均分配给每个主机

## 配置集群

```shell
mkdir -p /myredis/cluster

vim /myredis/cluster/redisCluster6381.conf

binding 0.0.0.0

daemonize yes

protected-mode no

port 6381

logfile "/myredis/cluster/cluster6381.log"

pid /myredis/c;uster6381.pid

dir /myredis/cluster

dbfilename dump6381.rdb

appendonly yes

appendfilename "appendonly6381.aof"

requirepass 123456

masterauth 123456

cluter-enabled yes

cluster-config-flie nodes-6381.conf

cluster-node-timeout 5000
```

**启动服务**

```bash
redis-cli -a 123456 --cluster create --cluster-replicas 1 ip port
# --cluster create 以集群的形式创建
# --cluster-replicas 1 为每个master创建一共slave节点
```



# 线程

redis一开始是单线程，redis4之后才开始逐渐支持多线程

**Redis是单线程**

主要指网路IO和键值对读写由一个线程完成。Redis在处理客户端的请求时由一个主线程执行。

但在执行AOF，RDB持久化，异步删除时，是由额外的线程执行的

命令工作线程是单线程的，但整个redis是多线程的

**高并发和快速执行**

- redis是基于内存的，内存的读写速度非常快（纯内存）; 数据存在内存中，数据结构用HashMap，HashMap的优势就是查找和操作的时间复杂度都是O(1)。

- redis是单线程的，省去了很多上下文切换线程的时间（避免线程切换和竞态消耗）。

- redis使用IO多路复用技术（IO multiplexing, 解决对多个I/O监听时,一个I/O阻塞影响其他I/O的问题），可以处理并发的连接（非阻塞IO）。
- redis的数据结构都比较简单，属于key-value型数据库，大部分操作都是O（1）。

**Redis4之前使用单线程的原因**

- 单线程维护开发更简单
- IO多路复用和非阻塞IO可以处理并发的多客户端请求
- 主要的性能瓶颈是内存和网络带宽，而不是CPU

**为什么转多线程--删除大数**

删除大数据（包含多个kv键值对），会导致主线程卡顿。使用惰性删除可以有效解决。

****

惰性删除：所有数据过期但保留不删除。只有在查询数据，当数据没有过期时，直接返回数据；当数据过期时，删除数据，然后返回不存在。

利用空间换取时间

****

或者使用`unlink``flushdb async`将删除操作交给子线程执行

**多线程特性&IO多路复用**

随着网络性能的提升，Redis的性能瓶颈可能出现在网络IO上，即单个主线程处理网络请求速度跟不上网络硬件的处理速度。

采用了多个IO线程处理网络iqngiqu，提高网络并行度

- 阻塞IO
- 非阻塞IO
- IO多路复用：IO指数据在内核态和用户态之间读写，一个服务器进程可以处理多个套接字描述符。实现的模型由三种：select->pol->epoll
- 信号驱动IO
- 异步IO

Redis多线程机制默认是关闭的，如果要开启，在redis.conf中修改配置

```shell
io-threads 4
io-threads-do-reads yes
```



# bigkey
