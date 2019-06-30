---
title: 安装manjaro
toc: true
categories:
  - 编程基础
  - 安装与配置
date: 2019-03-17 08:55:36
tags:
---



## 零. 个人使用体验

只使用了一周，还不太熟悉。再尝试一周，如果没有什么特别的优点就换成deepin试试。

**优点**

1. 硬件支持好
2. 软件版本非常新（滚动更新）

**缺点**

1. 缺少软件360浏览器
2. 对中文支持较差，需要自己配置的内容较多
3. 很多软件都是deepin的，例如微信和naivicat（那我为什么不直接用deepin呢）

## 一. 安装manjaro系统



## 二. 中文相关配置

### 注意事项

如果代码更新一直等待状态可以尝试删除/var/lib/pacman/db.lck

### 配置镜像源 测试国内的镜像源

```bash
sudo pacman-mirrors -i -c China -m rank
```

### 设置 archlinuxcn 源

```bash
# 修改 /etc/pacman.conf 添加以下内容
[archlinuxcn]
SigLevel = Optional TrustedOnly
Server = http://repo.archlinuxcn.org/$arch
## 添加cn源签名key(这步不做，会报签名错误）
sudo pacman -S archlinuxcn-keyring
#  完成后执行下面的命令使配置生效
## 更新源列表
sudo pacman-mirrors -g
## 更新pacman数据库并全面更新系统
sudo pacman -Syyu  #（必须先更新系统，不然无法安装输入法）
```
### 使界面可以输入中文

```bash
在~/.xprofile中添加
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
如果还是无法使用，可能需要安装fcitx-gtk2
sudo pacman -S fcitx-gtk2
```

### 把系统界面设置为中文

```bash
点击设置--Manjaro Settings Manager--本地化设置：添加 中国-中文，然后在语言包中点击安装软件包
在~/.xprofile中添加
export LC_ALL="zh_CN.UTF-8"
export LANG=zh_CN.UTF-8
```

## 三. 安装软件和系统配置

### 安装yay

```bash
# 1.  下载代码
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```
### 安装git

```bash
sudo pacman -S git
sudo pacman -S git-lfs
```

### 安装 wps

```bash
sudo pacman -S wps-office
sudo pacman -S ttf-wps-fonts
```

### 安装 typora
```bash
## 下载二进制文件（x64）  解压
https://www.typora.io/#linux
## 创建程序的软链接
sudo ln -s /home/fish/soft/Typora-linux-x64/Typora /usr/bin/typora
## 编辑/usr/share/applications/typora.desktop 文件
[Desktop Entry]
Version=1.0
Terminal=false
Icon=/home/aifish2/soft/typora/Typora-linux-x64/resources/app/asserts/icon/icon_256x256.png
Type=Application
Categories=Office;
Exec=/usr/bin/typora %U
Name=Typora
Comment=MarkDown Editor
```

### 安装node/npm

```bash
sudo pacman -S nvm 
nvm install --latest-npm

然后把/home/fish/.nvm/versions/node/v11.12.0/bin添加到系统路径
```



### 安装jdk

```bash
sudo pacman -S jdk8

# 配置环境
export JAVA_HOME=/usr/lib/jvm/default
export JRE_HOME=${JAVA_HOEM}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib 
```

### 命令简单安装： vscode/ vim/ 微信/ shadownsocks/ 网易云音乐/ qq/ chrome/docker

```bash
sudo pacman -S code
sudo pacman -S electronic-wechat   （网页版不能复制粘帖图片）
sudo pacman -S shadownsocks-qt5
sudo pacman -S vim
sudo pacman -S netease-cloud-music   # 网易云音乐
sudo pacman -S deepin.com.qq.office  # 可以先搜索qq 看看版本
sudo pacman -S google-chrome
sudo pacman -S docker
```

### 安装下载工具Gwget

```bash
打开系统工具：添加/删除软件
搜索工具后下载
```

### 百度云下载

```bash
打开系统工具：添加/删除软件：安装baidupcs-go-git
说明：https://github.com/iikira/BaiduPCS-Go

# 进入命令交互工具
baidupcs
# 帮助
help

```

### 安装截图工具

```bash
sudo pacman -S deepin-screenshot

添加快捷键： deepin-screenshot  
```



### 安装zsh   autojump

```bash
# zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# autojump（zsh设置ubuntu通用）
sudo pacman -S autojump
再在~/.zshrc中添加:   
plugins=(git autojump)
```

### 安装googlepinyin谷歌拼音

```bash
sudo pacman -S fcitx-im fcitx-configtool fcitx-googlepinyin

sudo vim ~/.xprofile  输入下面命令：
exportGTK_IM_MODULE=fcitx
exportQT_IM_MODULE=fcitx
exportXMODIFIERS="@im=fcitx"
```

### 安装搜狗拼音

```bash
# 前置：设置中国软件源

sudo pacman -S fcitx-im #默认全部安装
sudo pacman -S fcitx-configtool
sudo pacman -S fcitx-sogoupinyin

在~/.xprofile添加如下内容：
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
```



### 关闭ssh远程root登录

```bash
# 设置不允许root帐号登录 修改文件 /etc/ssh/sshd_config
	PermitRootLogin no
# 重启sshd服务
sudo systemctl restart sshd
```

### 安装pycharm（ubuntu通用）

```bash
1.下载并解压pycharm.tar文件
2.进入bin文件夹
3.执行./pycharm.sh
4.打开pycharm，在菜单栏选择tool--->添加桌面快捷方式
```

### 时间显示设置

操作：右键点击任务栏右下角的时间，选择属性：
tips配置：%m-%d   %j/365  第%V周
时钟配置：周%u %H:%M

### 

### 切换deepin桌面

```bash
# 安装桌面，然后重启电脑，选择桌面
sudo pacman -S deepin deepin-extra lightdm

```

[参考arch-wiki](<https://wiki.archlinux.org/index.php/Deepin_Desktop_Environment>)

### chrome安装插件

1. 去官网下载插件文件  xxx.crx
2. 去http://crxextractor.com/ 网站上传crx文件，获得zip文件
3. 解压zip文件获得一个文件夹
4. 打开chrome，打开开发者模式，加载已解压的扩展程序，选中解压文件夹，安装即可

## 四. 常用快捷键

**Ctrl+Alt+D  回到桌面（在设置界面里看不见这个快捷键，但是超级方便）**

Ctrl+Alt+F  exo-open --launch FileManager 打开文件管理器  我改成了 Super E
Ctrl+Alt+M  xfce4-taskmanager  资源监控器
Ctrl+Alt+Delete  xflock4  锁屏并黑屏
Ctrl+Alt+X  xkill  通过鼠标关闭某个程序
新增： Ctrl+Alt+Q xfce4-terminal  终端
Ctrl+H    文件管理器，显示隐藏文件

## 参考资料
> - []()
> - []()
