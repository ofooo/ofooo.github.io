---
title: mongo
toc: true
date: 2019-02-28 16:41:56
tags:
  - mongo
categories:
  - 编程基础
  - 数据库
---







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





### 客户端调用mongo集群

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



## 参考资料
> - [官方文档 ](https://docs.mongodb.com/manual/tutorial/)
> - []()
