title: mac iterm2 开启颜色高亮方法
author: Beeant
tags:
  - mac iterm
categories:
  - Mac
date: 2017-04-01 08:46:00
---
### 编辑~/.bash_profile  
拷贝以下代码到~/.bash_profile中  
``` bash
#enables colorin the terminal bash shell export
export CLICOLOR=1
#sets up thecolor scheme for list export
export LSCOLORS=gxfxcxdxbxegedabagacad
#sets up theprompt color (currently a green similar to linux terminal)
export PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;36m\]\w\[\033[00m\]\$ '
#enables colorfor iTerm
export TERM=xterm-color
```

### 配置iterm
preference->profiles->Terminal->xterm-new  

### 使~/.bash_profile生效
```bash
source ~/.bash_profile
```