---
title: 安装ES
toc: true
date: 2019-03-17 09:21:17
tags: [es, elastic_search, Kibana]
categories:
---

## 安装ES

-E <KeyValuePair>     Configure a setting
-V, --version
-d, --daemonize      守护进程，后台启动
-p, --pidfile <Path>  Creates a pid file in the specified path on start
-q, --quiet           Turns off standard output/error streams logging in console
-s, --silent          show minimal output
-v, --verbose         show verbose output

```bash 
# 启动(先-s 启动成功, 再用-d后台启动)
elasticsearch/bin/elasticsearch -s   
# 配置文件
elasticsearch/config/elasticsearch.yml

# 检查状态
curl -XGET '192.168.31.185:9200/_cat/health?v'
# 测试是否启动成功
curl 'http://192.168.31.185:9200/?pretty'
# 查看所有索引！！
curl -XGET '192.168.31.185:9200/_cat/indices?v'


# 创建一个名字=ip_focus 的索引   pretty参数让返回结果更易读
curl -XPUT '192.168.31.185:9200/ip_focus?pretty'
# 删除一个索引
curl -XDELETE '192.168.31.185:9200/customer?pretty'
# 新建/修改一个文档（一行数据）  _id=1   如果索引不存在，会自动新建索引=customer
# 当我们没有明确指定ID的时候，我们需要使用POST方法代替PUT来发送请求
PUT /customer/doc/1    { "name": "John Doe" }
```

启动时报错：elasticsearch max virtual memory areas vm.max_map_count [65530] is too low

```bash
sudo vim /etc/sysctl.conf 
# 在文件末尾加入
vm.max_map_count=655360
# 然后执行
sudo sysctl -p
```



## 安装Kibana

```bash
去官网下载
https://www.elastic.co/cn/downloads/kibana

# 解压文件
tar –zxvf kibana-5.5.2-linux-x86_64.tar.gz–C ./kibana/

# 去config文件夹编辑kibana.yml
#配置本机ip  
server.host: "192.168.252.129"  
#配置es集群url  
elasticsearch.url: "http://192.168.252.129:9200"  

# 启动程序   使用&命令启动后，退出当前窗口时需要使用exit退出
cd /bin
./kibana &

访问：http://ip:port ip为kibana安装节点ip，端口默认为5061
```

## 参考资料
> - []()
> - []()
