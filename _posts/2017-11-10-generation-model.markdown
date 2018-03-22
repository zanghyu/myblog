---
layout:     post
title:      "生成对话模型"
date:       2017-11-10 12:00:00
author:     "ZhY"
header-img: "img/post-bg-basic.jpg"
header-mask: 0.3
catalog:    true
tags:
    - nlp
---

## sentence representation

[Supervised Learning of Universal Sentence Representations from Natural Language Inference Data][1]

比较了很多模型的sentence representation的效果，最后得出bi-lstm+max-pooling最有效。（实验中，如果将max-pooling放在encoder层的后面会导致不收敛，因此没有使用


[Learning Discourse-level Diversity for Neural Dialog Models Using Conditional VAE][2]

链接：https://zhuanlan.zhihu.com/p/26898768

response是多种可能的，不应该只有一个标准答案，所以应该按照one-to-many的方式来建模训练。这些多样性用隐变量来表征，然后decoder从学到的隐变量概率分布采样重建，生成不同的response。

源码：https://github.com/snakeztc/NeuralDialog-CVAE

[关于VAE的一部分论文][3]



dialog system的总结

链接：http://blog.csdn.net/abcjennifer/article/details/53428053


论文阅读笔记

链接：https://github.com/xwzhong/papernote/tree/master/chatbot


[《Learning Symmetric Collaborative Dialogue Agents with Dynamic Knowledge Graph Embeddings》阅读笔记][6]

论文的亮点有两个，第一是让对话机器人在对称协同的设定下完成任务；第二通过将对话和知识图谱结合，用结构化的知识图谱去表征开放式对话的状态。论文提出的整个动态知识图谱，节点和关系都是通过向量来表征的。


[《Latent Intention Dialogue Models》阅读笔记][7]

目标导向型对话系统的自动决策和对话能力是非常重要的。传统基于强化学习训练的对话系统依赖于手工构建的状态-动作集，不利于扩展和生成对话的多样性。论文提出了一种隐意图对话模型（Latent Intention Dialogue Model, LIDM），通过离散的隐变量来学习对话意图，这些隐变量可以看作引导对话生成的动作决策，进而运用强化学习可以提升性能。


[《A Conditional Variational Framework for Dialog Generation》阅读笔记][8]

论文受Kingma等的半监督深度生成模型的启发[1]，提出一种基于特定属性标签做conditional response generation的框架,提升了对话生成的可控性。






---
[1]:
[2]:
[3]:http://rsarxiv.github.io/2017/03/02/PaperWeekly第二十七期/
[4]:
[5]:
[6]:https://zhuanlan.zhihu.com/p/27910259
[7]:https://zhuanlan.zhihu.com/p/27399471
[8]:https://zhuanlan.zhihu.com/p/26681512
