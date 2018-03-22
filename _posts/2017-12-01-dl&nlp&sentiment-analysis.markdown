---
layout:     post
title:      "深度学习 & NLP & 情感分析 入门材料"
date:       2017-12-01 12:00:00
author:     "ZhY"
header-img: "img/post-bg-basic.jpg"
header-mask: 0.3
catalog:    true
tags:
    - nlp
---

## 深度学习 & NLP & 情感分析 入门材料

#### 深度学习

[廖星宇的博客][1]，讲了很多入门知识，比如cnn的基本模型结构等等

[莫烦的python][2]，里面有很多入门级教程，包括了数据处理、python基础、强化学习、git入门、linux入门教程等

[Must Know Tips/Tricks in Deep Neural Networks][5]，cnn的一些特别实用的小trick 当然有的也是大杀器，比如较大网络中的drop out 论文

[深度学习网络调参技巧][9]

[LSTM和GRU的比较][15]

#### NLP

[斯坦福cs224n深度学习自然语言处理][3]

[基于gensim的word2vector的实践][4]，主要简单介绍了word2vec的简单使用

[LICSTAR的博客][6]，关于nlp和数据挖掘的

[西土城的搬砖日常][10]，知乎专栏  北邮nlp组

[LTP][14]，哈工大做情感分析的一套工具（包括了分词、依存句法、提取实体、处理文本信息等

[isaacchanghau博客][16]

#### 情感分析

[PhraseRNN: Phrase Recursive Neural Network for Aspect-based Sentiment Analysis][7]，依存句法加RNN 针对实体进行情感分析 论文

[微博舆情 之 特定话题情感分析][8]，介绍判定微博情感极性的流程

[GermEval2017][11]，似乎是专门做情感分析的一个比赛，这个是赛后论文

[Document-Level Multi-Aspect Sentiment Classification as Machine Comprehension][12]，层级网络多目标情感分类 论文

[A TARGET-DEPENDENT SENTIMENT ANALYSIS METHOD FOR CHINESE MICRO-BLOG][13]，一篇微博情感分析的论文(依存关系+SVM) 论文



---
[1]:https://sherlockliao.github.io/ 
[2]:https://morvanzhou.github.io
[3]:https://zhuanlan.zhihu.com/p/26259699
[4]:https://segmentfault.com/a/1190000008173404?from=timeline
[5]:http://lamda.nju.edu.cn/weixs/project/CNNTricks/CNNTricks.html
[6]:http://licstar.net/archives/category/data-mining
[7]:http://www.anthology.aclweb.org/D/D15/D15-1298.pdf
[8]:http://blog.csdn.net/claire7/article/details/46701591
[9]:http://blog.csdn.net/ch1209498273/article/details/78452575
[10]:https://zhuanlan.zhihu.com/p/24328777
[11]:https://www.researchgate.net/publication/320691578_Proceedings_of_the_GermEval_2017-Shared_Task_on_Aspect-based_Sentiment_in_Social_Media_Customer_Feedback?enrichId=rgreq-b0eba73f374749dd52d59b25adee4349-XXX&enrichSource=Y292ZXJQYWdlOzMyMDY5MTU3ODtBUzo1NTQ0Njc4OTAxMzA5NDVAMTUwOTIwNjg1NDYzMA%3D%3D&el=1_x_3&_esc=publicationCoverPdf
[12]:http://www.aclweb.org/anthology/D17-1216
[13]:http://www.worldresearchlibrary.org/up_proc/pdf/6-141992851736-41.pdf
[14]:http://ltp.readthedocs.io/zh_CN/latest/begin.html
[15]:https://www.cnblogs.com/taojake-ML/p/6272605.html
[16]:https://isaacchanghau.github.io
