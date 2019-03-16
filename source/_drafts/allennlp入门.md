---
title: allennlp入门
tags: [NLP, allennlp, pytorch]
---



### Allennlp代码整体逻辑

1. 自定义对象 datareader(数据读取器)
   1. 必须有方法.read   dataset = datareader.read(数据文件)
   2. 默认dataset.instances 是数据集的每个实例，Instance 是由一个命名的field集合组成的
      1. instance.fields  是一个实例的所有字段
         1. fields['title'].tokens 是文本标记序列 
            1. tokens[0].text 是一个词汇文本
         2. fields['label'].label  是实例的正确分类标签文本
            key=‘label’ 能让数据变得更加通用（而不写具体数据种类）
   3. Field字段类(字段数据)
      1. 这些字段的数据是普通字符串，但是进入模型前会转化成ID
      2. TextField文本字段类
      3. LabelerField 范畴标签字段类
   4. Vocabulary类(词典)
      1. 有多个命名空间
      2. 默认命名空间 token 输入的词汇标记
      3. 默认命名空间 label 输出的标签
   5. Predictor类(预测器)  
      1. 包装一个模型，进行预测：json输入，json输出（而非张量）
      2. 需要重写predicotr.predict_json()函数，从输入json转成instance（带张量）
      3. 预测命令：```allennlp predict```
         1. 需要一个归档文件 ( 即一个训练好的模型 ) 
         2. 需要一个输入文件 ( 每行有一个 JSON 输入 )
   6. 网页演示
      1. 需要一个训练好的模型
      2. 需要写好预测器
2. 自定义对象 model
   1. 输入输出字典的value是张量
3. 配置一个json文件：写入模型和训练等参数

