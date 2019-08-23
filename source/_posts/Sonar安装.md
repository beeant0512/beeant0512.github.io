title: Sonar安装
author: Beeant
tags: []
categories:
  - Sonar
date: 2016-06-30 08:53:00
---
### 下载
下载并解压SonarQube （例如： `C:\sonarqube\server` 或 `/etc/sonarqube/server`）

### 启动SonarQube服务
```
On Windows, execute:
C:\sonarqube\server\bin\windows-x86-xx\StartSonar.bat
On other operating system, execute:
/etc/sonarqube/server/bin/[OS]/sonar.sh console
```
### SonarQube Scanner
下载并解压SonarQube Scanner （例如： `C:\sonarqube\scanner` 或 `/etc/sonarqube/scanner`）

### SonarQube的工程示例
下载并解压SonarQube的工程示例 （例如： `C:\sonarqube\example` 或 `/etc/sonarqube/example`)

### 分析项目
```
On Windows:
cd C:\sonarqube\example\projects\languages\java\sonar-runner\java-sonar-runner-simple
C:\sonarqube\scanner\bin\sonar-scanner.bat
 
cd C:\sonarqube\example\projects\languages\javascript\javascript-sonar-runner
C:\sonarqube\scanner\bin\sonar-scanner.bat
 
On other operating system:
cd /etc/sonarqube/example/projects/languages/java/sonar-runner/java-sonar-runner-simple
/etc/sonarqube/scanner/bin/sonar-scanner
 
cd /etc/sonar-examples/projects/languages/javascript/javascript-sonar-runner
/etc/sonarqube/scanner/bin/sonar-scanner
```
### 访问
打开浏览器，访问结果 [http://localhost:9000](http://localhost:9000) (默认的管理员帐号/密码： `admin/admin`)