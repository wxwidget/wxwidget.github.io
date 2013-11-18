---
layout: post
title: "ADMM and Large Scale Regression"
description: ""
category: 
tags: []
---

## 讨论主题

ADMM是一种通用的并行优化策略, 它可以非常方便的在分布式环境的迭代优化计算，ADMM的算法文档可参考:[ADMM文档](www.stanford.edu/~boyd/papers/pdf/admm_distr_stats.pdf)

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


