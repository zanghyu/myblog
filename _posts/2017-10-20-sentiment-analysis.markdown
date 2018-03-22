---
layout:     post
title:      "情感分类模型"
date:       2017-12-22 12:00:00
author:     "ZhY"
header-img: "img/post-bg-basic.jpg"
header-mask: 0.3
catalog:    true
tags:
    - nlp
---

### 面对评价对象的情感分类

#### 一、Attention-based LSTM (AT-LSTM) 可以考虑到评价对象的类别信息

论文：[Attention-based LSTM for Aspect-level Sentiment Classification][1]

![](/img/in-post/sentiment-analysis/AT-LSTM.png)

** 模型说明： **

每一时刻输入word embedding，LSTM的状态更新，将隐层状态和aspect embedding结合起来，aspect embedding作为模型参数一起训练，得到句子在给定aspect下的权重表示r。


#### 二、Attention-based LSTM with Aspect Embedding (ATAE-LSTM)

![](/img/in-post/sentiment-analysis/ATAE-LSTM.png)

和第一种是同一篇文章中提出的

** 模型说明： **

在AT-LSTM的基础上，将aspect embedding和word embedding结合起来作为输入，aspect embedding依然是作为模型参数一起训练。

** 缺点： **

目前的模型中，不同的aspect只能独立输入处理。

** 使用数据： **

[SemEval-2014 Task 4的数据集][5]

** 实验结果: **

![](/img/in-post/sentiment-analysis/ATAE-LSTM_result.png)

#### 三、Memory Network + Attention 可以显示地利用上下文对于不同评价对象的差异

论文：[Aspect Level Sentiment Classification with Deep Memory Network][2]

![](/img/in-post/sentiment-analysis/memory_network+attention.png)

** 模型说明： **

1.word vectors包括context vectors和aspect vectors。


2.模型包括多个computational layers,每个computational layer包括一个attention layer和一个linear layer。

3.包括content attention和location attention两部分。

** 使用数据： **

SemEval 2014

** 实验结果: **

![](/img/in-post/sentiment-analysis/memory_network+attention_result.png)


#### 四、TD-LSTM

论文：[Effective LSTMs for Target-Dependent Sentiment Classification][3]

![](/img/in-post/sentiment-analysis/TD-LSTM.png) 

** 模型说明: **

1.两个LSTM，分别是 LSTM_{L}  和  LSTM_{R}。

LSTM_{L} ：从句子的第一个词w_{1} ，到target word w_{r-1} 依次输入

LSTM_{R} ：从句子的最后一个词w_{n} ,到target word w_{l+1} 依次输入



#### 五、TC-LSTM

和上个模型是同一篇文章提出

![](/img/in-post/sentiment-analysis/TC-LSTM.png)

模型说明：

1.在target-connection LSTM的基础上，在输入端引入target word的信息，具体说来就是把target word的向量表示v_{target} 与输入端的word embedding拼接起来。

2.v_{target} 是所有target word的词向量的平均值。

3.把LSTM_{L} 和LSTM_{R} 的最后一个隐层输出结合起来作为整个句子结合target word信息的语义表示。

** 使用数据： **

Adaptive Recursive Neural Network for Target-dependent Twitter Sentiment Classification收集标注的twitter，训练数据6248条，测试数据692条

** 实验结果 **

![](/img/in-post/sentiment-analysis/TD-LSTM_result.png)


#### 六、TDParse

论文： [TDParse: Multi-target-specific sentiment recognition on Twitter][6]

** 模型说明： **

通过依存句法的分析树找到对应target路径，并针对该路径进行word embedding，与此同时针对left-target-right分别进行embedding。将这些feature vector放入一个final feature vector:

F = [P(D),P(L),P(T),P(R)]; with P(X) = [f1(X),...,fk(X)]，

where P (X ) presents a list of k different pooling functions on an embedding matrix X.

对于某个target出现多次的情况，有：

P(X) = [P_medium([f_1(X_1),...,f_1(X_m)]),  P_medium([f_k(X_1), ..., f_k(X_m)])]

where m is the number of appearances of the tar- get and Pmedium represents the dimension-wise medium pooling function.

最后将结果作为输入放入到svm中进行分类

** 使用数据： **

a corpus of tweets about the 2015 UK election.

** 实验结果： **

![](/img/in-post/sentiment-analysis/TD-Parse_result.png)

#### 七、RAM

论文：[Recurrent Attention Network on Memory for Aspect Sentiment Analysis][7]

** 模型说明： **

![](/img/in-post/sentiment-analysis/RAM.png)

首先进行word embedding，然后使用两层的BLSTM建立memory。根据依存关系来构建position-weighted Memory，用多个attention保证蒸馏正确的相关信息，用recurrent network通过GRU与多attention来连接。最后经过n轮之后放入softmax进行预测。

** 使用数据： **

4个数据集：Laptop和restaurant是SemEval 2014的，tweets(Dong et al., 2014)，news comments腾讯自己使用的

** 实验结果： **

![](/img/in-post/sentiment-analysis/Ram_result.png)

### 购买意向提取

#### 一、LSTM+UPA

论文：[Neural Sentiment Classification with User and Product Attention][4]

![](/img/in-post/sentiment-analysis/UPA.png)

Document-level的情感分析。假设每个document对某个产品表达一定的情感倾向，document-level的情感分析的目标是确定document对产品的整体的情感倾向。

** 模型说明: **

1.层级LSTM： 从word到sentence，sentence到document分别利用LSTM进行语义建模。

2.在不同语义级别中引入user和product的信息。

** 使用数据： ** 

IMDB, Yelp 2013 and Yelp 2014

 ** 实验结果: **

 ![](/img/in-post/sentiment-analysis/UPA_result.png)



### 文本分类

#### 一、conv-RNN

论文：[A Hybrid Framework for Text Modeling with Convolutional RNN][8]

CNN + RNN 

** 模型说明：**

基础模型：

![](/img/in-post/sentiment-analysis/conv-RNN.png)

word embedding 作为输入，输入到Bi-RNN中，Bi-RNN的结果输入到CNN中，卷积层窗的大小为1，激活函数为ReLU，pooling层选用max-pooling

![](/img/in-post/sentiment-analysis/conv-RNN_formula_01.png)

文本分类模型sentence classification：

![](/img/in-post/sentiment-analysis/conv-RNNSC.png)

和基础模型类似，不同之处在于将Bi-RNN的最后一个隐层输出和卷积结果concate，然后再加一层隐层，最后通过softmax分类

答案选择answer selection：

![](/img/in-post/sentiment-analysis/conv-RNNQA.png)

对question中的每个词和答案中的每个词的embedding做内积，再与原来的词concate，基础模型的基础上加了attention，最后的X_q和X_a通过GESD得到X_sim，将X_q X_sim X_a concate到一起，最后通过两层全联接输出。

** 实验结果: **

![](/img/in-post/sentiment-analysis/conv-RNN_result_01.png)

![](/img/in-post/sentiment-analysis/conv-RNN_result_03.png)

![](/img/in-post/sentiment-analysis/conv-RNN_result_02.png)






## 其他的一些文本分类和情感分析的论文：

[PhraseRNN: Phrase Recursive Neural Network for Aspect-based Sentiment Analysis][9]


[Convolutional Neural Networks for Sentence Classification][10]


[Dependency Sensitive Convolutional Neural Networks for Modeling Sentences and Documents][11]


[Semi-Supervised Recursive Autoencoders for Predicting Sentiment Distributions][12]


[Recursive Deep Models for Semantic Compositionality Over a Sentiment Treebank][13]


[A Hybrid Framework for Text Modeling with Convolutional RNN][14]


[Deep Learning for Aspect-Based Sentiment Analysis][15]


[A Cognition Based Attention Model for Sentiment Analysis][16]


[FRUSTRATINGLY SHORT ATTENTION SPANS IN NEURAL LANGUAGE MODELING][17]


[Hierarchical Attention Networks for Document Classification][18]


[A Review of Sentiment Analysis Research in Chinese Language][19]



---
[1]:http://aclweb.org/anthology/D16-1058
[2]:https://arxiv.org/pdf/1605.08900v2.pdf
[3]:https://arxiv.org/pdf/1512.01100v2.pdf
[4]:http://www.thunlp.org/~chm/publications/emnlp2016_NSCUPA.pdf
[5]:http://alt.qcri.org/semeval2014/task4/index.php?id=data-and-tools
[6]:http://www.aclweb.org/anthology/E17-1046
[7]:http://www.aclweb.org/anthology/D17-1048
[8]:https://dl.acm.org/citation.cfm?id=3098140&CFID=827483452&CFTOKEN=13473838
[9]:http://www.anthology.aclweb.org/D/D15/D15-1298.pdf
[10]:http://www.aclweb.org/anthology/D14-1181
[11]:http://clair.si.umich.edu/~radev/papers/201.pdf
[12]:http://delivery.acm.org/10.1145/2150000/2145450/p151-socher.pdf?ip=45.77.188.223&id=2145450&acc=OPEN&key=4D4702B0C3E38B35%2E4D4702B0C3E38B35%2E4D4702B0C3E38B35%2E6D218144511F3437&CFID=827483452&CFTOKEN=13473838&__acm__=1510741992_a3d27e2dcb0db6683b5f0b17685ac594
[13]:http://www.aclweb.org/anthology/D13-1170
[14]:https://dl.acm.org/citation.cfm?id=3098140&CFID=827483452&CFTOKEN=13473838
[15]:https://cs224d.stanford.edu/reports/WangBo.pdf
[16]:http://www.aclweb.org/anthology/D17-1048
[17]:https://arxiv.org/pdf/1702.04521.pdf
[18]:https://www.cs.cmu.edu/~diyiy/docs/naacl16.pdf
[19]:http://sentic.net/chinese-sentiment-analysis-review.pdf

