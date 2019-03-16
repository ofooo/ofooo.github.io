---
title: zsh
tags: [终端, linux, shell]
---

### 安装

```bash
# 如果是Ubuntu需要先安装（manjaro自带zsh）
sudo apt install zsh
# 安装插件，并切换默认sh为zsh
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
# 修改 ~/.zshrc 的插件配置（其中id_rsa coding_net是ssh私钥名，用空格间隔）
plugins=(
  git
  ssh-agent
)
zstyle :omz:plugins:ssh-agent indentities id_rsa coding_net
# 登出操作系统，再登录，打开shell即会进入zsh
```

[官网参考](https://ohmyz.sh/)