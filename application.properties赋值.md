## `application.properties`文件进行赋值的方法

```properties
name=gohoy
```

```java
@PropertySource(value="classpath:allication.properties")
Public class Person{
    @Value("${name}")
    private String name;
}
```

### 可见相当麻烦

### TIPS:

上文中 ${name}

是`SPEL表达式`

在yam中可以写 

```yaml
#gohoy后面加上随机uuid
name: gohoy${random.uuid}
#age取随机int数
age: ${random.int}
#如果没有person.hello 的这项则happy配置为冒号后面的值
happy: ${person.hello:hello} 
```

### 可见yaml比properties高级