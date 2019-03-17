---
title: 安装ubuntu
toc: true
date: 2019-03-17 08:55:46
tags:
categories:
---



## 一 安装系统



## 二 安装软件

### 安装输入法

```bash
sudo  apt-get install fcitx-googlepinyin
然后注销再登陆操作系统
```

### 安装zsh

```bash
sudo apt install zsh

sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

重启操作系统后终端变成zsh
如果要切换回去bash
chsh -s /bin/bash


```

### 安装node/npm

```bash
# 1. 安装默认版本
sudo apt-get install npm
# 2. 安装版本管理工具
sudo npm install -g n
# 3. 安装对应版本
sudo n latest   #最新版本
sudo n stable   #最新的稳定版本
```



### 配置Ubuntu界面

```bash
sudo apt install chrome-gnome-shell
打开Ubuntu软件商店安装：GNOME Tweaks
https://extensions.gnome.org/
```

### 快捷键设置

| 快捷键     | 配置路径                | 说明       |
| ---------- | ----------------------- | ---------- |
| Super+E    | 启动器---主目录         | 文件管理器 |
| Ctrl+Alt+E | 启动网页浏览器          | 浏览器     |
| Super+D    | 导航---隐藏所有正常窗口 | 回到桌面   |
|            |                         |            |
|            |                         |            |
|            |                         |            |

## 参考资料
> - []()
> - []()
