---
title: mongo
toc: true
tags:
  - mongo
categories:
  - 人工智能
  - 搜索引擎
date: 2019-02-28 16:41:56
---





### 



## 服务器

### 服务器启用mongo集群

```bash
# 进入mongo客户端
mongo
# 以下操作是在mongo客户端命令行内：
# 创建集群，集群名字=“rs0”
rs.initiate(
    {
        _id: "rs0",
        members: [
            {
                _id: 0,
                host: "mongo-r0:27017"
            },
            {
                _id: 1,
                host: "mongo-r1:27017"
            },
            {
                _id: 2,
                host: "mongo-r2:27017"
            }
        ]
    }
)
# 查看集群状态
rs.conf()
rs.status()


```



## mongo客户端使用

### 登录/验证/切换数据库

```bash
# 进入mongo客户端(默认链接27017)
mongo

# 指定端口
mongo --port 1234

```



## 客户端模块调用

### pymongo/motor调用mongo集群

当 mongo 是集群时，客户端连接时需要设置好要连接的所有 mongo 节点。

```python
import pymongo
# uri里的“rs0”是集群名称，前面是每个节点的IP和端口
uri = 'mongodb://mongo-r0:27017,mongo-r1:27017,mongo-r2:27017/?replicaSet=rs0'
conn = pymongo.MongoClient()
[i for i in conn.list_databases()]
```

注释：pymongo和motor连接时使用的uri字符串可以是相同的，因为motor实际是调用pymongo实现的。

[集群--官方文档 ](https://docs.mongodb.com/manual/tutorial/deploy-replica-set/)



### pymongo调用基础功能

```python
import pymongo
# 链接到 数据库
db = pymongo.MongoClient('mongodb://{$ip}:{$port}')[$db_name]
# 链接到 数据集合
db_col = db[$col_name]

# 数据集合的总数量
total = db_col.count_documents()

# find    sort()排序   limit()结果数量限制
resp = db_col.find({}, keys).sort([(key1, 1), (key2, -1)]).limit(10)





```







## 参考资料
> - [官方文档 ](https://docs.mongodb.com/manual/tutorial/)
> - []()
