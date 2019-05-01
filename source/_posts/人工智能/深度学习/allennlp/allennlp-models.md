---
title: allennlp_models
toc: true
tags:
  - allennlp
  - pytorch
categories:
  - 人工智能
  - 深度学习
  - allennlp
date: 2019-03-29 17:29:52
---





## crf_tagger

allennlp/models/crf_tagger.py   class CrfTagger

```python
`CrfTagger`使用`Seq2SeqEncoder`编码一系列文本，
然后使用条件随机场模型来预测序列中每个标记的标记。

参数
----------
vocab：`Vocabulary'，必需
 用于计算输入/输出尺寸大小所需的词汇表。
text_field_embedder：`TextFieldEmbedder`，必需
    用于嵌入标记`TextField`，我们将其作为模型的输入。
encoder：`Seq2SeqEncoder`
    我们将在嵌入令牌和预测输出标签之间使用的编码器。
label_namespace：`str`，optional（默认 =`labels`）
    这是计算SpanBasedF1Measure指标所必需的。
    除非你做了一些特殊处理，否则默认值即可。
feedforward：`FeedForward`，可选，（默认=None）。
    在编码器之后应用的可选前馈层。
label_encoding：`str`，optional（默认=None）
    在计算跨度f1时使用的标签编码，并在解码时限制CRF。有效选项是“BIO”，“BIOUL”，“IOB1”，“BMES”。
    如果`calculate_span_f1`或`constrain_crf_decoding`为真，则为必需。
include_start_end_transitions：`bool`，可选（默认=True）
    是否在CRF中包含开始和结束转换参数。
constrain_crf_decoding：`bool`，optional（默认=None）
    如果为“True”，则CRF在解码时被约束以产生有效的标签序列。如果这是'True`，则需要`label_encoding`。如果指定了“None”和label_encoding，则将其设置为“True”。
    如果未指定`None`和label_encoding，则默认为'False`。
calculate_span_f1：`bool`，可选（默认=None）
    在培训期间计算跨度级F1指标。如果这是'True`，则需要`label_encoding`。如果指定了“None”和label_encoding，则将其设置为“True”。
    如果未指定`None`和label_encoding，则默认为'False`。
dropout：`float`，optional（默认=None）
verbose_metrics：`bool`，可选（默认= False）
    如果为true，则除了整体统计信息之外，还将为每个标签类返回指标。
初始化程序：`InitializerApplicator`，可选（默认=`InitializerApplicator（）`）
    用于初始化模型参数。
正规化器：`RegularizerApplicator`，可选（默认=None）
    如果提供，将用于计算训练期间的正则化惩罚。
```





## Coreference Resolution 指代消解

该模型在CoNLL测试集的F1达到63.0%

```python
# 引用模型
from allennlp.predictors.predictor import Predictor
predictor = Predictor.from_path("https://s3-us-west-2.amazonaws.com/allennlp/models/coref-model-2018.02.05.tar.gz")
predictor.predict(
  document="The woman reading a newspaper sat on the bench with her dog."
)
```

## Named Entity Recognition 命名实体识别

模型使用ELMo嵌入的biLSTM







## 参考资料
> - [<https://allennlp.org/models>](<https://allennlp.org/models>)
> - []()
