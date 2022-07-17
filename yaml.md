## yaml的基本格式

### spring官方更推荐yaml配置文件的写法.

yaml文件对空格要求极为严格

``` yaml
server:
  port: 8080

# normal key:value
name: gohoy

#object
student:
  name: gohoy
  age: 18

# in a line
student: {name: gohoy,age: 18}

# arraylist
pets:
  - cat
  - pig
  - dog
#in a line
pets: [cat,pig,dog]
```

### 强大之处:可以进行赋值,例如:实体类

**在`application.yaml`中给实体类Person赋值,然后在实体类Person.java 中加入注解`@ConfigurationProperties(prefix ="person")`**

``` yaml
person:
  name: gohoy
  age: 18
  happy: false
```

在写了注解之后这个person对象就可以创建出来.然后进行

```java
@Autowired
private Person person;
System.out.Println(person);
```

### TIPS:

平时的注入对象的方法是在实体类的数据上 @Value

```java
@Value("gohoy")
private String name;
```

### `SPEL表达式`

```yaml
#gohoy后面加上随机uuid
name: gohoy${random.uuid}
#age取随机int数
age: ${random.int}
#如果没有person.hello 的这项则happy配置为冒号后面的值
happy: ${person.hello:hello} 
```

#### 可见yaml比properties高级

#### [`application.properties`文件进行赋值的方法](application.properties赋值.md)

### 松散绑定

在yaml中定义的last-name 可以匹配到实体类中的 lastName

### [JSR303校验](JSR303数据校验.md)