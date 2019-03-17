---
title: es-搜索操作
toc: true
date: 2019-03-17 09:25:03
tags: [es, elastic_search, search, 搜索]
categories:
---



## 搜索备忘一

#### 	原生的url接口

```json 
# 搜索位置(url)
/_search					# 在所有的索引中搜索所有的类型
/gb/_search					# 在 gb 索引中搜索所有的类型
/gb,us/_search				# 在 gb 和 us 索引中搜索所有的文档
/g*,u*/_search				# 在任何以 g 或者 u 开头的索引中搜索所有的类型
/gb/user/_search			# 在 gb 索引中搜索 user 类型
/gb,us/user,tweet/_search	# 在 gb 和 us 索引中搜索 user 和 tweet 类型
/_all/user,tweet/_search	# 在所有的索引中搜索 user 和 tweet 类型

# 分页(url)
POST /_search				# 默认size=10, from=0 从0返回
POST /_search?size=5			# 第二页
POST /_search?size=5&from=5
POST /_search?size=5&from=10



# term  精确查找,不计算相关度.
{
    "term" : {
        "price" : 20
    }
}
# 用constant_score 把term包装成filter
POST /my_store/products/_search
{
    "query" : {
        "constant_score" : {
            "filter" : {
                "term" : {
                    "productID" : "XHDK-A-1293-#fJ3"
                }
            }
        }
    }
}


# range 过滤器(filter): age　> 30
# 过滤器执行速度非常快，不会计算相关度. 精确的筛选.
POST /megacorp/employee/_search
{
    "query" : {
        "bool": {
            "must": {
                		"match" : {"last_name" : "smith"  }
                    },
            "filter": {
                        "range" : {
                            "age" : { "gt" : 30 } 
                                  }
           			 }
       		  }
    }
}




# 全文搜索: 返回相关性排序的结果．　　如果有rock没有climbing也可能会返回结果.
POST /megacorp/employee/_search
{
    "query" : {
        "match" : {
            "about" : "rock climbing"
        }
    }
}
{
  "query": {
    "match_phrase": {
        "content" : {
            "query" : "我的宝马多少马力",
            "slop" : 1
        }
    }
  }
}
# 实际上下面的query才能正确返回结果，搜索的是content这个字段里包含对应文本的文档


# 精确匹配一系列单词或者短语
POST /megacorp/employee/_search
{
    "query" : {
        "match_phrase" : {
            "about" : "rock climbing"
        }
    }
}

# 高亮搜索
POST /megacorp/employee/_search
{
    "query" : {
        "match_phrase" : {
            "about" : "rock climbing"
        }
    },
    "highlight": {
        "fields" : {
            "about" : {}
        }
    }
}
# 返回:
{  ...
   "hits": {
      "total":      1,
      "max_score":  0.23013961,
      "hits": [
         {  ...
            "_score":         0.23013961,
            "_source": {
               "first_name":  "John",
               "about":       "I love to go rock climbing",
               "interests": [ "sports", "music" ]
            },
            "highlight": {
               "about": [
                  "I love to go <em>rock</em> <em>climbing</em>" 
               ]
            }
         }
      ]
   }
}

# 聚合（aggregations）: 统计某些标签的数量(是在搜索结果中进行统计,可以结合其他query)
POST /megacorp/employee/_search
{
  "aggs": {
    "all_interests": {
      "terms": { "field": "interests" }
    }
  }
}
```



## 搜索备忘二

http://www.cnblogs.com/yjf512/p/4897294.html



```json
组合式搜索
{
  "query": { 
    {
        "bool": {
            "must":     { "match": { "tweet": "elasticsearch" }},
            "must_not": { "match": { "name":  "mary" }},
            "should":   { "match": { "tweet": "full text" }},	# 这些match可以是数组
            "filter":   { "range": { "age" : { "gt" : 30 }} }
        }
    }  
  }  
}

```



# elasticsearch 查询（match和term）

es中的查询请求有两种方式，一种是简易版的查询，另外一种是使用JSON完整的请求体，叫做结构化查询（DSL）。
由于DSL查询更为直观也更为简易，所以大都使用这种方式。
DSL查询是POST过去一个json，由于post的请求是json格式的，所以存在很多灵活性，也有很多形式。
这里有一个地方注意的是官方文档里面给的例子的json结构只是一部分，并不是可以直接黏贴复制进去使用的。一般要在外面加个query为key的机构。

## match

最简单的一个match例子：

查询和"我的宝马多少马力"这个查询语句匹配的文档。

```
{
  "query": {
    "match": {
        "content" : {
            "query" : "我的宝马多少马力"
        }
    }
  }
}
```

上面的查询匹配就会进行分词，比如"宝马多少马力"会被分词为"宝马 多少 马力", 所有有关"宝马 多少 马力", 那么所有包含这三个词中的一个或多个的文档就会被搜索出来。
并且根据lucene的评分机制(TF/IDF)来进行评分。

## match_phrase

比如上面一个例子，一个文档"我的保时捷马力不错"也会被搜索出来，那么想要精确匹配所有同时包含"宝马 多少 马力"的文档怎么做？就要使用 match_phrase 了

```
{
  "query": {
    "match_phrase": {
        "content" : {
            "query" : "我的宝马多少马力"
        }
    }
  }
}
```

完全匹配可能比较严，我们会希望有个可调节因子，少匹配一个也满足，那就需要使用到slop。

```
{
  "query": {
    "match_phrase": {
        "content" : {
            "query" : "我的宝马多少马力",
            "slop" : 1
        }
    }
  }
}
```

## multi_match

如果我们希望两个字段进行匹配，其中一个字段有这个文档就满足的话，使用multi_match

```
{
  "query": {
    "multi_match": {
        "query" : "我的宝马多少马力",
        "fields" : ["title", "content"]
    }
  }
}
```

但是multi_match就涉及到匹配评分的问题了。

## 我们希望完全匹配的文档占的评分比较高，则需要使用best_fields

```
{
  "query": {
    "multi_match": {
      "query": "我的宝马发动机多少",
      "type": "best_fields",
      "fields": [
        "tag",
        "content"
      ],
      "tie_breaker": 0.3
    }
  }
}
```

意思就是完全匹配"宝马 发动机"的文档评分会比较靠前，如果只匹配宝马的文档评分乘以0.3的系数

## 我们希望越多字段匹配的文档评分越高，就要使用most_fields

```
{
  "query": {
    "multi_match": {
      "query": "我的宝马发动机多少",
      "type": "most_fields",
      "fields": [
        "tag",
        "content"
      ]
    }
  }
}
```

## 我们会希望这个词条的分词词汇是分配到不同字段中的，那么就使用cross_fields

```
{
  "query": {
    "multi_match": {
      "query": "我的宝马发动机多少",
      "type": "cross_fields",
      "fields": [
        "tag",
        "content"
      ]
    }
  }
}
```

# term

term是代表完全匹配，即不进行分词器分析，文档中必须包含整个搜索的词汇

```
{
  "query": {
    "term": {
      "content": "汽车保养"
    }
  }
}
```

查出的所有文档都包含"汽车保养"这个词组的词汇。

使用term要确定的是这个字段是否“被分析”(analyzed)，默认的字符串是被分析的。

拿官网上的例子举例：

mapping是这样的：

```
PUT my_index
{
  "mappings": {
    "my_type": {
      "properties": {
        "full_text": {
          "type":  "string"
        },
        "exact_value": {
          "type":  "string",
          "index": "not_analyzed"
        }
      }
    }
  }
}

PUT my_index/my_type/1
{
  "full_text":   "Quick Foxes!",
  "exact_value": "Quick Foxes!"  
}
```

其中的full_text是被分析过的，所以full_text的索引中存的就是[quick, foxes]，而extra_value中存的是[Quick Foxes!]。

那下面的几个请求：

```
GET my_index/my_type/_search
{
  "query": {
    "term": {
      "exact_value": "Quick Foxes!"
    }
  }
}
```

请求的出数据，因为完全匹配

```
GET my_index/my_type/_search
{
  "query": {
    "term": {
      "full_text": "Quick Foxes!"
    }
  }
}
```

请求不出数据的，因为full_text分词后的结果中没有[Quick Foxes!]这个分词。

## bool联合查询: must,should,must_not

如果我们想要请求"content中带宝马，但是tag中不带宝马"这样类似的需求，就需要用到bool联合查询。
联合查询就会使用到must,should,must_not三种关键词。

这三个可以这么理解

- must: 文档必须完全匹配条件
- should: should下面会带一个以上的条件，至少满足一个条件，这个文档就符合should
- must_not: 文档必须不匹配条件

比如上面那个需求：

```
{
  "query": {
    "bool": {
      "must": {
        "term": {
          "content": "宝马"
        }
      },
      "must_not": {
        "term": {
          "tags": "宝马"
        }
      }
    }
  }
}
```

## 参考资料
> - []()
> - []()
