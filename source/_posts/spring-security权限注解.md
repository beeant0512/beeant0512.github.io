title: spring security权限注解
author: Beeant
tags:
  - spring
  - springSecurity
  - ''
categories:
  - Spring
date: 2018-11-26 10:17:00
---
spring security 内置权限注解

方法类在`org.springframework.security.access.expression`中

| 表达式 | 说明 | 
| ------ | ------ | 
| * hasRole([role]) | 当前账户有指定角色时返回`true`, 默认情况下，角色都是以`ROLE_`开头，当然也可以在修改`DefaultWebSecurityExpressionHandler`中修改`defaultRolePrefix`自定义角色前缀 |
| * hasAnyRole([role1,role2]) | 当前账户有指定角色中的任意一个时返回`true`, 默认情况下，角色都是以`ROLE_`开头，当然也可以在修改`DefaultWebSecurityExpressionHandler`中修改`defaultRolePrefix`自定义角色前缀 |
| hasAuthority([authority]) | 当前账户有指定权限时返回`true` |
| hasAnyAuthority([authority1,authority2]) | 当前账户有指定权限中任何一个时返回`true` |
| principal | 允许当前用户直接访问的对象主体 |
| authentication | 允许直接访问从SecurityContext获得的当前身份验证对象 |
| permitAll | 允许所有 |
| denyAll | 拒绝所有 |
| isAnonymous() | 是否匿名用户 |
| isRememberMe() | 当前是否被记住 |
| * isAuthenticated() | 是否已经登录 |
| isFullyAuthenticated() | 是否已经登录 或 被记住 |
| * hasPermission(Object target, Object permission) | Returns true if the user has access to the provided target for the given permission. For example, hasPermission(domainObject, 'read') |
| * hasPermission(Object targetId, String targetType, Object permission) | Returns true if the user has access to the provided target for the given permission. For example, hasPermission(1, 'com.example.domain.Message', 'read') |
| hasIpAddress([ip address]) | IP地址是否是？？？ |