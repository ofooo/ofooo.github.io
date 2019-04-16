---
title: allennlp 命令执行流程
toc: true
tags:
  - allennlp
  - command
  - 命令
categories:
  - 人工智能
  - 深度学习
  - allennlp
date: 2019-03-31 19:09:04
---

## 安装tensorboard

```bash
# 先要安装tensorboard和tensorflow
pip install tensorflow tensorboard

# 再安装tensorboardx
pip install tensorboardX

```





## 命令执行流程

```python
# 程序入口： allennlp.commands.main()


# subparser 子命令:
"configure": allennlp.commands.configure.Configure()
"train": allennlp.commands.train.Train()
"evaluate": allennlp.commands.evaluate.Evaluate()
"predict": allennlp.commands.predict.Predict()
"make-vocab": allennlp.commands.make_vocab.MakeVocab()
"elmo": allennlp.commands.elmo.Elmo()
"fine-tune": allennlp.commands.fine_tune.FineTune()
"dry-run": allennlp.commands.dry_run.DryRun()
"test-install": allennlp.commands.test_install.TestInstall()
"find-lr": allennlp.commands.find_learning_rate.FindLearningRate()
```

## 训练流程调用的类和方法

```python
>>> allennlp train XXX
allennlp/commands/__init__.py  main()
allennlp/commands/train.py  Train()
allennlp/commands/train.py  Train.train_model_from_args()
allennlp/commands/train.py  Train.train_model_from_file()
allennlp/commands/train.py  Train.train_model()
allennlp/training/trainer.py  Trainer()
allennlp/training/trainer.py  Trainer.train()
allennlp/training/trainer.py  Trainer._train_epoch()

```






```bash
# 训练
# -r就会使用之前已经创建好的词典
allennlp train XXX -s XXX



# 启动配置助手(网页)
allennlp configure --port 8123

```

### Trainer初始化参数

```bash
Trainer
初始化参数
----------
model：``Model``，必需。
要优化的AllenNLP模型，或者是Pytorch模块（它的forward方法必须返回字典，并包含key=“loss”，value=scalar tensor）

optimizer：``torch.nn.Optimizer``，必需。
  Pytorch Optimizer的一个实例，使用要优化的模型的参数进行实例化。
  
iterator：``DataIterator``，必需。
    迭代“Dataset”的方法，产生填充并转成索引的批次数据。
    
train_dataset：``Dataset``，必需。
    要训练的“Dataset”。数据集应该已经转成索引。
    
validation_dataset：``Dataset``，可选，（默认=None）。
    要评估的“Dataset”。数据集应该已经转成索引。
    
patience：可选[int]> 0，可选（默认=None）
    在early stopping之前要观察的epoch数量：在“patience”个epoch都没有改善则提早停止。如果给出，它必须是“> 0”。
    如果为None，则禁用early stopping。
    
validation_metric：str，optional（default =“loss”）
    用来衡量是否使用提早停止以及是否在每个epoch存储is_best模型。度量标准名称必须以“+”或“ - ”为前缀，指定度量标准是增加还是减少。
    
validation_iterator：``DataIterator``，可选（默认=None）
    用于验证集的迭代器。如果是None，那么使用训练集的iterator。
    
shuffle：``bool``，可选（默认= True）
    是否在迭代器中对实例进行随机洗牌。
    
num_epochs：int，optional（默认值= 20）
    培训epoch数量。 
    
serialization_dir：str，optional（默认=None）
    用于保存和加载模型文件的目录路径。如果未传递此参数，则不会保存模型。
    
num_serialized_models_to_keep：``int``，可选（默认= 20）
    要保留的先前模型检查点的数量。默认是保留20个检查点。
    值为None或-1表示将保留所有检查点。
    
keep_serialized_model_every_num_seconds：``int``，可选（默认=None）
    如果num_serialized_models_to_keep不是None，那么除了最后一个
num_serialized_models_to_keep之外，偶尔以给定间隔保存模型也很有用。
    为此，请将keep_serialized_model_every_num_seconds指定为永久保存的检查点之间的秒数。请注意，此选项仅在以下情况下使用
    num_serialized_models_to_keep不是None，否则保留所有检查点。
    
model_save_interval：``float``，可选（默认=None）
    如果提供，则在单个epoch中每隔N秒存储一次模型。如果提供serialization_dir在每个epoch结束时也会保存模型。
    
cuda_device：``int``，可选（默认= -1）
    一个整数，指定要使用的CUDA设备。如果为-1，则使用CPU。
    
grad_norm：``float``，可选，（默认=None）。
    如果提供，则会按最大值调整梯度。
    
grad_clipping：``float``，可选（默认=``无``）。
    如果提供，渐变将在“向后传递”期间被剪切以具有该值的（绝对）最大值。如果你在训练期间在渐变中得到“NaNs”
    使用``grad_norm``无法解决，你可能需要这个。
    
learning_rate_scheduler：``PytorchLRScheduler``，可选，（默认=None）
    Pytorch学习速率调度程序。在每个epoch结束时，学习率将相对于该时间表衰减。如果你使用`torch.optim.lr_scheduler.ReduceLROnPlateau类`，这将使用提供的`validation_metric`来确定学习是否已达到稳定状态。支持每个batch更新学习率，这可以选择实现step_batch（batch_num_total），它更新给定batch的学习率。
    
summary_interval：``int``，可选，（默认= 100）
    记录标量到tensorboard之间的批次数
    
histogram_interval：``int``，optional，（default =``None``）
    如果不是None，则每N个batch的柱状图记录到tensorboard。
    指定此参数后，将启用以下附加日志记录：
        *模型参数的柱状图
        *参数更新率
        *层激活的柱状图
    我们记录model.get_parameters_for_histogram_tensorboard_logging 返回的参数的柱状图。
    对于``Model``中具有属性``should_log_activations``设置为``True``的任何模块，都会记录图层激活。记录柱状图在训练期间需要许多GPU-CPU副本，并且通常很慢，因此我们建议相对不频繁地记录柱状图。
    注意：只有返回张量的模块，张量的元组或dict支持activations日志。
    
should_log_parameter_statistics：``bool``，可选，（默认= True）
是否发送参数统计（平均值和标准差）
参数和梯度）到张量板。

should_log_learning_rate：``bool``，可选，（默认= False）
是否将参数特定学习率发送到tensorboard。

log_batch_size_period：``int``，optional，（default =``None``）
如果已定义，则记录平均批量大小的频率。“”
```

### Vocabulary

```bash
tag--序列标记（NER输出等）    label--类别标签（分类任务输出等）

词汇表将字符串映射到整数，允许将字符串映射到OOV标记（out-of-vocabulary OOV）。

词汇表适合特定的数据集，我们用它来决定哪些tokens是词汇表内的。

词汇表还允许使用多个不同的命名空间，因此你可以有不同的index对应单词“a”和字符“a”。例如我们可以使用此对象将tags和labels文本映射到index，用一个统一的类：xxx_Field。此类中的大多数方法都允许你传入命名空间; 默认情况下，我们使用'tokens'命名空间，你可以在任何地方省略命名空间参数，只使用默认值。

参数
----------
counter：`Dict [str，Dict [str，int]]`，可选（默认=`None`）
    用于初始化此词汇表的计数集合。我们将检查计数，并与该类的其他参数一起使用它们来决定哪些单词是词汇表。如果这是None，我们就不会用任何东西初始化词汇表。
min_count：`Dict [str，int]`，可选（默认=None）
    从计数器初始化词汇表时，你可以指定最小计数，并且计数小于此值的每个标记都不会添加到词典中。这些最小计数是“特定于命名空间的”，因此你可以为标签与单词指定不同的最小值。如果命名空间在给定的字典中没有key，我们将所有看到的标记添加到该命名空间。
max_vocab_size：`Union [int，Dict [str，int]]`，可选（默认=None）
    如果要限制词汇表中的令牌数量，可以使用此参数执行此操作。如果指定单个整数，则每个命名空间的词汇表都将固定为不大于此值。如果指定一个字典，那么`counter`中的每个命名空间都可以有一个单独的最大词汇量。任何缺失的键都将具有值“None”，这意味着词汇量大小没有上限。
non_padded_namespaces：`Iterable [str]`，可选
    默认情况下，我们假设你将单词/字符标记映射为整数，因此你希望为padding和OOV保留单词索引。但是，如果要将NER或SRL的tag或类别标签映射到整数，则可能不希望保留padding和OOV索引。使用此字段指定哪些名称空间不应添加padding和OOV标记。

    这个元素的格式是一个字符串，它必须与字段名称完全匹配，或者`*`后跟一个字符串，我们将它们作为字段名称的后缀。

    我们尝试使默认值合理，这样你就不必考虑这一点。 默认为（tags，labels），因此只要您的命名空间以“tags”或“labels”结尾（默认情况下，此代码中的所有tag和labels字段均为true）， 不必在这里指定任何东西。
pretrained_files：`Dict [str，str]`，可选
    如果提供，此映射指定每个命名空间的可选预训练嵌入文件的路径。这可以用于将词汇表限制为仅出现在此文件中的单词，或者确保此文件中的任何单词都包含在词汇表中，而不管其计数如何，具体取决于“only_include_pretrained_words”的值。
    出现在预训练嵌入文件中但未出现在数据中的单词不包含在词汇表中。
min_pretrained_embeddings：`Dict [str，int]`，可选
    如果提供，则为每个命名空间指定与预训练嵌入文件保持一致的最小行数（通常是最常用的单词），即使对于未出现在数据中的单词也是如此。
only_include_pretrained_words：`bool`，可选（默认= False）
    这定义了使用可能在`pretrained_files`中指定的任何预训练嵌入文件的策略。如果为False，则使用包含策略：并且将“计数器”和预训练文件中的单词添加到“词汇表”中，而不管它们的计数是否超过“min_count”。如果为True，我们使用独占策略：如果单词位于预训练嵌入文件中，则单词仅包含在词汇表中（它们的计数必须至少为'min_count`）。
tokens_to_add：`Dict [str，List [str]]`，可选（默认=None）
    如果给定，这是一个要添加到词汇表的标记列表，由命名空间键入以添加标记。这是一种确保某些项目出现在词汇表中的方法，无论其他任何词汇计算如何。
```

### tensorboard



```python
class TensorboardWriter(get_batch_num_total: Callable[int], serialization_dir: Optional[str] = None, summary_interval: int = 100, histogram_interval: int = None, should_log_parameter_statistics: bool = True, should_log_learning_rate: bool = False)

get_batch_num_total：Callable [[]，int]
到目前为止返回批次数的thunk。 很可能这将是一个围绕Trainer类中的实例变量的闭包。

serialization_dir：str，optional（默认=None）
如果提供，则这是Tensorboard日志的写入位置。

summary_interval：int，optional（默认值= 100）
大多数统计数据只会在这么多批次中写出来。

histogram_interval：int，optional（default = None）
如果提供，则每隔这些批次就会记录激活柱状图。 如果为None，则不会写。

should_log_parameter_statistics：bool，optional（default = True）
是否记录参数统计信息。

should_log_learning_rate：bool，optional（默认= False）
是否记录学习率。
```



## 参考资料
> - []()
> - []()
