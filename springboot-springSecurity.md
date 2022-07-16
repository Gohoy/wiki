## SpringBoot 整合 SpringSecurity最新版

### pox.xml 文件

``` pox.xml
        <dependency>
            <groupId>org.springframework.security</groupId>
            <artifactId>spring-security-oauth2-authorization-server</artifactId>
            <version>0.3.1</version>
        </dependency>
```

### SecurityConfiguration.java

``` SecurityConfiguration.java
package com.example.springsecurity.config;

import org.springframework.context.annotation.Bean;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.provisioning.InMemoryUserDetailsManager;
import org.springframework.security.web.SecurityFilterChain;

import static org.springframework.security.config.Customizer.withDefaults;

/**
 * @author Joe Grandja
 * @since 0.1.0
 */
@EnableWebSecurity
public class SecurityConfiguration {
    @Bean
    SecurityFilterChain defaultSecurityFilterChain(HttpSecurity http) throws Exception {
        http
                .authorizeRequests(authorizeRequests ->
                        authorizeRequests.antMatchers("/level1/**").hasRole("USER1")
                                .antMatchers("/level2/**").hasRole("USER2")
                                .antMatchers("/level3/**").hasRole("USER3")
                )
                .formLogin(withDefaults());
        return http.build();
    }

    @Bean
    UserDetailsService users() {
        UserDetails user = User.withDefaultPasswordEncoder()
                .username("user1")
                .password("123456")
                .roles("USER1")
                .build();
        UserDetails user1 = User.withDefaultPasswordEncoder()
                .username("root")
                .password("123456")
                .roles("USER2")
                .build();
        UserDetails user2 = User.withDefaultPasswordEncoder()

                .username("gohoy")
                .password("123456")
                .roles("USER3")
                .build();

        return new InMemoryUserDetailsManager(user, user1, user2);
    }
}
```

### 数据库链接

TODO