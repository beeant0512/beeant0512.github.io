title: 'mac osx下apache下的坑: you don’t have permission to access / on this server'
author: Beeant
tags: 
  - apache
categories:
  - Mac
date: 2016-06-17 08:58:00
---
要在Directory指令里，增加一条 Require all granted，如下示：

```
<Directory "/Users/jnovack/Sites/">
  Options Indexes MultiViews
  AllowOverride All
  # OSX 10.10 / Apache 2.4
  Require all granted
</Directory>
```