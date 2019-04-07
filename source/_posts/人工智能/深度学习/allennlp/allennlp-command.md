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



## 参考资料
> - []()
> - []()
