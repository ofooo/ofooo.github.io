---
title: elastic_search基础
toc: true
date: 2019-03-05 10:39:39
tags: [elastic, elastic_search, elasticsearch, es]
categories: [人工智能, 搜索引擎]
---





## 索引(库)、分类(表)





## 数据

### 查询数据



### 删除数据

```bash
# es参考版本：elasticsearch：5.5
# _delete_by_query会删除所有query语句匹配上的文档，用法如下：
curl -X POST "localhost:9200/twitter/_delete_by_query" -H 'Content-Type: application/json' -d'
{
  "query": { 
    "match": {
      "name": "测试删除"
    }
  }
}
# 其中twitter是索引名称
#　因为internal版本控制不支持0为有效数字，所以版本号为0的文档不能删除，并且请求将会失败。

# 删除多个索引(twitter,blog)的多个type(_docs,post)
curl -X POST "localhost:9200/twitter,blog/_docs,post/_delete_by_query" -H 'Content-Type: application/json' -d'
{
  "query": {
    "match_all": {}
  }
}

#  出自上向下删除1000条数据
curl -X POST "localhost:9200/twitter/_delete_by_query?scroll_size=1000" -H 'Content-Type: application/json' -d'
{
  "query": {
    "term": {
      "user": "kimchy"
    }
  }
}
```





## 参考资料
> - [Elasticsearch删除数据之_delete_by_query](https://www.jianshu.com/p/60a6ad164035)
> - []()
