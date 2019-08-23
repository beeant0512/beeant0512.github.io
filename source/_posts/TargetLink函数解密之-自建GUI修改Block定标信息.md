---
title: TargetLink函数解密之-自建GUI修改Block定标信息
tags:
  - Targetlink
categories:
  - Targetlink
date: 2016-04-21 23:21:17
---

之前介绍过get_tlcg_data, set_tlcg_data, dsdd之SelectObject，今日就使用一个简单的例子来，结合这三个函数来实现修改block的变量标定。

### 1.建立GUI ###
在建立GUI之前，如果还不会怎么建立GUI的话，执行脑补一下。
#### 新建GUI
<img src="/images/targetlink/gui-variable/new-gui.png"  alt="建立GUI" />

#### 添加按钮
<img src="/images/targetlink/gui-variable/gui-variable-btn.png"  alt="添加按钮" />

### 2.设置回调函数 ###
设置Variable的回调函数 callback
```
% --- Executes on button press in tl_variable.
function tl_variable_Callback(hObject, eventdata, handles)
% hObject    handle to tl_variable (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
tlcg_data = get_tlcg_data(gcbh);
output = tlcg_data.output;
[currentPath,bModified] = dsdd('SelectObject','CurrentPath',output.variable ,'objectKind','Variable');
if bModified == 1
    output.variable = currentPath;
    tlcg_data.output = output;
    set_tlcg_data(gcbh, tlcg_data);
end
```

### 3.结果演示 ###
#### 选中一个Block,此处选中了Gain模块 #### 
<img src="/images/targetlink/gui-variable/gain.png"  alt="设置前" />
<img src="/images/targetlink/gui-variable/before-set.png"  alt="设置前" />

#### 点击Variable按钮 #### 
<img src="/images/targetlink/gui-variable/mygui.png"  alt="设置前" />
#### 选中变量 #### 
<img src="/images/targetlink/gui-variable/select-variable.png"  alt="设置前" />

#### 确定查看效果
<img src="/images/targetlink/gui-variable/after-set.png"  alt="设置后效果" />
