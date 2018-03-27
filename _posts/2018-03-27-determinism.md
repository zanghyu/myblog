---
layout:     post
title:      "随机性对agent的影响"
date:       2018-03-27 12:00:00
author:     "ZhY"
header-img: "img/post-bg-basic.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 强化学习
---

## The Impact of Determinism on Learning Atari 2600 Games

## 概览

本篇文章主要提出了Atari游戏在给了一定的policy时产生的是deterministic的action序列，这种状态下的agent可能会因为记住了action序列而造成过拟合，因此提出了一些加入stochastic的方法，并说明了为什么这样做重要。

本篇文章一共提出了三种方式来增加stochasticity:

1) randomly skipping frames at the beginning of an episode 随机跳帧

2) epsilon-greedy action selection epsilon-贪心

3) randomly repeating actions throughout an episode 随机重复action

作者复用了[Hausknecht et al. 2013][1]的agent——memorizing-NEAT和randomized-NEAT，其中randomized-NEAT虽然表现欠佳，但是对随机性的承受能力较好。

所有图中的实心长方形都代表memorizing-NEAT，空心图形代表randomized-NEAT

## 随机初始化

![](/img/in-post/determinism/1.jpg)

通过设置ALE中的-use_environment_distribution参数控制在游戏开始时使用随机的NOOP action。随机初始化的memorizing-NEAT在所有游戏中的表现有所差异，说明随机初始化强制memorizing-NEAT在一个不熟悉的状态中开始玩游戏。而随机初始化使randomized-NEAT表现降低了很多，说明随机初始化对随机化方法要求很严格。

## epsilon-贪心的action选择

![](/img/in-post/determinism/2.jpg)

选用epsilon=0.005时对于memorizing-NEAT都很有效，因此可以适当放宽epsilon=0.05的限制

## epsilon-repeat的action选择

![](/img/in-post/determinism/3.jpg)

依旧是对memorizing-NEAT更有效，对randomized-NEAT的效果差一些

## 总结

epsilon-repeat的action选择是最有效的一个方法。当然克服deterministic的方法最好是双人游戏，由其他玩家来创造随机性。


---
[1]:http://www.cs.utexas.edu/users/mhauskn/papers/atari.pdf



