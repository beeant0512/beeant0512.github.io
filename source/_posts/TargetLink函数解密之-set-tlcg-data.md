---
title: TargetLink函数解密 之 set_tlcg_data
tags:
  - Targetlink
categories:
  - Targetlink
date: 2016-03-17 22:23:31
---

set_tlcg_data
========
set_tlcg_data是用于设置TargetLink模块或Stateflow对象的配置属性的一个函数，其语法如下：
``` perl
set_tlcg_data(block,data,bCheck,newPropNames)
```
输入参数
----
``` perl
block 模块的路径、或模块/Stateflow的操作句柄,通过gcb、gcbh可获得
```
``` perl
data  需要设置的数据,具体结构可使用get_tlcg_data获得
```
``` perl
bCheck if set to 1, data will be checked for consistency (set to 0 if nargin == 2)
newPropNames
```
``` perl
bSync 启用/停用同步
```
输出参数
---
``` perl
data 模块的数据
```
``` perl
info 信息（只有当bSync=true时）
```
``` perl
msgStrunc 在数据收集时所产生的信息
```
Targetlink和Stateflow的返回数据是不一样的

#### info数据 ####
``` perl
info.hVariable DD中'variable'的句柄
```
``` perl
info.hClass   DD中'class'的句柄
```
``` perl
info.hType    DD中'type'的句柄
```
``` perl
info.hScaling  DD中'scaling'的句柄
```
``` perl
info.bWritable 所有属性的可写标志位
```
``` perl
info.bWritable.<property>各属性是否可写的信息
```
``` perl
info.bInteger  是否是整型Int8, Int16, Int32, UInt8, UInt16，UInt32
```
``` perl
info.sBaseTypeRename Path of BaseTypeRename if it exists, otherwise ''
```

举例:
---
``` perl
   TL_Gain模块的数据主要是'output'和'gain'.
   data.output.<blockproperties>
   data.gain.<properties>
   info.output.<properties>
   info.gain.<properties>
```
``` perl
   未配置的Stateflow对象的数据
   data.<blockproperties>
   info.<blockproperties>
 ```

更多内容参看 set_tlcg_data