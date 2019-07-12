---
title: jupyter_notebook
toc: true
tags:
  - jupyter
  - notebook
categories:
  - python
date: 2019-04-07 17:58:44
---

## 配置远程密码

```bash
# 生产配置文件
jupyter notebook --generate-config

# 生成密码
# 1. 打开ipython 执行下面2行代码
from notebook.auth import passwd
passwd()
# 输入2两次密码，生成sha值

# 编辑配置文件 ~/.jupyter/jupyter_notebook_config.py
c.NotebookApp.ip='127.0.0.1'
c.NotebookApp.allow_remote_access=True
c.NotebookApp.password=u'sha:xxxxxx生成内容'
c.NotebookApp.open_browser=False
c.NotebookApp.port=8888

# 配置代码根目录
c.ContentsManager.root_dir = '/home/aifish/FishCode'

# 启动服务
jupyter notebook

# 设置开机启动
#　加入 rc.local
nohup /home/aifish/anaconda3/bin/jupyter notebook>/home/aifish/.jupyter/notebook.log 2>&1 &
```

### 把虚拟环境添加到jupyter的kernel

```python
进入虚拟环境
# 安装 ipykernel
pip install ipykernel
# 找到python位置（因为加入kernel时需要sudo权限，要制定python路径
which python
# 使用python绝对路径, 把虚拟环境XXXX加入kernel
sudo /anaconda/env/python -m ipykernel install --name XXXX

```





## 参考资料
> - []()
> - []()
