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

* String(字符串)
* List
* Set
* Hash
* 