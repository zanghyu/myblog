---
layout:     post
title:      "PageRank算法&TrustRank算法"
subtitle:   "PR&TR的介绍及实现"
date:       2017-03-10 14:00:00
author:     "ZhY"
header-img: "img/post-bg-basic.jpg"
header-mask: 0.3
catalog:    true
tags:
    - nlp
---


## word embedding

word embedding 也即平时所说的词向量。

### 两种表示

1.one-hot:统计出语料中的所有词汇，然后对每个词汇编号，针对每个词建立V维的向量，向量的每个维度表示一个词，所以，对应编号位置上的维度数值为1，其他维度全为0。

2.distributed representation 通过训练将某种语言的每一个词映射成固定长度的短向量。（类似于提取词的特征，降维

### word embedding模型

n-gram模型：假定一个词出现的概率只与它前面n-1个词相关。一般来讲 n-gram 取n=3

神经概率语言模型：

输入层、投影层、隐藏层、输出层

![](/img/in-post/word2vec/01.jpg)

其中Context(W)是上下文（即前面的n-1个词），投影层的规模为(n-1)m，输出层的规模为N=|D|

![](/img/in-post/word2vec/02.jpg)

### word2vector的两个模型

![](/img/in-post/word2vec/03.jpg)

#### 基于 Hierarchical Softmax 的模型

##### CBOW模型

![](/img/in-post/word2vec/04.jpg)

其投影层是将所有的词向量求和累加，输出层是一个Huffman树。

##### skip-gram模型

![](/img/in-post/word2vec/05.jpg)

投影层和输入层是一样的，输出层为Huffman树

#### 基于 Negative Sampling 的模型

关于负采样：http://blog.csdn.net/itplus/article/details/37998797

## 总结

word embedding实际上就是将一篇文章的词都用向量化表示。而word2vector就是word embedding的一种方法
