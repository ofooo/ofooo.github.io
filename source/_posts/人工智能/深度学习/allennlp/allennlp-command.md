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

```
Trainer
参数
----------
model：``Model``，必需。
要优化的AllenNLP模型，或者是Pytorch模块（它的forward方法必须返回字典，并包含key=“loss”，value=scalar tensor）

optimizer：``torch.nn.Optimizer``，必需。
  Pytorch Optimizer的一个实例，使用要优化的模型的参数进行实例化。
  
iterator：``DataIterator``，必需。
    迭代“Dataset”的方法，产生填充并转成索引的批次数据。
    
train_dataset：``Dataset``，必需。
    要训练的“Dataset”。数据集应该已经转成索引。
    
validation_dataset：``Dataset``，可选，（默认=无）。
    要评估的“Dataset”。数据集应该已经转成索引。
    
patience：可选[int]> 0，可选（默认=无）
    在early stopping之前要观察的epoch数量：在“patience”个epoch都没有改善则提早停止。如果给出，它必须是“> 0”。
    如果为None，则禁用early stopping。
    
validation_metric：str，optional（default =“loss”）
    用来衡量是否使用提早停止以及是否在每个epoch存储is_best模型。度量标准名称必须以“+”或“ - ”为前缀，指定度量标准是增加还是减少。
    
validation_iterator：``DataIterator``，可选（默认=无）
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
    
model_save_interval：``float``，可选（默认=无）
    如果提供，则在单个epoch中每隔N秒存储一次模型。如果提供serialization_dir在每个epoch结束时也会保存模型。
    
cuda_device：``int``，可选（默认= -1）
    一个整数，指定要使用的CUDA设备。如果为-1，则使用CPU。
    
grad_norm：``float``，可选，（默认=无）。
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



### tensorboard



```python
class TensorboardWriter(get_batch_num_total: Callable[int], serialization_dir: Optional[str] = None, summary_interval: int = 100, histogram_interval: int = None, should_log_parameter_statistics: bool = True, should_log_learning_rate: bool = False)

get_batch_num_total：Callable [[]，int]
到目前为止返回批次数的thunk。 很可能这将是一个围绕Trainer类中的实例变量的闭包。

serialization_dir：str，optional（默认=无）
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
