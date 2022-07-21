## Nosql

> ### 什么是 nosql

 nosql =  Not Only Sql

泛指非关系型数据库

> ### Nosql 的数据分类

#### KV 键值对:

* **[redis](Redis.md)**
* redis + tair   
* redis + memecache

#### 文档型数据库(bson 格式 (二进制json)):

* MongDB
  * 基于分布式文件存储的数据库,c++ 编写,主要用来处理大量文档
  * 是介于非关系和关系型数据库之间的产品,是非关系型数据库中功能最丰富,最想关系型数据库
* ConthDB(国外的)

#### 列存储数据库

* HBase
* 分布式文件系统

#### 图关系数据库

* 不是存图形,存的是关系,比如: 朋友圈社交网络,.广告推荐
* Neo4j,InfoGrid