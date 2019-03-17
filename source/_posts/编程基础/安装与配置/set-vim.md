---
title: 配置vim
toc: true
categories:
  - 编程基础
  - 安装与配置
date: 2019-03-17 08:56:04
tags:
---



### vim配置（linux/manjaro/ubuntu/deepin通用）

```bash
sudo pacman -S vim

":关闭与vi的兼容模式
set nocompatible 
":显示行号
set number 
":显示匹配的括号
set showmatch   
":距离顶部和底部3行
set scrolloff=3       
":编码
set encoding=utf-8 
set fenc=utf-8     
"编码设定Encoding
set fileencoding=utf-8
set fileencodings=utf-8,gbk,utf-16,big5
 
set langmenu=zh_CN.UTF-8
source $VIMRUNTIME/delmenu.vim
source $VIMRUNTIME/menu.vim
language messages zh_CN.UTF-8

"忽略大小写检索
set ignorecase
":搜索高亮
set hlsearch  
"输入检索时动态变化
set incsearch
":语法高亮
syntax on    
":命令显示历史
set history=500
"开启插件和缩进
filetype plugin indent on
":鼠标
set autoread
set mouse=
set mousehide
 
```

## 参考资料
> - []()
> - []()
