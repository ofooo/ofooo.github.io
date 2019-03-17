### 重启桌面程序

	``` sudo /etc/init.d/lightdm restart ```

### 系统设置

```bash 
# 设置输入时禁用触摸板的时间，默认是1秒
sudo gsettings set com.deepin.dde.touchpad disable-while-typing-cmd 'syndaemon -i 1 -K -t'
sudo gsettings set com.deepin.dde.touchpad disable-while-typing-cmd 'syndaemon -i 3 -K -t'
```



### 查看鼠标、触摸板问题

```bash
# 查看输入设备
xinput list

# 查看键盘属性
xinput list-props 'AT Translated Set 2 keyboard'
# 查看鼠标属性
xinput list-props 'SynPS/2 Synaptics TouchPad'

#　设置id=8的设备的127属性值=0
xinput set-prop 8 127 0
```





触摸板被禁用

```bash
xinput list　　　　＃　查看设备号
xinput set-prop 12 "Device Enabled" 1   # 把１２设备设为１
```



xinput set-prop 12 "Device Enabled" 0



#### 系统目录

| 功能           | 位置                                |
| ------------ | --------------------------------- |
| 系统图标icon（主题） | /usr/share/icons/deepin/mimetypes |
| 桌面图标的配置路径    | /usr/share/applications           |
|              |                                   |





### 添加图标

程序图标目录：  /usr/share/applications

每个图标是一个 xxxx.desktop 文件

Exec是执行文件目录；Icon是图标位置；Category是图标所在分类

> [Desktop Entry]
> Name=Fire Fox
> GenericName=Fire Fox
> Comment=火狐浏览器
> **Exec=/home/fish/soft/firefox56/firefox**
> **Icon=/home/fish/soft/firefox56/browser/icons/mozicon128.png**
> Terminal=false
> Type=Application
> **Categories=Network;WebBrowser;**
> StartupNotify=false

``` Exec=gedit %U
Exec=gedit %U
%u 代表一个URL。也可以是一个本地文件路径。
%U 代表一系列URL，其中每一个URL作为一个单独的参数传递给可执行程序。也可以是一系列本地文件路径。
```

| 关键词             | 意义          | 参数                        |
| :-------------- | ----------- | ------------------------- |
| [Desktop Entry] | 文件头         |                           |
| Encoding        | 编码          |                           |
| Name            | 应用名称        |                           |
| Name[xx]        | 不同语言的应用名称   |                           |
| GenericName     | 描述          |                           |
| Comment         | 注释          |                           |
| Exec            | 执行的命令       | %f单文件 %F多文件 %u单url %U多url |
| Icon            | 图标路径        |                           |
| Terminal        | 是否使用终端      |                           |
| Type            | 启动器类型       |                           |
| Categories      | 应用的类型（内容相关） |                           |







#### 管理默认程序

sudo apt-get install nautilus	

用该文件管理器，右键文件属性，选择默认程序即可

![nautilus文件管理器图标](/home/fish/Documents/md_img/nautilus文件管理器图标.png)