### `SPEL表达式`

```yaml
#gohoy后面加上随机uuid
name: gohoy${random.uuid}
#age取随机int数
age: ${random.int}
#如果没有person.hello 的这项则happy配置为冒号后面的值
happy: ${person.hello:hello} 
```

#### 