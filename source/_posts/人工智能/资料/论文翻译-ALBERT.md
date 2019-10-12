---
title: 论文翻译: ALBERT: A LITE BERT FOR SELF-SUPERVISED LEARNING OF LANGUAGE REPRESENTATIONS
toc: true
date: 2019-10-12 18:21:20
tags:
categories:
---

## A LITE BERT FOR SELF-SUPERVISED LEARNING OF LANGUAGE REPRESENTATIONS

## 小型BERT (自监督学习语言表征)

原文链接: https://openreview.net/pdf?id=H1eA7AEtvS



> ABSTRACT
>
> Increasing model size when pretraining natural language representations often results in improved performance on downstream tasks. However, at some point further model increases become harder due to GPU/TPU memory limitations, longer training times, and unexpected model degradation. To address these problems, we present two parameter-reduction techniques to lower memory consumption and increase the training speed of BERT (Devlin et al., 2019). Comprehensive empirical evidence shows that our proposed methods lead to models that scale much better compared to the original BERT. We also use a self-supervised loss that focuses on modeling inter-sentence coherence, and show it consistently helps downstream tasks with multi-sentence inputs. As a result, our best model establishes new state-of-the-art results on the GLUE, RACE, and SQuAD benchmarks while having fewer parameters compared to BERT-large.

> 摘要 
>
> 在预训练自然语言表示时增加模型大小通常会导致下游任务的性能得到改善。 但是，由于GPU / TPU内存的限制，更长的训练时间以及意外的模型降级，在某些时候，进一步的模型增加变得更加困难。 为了解决这些问题，我们提出了两种参数减少技术，以降低内存消耗并提高BERT的训练速度（Devlin等人，2019）。 全面的经验证据表明，与原始BERT相比，我们提出的方法所导致的模型可扩展性更好。 我们还使用了一个自我监督的损失，该损失专注于模拟句子间的连贯性，并表明它始终可以帮助多句子输入的下游任务。 因此，我们的最佳模型在GLUE，RACE和SQuAD基准测试中建立了最新的结果，而与BERT-large相比，参数却更少。

### 1  INTRODUCTION  介绍

Full network pre-training (Radford et al., 2018; Devlin et al., 2019) has led to a series of breakthroughs in language representation learning. Many nontrivial NLP tasks, including those that have limited training data, have greatly benefited from these pre-trained models. One of the most compelling signs of these breakthroughs is the evolution of machine performance on a reading comprehension task designed for middle and high-school English exams in China, the RACE test (Lai et al., 2017): the paper that originally describes the task and formulates the modeling challenge reports then state-of-the-art machine accuracy at 44.1%; the latest published result reports their model performance at 83.2% (Liu et al., 2019); the work we present here pushes it even higher to 89.4%, a stunning 45.3% improvement that is mainly attributable to our current ability to build high-performance pretrained language representations.

全面的预训练网络（Radford 2018; Devlin 2019）在语言表征学习方面取得了一系列突破。 许多很难的NLP任务，包括那些训练数据有限的任务，都从这些预训练模型中受益匪浅。 这些突破最令人信服的迹象之一是，针对中国的中学和高中英语考试的RACE考试（Lai 2017）设计的阅读理解任务上性能的提升：论文最初描述了 任务并制定建模挑战报告，然后将最新机器的准确性提高到44.1％； 最新公布的结果报告其模型性能为83.2％（Liu等，2019）; 我们在这里所做的工作将其提高到了89.4％，惊人的45.3％的提高，这主要归功于预训练模型高超的语言表征能力。







## 参考资料
> - []()
> - []()

