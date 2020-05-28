---
title: 使用docker
toc: true
categories:
  - 编程基础
  - 软件使用备忘
date: 2019-03-19 14:49:42
tags:
---



## 配置

### 



### debug: 直接运行命令会报错, 进入bash再执行可用

**现象:**

1. docker的command=apachectl -D FOREGROUND执行失败
2. docker的command=bash, 在bash手工执行命令可成功

**原因:**

电脑性能差, apachectl依赖程序未全部启动, 此时执行命令所以报错. 

**解决方法:**

把command命令放在command.sh 中, 在最开始执行sleep 5 等待5秒.

然后把command.sh映射到容器内, command=bash command.sh



## 把目录挪动到机械硬盘

镜像和容器通常会占据很大的硬盘空间，所以最好移动到机械硬盘。

```bash
# 关闭dockder服务
sudo systemctl stop docker

# move
sudo mv /var/lib/docker /机械硬盘位置

# link
sudo ln -s /机械硬盘位置/docker /var/lib/docker

# 启动docker服务
sudo systemctl start docker
```







### 服务设置

刚安装完成后，需要重启机器，才能启动服务

```
# Ubuntu
sudo service docker start  # 启动服务

# manjaro
sudo systemctl start docker   # 启动服务
sudo systemctl status docker  # 查看服务状态
systemctl enable docker       # 开机启动
```

### 设置信任本地仓库

```bash
### 方法1  (如果不行可以尝试方法2)
# 1. 在/etc/default/docker添加：
-- insecure-registry 127.0.0.1:5000
-- insecure-registry 192.168.31.103:5000
# 2. 再重启docker 服务

### 方法2
# 1. 创建文件/etc/docker/daemon.json
{ "insecure-registries":["192.168.163.131:5000"]}
# 2. 再重启docker 服务
```

## 容器-常用命令

```bash
# 查看容器列表 
## -a 查看全部，否则查看运行中的
docker ps

# 删除容器    -f强制删除
docker rm -f xxx

# 实时查看容器占用的CPU和内存资源
docker stats

# 从容器生成镜像
docker commit -m "change somth" -a "somebody info" container_id(docker ps -a获取id) 新镜像名字
```

### 容器自启动设置

```bash
docker run --restart=on-failure:10 xxx
docker run --restart=always xxx
```

- no   容器退出时不要自动重启。这个是默认值。
- on-failure[:max-retries]     只在容器以非0状态码退出时重启。可选的，可以退出docker daemon尝试重启容器的次数。在每次重启容器之前，重启延迟比上次增加一倍，从100毫秒开始，来防止影响服务器。这意味着daemon将等待100ms,然后200ms，直到超过on-failure限制，或执行docker stop或docker rm -f 。如果容器重启成功[容器启动后并运行至少10秒]，然后delay重置为默认的100ms。
  ms, 400, 800, 1600等等，直到超过on-failure限制，或执行docker stop或docker rm -f
- always     不管退出状态码是什么始终重启容器。当指定always时，docker daemon将无限次数地重启容器。容器也会在daemon启动时尝试重启，不管容器当时的状态如何。(和unless-stopped 参数值效果一样)

  



## 镜像-常用命令

```bash
# 查看镜像列表
docker images

# 导出镜像的压缩文件（可以压缩多个镜像，例如xxx和yyy）
docker save xxx:tag yyy:tag2 | gzip > img.tar.gz  

# 镜像重命名
docker tag xxx:tag  xxx2:tag2

# 删除镜像  
## -f强制删除
docker rmi -f xxx:tag

```

## DockerFile

```bash
# 使用dockerfile生成镜像  -t添加标签名称(可以多个)

 docker build -t shykes/myapp:1.0.2 -t shykes/myapp:latest .

```









## 参考资料
> - []()
> - []()
