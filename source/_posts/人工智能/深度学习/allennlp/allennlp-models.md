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
