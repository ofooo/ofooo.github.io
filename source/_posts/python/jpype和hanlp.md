---
title: jpype和hanlp 安装
toc: true
categories:
  - python
date: 2019-10-08 20:17:31
tags:
---



## 安装jpype

1. 安装jpype模块

```pip install jpype1```

2. 安装jvm

```bash
java -version  # bash会提示如何安装openjdk

sudo apt-get install openjdk-11-jre-headless  # ubuntu18

sudo apt-get install -y openjdk-9-jre-headless  # ubuntu16
```

3. 测试是否成功

```python
from jpype import *

startJVM(getDefaultJVMPath(), "-ea")

java.lang.System.out.println("Hello World")

shutdownJVM() 
```



## 使用hanlp

1. 安装包

```bash
pip install pyhanlp
```

2. 目录格式

```bash
static
|
|---data
|
|---hanlp.properties
|
|---hanlp-1.7.4.jar
```

3. 配置文件修改data文件夹所在的文件夹```hanlp.properties```
4. 设置环境变量

```python
import os
# jar所在文件夹
os.environ['HANLP_STATIC_ROOT'] = '/home/fish3/code/fish_code/hanlp_data/hanlp-1.7.4-release'
# jar文件所在路径
os.environ['HANLP_JAR_PATH'] = '/home/fish3/code/fish_code/hanlp_data/hanlp-1.7.4-release/hanlp-1.7.4.jar'  

import pyhanlp
```



5. 测试

```python
for term in pyhanlp.HanLP.segment('下雨天地面积水'):
    print('{}\t{}'.format(term.word, term.nature))  # 获取单词与词性


def test():
    sentence = pyhanlp.HanLP.parseDependency("徐先生还具体帮助他确定了把画雄鹰、松鼠和麻雀作为主攻目标。")
    for word in sentence.iterator():  # 通过dir()可以查看sentence的方法
        print("%s --(%s)--> %s" % (word.LEMMA, word.DEPREL, word.HEAD.LEMMA))
    print()
    # 也可以直接拿到数组，任意顺序或逆序遍历
    word_array = sentence.getWordArray()
    for word in word_array:
        print("%s --(%s)--> %s" % (word.LEMMA, word.DEPREL, word.HEAD.LEMMA))
    print()

    # 还可以直接遍历子树，从某棵子树的某个节点一路遍历到虚根
    CoNLLWord = pyhanlp.JClass("com.hankcs.hanlp.corpus.dependency.CoNll.CoNLLWord")
    head = word_array[12]
    while head.HEAD:
        head = head.HEAD
        if (head == CoNLLWord.ROOT):
            print(head.LEMMA)
        else:
            print("%s --(%s)--> " % (head.LEMMA, head.DEPREL))
    """
    输出：
        下雨天	n
        地面	n
        积水	n
        徐先生 --(主谓关系)--> 帮助
        还 --(状中结构)--> 帮助
        具体 --(状中结构)--> 帮助
        帮助 --(核心关系)--> ##核心##
        他 --(兼语)--> 帮助
        确定 --(动宾关系)--> 帮助
        了 --(右附加关系)--> 确定
        把 --(状中结构)--> 作为
        画 --(介宾关系)--> 把
        雄鹰 --(动宾关系)--> 画
        、 --(标点符号)--> 松鼠
        松鼠 --(并列关系)--> 雄鹰
        和 --(左附加关系)--> 麻雀
        麻雀 --(并列关系)--> 雄鹰
        作为 --(动宾关系)--> 确定
        主攻 --(定中关系)--> 目标
        目标 --(动宾关系)--> 作为
        。 --(标点符号)--> 帮助
        
        徐先生 --(主谓关系)--> 帮助
        还 --(状中结构)--> 帮助
        具体 --(状中结构)--> 帮助
        帮助 --(核心关系)--> ##核心##
        他 --(兼语)--> 帮助
        确定 --(动宾关系)--> 帮助
        了 --(右附加关系)--> 确定
        把 --(状中结构)--> 作为
        画 --(介宾关系)--> 把
        雄鹰 --(动宾关系)--> 画
        、 --(标点符号)--> 松鼠
        松鼠 --(并列关系)--> 雄鹰
        和 --(左附加关系)--> 麻雀
        麻雀 --(并列关系)--> 雄鹰
        作为 --(动宾关系)--> 确定
        主攻 --(定中关系)--> 目标
        目标 --(动宾关系)--> 作为
        。 --(标点符号)--> 帮助
        
        麻雀 --(并列关系)--> 
        雄鹰 --(动宾关系)--> 
        画 --(介宾关系)--> 
        把 --(状中结构)--> 
        作为 --(动宾关系)--> 
        确定 --(动宾关系)--> 
        帮助 --(核心关系)--> 
        ##核心##
    """

```







## 参考资料
> - []()
> - []()
