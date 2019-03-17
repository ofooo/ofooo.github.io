### conda添加虚拟环境

1、创建环境

conda create -n py36 python=3.6

2、进入环境

source activate py36

3、然后添加kernel

~~sudo python -m ipykernel install --name py36~~     如果当前虚拟环境不是root用户的，而仅用有user权限。则sudo安装的kernel位置不会是当前虚拟环境的位置。

python -m ipykernel install --user --name py36   仅安装到当前用户，这个位置正确。如果提示没有权限，则给要写入的文件夹权限。

如果提示没有ipykernel，使用:python -m pip install ipykernel

4、退出虚拟环境

source deactivate

（ jupyter可以使用。 这个过程jupyter貌似不用重启，刷新页面即可。）



### 删除kernel

先找到配置文件kernel.json

sudo find / -name "kernel.json"

判断倒数第一行是我的配置，所以删除/usr/local/share/jupyter/kernels/py36/的话即是删除了这个kernel。

/usr/local/share/jupyter/kernels/py36/kernel.json

/home/fish/.local/share/jupyter/kernels/py27



#### 用virtualenv安装虚拟环境


```bash
# 安装virtualenv
pip install virtualenv

# 列出所有环境
lsvirtualenv

# 创建环境
virtualenv venvname
# 创建环境，以  /usr/bin/python3  为python程序
virtualenv -p /usr/bin/python3 venvname

# 激活环境
activate venvname
# 退出环境
deactivate
# 删除环境
rmvirtualenv venvname　
```

