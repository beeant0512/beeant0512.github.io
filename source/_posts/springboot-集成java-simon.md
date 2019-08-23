title: springboot 集成java simon
author: Beeant
tags:
  - spring
  - 性能监控
categories:
  - Spring
  - ''
date: 2018-09-25 10:47:00
---
### 项目情况

* springboot （无xml配置，都是java代码的配置）
* gradle


### 集成simon

添加依赖
```
compile group: 'org.javasimon', name: 'javasimon-spring', version: '4.1.4'
compile group: 'org.javasimon', name: 'javasimon-console-embed', version: '4.1.4'
compile group: 'org.javasimon', name: 'javasimon-jdbc4', version: '3.5.2'
```
添加配置文件
```java  
/**
 * @author xiaobiao
 * @version 2018/9/21
 */
@Configuration
public class JavaSimonConfig {

    // 定义AOP
    @Bean(name = "monitoringAdvisor")
    public DefaultPointcutAdvisor monitoringAdvisor() {
        DefaultPointcutAdvisor monitoringAdvisor = new DefaultPointcutAdvisor();
        monitoringAdvisor.setAdvice(new MonitoringInterceptor());
        monitoringAdvisor.setPointcut(new MonitoredMeasuringPointcut());
        return monitoringAdvisor;
    }

    // 定义Servlet URL Mapping
    @Bean
    public ServletRegistrationBean dispatcherRegistration() {
        ServletRegistrationBean registration = new ServletRegistrationBean(new SimonConsoleServlet());
        registration.addInitParameter("url-prefix", "/javasimon");
        registration.addUrlMappings("/javasimon/*");
        return registration;
    }

}
```