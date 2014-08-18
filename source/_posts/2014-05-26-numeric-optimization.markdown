---
layout: post
title: "机器学习的通用指南: 优化理论"
date: 2014-05-26 11:18
comments: true
math: true
categories: "Machine&nbspLearning Numeric&nbspOptimization"
abstract: 机器学习本质上是一种最优化问题，本文试图通过介绍求解最优化问题中最常见的梯度法，以窥见机器学习的通用学习策略。
---

通常我们会把机器学习过程分成两个阶段，建模阶段和求解阶段。在大数据的推动下，求解的问题慢慢大于建模的问题。比如，业界一般采用逻辑回归做CTR预估或者其他的预测模型，但是在数据规模非常大的条件下，如何在分布式的环境下，更快更准的求解模型就变得非常重要。精确的解析求解场景是非常少的，人们更多的去研究模型的数值求解过程，比如梯度下降法；近似求解，比如：蒙特卡洛法。这里我只想讨论下梯度下降法，该方法是一种非常神奇的通用的数学最优化方法。

下面会分几个阶段去讲梯度法的基本原理，本文更多的是偏理解。

1. 梯度下降法
2. 牛顿法
3. 拟牛顿法
4. 共轭梯度法

<!-- more -->

## 符号说明

- $x$表示自变量
- $y$表示因变量，是自变量的函数$y(x)$
- $\nabla$ 梯度算子
- $\eta$ 学习率，大于0的数
- g 或者$\nabla f$ 一阶梯度，
- H 或者$\nabla^2 f$ 二阶梯度

## 梯度法

简单的无约束的优化问题是，找到使得f(x)取最小值时的x。迭代法的基本思路是找到一种迭代的方法, x变化导致y下降,用数学的方法表示就是。

$$
x_{k+1} = x_k + p = x_k + \eta d
$$

其中p表示x的增加的部分，分解成大小$\eta$，和方向$d$

我们先得知道函数的近似公式：

<div class="definition">
    一阶泰勒展开公式: 
    $$f(x_k+p) = f(x_k)+ \nabla f(x_k) p + O(p^2)$$
    去掉无穷小部分:
    $$f(x+p) = f(x)+ g^Tp  $$
</div>

从一阶的泰勒展开公式我们可以知道要想使得更新后的函数$f(x+p) \leq f(x)$，必须使得 $g^T*p \leq 0$，我们又知道g和d都是向量,
他们的向量表示法：

$$
    g^Tp = |g|*|p|*cos \theta
$$

只要保证\$theta$小于0，就可以保证 $g^Tp$小于0。使得$p = -\eta g$， 这就是传说中的最速梯度法了.

<div class="definition">
    梯度下降法: 
    $$p = -\eta * g,  满足 \eta \gt 0 $$
    那么x写成迭代形式是
    $$
    x_{k+1} = x_k - \eta * g
    $$
</div>


通过梯度下降法，我们知道，我们确实有一种方法，能找到x的一种迭代方式，使得函数y不增加。$x_{k+1} = x_k + \eta *g $中我们只解决了方向的问题，
还有一个学习率的问题没有解决。就是我们如何确定 $\eta$，有一种非常简单的方法是预设$\eta$为一个固定的值比如0.1；或者
$\eta$是在一个区间了下降，比如从0.5下降到0.001；或者不同的x的分量有不同的学习率，等等。这些方法通常表现都不错

## 牛顿法

为了得到更快的收敛速度，挑选合适的学习速率也是一件比较困难的事情。回到泰勒展开公式，我们知道还有一个更加精确的二阶泰勒展开公式

<div class="definition">
    二阶泰勒展开公式: 
    $$f(x_k+p) = f(x_k)+ \nabla f(x_k) p + \frac{1}{2} p^T \nabla ^2 f(x_k) p $$
    知道 $p = x - x_k$得到:
    $$f(x) = f(x_k)+ \nabla f(x_k) (x-x_k) + \frac{1}{2} (x-x_k)^T \nabla ^2 f(x_k) (x-x_k) $$
</div>


我们知道函数极值的条件是倒数为0,所以

$$ \frac{\partial f}{\partial x} = 0 $$

求解得到

$$ x = {x_k} - \frac{\nabla f({x_k})}{\nabla ^2 f({x_k})} = {x_k} - {H^{ - 1}}g$$

当然算法工程通常不会直接求H的逆，而是通过 $Hp ＝ －g$去计算p

牛顿法的好处是对强二次型的函数效果收敛速度非常快，但是对非二次型的函数很有可能导致迭代过程中函数上升。

## line search

为了避免此类问题，出现了line search方法：

$$
 \eta_k = argmin \ f(x_k + \eta_k p_k) 
  \\
  x_{k+1}=x_k-\eta_k g_k
$$

我们知道要想使得函数f最小，满足
$$
\frac{\partial f(x_{k+1})} {\partial \eta}=0
$$

更加函数的求导数法则

$$
\frac{\partial f(x_{k+1})} {\partial \eta} = 
\frac{\partial f(x_{k+1})}{\partial x_{k+1}} \times \frac{\partial x_{k+1}}{\partial \eta_k} = g_{k+1} g_{k} = 0
$$

即为了满足line search的条件，需要将下一次的迭代方向和本次的迭代方向垂直。这就是衍生出共轭梯度法了。

当然，[line search](http://en.wikipedia.org/wiki/Line_search)其实有很多其他的启发式方法，比如最直观[backtracing法](http://en.wikipedia.org/wiki/Backtracking_line_search)


## 拟牛顿法

我们再回到牛顿法的Hession矩阵H和$H^{-1}$上，我们知道每一步如果都求解H或者$H^{-1}$是非常耗费时间的，拟牛顿法的思路是，通过近似的方法加迭代的思路求H。回到二阶的泰勒公式：

 $$f(x) = f(x_k)+ \nabla f(x_k) (x-x_k) + \frac{1}{2} (x-x_k)^T \nabla ^2 f(x_k)$$
 
 对f(x)求导数：
 
 $$
 g(x) = g(x_k) + H_k(x-x_k)
 $$
 
 另x为$x_{x+1}$,
 
 $$
 g(x_{k+1}) - g(x_k) = H_k(x_{k+1}-x_k)
 $$
 
 再另$$y_k=g(x_{k+1})-g(x_k), s_k=x_{k+1}-x_k$$,可以简写为：
 
 $$
 y_k = H_k s_k
 $$
 $$
 s_k = H^{-1}_k y_k
 $$
 
 这就是拟牛顿法的条件公式。
 
 
### DFP算法

DFP是3个人名称的首字母，想看八卦可以参考[DFP](http://en.wikipedia.org/wiki/Davidon%E2%80%93Fletcher%E2%80%93Powell_formula),DFP的思想很直接，我们不是要求逆矩阵$H^{-1}$吗？是不是可以找到一直简单的迭代方式，比如：
$$
	H^{-1}_{k+1} = H^{-1}_k + \delta H^{-1}
$$

我们要求H是正定矩阵（原因以后解释），那么就假设一种简单的形式
$$
\delta H^{-1} = \alpha * w w^T + \beta * u u^T
$$

ok，到目前我们带入到拟牛顿条件公式  $$ s_k = H^{-1}_k y_k $$，

$$
( H^{-1}_k  + \alpha * w w^T + \beta * u u^T) \times y_k = s_k
$$

注意到w，u和y都是向量，那么$w^Ty$,$u^Ty$都是表量。
$$
H^{-1}_k y_k + \alpha * w w^T y_k + \beta * u u^T y_k = s_k
$$

$$
(\alpha w^T y_k) * w + (\beta  u^T y_k) u = s_k － H^{-1}_k y_k  
$$

天啦，这个方程如何求解呢？但是，我们只需要找到一组可行的解就ok了，好吧，那么我们就另：

$$
\alpha w^T y_k = 1, => \alpha = \frac{1} {w^T y_k}
$$
$$
\beta  u^T y_k = -1, => \beta = \frac{1} {u^T y_k}
$$

那么
$$
w - u = s_k － H^{-1}_k y_k  
$$

呵呵，还是不能解，能在简单点吗？行！
$$
w = s_k
u = H^{-1}_k y_k  
$$

就这样我们得到:

$$
\alpha = \frac{1} {s_k^T y_k}
$$

$$
\beta = \frac{1} {H^{-T}_k y_k}
$$

$$
H^{-1}_{k+1} = \alpha s_k s_k^T + \beta H^{-1}_k y_k y_k^T H^{-T}_k
$$

到这里DFP我们就完成了$H^{-1}$的迭代求解过程。

### BFGS

BFGS和DFP非常的类似，但是他利用拟牛顿条件公式，H（注意不是$H^{-1}$）做近似，然后在通过Sherman Morrison公式计算$H^{-1}$。是目前表现最好的拟牛顿算法。

和DFP一样，我么只需要兑换s和y的位置就可以得到H的近似公式，然后在计算$H^{-1}$,这里我就不详细讨论了，直接拿结果吧
$$
H_{k+1} = \frac{y_k y_k^T} {y_k^T y_k} + \frac{ H_k s_k s_k^T H^T_k } {H^T_k s_k}
$$

<div class="definition">
BFGS Hession矩阵迭代方程：
$$
H^{-1}_{k+1} = (I - \frac{s_k y^T_k} {y^T_k s_k})H^{-1}_k(I-\frac{y_k s^T_k} {y^T_k s_k}) + \frac{s_k s^T_k} {y^T_k s_k}
$$
</div>
更多见[wiki](http://en.wikipedia.org/wiki/Quasi-Newton_method)

### LBFGS算法

BFGS算法需要记录H，当问题的维度比较高的时候，说需要的存储空间是非常大的。LBFGS又成为Limited－Memory BFGS算法，它对内存进行了优化。

我们从BFGS的公式知道 $$H^{-1}_{k+1}$$总是从(s_0,y_0),(s_1,y_1),...,(s_k,y_k)计算得到，因此我们完全不必要存储 $O(n^2)$内存，二存储 $O(k n)$ 具体的算法因为不设计到原理性的算法问题，这里就不讨论，如果想了解，可以参考[LBFGS](http://en.wikipedia.org/wiki/Limited-memory_BFGS)

主要我们并不是要求出$H^{-1}$,而是 $H^{-1}g_k$

当然LBFGS有很多变种，其中比较重要的是：

- LBFGS-B：带条件约束的LBFGS
- OWL-QN： LBFGS with L1
- O-LBFGS： online learning版本
