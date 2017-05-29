---
layout:     post
title:      "拉格朗日乘子法"
subtitle:   "拉格朗日乘子法及KKT条件"
date:       2017-04-27 14:00:00
author:     "ZhY"
header-img: "img/post-bg-basic.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 优化算法
---


## 拉格朗日乘子法

拉格朗日乘子法和KKT条件时求解约束优化问题的重要方法，在**有等式的约束情况下**使用**拉格朗日乘子法**，在**有不等式约束情况下**使用**KKT条件**。

前提： 只有当目标函数为凸函数时，使用这两种方法才能保证求得的时最优解。

$$ min\quad f(x) $$

$$ s.t. h_i(x)=0    i=1,2,...,n $$

转换为$$\qquad\qquad\qquad\qquad\qquad min\quad f(x)+\sum_{i=1}^n\lambda_i h_i(x) $$

其中系数$$\lambda_i$$称为拉格朗日乘子。

为什么可以这样做呢？

首先来看一个二维的优化问题：

$$ max\quad f(x,y) $$

$$ s.t. g(x,y)=c $$

我们可以画图来辅助思考

![](/img/in-post/lagrange/alg-01.png)

其中绿线标出的时约束g(x,y)=c的轨迹，蓝线是f的等高线。箭头表示斜率。

从图上可以看出，在最优解处，f和g的斜率平行。

即 $$ $$

一旦求出$$\lambda$$的值，即可求出极值的对应点。

因为在$$F(x,y)$$到达极值的时候，$$g(x,y)-c$$为零。因此$$F(x,y)$$在到达极值时与$$f(x,y)$$相等。

因此，对$$F(x,y)$$中的$$x$$,$$y$$,$$\lambda$$求一节偏导，可求出$$F$$的驻点。如果这个实际问题的最大或最小值存在,一般来说驻点唯一，因此若只求出一个驻点，则该驻点即为极值点。

例如 

$$ min\quad xy $$

$$ x^2+y^2=1 $$

则我们可以将其化为拉格朗日函数 $$ h(x,y)=xy-\lambda(x^2+y^2-1) $$，则:

$$ \frac{\partial h(x,y)}{\partial x} = y-2\lambda x = 0 $$

$$ \frac{\partial h(x,y)}{\partial y} = x - 2\lambda y = 0 $$

$$ \frac{\partial h(x,y)}{\partial \lambda} = -x^2-y^2+1 = 0 $$

上面三个式子联立可得 $$\lambda = \frac 1 2 , x = y = \frac {\sqrt{2}}{2} $$

可以得出 $$ \qquad\qquad\qquad\qquad\qquad max\quad xy = \frac 1 2 $$

## KKT条件

KKT条件是解决不等式约束的方法。

$$ min\quad f(X)$$

$$ s.t.\quad h_j(X) = 0\qquad j=1,2,...,p \\

\qquad g_k(X)\leq0\qquad k=1,2,...,q$$

转化为$$\qquad\qquad\qquad\qquad\qquad L(X,j,k) = f(X) + \sum_{j=1}^p \lambda_j h_j(X) + \sum_{k=1}^q \mu_k g_k(X)$$

应满足：

1) $$\frac{\partial L(X,j,k)}{\partial X} = 0$$

2) $$ \mu_k g_k(X) = 0$$

3) $$\lambda_j \neq 0$$,$$\mu_k \ge 0$$

<script src="//cdn.bootcss.com/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
