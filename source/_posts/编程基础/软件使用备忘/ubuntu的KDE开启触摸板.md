---
title: ubuntu的KDE开启触摸板
toc: true
categories:
  - 编程基础
  - 软件使用备忘
date: 2019-07-11 22:37:20
tags:
---







安装KDE后触摸板失效了, 今天终于解决了问题

### xinput

```bash
# 查看设备
xinput
# TouchPad是触摸板,  Mouse是鼠标,  Touchscreen是触摸屏, 根据名字找到触摸板的设备ID(我这里是17)

# 禁用
xinput --disable 17
# 启用
xinput --enable 17

# 查看设备的属性
xinput --list-props 17
# 结果如下: 
Device 'SynPS/2 Synaptics TouchPad':
	Device Enabled (143):	1
	Coordinate Transformation Matrix (145):	1.000000, 0.000000, 0.000000, 0.000000, 1.000000, 0.000000, 0.000000, 0.000000, 1.000000
	libinput Tapping Enabled (302):	0
	libinput Tapping Enabled Default (303):	0
	libinput Tapping Drag Enabled (304):	1
	libinput Tapping Drag Enabled Default (305):	1
	libinput Tapping Drag Lock Enabled (306):	0
	libinput Tapping Drag Lock Enabled Default (307):	0
	libinput Tapping Button Mapping Enabled (308):	1, 0
	libinput Tapping Button Mapping Default (309):	1, 0
	libinput Natural Scrolling Enabled (280):	0
	libinput Natural Scrolling Enabled Default (281):	0
	libinput Disable While Typing Enabled (310):	1
	libinput Disable While Typing Enabled Default (311):	1
	libinput Scroll Methods Available (282):	1, 1, 0
	libinput Scroll Method Enabled (283):	1, 0, 0
	libinput Scroll Method Enabled Default (284):	1, 0, 0
	libinput Click Methods Available (312):	1, 1
	libinput Click Method Enabled (313):	1, 0
	libinput Click Method Enabled Default (314):	1, 0
	libinput Middle Emulation Enabled (287):	0
	libinput Middle Emulation Enabled Default (288):	0
	libinput Accel Speed (289):	0.000000
	libinput Accel Speed Default (290):	0.000000
	libinput Left Handed Enabled (294):	0
	libinput Left Handed Enabled Default (295):	0
	libinput Send Events Modes Available (265):	1, 1
	libinput Send Events Mode Enabled (266):	0, 0
	libinput Send Events Mode Enabled Default (267):	0, 0
	Device Node (268):	"/dev/input/event4"
	Device Product ID (269):	2, 7
	libinput Drag Lock Buttons (296):	<no items>
	libinput Horizontal Scroll Enabled (297):	1

其中 libinput Tapping Enabled (302) 这个属性是触摸板点击生效属性

# 设置设备17的属性302的值为1
xinput --set-prop 17 302 1
```







## 参考资料

> - []()
> - []()
