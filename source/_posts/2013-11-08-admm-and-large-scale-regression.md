---
layout: post
title: "ADMM and Large Scale Regression"
description: ""
category: 
tags: []
math: true 
abstract: 简单的阐述ADMM的算法原理，并且结合具体的场景给出一些代码实现。
---
## 预备知识

共轭函数，凸优化，对偶函数，对偶问题

1. 对偶问题

首先，以等价约束的凸优化问题为例：

$$
\text{minimize} \; f(x)  \\\\
\text{subject to} \; Ax = b 
$$

f(x)是凸函数, x是N维变量

该问题的拉格朗日问题是：

$$ 
L(x,y) = f(x) + y^t(Ax-b)
$$

对偶函数：
$$
g(y) = \inf_{x}{L(x,y)} = -f^\star(-A^Ty)-b^Ty
$$

y是对偶变量，$f^\star$是f的[凸共轭函数](http://en.wikipedia.org/wiki/Convex_conjugate)

对偶问题

$$
\text{maximize}\; g(y)
$$

ADMM的方法：先确定y，然后根据y得到x;交换顺序，确定x，计算y

$$
x^{k+1} = argminL(x,y^k) \\
y^{k+1} = y^k + \alpha^k (Ax^{k+1} - b)
$$

## 相关资料 

ADMM是一种通用的并行优化策略, 它可以非常方便的在分布式环境的迭代优化计算，ADMM的算法文档可参考:[ADMM文档](http://www.stanford.edu/~boyd/papers/pdf/admm_distr_stats.pdf)

- [ADMM](https://speakerdeck.com/pld/distributed-classification-with-admm)
- [MPI example for alternating direction method of multipliers](http://www.stanford.edu/~boyd/papers/admm/mpi/)
- [Distributed Optimization and Statistical Learning via the Alternating Direction Method of Multipliers](http://www.stanford.edu/~boyd/papers/admm_distr_stats.html)

## 算法
1. paralled Dual-ADMM
2. FISTA
3. GRock


## 代码

- [admm-hadoop](https://github.com/intentmedia/admm)
- [admm-lasso-without-mpi](https://github.com/brianmartin/admm-lasso-without-mpi)
- [admm-mpi](http://www.stanford.edu/~boyd/papers/admm/mpi/)
- [Parallel and Distributed Sparse Optimization](http://www.caam.rice.edu/~optimization/disparse/)


