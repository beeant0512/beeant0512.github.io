title: pentaho server配置mysql数据库存储
author: Beeant
tags: []
categories: []
date: 2019-06-07 19:10:00
---
由于最近业务需要，接触到pentaho server,由于网上提供的配置方式都不是太完整可用，经过几经摸索，触碰到了一些可行的方式，顺便记录一下 pentaho server配置数据库存储的配置方式。

### 1 数据库表创建
执行`pentaho/server/pentaho-server/data/mysql5` 下的几个sql文件即可，网上大部分教程都会有`pentaho_mart_mysql.sql` 但是现在的版本基本上也没有这个文件了，忽略也不影响后续的使用。 
注意：各个数据库中的账号及密码可自行修改

### 2 quartz配置修改
修改`pentaho/server/pentaho-server/pentaho-solutions/system/quartz/quartz.properties`文件中的两处配置
修改后的配置如下：
```
org.quartz.jobStore.driverDelegateClass = org.quartz.impl.jdbcjobstore.StdJDBCDelegate
```

```
org.quartz.dataSource.myDS.jndiURL = Quartz
```

### 3 mysql的Hibernate配置修改

修改 `pentaho/server/pentaho-server/pentaho-solutions/system/hibernate` 下的 `hibernate-settings.xml`文件

修改前
```
<config-file>system/hibernate/postgresql.hibernate.cfg.xml</config-file>
```

修改后
```
<config-file>system/hibernate/mysql5.hibernate.cfg.xml</config-file>
```

### 4 日志配置
复制`pentaho-solutions/system/dialects/mysql5/audit_sql.xml`文件到`pentaho-solutions/system`目录下

### 5 Jackrabbit数据库配置
修改`pentaho/server/pentaho-server/pentaho-solutions/system/jackrabbit/repository.xml`文件

|修改项|修改后结果|
|-|-|
| Repository | ```\\<FileSystem class="org.apache.jackrabbit.core.fs.db.DbFileSystem">
     <param name="driver" value="com.mysql.jdbc.Driver"/>
     <param name="url" value="jdbc:mysql://localhost:3306/jackrabbit"/>
…
</FileSystem>
```| 
| DataStore | ``` <DataStore class="org.apache.jackrabbit.core.data.db.DbDataStore">
    <param name="url" value="jdbc:mysql://localhost:3306/jackrabbit"/>
…
</DataStore>
```|
| Workspaces | <FileSystem class="org.apache.jackrabbit.core.fs.db.DbFileSystem">
      <param name="driver" value="com.mysql.jdbc.Driver"/>
      <param name="url" value="jdbc:mysql://localhost:3306/jackrabbit"/>
…
</FileSystem> |
| PersistenceManager (1st part) | ```
<PersistenceManager class="org.apache.jackrabbit.core.persistence.bundle.MySqlPersistenceManager">
      <param name="url" value="jdbc:mysql://localhost:3306/jackrabbit"/>
…
</PersistenceManager>
``` |
| Versioning | ``` <FileSystem class="org.apache.jackrabbit.core.fs.db.DbFileSystem">
      <param name="driver" value="com.mysql.jdbc.Driver"/>
      <param name="url" value="jdbc:mysql://localhost:3306/jackrabbit"/>
…
</FileSystem> ```|
| PersistenceManager (2nd part) | ``` <PersistenceManager class="org.apache.jackrabbit.core.persistence.bundle.MySqlPersistenceManager">
      <param name="url" value="jdbc:mysql://localhost:3306/jackrabbit"/>
      …
</PersistenceManager>```	|
| DatabaseJournal | ``` <Journal class="org.apache.jackrabbit.core.journal.DatabaseJournal">
    <param name="revision" value="${rep.home}/revision.log"/>
    <param name="driver" value="com.mysql.jdbc.Driver"/>
    <param name="url" value="jdbc:mysql://localhost:3306/jackrabbit"/>
    <param name="user" value="jcr_user"/>
    <param name="password" value="password"/>
    <param name="schema" value="mysql"/>
    <param name="schemaObjectPrefix" value="J_C_"/>
</Journal>``` |