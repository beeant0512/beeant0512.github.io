title: dojo-模板使用小结
author: Beeant
tags:
  - dojo
categories: 
  - dojo
date: 2016-11-08 08:48:00
---
### dojo 模板使用小结
在使用dojo的模板引擎时，需要引入`"dojox/dtl"`,`"dojox/dtl/Context"`,`"dojox/dtl/tag/logic"`

* dojox/dtl 还不清楚为什么非要引用
* dojox/dtl/Context
* dojox/dtl/tab/logic 使用模板的逻辑标签，不引用会无法解析for,之类的逻辑标签
```javascript
var template = new dtl.Template(dom.byId('menuTemplate').value);
var context = new Context({menus: appMenu});
template.render(context);
```
模板
```javascript
<textarea id="menuTemplate" style="display: none;">
{% for item in menus %}
<li class="{{item.class}}"><a href="{{item.link}}">{{item.name}}</a></li>
{% endfor %}
</textarea>
```