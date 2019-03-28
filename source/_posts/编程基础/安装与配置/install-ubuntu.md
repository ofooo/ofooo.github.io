---
title: 安装ubuntu
toc: true
categories:
  - 编程基础
  - 安装与配置
date: 2019-03-17 08:55:46
tags:
---



## 一 安装系统



## 二 安装软件

### 科学上网

```bash
# 安装ss的GUI客户端
sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
sudo apt-get install shadowsocks-qt5
```

### 安装git git-lfs

```bash
# 安装git
sudo apt install git

# 安装git-lfs
## 1. 设置url源
curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash
## 2. 安装lfs
sudo apt-get install git-lfs
## 3. 初始化
git lfs install
```

### 安装google输入法(不好用)

```bash
sudo  apt-get install fcitx-googlepinyin
然后注销再登陆操作系统
```

### 安装搜狗输入法

![ibus配置](install-ubuntu/1553342505304.png)

![1553344201236](install-ubuntu/1553344201236.png)

```bash
1. 去搜狗拼音官网,下载linux版本安装文件(.deb)
2. 双击打开界面安装
3. 登出后登录操作系统
4. 右键点击顶栏的键盘图标，选择配置
5. 添加搜狗输入法
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
