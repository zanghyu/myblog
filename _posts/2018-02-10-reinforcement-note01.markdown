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
    - 强化学习
---


## 强化学习笔记

environment state，S_t^e，环境当前的状态，它反应了环境发生什么改变。

agent state，S_t^a，是agent的现在所处状态的表示

information(Markov) state，它包含了history的所有有用信息。


如果说environment是Fully Observable的,在这种情况下agent state与environment state是相等的。

如果说environment是Partially Observable Environments,agent能获取到的不是直接的环境状态。

一个agent由三部分组成Policy、Value function、Model，但这三部分不是必须同时存在的。



Model:

一种是预测下一个state的transition model

一种是预测下一次reward的reward model

Model Free是指不需要去猜测environment的工作方式，而Model based则是需要学习environment的工作方式。

Exploration和Exploitation之间的权衡：

即Exploration希望能够探索更多关于environment的信息。而后者是指根据已知的信息最大化reward。

例如，在选择一个餐馆时，Exploitation会选择你最喜欢的餐馆，而Exploration会尝试选择一个新的餐馆。

