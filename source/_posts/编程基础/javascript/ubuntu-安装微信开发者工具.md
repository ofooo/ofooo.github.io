---
title: ubuntu安装微信开发者工具
toc: true
tags:
  - 微信开发者工具
  - 图标下载
categories:
  - 编程基础
  - javascript
date: 2019-11-08 14:10:26
---



## ubuntu安装微信开发者工具



克隆代码到某个文件夹(例如/opt)

```bash
cd /opt/
git clone https://github.com/cytle/wechat_web_devtools.git
sudo chown -R [用户名]:[用户名] ./wechat_web_devtools
cd wechat_web_devtools
./bin/wxdt
```

如果报错则安装以下 wine

```bash
sudo apt install wine
```

添加快捷方式

```bash
 sudo vim /usr/share/applications/wechat-ide.desktop

```

```bash
[Desktop Entry]
Encoding=UTF-8
Version=1.0
Type=Application
Name=WeChat-IDE
Icon=/opt/wechat_web_devtools/wechat-ide.png
Exec=/opt/wechat_web_devtools/bin/wxdt
StartupNotify=false
StartupWMClass=wechat-ide
```

安装桌面图标: 执行 bin/install_desktop.sh





## 参考资料
> - [Ubuntu 安装 微信开发者工具](https://blog.csdn.net/qq_14824885/article/details/81033070)
> - []()
