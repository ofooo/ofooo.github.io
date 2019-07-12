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



Successfully installed Jinja2-2.10.1 MarkupSafe-1.1.1 PyYAML-5.1 Pygments-2.4.2 Werkzeug-0.15.4 alabaster-0.7.12 allennlp-0.8.4 atomicwrites-1.3.0 attrs-19.1.0 awscli-1.16.190 babel-2.7.0 blis-0.2.4 boto3-1.9.180 botocore-1.12.180 click-7.0 colorama-0.3.9 conllu-0.11 cycler-0.10.0 cymem-2.0.2 docutils-0.14 editdistance-0.5.3 flaky-3.6.0 flask-1.0.3 flask-cors-3.0.8 ftfy-5.5.1 gevent-1.4.0 greenlet-0.4.15 h5py-2.9.0 imagesize-1.1.0 importlib-metadata-0.18 itsdangerous-1.1.0 jmespath-0.9.4 joblib-0.13.2 jsonnet-0.13.0 jsonpickle-1.2 jsonschema-3.0.1 kiwisolver-1.1.0 matplotlib-3.1.0 more-itertools-7.1.0 murmurhash-1.0.2 nltk-3.4.3 numpy-1.16.4 numpydoc-0.9.1 overrides-1.9 packaging-19.0 parsimonious-0.8.1 plac-0.9.6 pluggy-0.12.0 preshed-2.0.1 protobuf-3.8.0 py-1.8.0 pyasn1-0.4.5 pyparsing-2.4.0 pyrsistent-0.15.2 pytest-5.0.0 python-dateutil-2.8.0 pytorch-pretrained-bert-0.6.2 pytz-2019.1 regex-2019.6.8 responses-0.10.6 rsa-3.4.2 s3transfer-0.2.1 scikit-learn-0.21.2 scipy-1.3.0 snowballstemmer-1.9.0 spacy-2.1.4 sphinx-2.1.2 sphinxcontrib-applehelp-1.0.1 sphinxcontrib-devhelp-1.0.1 sphinxcontrib-htmlhelp-1.0.2 sphinxcontrib-jsmath-1.0.1 sphinxcontrib-qthelp-1.0.2 sphinxcontrib-serializinghtml-1.1.3 sqlparse-0.3.0 srsly-0.0.7 tensorboardX-1.7 thinc-7.0.4 torch-1.1.0 tqdm-4.32.2 unidecode-1.1.1 wasabi-0.2.2 wcwidth-0.1.7 word2number-1.1 zipp-0.5.1



## 安装tensorboard

```bash
# 先要安装tensorboard和tensorflow
pip install tensorflow tensorboard

# 再安装tensorboardx
pip install tensorboardX

```





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






```python
# 训练
# -r就会使用之前已经创建好的词典
allennlp train XXX -s XXX



# 启动配置助手(网页)
allennlp configure --port 8123

```

## 词汇对照表

| 英文    | 中文                       |
| ------- | -------------------------- |
| tag     | 序列标记（NER输出等）      |
| label   | 类别标签（分类任务输出等） |
| index   | 索引                       |
| padding | 填充                       |
|         |                            |
|         |                            |
|         |                            |
|         |                            |
|         |                            |



### Trainer初始化参数

```python
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

```python


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

## indexer索引器

```python
TokenIndexer
“TokenIndexer”确定字符串标记如何表示为模型中的索引数组。
这个类在a的帮助下将字符串转换为数值
：class：`~allennlp.data.vocabulary.Vocabulary`，它产生实际的数组。

标记可以表示为单个ID（例如，单词“cat”由数字表示
34），或作为字符ID列表（例如，“cat”由数字[23,10,18]表示），
或以某种其他方式，你可以提出（例如，如果你有一些结构化的输入你
想要在数据数组中以特殊方式表示，你可以在这里做到这一点）。
default_implementation ='single_id'

def count_vocab_items（self，token：Token，counter：Dict [str，dict [str，int]]）：
  ：class：`Vocabulary`需要为我们在训练数据中看到的任何字符串分配索引（可能进行一些频率过滤和使用OOV，或者使用词汇表，令牌）。对于令牌中存在的任何词汇项，此方法采用令牌和计数字典和增量计数。如果这是单个令牌ID表示，则词汇表项可能是令牌本身。如果这是令牌字符表示，则词汇表项是令牌中的所有字符。
def tokens_to_indices（self，tokens：List [Token]，词汇：Vocabulary，index_name：str） - > Dict [str，List [TokenType]]：
  获取令牌列表并将其转换为一组或多组索引。这可能只是词​​汇表中每个标记的ID。或者它可以将每个标记分成字符并返回每个字符一个ID。或者（例如，在字节对编码的情况下）可能没有从单个令牌到索引的干净映射。

def get_padding_token（self） - > TokenType：
  当我们需要添加填充令牌时，它们应该是什么样的？此方法返回由以下函数返回的任何类型的“空白”标记：func：`tokens_to_indices`。

def get_padding_lengths（self，token：TokenType） - > Dict [str，int]：
  此方法返回给定标记的填充字典，该字典指定需要填充的所有数组的长度。例如，对于单个ID令牌，返回的字典将为空，但对于令牌字符表示，这将返回令牌中的字符数。

def pad_token_sequence（self，tokens：Dict [str，List [TokenType]]，desired_num_tokens：Dict [str，int]，padding_lengths：Dict [str，int]） - > Dict [str，List [TokenType]]：
  此方法将令牌列表填充到“desired_num_tokens”并返回输入令牌的填充副本。如果输入标记列表长于“desired_num_tokens”，那么它将被截断。
 `padding_lengths`用于提供在某些情况下需要的补充填充参数。例如，它包含在执行字符级填充时填充字符的宽度。

def get_keys（self，index_name：str） - > List [str]：
  返回此索引器从`tokens_to_indices`返回的键列表。
```



## Field 字段

### Field 字段基类



```python
Field
“字段”是instance数据实例的一部分，最终作为模型中的张量（作为输入或输出）。 数据实例只是字段的集合。
  字段最多经历两个处理步骤：（1）将标记化字段转换为标记ID，（2）填充包含标记id（或任何其他数字数据）的字段（如果需要）并转换为张量。 `Field`API有这两个步骤的方法，虽然它们可能不需要一些具体的`Field`类 - 如果你的字段没有任何需要索引的字符串，你不需要实现`count_vocab_items` 或`索引`。 这些方法默认为`pass`。
  一旦计算出词汇表并对所有字段编制索引，我们将确定填充长度，然后智能地将实例批处理并将它们填充到实际张量中。

def count_vocab_items（self，counter：Dict [str，dict [str，int]]）：“”“如果这个字段中的字符串需要通过：class：`Vocabulary`转换成整数，这里就是我们统计它们的位置，以确定哪些令牌在词汇表之内或之外。
 如果你的`Field`没有任何需要转换为索引的字符串，你不需要实现这个方法。
 关于这个`counter`的注释：因为`Fields`可以代表概念上不同的东西，我们用`namespaces`分隔词汇项。这样，我们可以使用单个共享机制来处理从字符串到所有字段中的整数的所有映射，同时保持`TextField`中的单词与`LabelField`中的标签共享相同的id（例如，"entailment" or "contradiction"是蕴涵任务中的标签”
 另外，单个`Field`可能想要使用多个名称空间 - “TextFields”可以表示为单词ID和字符id的组合，并且您不希望单词和字符共享相同的vocabulary - “a”作为单词应该从“a”作为一个字符获得不同的id，并且单词和字符的词汇量大小非常不同。
 因此，`counter`对象中的第一个键是`namespace'，如“tokens”，“token_characters”，“tags”或“labels”，第二个键是实际的词汇表项item。 

def index（self，vocab：Vocabulary）：
 给定一个：class：`Vocabulary`，将该字段中的所有字符串转换为（通常）整数。这个`修改``Field`对象，它不返回任何东西。
 如果你的`Field`没有任何需要转换为索引的字符串，你不需要实现这个方法。

def get_padding_lengths（self） - > Dict [str，int]：
 如果此字段中有需要填充的内容，请在此处记下。为了填充一批实例，我们从批处理中获取所有长度，取最大值，并将所有内容填充到该长度（或使用预先指定的最大长度）。返回值是将键映射到长度的字典，例如{'num_tokens'：13}。
 这总是在：func：`index`之后调用。 msgstr“”“引发NotImplementedError

def as_tensor（self，padding_lengths：Dict [str，int]） - > DataArray：
 给定一组指定的填充长度，实际填充此字段中的数据并返回正确形状的割炬张量（或更复杂的数据结构）。我们还采用了一些在构建火炬传感器时很重要的参数。
 参数---------- padding_lengths：`Dict [str，int]`这个字典将具有与func：`get_padding_lengths`相同的键。这些值指定填充每个相关维度时使用的长度，这些维度在批处理中的所有实例之间聚合。 msgstr“”“引发NotImplementedError

def empty_field（self） - >'Field'：
 因此`ListField`可以填充列表中的字段数（例如，答案选项`TextFields`的数量），我们需要表示每种类型的空字段。这会返回。这只会在我们调用时调用：func：`as_tensor`，所以你不必担心在这个空字段上调用`get_padding_lengths`，`count_vocab_items`等等。
 我们使这个实例方法而不是静态方法，这样如果Field中有任何状态，我们可以复制它（例如，`TextField`中的标记索引器）。 msgstr“”“引发NotImplementedError

def batch_tensors（self，tensor_list：List [DataArray]） - > DataArray：#type：ignore从`Instances`列表中获取`Field.as_tensor（）`的输出，并将其合并为一个批量张量为此`Field` 。这里基类的默认实现处理`as_tensor`为每个实例返回一个火炬张量的情况。如果您的子类返回除此之外的其他内容，则需要覆盖此方法。
 这个操作不会修改`self`，但在某些情况下我们需要`self`中包含的信息来执行批处理，所以这是一个实例方法，而不是类方法。 “”#pylint：disable = no-self-use return torch.stack（tensor_list）
```

### SequenceField  序列字段

```python
SequenceField
`SequenceField`代表一系列事物。 这个类只是在`Field` :: func：`sequence_length`上添加了一个方法。 它的存在使得`SequenceLabelField`，`IndexField`和其他类似的`Fields`可以有一个类型要求，具有一致的API，它们是指向`TextField`中的单词，`ListField`中的项目，还是 别的。
```

### TextField 文本字段

```python
TextField
这个`Field`代表一个字符串标记列表。 在构造此对象之前，需要使用：class：`~allennlp.data.tokenizers.tokenizer.Tokenizer`来标记原始字符串。

因为字符串标记可以通过多种方式表示为索引数组，所以我们还会使用以下字典：class：`~allennlp.data.token_indexers.token_indexer.TokenIndexer`对象，用于将标记转换为索引。 每个“TokenIndexer”可以将每个标记表示为单个ID，或者字符ID列表或其他内容。

该字段将被转换为数组字典，每个`TokenIndexer`一个。 `SingleIdTokenIndexer`生成一个形状数组（num_tokens，），而`TokenCharactersIndexer`生成一个形状数组（num_tokens，num_characters）。
```

### SequenceLabelField

```python
SequenceLabelField

`SequenceLabelField`为a中的每个元素分配一个分类标签
产品类别：`〜allennlp.data.fields.sequence_field.SequenceField`。
因为它是某个其他字段的标签，我们在此处将该字段作为输入，我们将其用于
确定我们的填充和其他东西。

此字段将转换为整数类ID列表，表示正确的类
对于序列中的每个元素。

参数
----------
标签：`Union [List [str]，List [int]]`
 一系列分类标签，编码为字符串或整数。这些可能是POS标签，如[NN，JJ，...]，BIO标签，如[B-PERS，I-PERS，O，O，...]，或任何其他分类标签序列。如果标签被编码为整数，则不会使用词汇对其进行索引。
sequence_field：`SequenceField`
 包含此SequenceLabelField`标记序列的字段。大多数情况下，这是一个“TextField”，用于标记句子中的单个标记。
label_namespace：`str`，optional（default ='labels'）
 用于将标记字符串转换为整数的命名空间。我们将标记字符串转换为整数，并且此参数告诉`Vocabulary`对象从字符串到整数的映射使用（因此“O”作为标记不会获得与“O”作为单词相同的id） 。
“””
＃用户可能希望将此字段与使用OOV / PAD令牌的命名空间一起使用。
＃对于此类的每个实例化（即每个数据），将重复此警告
#instance），喷出很多警告，所以这个类变量只用于记录单个变量
每个命名空间＃警告。
```



## 参考资料
> - []()
> - []()
