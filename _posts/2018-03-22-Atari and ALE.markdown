---
layout:     post
title:      "ALE和OpenAI Gym"
date:       2018-03-21 12:00:00
author:     "ZhY"
header-img: "img/post-bg-basic.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 强化学习
---

## ALE和OpenAI Gym的不同之处

## 关于安装

ALE似乎只有python2版本，而OpenAI Gym里面有封装好的ALE的接口。可以参见[atari_py][1]里面关于wrapper的文件。

## 关于环境的初始化

### action

即使用同样的breakout.bin的ROM文件，ALE中的最小action集合为4个(0,1,3,4)，然而OpenAI Gym的则是6个action(0,1,3,4,11,12)。

### frame_skip

ALE的默认framskip是4，而OpenAI Gym的每个game都有不同的环境。比如Breakout-v0是在2到5之间stochastically的skipframe（参见gym/envs/atari/atari_env.py 下的def _step()) 而BreakoutDeterministic-v0是设置为4（参见gym/envs/__init__.py)。（stochastic的frameskip在很多情况下会比deterministic的效果好）

**关于frame skip**

参见[discuss][2],关于OpenAI的Gym使用4帧的frame skip的原因是：

1) 可比性：用4帧的frameskip是现在的标准做法，这和常见的pong的环境时一样的。

2) 学习性能： 如今的RL算法都不能很好地解决长期依赖的问题，使用frameskip有助于提高算法性能

3) 速度：使用frameskip可以加速训练

关于frame_skip的链接和论文：

[Frame Skipping and Pre-Processing for Deep Q-Networks on Atari 2600 Games][3]

Frame Skip Is a Powerful Parameter for Learning to Play Atari - braylan.aaai15 本地已下载

Dynamic frame skip deep q network 本地已下载


### repeat_action_probability

ALE环境和Gym环境的*-v0都设置repeat_action_probability为0.25，然而Gym的*-v3设置为0



---
[1]:https://github.com/openai/atari-py/tree/master/atari_py
[2]:https://discuss.openai.com/t/why-use-frameskip-in-a-realtime-environment/502/3
[3]:https://danieltakeshi.github.io/2016/11/25/frame-skipping-and-preprocessing-for-deep-q-networks-on-atari-2600-games/







