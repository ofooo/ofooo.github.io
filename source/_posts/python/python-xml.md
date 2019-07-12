---
title: python-xml解析
toc: true
tags:
  - python
  - xml
date: 2019-07-12 08:58:58
categories:
---





## 参考资料
> - []()
> - []()




asd

### xml--可扩展标记语言

```xml
<?xml version="1.0" encoding="utf-8"?>
<catalog>
    <maxid>4</maxid>
    <login username="pytest" passwd='123456'>
        <caption>Python</caption>
        <item id="4">
            <caption>test</caption>
        </item>
    </login>
    <item id="2">
        <caption>Zope</caption>
    </item>
</catalog>
```

- xml是由**标签对**组成，```<aa></aa>```
  - 标签可以有属性： ``` <aa id='123'></aa>```
  - 标签对可以嵌入数据：```<aa>数据</aa>```
  - 标签可以嵌入子标签（具有层级关系）



### 获取标签和属性

```python
#coding: utf-8
import xml.dom.minidom
dom = xml.dom.minidom.parse("xxx.xml")  #打开xml文档

root = dom.documentElement             #得到xml文档对象
print("nodeName:", root.nodeName)      #每一个结点都有它的nodeName，nodeValue，nodeType属性
print("nodeValue:", root.nodeValue)    #nodeValue是结点的值，只对文本结点有效
print("nodeType:", root.nodeType)
print("ELEMENT_NODE:", root.ELEMENT_NODE)
# 输出 nodeName: catalog
# 输出 nodeValue: None
# 输出 nodeType: 1
# 输出 ELEMENT_NODE: 1
```

nodeType是结点的类型。catalog是ELEMENT_NODE类型

| 节点编号： | 节点类型的名称：      | 说明                                                   | 返回的节点名称     | 返回的节点值 |
| ---------- | --------------------- | ------------------------------------------------------ | ------------------ | ------------ |
| 1          | Element               | 表示一个元素                                           | 元素名称           | null         |
| 2          | Attribute             | 代表一个属性                                           | 属性名称           | 属性值       |
| 3          | Text                  | 代表元素或属性的文本内容                               | #text              | 节点的内容   |
| 4          | CDATA Section         | 代表文档中的 CDATA 区段（文本不会被解析器解析）        | #cdata-section     | 节点的内容   |
| 5          | Entity Reference      | 代表一个实体引用                                       | 实体引用名称       | null         |
| 6          | Entity                | 代表一个实体                                           | 实体名称           | null         |
| 7          | Processing Instrucion | 代表一个处理指令                                       | 目标               | 节点的内容   |
| 8          | Comment               | 代表一个注释                                           | #comment           | 注释文本     |
| 9          | Document              | 代表整个文档（DOM 树的根节点）                         | #document          | null         |
| 10         | Document Type         | 为文档中定义的实体提供了一个接口                       | 文档类型名称       | null         |
| 11         | Document Fragment     | 代表"轻量级"的 Document 对象，它可以保留文档中的一部分 | #document fragment | null         |
| 12         | Notation              | 定义一个在 DTD 中声明的符号                            | 符号名称           | null         |

[w3school](http://www.w3school.com.cn/xmldom/prop_element_nodetype.asp)

[菜鸟教程--更详细](http://www.runoob.com/dom/dom-nodetype.html)

### 获取子标签

```python
bb = root.getElementsByTagName('maxid')
print(type(bb))  	# === <class 'xml.dom.minicompat.NodeList'>
print(bb)    		# === [<DOM Element: maxid at 0x2707a48>]
b = bb[0]
print(b.nodeName)	# === maxid
print(b.nodeValue)	# === None
```



```python
minidom.parse(filename)
加载读取XML文件
 
doc.documentElement
获取XML文档对象
 
node.getAttribute(AttributeName)
获取XML节点属性值
 
node.getElementsByTagName(TagName)
获取XML节点对象集合
 
node.childNodes #返回子节点列表。
 
node.childNodes[index].nodeValue
获取XML节点值
 
node.firstChild
#访问第一个节点。等价于pagexml.childNodes[0]
 
doc = minidom.parse(filename)
doc.toxml('UTF-8')
返回Node节点的xml表示的文本
 
Node.attributes["id"]
a.name #就是上面的 "id"
a.value #属性的值
访问元素属性
```

