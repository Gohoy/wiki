## Jedis

> #### jedis 时 java 操作 redis 的 中间件,其api和redis 的命令基本相同

> 测试

* pox.xml文件

  ```xml
     <!-- https://mvnrepository.com/artifact/redis.clients/jedis -->
          <dependency>
              <groupId>redis.clients</groupId>
              <artifactId>jedis</artifactId>
              <version>3.2.0</version>
          </dependency>
  
          <dependency>
              <groupId>com.alibaba</groupId>
              <artifactId>fastjson</artifactId>
              <version>1.2.66</version>
          </dependency>
  ```

* 测试java文件

```java
public class TestPing {
    public static void main(String[] args) {
//        创建jedis对象
        Jedis jedis = new Jedis("127.0.0.1",6379);
//      jedis方法 就是redis 的命令
        System.out.println(jedis.ping());
    }
}
```

* 开启事务

``` java
package com.gohoy;

import com.alibaba.fastjson.JSONObject;
import redis.clients.jedis.Jedis;
import redis.clients.jedis.Transaction;

public class TestTX {
    public static void main(String[] args) {
        Jedis jedis = new Jedis("127.0.0.1",6379);
        jedis.flushDB();
        JSONObject jsonObject = new JSONObject();
        jsonObject.put("hello","world");
        jsonObject.put("name","gohoy");
//        开启事务
        Transaction multi = jedis.multi();
        String result =  jsonObject.toJSONString();
        try {

            multi.set("user1",result);
            multi.set("user2",result);
            multi.exec();
        }catch (Exception e){
            multi.discard();
            e.printStackTrace();
        }finally {
            System.out.println(jedis.get("user1"));
            System.out.println(jedis.get("user2"));
            jedis.close();
        }
    }
}

```



