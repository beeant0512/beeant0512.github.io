title: spring security4 多登录页方法
author: Beeant
tags:
  - spring
categories:
  - Spring
date: 2017-04-11 08:42:00
---
对于多登陆页在网上查找了很多资料，但由于项目中的所有配置已经不使用xml方式了，因此，网上的很多方法都不试用了。

最后，还是在spring security的文档中找到了解决方法。在配置文件中，配置多个配置实现。

记录如下：
```java
@EnableWebSecurity
@EnableGlobalMethodSecurity(prePostEnabled = true)
public class MultiHttpSecurityConfiguration {
    @Autowired
    public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception {
        auth
                .inMemoryAuthentication()
                .withUser("admin").password("123456").roles("USER");
    }
    @Configuration
    @Order(1)
    public static class FormLoginWebSecurityConfigurerAdapter extends WebSecurityConfigurerAdapter {
        @Override
        protected void configure(HttpSecurity http) throws Exception {
            http.antMatcher("/user/**")
                    .authorizeRequests().anyRequest().authenticated()
                    .and()
                    .formLogin().loginPage("/user/login").permitAll().and()
                    .logout()
                    .clearAuthentication(true)
                    .logoutSuccessUrl("/user/index") //退出登录后的默认网址是”/”
                    .invalidateHttpSession(true);;
        }
    }
    @Configuration
    public static class AppLoginSecurityConfigurationAdapter extends WebSecurityConfigurerAdapter {
        protected void configure(HttpSecurity http) throws Exception {
            http.antMatcher("/app/**")
                    .authorizeRequests().anyRequest().authenticated()
                    .and()
                    .formLogin().loginPage("/app/login").permitAll().and()
                    .logout()
                    .clearAuthentication(true)
                    .logoutSuccessUrl("/app/index") //退出登录后的默认网址是”/”
                    .invalidateHttpSession(true);
        }
    }
}
```

