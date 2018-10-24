---
layout:     post
title:      "Policy gradient小总结"
date:       2018-09-27 12:00:00
author:     "ZhY"
header-img: "img/post-bg-basic.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 强化学习
---


policy gradient 的问题：

高variance：
降低variance我们可以对梯度有个更好的评价 这样有利于收敛到一个更好的结果
或者用一个较大的学习率可以让我们收敛更快




Q值表示的是s_t时候做了动作a_t之后的reward之和

V值表示的是s_t时候做了不同动作的reward之和的平均值

A值表示的是s_t的时候做了动作a_t会比平均值高出多少，有多少优势

**思路：因为A=Q-V，很多强化学习算法都是在想办法更好的能够得到准确的A值，现在已有的方式都会带来方差和偏差的问题，如何能够同时减小这两者是一个研究方向**


需要注意的一点是，
$$Q(s_t,a_t)=r(s_t,a_t)+\sum_{t^{\prime}=t+1}^TE_{\pi_\theta}[r(s_t^\prime,a_t^\prime)|s_t,a_t]$$

即$$Q(s_t,a_t)$$代表及时reward加$$s_{t+1}$$之后reward之和

而我们又知道$$V^\pi(s_t)$$是$$s_t$$时候做了不同动作的reward之和的平均值，因此$$V^\pi(s_{t+1})$$是$$s_{t+1}$$的时候的reward平均值。

由于我们的系统是随机的，$$s_t$$时候做了$$a_t$$到达的$$s_{t+1}$$的状态不确定，因此上面的式子可以改写成,

$$Q(s_t,a_t)=r(s_t,a_t)+E_{s_{t+1}~p(s_{t+1}|s_t,a_t)}[V^\pi(s_{t+1})]$$

可是如果我们愿意做一点近似，只在$$s_{t+1}$$这一位置的期望值用$$V^\pi(s_{t+1})$$来近似，整个过程只会有一点点偏差。

这个时候$$A^\pi(s_t,a_t)$$就近似于$$r(s_t,a_t)+V^\pi(s_{t+1})$$-V^\pi(s_t)$$




