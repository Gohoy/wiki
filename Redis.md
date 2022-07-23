## Redis

> #### Redis 是什么

Redis  (**Re**mote **Di**ctionary **S**erver) , 即远程字典服务

c语言编写,支持网络

Key:Value型数据库

> #### Redis 能做什么

* 内存存储,持久化(rdb,aof)
* 效率高,用于告诉缓存
* 发布订阅系统
* 地图信息分析
* 计时器,计数器(浏览量)

> #### 特性

* 多样的数据类型
* 持久化
* 集群
* 事务

> #### 网站

* [官网]( https://redis.io/)
* [中文网](http://www.redis.cn)

> #### 基本操作
>
> Redis 不区分大小写

* `ping` 测试链接
* `set name gohoy`存储键值对 name:gohoy
* `get name`获取name的值
* `shutdown`关闭redis
* `redis-benchmark`  官方的压力测试工具

```bash
# 测试: 100并发连接  100000请求
redis-benchmark -h localhost -p 6379 -c 100 -n 100000
```

* `select 3`切换第三个数据库(redis默认有16个数据库,默认使用的第0个数据库)
* `dbsize`获取当前数据库的大小
* `keys *` 查看所有的key
* `flushdb`清空当前数据库
* `flushall`清空所有数据库
* `expire name 10`10秒后name键失效
* `move name 1`将name键移除数据库1
* `ttl name`查看当前key的剩余时间
* `type name`查看name 类型
* `exists name`判断name是否存在
* 

> #### redis 五大数据类型

**String**(字符串)

* `append name "11"` 给name后面追加字段,如果没有该字段相当于set
* `strlen name`获取name值的长度
* 实现数据增加
  * `set views 0`
  * `incr views` 现在views 是1
  * `decr views` 现在views 是0
  * `incrby views 10`现在views 是10
  * `decrby views 5`现在views 是 5 
* 实现截取字符串
  * `set name "gohoy"`
  * `getrange name 0 2`截取第0个到第2个,结果是"goh"
  * `getrange name 0 -1`查看所有字符串

* 实现替换字符串
  * `setrange name 1 oo`从第一位将oo替换后面的字符串,结果是 "goooy"
* `setex name 30 "gohoy"` (set with expire)设置过期时间,name在30秒后清空
* `setnx name "gohoy"` (set if not exist),设置成功返回1 ,否则返回0
*  `mset k1 v1 k2 v2 k3 v3`一次创建3个量k1 k2 k3
* `msetnx k1 v1 k4 v4` k1无法设置,k4也没有设置成功,msetnx是一个原子操作,要么一起成功,要么一起失败.
* `meset user:1:name  gohoy  user:1:age 3`设置一个对象user:1 其属性 name 和age
* `getset name gohoy1`返回当前的值并设置新的值,返回gohoy 再次get返回 gohoy1

**List**(列表) 可以做栈,队列,阻塞队列

* 所有的list命令都是用**l**开头的
* `lpush list one`在list头部(左) 存入 one
* `Rpush list right`在list尾部(右) 存入 right
* `Lrange list 0 -1`取出list所有的值 
* `Lpop list`移除list第一个(最左)元素
* `Rpop list`移除list 的最后一个元素(最右)
* `Lindex list 0`取出list 第一个值
* `Llen list`获取list 长度
* `Lrem list 1 one`移除list 中 1个one(元素可以重复)
* `Ltrim list  1 2 `通过下标截取list中第二个和第三个元素,list被改变
* `rpoplpush list list1`移除list列表最后一个元素并存到list1
* `Lset list 0 item` 将list 中第一个元素更新为item,如果不存在该下标的元素会报错
* `Linsert list before(after) "one" "two"`在list中将"one"前面(后面)插入"two"

**Set(集合)**set中的值不能重复

* `Sadd myset "hello"`在myset 加入"hello"
* `Smembers myset `查看myset中的元素
* `Sismember myset world`判断 world 是否是在myset中,存在返回1 否则返回0
* `Scard myset`获取myset 值的个数
* `Srem myset hello`删除myset中的hello
* `SrandMember myset 2`随机从myset 中抽取2个元素
* `Spop myset`随机删除myset的一个元素
* `Smove myset myset2 "hello"`将hello 移动到myset2
* `Sdiff  myset1 myset2`求出myset1 myset2 的差集
* `Sinter myset1 myset2 `求出 myset1 myset2 的交集
* `Sunion myset1 myset2` 求出 myset1 myset2 的并集

**Hash(哈希)**Map<key : value>

* `Hset myhash field1 gohoy`在myhash里面存入<field :  gohoy>
* `Hget myhash field1` 
* `Hmset myhash field1 gohoy field2 gohoy2`同时存入多个
* `Hmget myhash field1 field2`同时取出多个
* `Hgetall myhash`取出myhash 所有的值
* `Hdel myhash field1` 删除myhash中的 field1键,其对应的值也消失
* `Hlen myhash`myhash 中键值对的个数
* `Hexists myhash field1`myhash中是否存在field1键
* `Hkeys myhash`获取所有键
* `Hvals myhash`获取所有值
* `Hinrcby myhash field3 1`field3 增加1
* `Hsetnx myhash field4  hello`不存在可以创建,否则不行
* `Hset user:1 name:gohoy age:3`
* `Hget user:1 name`

**ZSet(有序集合)**在set的基础上增加了一个值	`k1 score1 v1`

 * `Zadd myset 1 one`

 * `Zadd myset 2 two 3 three`

 * `Zrange myset 0 -1`

 * `ZRangeByScore myset -inf +inf `从最小到最大排序

 * `ZRevRange myset +inf -inf`从大到小排序

 * `ZRangeByScore myset -inf +inf withscores`结果显示scores

 * `ZRangeByScore myset -inf 2000` score2000以下的排序

 * `Zrem myset one`移除myset 中的one

 * `Zcard myset`获取myset元素个数

 * `Zcount myset 1 3`获取指定区间的成员数量

   

> ### 三种特殊数据类型

**geospatial(地理位置)**

* `geoadd china:city 116.40 39.90 beijing   121.47 31.23 shanghai` 纬度   经度  名称
  * 两级无法添加 
  * 参数: 经度 维度 名称
  * 有效经度 -180 到 180
  * 有效纬度 -85.05 到 85.05

* `geopos china:city beijing`获取指定城市的经纬度
* `geodist china:city beijing shanghai  km`获取北京和上海的距离,以km为单位
  * 单位 : m km mi(英里) ft(英尺)

* `georadius china:city 110 30 1000 km withdist withcoord count 1` 以给定经纬度(110,30)为中心找出某半径(1000)范围内的(1个)单位,伴随单位的距离(withdist)和经纬度(withcoord)
* `geoRadiusByMember china : city beijing 1000 km`找出beijing附近1000km的单位
* `geohash china:city  beijing` 将经纬度转化为字符串,很少使用

底层是**Zset**,所以可以通过zset的命令操作geospatial

​	如:`Zrange china:city 0 -1`

**Hyperloglogs**

* 基数是不重复的元素,可以接受误差
* hyperloglogs 数据结构用来 **统计基数** 0.81%错误率,统计userview任务
* `PFadd mykey a b c d e f g`
* `PFcount mykey`统计mykey不重复的元素个数
* `PFmerge mykey3 mykey1 mykey2`将mykey1 和 mykey2 取并集合成为 mykey3 

**Bitmap**位存储

* 只要是只有 0 1 两种状态的都可以用
* `setbit sign 0 1`可以看作 周一(0)完成了签到(1)
* `bitcount sign`获取1的次数,即完成签到的个数
* `getbit sign 3`看周四(3)是否签到

> ### 事务

* mysql中的事务是原子性:要么同时成功,要么同时失败
* redis中事务不保证原子性,执行后按照写的命令一个一个执行
  * 开启事务(multi)
  * 事务入队(...写命令例如 set k1 v1)
  * 执行事务(exec)  
  * 放弃事务(discard) 
* 如果命令出错,事务中所有命令都会失败；如果是运行时运行,那么这个异常的命令会失败,其他命令正常执行



> ### 监控 (**watch** 乐观锁): 

* 悲观锁: 很悲观,无论做什么都加锁
* 乐观锁:很乐观,所以不会上锁,更新数据的时候判断在此期间是否有人修改过这个数据,如果修改过则下列操作失败,如果发现事务出错,先解锁(unwatch)再获取最新值加锁(watch)

> ### [Jedis](Jedis.md):	使用java操作redis的中间件

> ### [Springboot整合redis](springboot-redis.md)

> ### 持久化rdb(快照  )

* 保存的文件是 dump.rdb

* 在配置文件`redis.conf`中快照中配置  

  ```bash 
  # 在60秒内修改5次就把数据持久化
  save 60 5  
  ```

* 触发rdb规则
  * 达到设置规则 save 60 5
  * 进行`flushall`
  * 推出redis
* 将 dump.rdb放到redis根目录,redis就可以获取到其中的数据

> ### 持久化 aof(append only file)

* 保存的文件时 appendonly.aof
* 就是把命令都记录下来,然后将它们全部执行一遍
* 默认不开启,需要在配置文件中将 appendonly no 改为 `appendonly yes`重启
* 如果aof文件有问题,redis无法开启,使用`redis-check-aof --fix appendonly.aof`修复aof文件

> ### Redis 发布订阅

* 订阅端`subscribe channel`订阅channel1 

* 发送端`publish channel1 "hello"`向channel1 发送一条信息'hello',此时订阅者可以收到这个消息
* `unsubscribe channel1`退订
* 应用场景:
  * 实时聊天
  * 订阅
* 使用mq实现复杂场景

> ### 主从复制

