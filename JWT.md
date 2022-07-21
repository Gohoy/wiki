## JWT

### Pom.xml

```xml
<!--        jwt依赖-->
        <dependency>
            <groupId>io.jsonwebtoken</groupId>
            <artifactId>jjwt</artifactId>
            <version>0.9.1</version>
        </dependency>
<!--        1.8的jdk以上需要加上以下依赖-->
        <dependency>
            <groupId>com.sun.xml.bind</groupId>
            <artifactId>jaxb-core</artifactId>
            <version>2.3.0.1</version>
        </dependency>
        <dependency>
            <groupId>javax.activation</groupId>
            <artifactId>activation</artifactId>
            <version>1.1.1</version>
        </dependency>
        <dependency>
            <groupId>com.sun.xml.bind</groupId>
            <artifactId>jaxb-impl</artifactId>
            <version>2.3.2</version>
        </dependency>
        <dependency>
            <groupId>javax.xml.bind</groupId>
            <artifactId>jaxb-api</artifactId>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
        </dependency>
```

#### 最好全部加上,否则可能会报错 `ClassNotFound`





### Jwt由三部分组成:header,payload,signature

```java
package com.example.jwt;

import io.jsonwebtoken.*;

import java.util.Date;
import java.util.UUID;

public class Test {
    private long time = 1000 * 60 * 60 * 24;
    private String signature = "admin";
	
    //加密
    @org.junit.Test
    public void jwt() {
        JwtBuilder jwtBuilder = Jwts.builder();
        String jwtToken = jwtBuilder
//                header
                .setHeaderParam("typ", "JWT")
                .setHeaderParam("alg", "HS256")
//                payload
                .claim("username", "gohoy")
                .claim("role", "admin")
                .setSubject("admin-Test")
                .setExpiration(new Date(System.currentTimeMillis() + time))
                .setId(UUID.randomUUID().toString())
//                signature
                .signWith(SignatureAlgorithm.HS256, signature)
                .compact();
        System.out.println(jwtToken);
    }

    //解密
    @org.junit.Test
    public void parse() {
        String token = "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6ImdvaG95Iiwicm9sZSI6ImFkbWluIiwic3ViIjoiYWRtaW4tVGVzdCIsImV4cCI6MTY1ODM5NTEzMCwianRpIjoiOTExMTQzOTMtMjRjZC00MTg4LWI1ZjEtODkxY2U0ZjY5NTM3In0.bHs3d1xlV9-3i64iBgTBTRDs7-bA8W64BFkdTfcIHLY";
        JwtParser jwtParser = Jwts.parser();
        Jws<Claims> jws = jwtParser.setSigningKey(signature).parseClaimsJws(token);
        Claims claims = jws.getBody();
        System.out.println(claims.get("username"));
        System.out.println(claims.get("role"));
        System.out.println(claims.getId());
        System.out.println(claims.getSubject());
        System.out.println(claims.getExpiration());
    }
}

```

