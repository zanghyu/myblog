---
layout:     post
title:      "线性回归及广义线性回归算法"
subtitle:   "线性回归及广义线性回归"
date:       2017-04-05 14:00:00
author:     "ZhY"
header-img: ""
header-mask: 0.3
catalog:    true
tags:
    - 机器学习算法
---
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
## 线性回归预备公式

$$\frac{\partial X\theta }{\partial \theta}= X^T$$

$$\frac{\partial \theta^T X} {\partial \theta^T}=X^T$$

$$\frac{\partial \theta^T X}{\partial \theta}=X$$

$$\frac{\partial \theta^T X \theta}{\partial \theta}=(X+X^T)\theta $$

## 什么是线性回归

首先要明确一点就是什么是回归？我们希望有一个模型可以具有一定的预测能力，当我们想要预测的是连续值时，这类的学习任务被称为是“回归”。回归的目的是建立一个回归方程用来预测目标值，回归的求解就是求这个回归方程的回归系数。

回归最简单的定义是 给出一个点集D，用一个函数去拟合这个点集，并且使得点集与拟合函数间的误差最小，如果这个函数曲线是一条直线，那就被称为线性回归。

比如样本值x与预测值y的函数为$$y = \theta \cdot x$$ 的图像是一条直线，因此是线性的。但是实际问题中往往样本值不止一个，因此实际函数一般为 

$$h(x)=\sum_{i=0}^n \theta_i x_i = \theta^T x$$

其中$$\theta$$表示未知参数，是要学习出来的值， $$x$$表示自变量，在这里是用列向量表示，而$$\theta$$是行向量，因此用$$\theta$$转置。

线性回归试图学习的是使得$$h(x_i)$$与$$y_i$$的差距尽可能小，而在这里衡量h(x)与y的差别所采用的标准是均方误差（也被称为平方损失），均方误差有着很好的几何意义，它对应了常用的欧几里得距离。
	
$$\theta^*=arg_\theta min\sum_{i=0}^m(h(x_i)-y_i)^2$$

#### 最小二乘

m为样本个数，最小二乘的函数为：

$$J(\theta)=\frac 1 2 \sum_{i=1}^m(h_\theta(x^{(i)})-y^{(i)})^2$$

由于该函数求二阶偏导偏导可知其为凸函数，因此当其导数为0时，取到该函数的极小值。
	
另外：最小二乘建立的目标函数，是在噪声在均值为0时的高斯分布下，极大似然估计的目标函数。

设真实值和样本值的偏差为$$\epsilon$$ 则可以表示为：

$$y^{(i)}=\theta^Tx^{(i)}+\epsilon^{(i)}$$

由于该偏差为多种不同噪声的叠加，而根据中心极限定理可知，$$\epsilon$$符合高斯分布。因此$$\epsilon^{(i)}$$的概率函数为

$$p(\epsilon ^{(i)})=\frac 1 {\sqrt {2\pi}\sigma}exp(-\frac {(\epsilon ^{(i)})^2} {2\sigma^2})$$

将$$x^{(i)}$$ $$y^{(i)}$$ $$\theta$$代入后得到

$$p(y^{(i)}|x^{(i)};\theta)=\frac 1 {\sqrt {2\pi}\sigma}exp(-\frac {(y^{(i)}-\theta^Tx^{(i)})^2} {2\sigma^2})$$

采用极大似然法计算其似然函数为：

$$\begin{array}{rcl} L(\theta) &=& \prod_{i=1}^m p(y^{(i)}|x^{(i)};\theta)\\&=& \prod_{i=1}^m \frac 1 {\sqrt {2\pi}\sigma}exp(-\frac {(y^{(i)}-\theta^Tx^{(i)})^2} {2\sigma^2})\end{array}$$

左右同时取对数后：

$$\begin{array}{rcl} l(\theta) &=& logL(\theta) \\&=& log\prod_{i=1}^m \frac 1 {\sqrt {2\pi}\sigma}exp(-\frac {(y^{(i)}-\theta^Tx^{(i)})^2} {2\sigma^2})\\ &=& mlog\frac 1 {\sqrt{2\pi}\sigma}-\frac 1 {\sigma^2}\cdot\frac 1 2\sum_{i=1}^m(y^{(i)}-\theta^Tx^{(i)})^2\end{array}$$

由于$$\sigma$$已知，并且要求$$l(\theta)$$的最大值，因此应该取$$\frac 1 2\sum_{i=1}^m(y^{(i)}-\theta^Tx^{(i)})^2$$ 的极小值。

这一点也证明了最小二乘是符合常理的。

#### 向量形式

函数$$J(\theta)$$可以表示为向量形式$$J(\theta) = \frac 1 2 (\theta X-y)^T \cdot (\theta X - y)$$

将该式打开后可得

$$J(\theta)=\frac 1 2 (\theta^T X^T X \theta - \theta^T X^T y-y^T X \theta +y^T y)$$


根据预备公式可得出 $$ \frac {\partial \theta^T X^T X \theta}{\partial\theta} = (X^T X + X X^T)\theta $$ 又因为 $$X X^T$$为对称阵($$(X X^T)^T=X X^T$$，因此为对称阵)，所以该式等于$$2X^T X\theta$$

因此

$$\begin{array}{rcl}\frac {\partial J(\theta)}{\partial \theta} &=& \frac 1 2 (2X^T X \theta -2X^Ty)\\&=&  X^T X \theta - X^T y \end{array}$$

当该偏导等于0时取得最优解，此时$$\theta = (X^T X)^{-1}X^T y $$  若X^T X不可逆时该式不可用，因此需要加上一个扰动量$$\lambda$$使其可逆，此时$$\theta = (X^T X + \lambda I)^{-1}X^T y $$

原因：$$X^T X$$半正定，加上扰动量后正定，因此可逆。（即岭回归方法）

#### 简单推导形式

由于已知$$ X\theta = y$$，则可推

$$X^T X \theta=X^T y$$

$$\theta = (X^T X)^{-1}X^T y $$


## 基本算法

#### 梯度下降算法

1.初始化$$\theta$$值

2.迭代$$ \theta_j := \theta_j-\alpha\frac {\partial}{\partial \theta_j}J(\theta)$$   其中$$\alpha$$为学习率

3.如果$$J(\theta)$$能继续减少，返回2

#### 批处理梯度下降算法

$$\theta_j :=\theta_j+\alpha\sum_{i=1}^m(y^{(i)}-h_\theta(x^{(i)}))x_j^{(i)}$$

该方式要得到所有样本时才下降一次，速度较慢，但一定能达到最优值。

#### 随机梯度下降算法

$$ \begin{equation} 
	\begin{split}
	for (i =& 1; i <= m ; i++ ) \\
	&\theta_j:=\theta_j+\alpha(y^{(i)}-h_\theta(x^{(i)}))x_j^{(i)} 
	\end{split}
	\end{equation}
$$

随机梯度不一定最终收敛，有可能在最终结果附近震荡，但是速度较快。

#### mini-batch算法

综合以上两种算法，每次选取b个

$$\begin{equation}
	\begin{split}
	for (i =& 1; i<=m; i+= b) \\
	&\theta_j :=\theta_j+\alpha\sum_{i=1}^b(y^{(i)}-h_\theta(x^{(i)}))x_j^{(i)}
	\end{split}
\end{equation}$$

#### 局部加权线性回归

由于最初的线性回归只能拟合出一条直线，但是大多数现实生活中的数据并非都能用线性模型描述，而有时候曲线反而更容易拟合。因此我们预测一个点时，选择与这个点相近的点做线性回归。赋予每个点一个权值，当一个点距离所要预测的点越近，其权值越大，对回归曲线的贡献越大。

最初的线性回归要求最小化$$\sum_{i=1}^m(h_\theta(x^{(i)})-y^{(i)})^2$$，而局部加权线性回归会增加一个权重：

$$J(\theta) = \sum_{i=1}^m\omega^{(i)}(h_\theta(x^{(i)})-y^{(i)})^2$$

权值的设置可以任选一种方式，一般取高斯核函数：

$$\omega^{(i)} = exp(-\frac{(x^{(i)}-x)^2}{2\tau^2})$$

其中$$\tau$$成为带宽，它控制着训练样本随着与$$x^{(i)}$$距离的衰减速率


## logistic回归

有函数$$g(z)=\frac 1 {1+e^{-z}} $$图像为

![](/img/in-post/regression/logistic.jpg)

若将z用某个线性组合表示，即用$$\theta^T x $$表示。则可得

$$h_\theta(x)=g(\theta^T x)=\frac 1 {1+e^{-\theta^T x}}$$

假设如下两个等式成立，

$$p(y=1|x;\theta)=h_\theta(x)$$

$$p(y=0|x;\theta)=1-h_\theta(x)$$

那么我们可以将他们整理为	

$$(p(y|x;\theta)=(h_\theta(x))^y(1-h_\theta(x))^{1-y}$$

极大似然法可得 $$L(\theta)=\prod_{i=1}^m {(h_\theta(x^{(i)}))^y}^{(i)}(1-h_\theta(x^{(i)}))^{1-y^{(i)}}$$

$$l(\theta)=\sum_{i=1}^m y^{(i)}log(h_\theta(x^{(i)}))+(1-y^{(i)})log(1-h_\theta(x^{(i)}))$$

$$\begin{array}{rcl}\frac {\partial l(\theta)}{\partial \theta_j} &=& (y^{(i)}\frac 1 {h_\theta(x^{(i)})} - (1-y^{(i)})\frac 1 {1-h_\theta(x^{(i)})})\frac {\partial h_\theta(x^{(i)})} {\partial \theta_j} \\&=& (y \frac 1 {g(\theta^T x)} - (1-y) \frac 1 {1 - g(\theta^T x)} ) g(\theta x) (1-g(\theta^T x ) ) \frac {\partial \theta^T x}{\partial \theta_j} \\&=& (y(1-g(\theta^T x))-(1-y)g(\theta^T x)) x_j \\&=& (y-h_\theta(x)x_j\end{array}$$

由此可以得出logistic回归的迭代式为：

$$\theta_j :=\theta_j + \alpha (y^{(i)}-h_\theta(x^{(i)}))x_j^{(i)}$$

## 对数线性模型

一个事件的几率odds，是指该事件发生的概率与该事件不发生的概率的比值。

则针对于logistic回归的对数几率：logit函数表示为：

$$logit(p)=log \frac{p}{1-p} = log\frac{h_\theta(x)}{1-h_\theta(x)} = log \frac{\frac 1 {1+e^{-\theta^T x}}}{\frac {e^{-\theta^T x}}{1+e^{-\theta^T x}}}=\theta^T x$$

因此其对数几率为线性函数。所以我们认为logistic回归为对数线性模型，也就是广义线性模型。


---

## 参考文献

《广义线性回归和对偶优化》——邹博

[机器学习经典算法详解及Python实现--线性回归（Linear Regression）算法][1]

[1]:http://blog.csdn.net/suipingsp/article/details/42101139/

[logistic回归][2]

[2]:http://baike.baidu.com/link?url=yp9q-n_7-hi2RFlvv3so1Ek1bZx1Lmrp-Rn1zXJNxjaryr6xSm1hMe4fGwPdCPPiF8lMduRvVij0bwUUe3LBLdfCfIGtPFLy6xj6t42T33XStVz4GLDe-ilMMrYJm72g

[logistic回归总结][3]

[3]:http://blog.csdn.net/dongtingzhizi/article/details/15962797

