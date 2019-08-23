title: Mac jenkins打包小计
author: Beeant
tags:
  - jenkins
categories: 
  - Mac
date: 2016-06-06 09:19:00
---
### 安装Homebrew
```
cd /usr/bin/
sudo ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
### 安装p7zip
```
brew install p7zip
```
### 安装ant
```
brew install ant
```
### 安装ant-contrib-1.0b3

拷贝ant-contrib-1.0b3到/usr/local/Cellar/ant/1.9.7/libexec目录下,其中1.9.7是ant的版本，可能有所不同