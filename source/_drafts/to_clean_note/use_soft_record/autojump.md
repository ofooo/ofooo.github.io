---
title: autojump
tags: []
---

```bash
j -s     	 # 显示所有目录和概率
j -a 目录     # 手工添加一个目录
j -i 权重值	# 增加当前目录的权重
j -d 权重值    # 降低当前目录的权重
```

安装

```bash
# 下载
git clone git://github.com/joelthelion/autojump.git 
# 安装。过程中,会在~/下建立.autojump文件夹
./install.python 

# 配置路径。在上面安装结束会提示加入，把路径加入到.bashrc
[[ -s /home/wangxiaoyu/.autojump/etc/profile.d/autojump.sh ]] && source /home/wangxiaoyu/.autojump/etc/profile.d/autojump.sh
# 激活
source .bashrc
```

