title: android不显示标题栏
author: Beeant
tags:
  - android
categories:
  - Android
date: 2018-10-04 12:48:00
---
1. 在res/values/styles.xml中添加如下代码
```
<style name="AppTheme">
    <item name="windowActionBar">false</item>
    <item name="windowNoTitle">true</item>
</style>
```

2. 在AndroidManifest.xml中的不要显示的activity结点中加android:theme="@style/AppTheme.NoActionBar"
```
<activity android:name=".MainActivity" android:theme="@style/AppTheme.NoActionBar">
```
这样在该activity中就不会显示标题了，如果多个别的activity中不显示也在其中添加即可

转自 [https://www.cnblogs.com/q149072205/p/5236025.html](https://www.cnblogs.com/q149072205/p/5236025.html)