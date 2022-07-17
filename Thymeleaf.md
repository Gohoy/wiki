## Thymeleaf

### 语法和vue相似

### 设值取值的方法:

**在springboot项目中**

```java
//在controller里
public String test(Model model){
    model.addAttribute("name","gohoy");
    return "test";
}
```

```html
<div th:text="${name}">
</div>
```

