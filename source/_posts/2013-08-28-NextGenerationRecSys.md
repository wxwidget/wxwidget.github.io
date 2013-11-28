---
layout: post
title: "下一代推荐系统"
date: 2013-08-08 10:47
categories: Recommender&nbspSysterm
abstract: "主要围绕Gediminas等的论文，讨论下一代推荐系统的形态"
---

##前言

讨论祖先和子孙的问题一向是比较困难的事情，什么是上一代，他们有什么特点？下一代推荐系统到底是什么？前后代有什么不一样，是什么关键特征定义了下一代？
本文的重点是，讨论一些论文观点，旨在回答以上的一些疑问
从Gediminas Adomavicius和Alexander Tuzhilin的Towards the Next Generation of Recommender Systems:
A Survey of the State-of-the-Art and Possible Extensions来看(这篇文章引用率非常高)，我的理解是：

第一代推荐系统主分三类:

1. content-based,基于内容的推荐
2. collaborative,基于协同过滤的推荐
3. hybrid recommendation, 混合型推荐

第二代推荐系统的主要特点是：

1. user和item的理解
2. 结合上下文信息
3. 支持多维度的评价指标
4. 提供更加有弹性和更少打扰的结果

##其人
[Gediminas Adomavicius](http://ids.csom.umn.edu/faculty/gedas/)在推荐系统方面有很多研究, 有兴趣可以看看[CAREER: Next Generation Personalization Technologies](http://ids.csom.umn.edu/faculty/gedas/NSFCareer/),研究主题包括：

1. 多准则推荐系统
2.  推荐查询语言
3.  推荐的多样性
4.  时效数据的聚类
5.  上下文感知推荐
6.  用户偏好对推荐的影响
7.  推荐算法的稳定性
8.  数据特性对推荐的影响

##相关讨论

###第一代推荐系统

早期的推荐系统主要是“评分预测”和“TOPN”预测，不论是哪一种推荐方式，其核心的目标是找到最适合用户c的项集合s，从集合里挑选集合是一个非常复杂的问题优化方案，通常采用的方案是用贪婪的方式，而我们只需要定义一个的效用函数,选取TOPN。

####基于内容的推荐
定义效用函数为：用户c和项s的内容上的"相似性"，比如商品推荐中，为了一个用户推荐一款合适的商品，会计算商品和用户历史上看过或者买过的某些特征上的相似性（比如：品牌的偏好，类目的偏好，商品的属性，商品标签等等）。很多推荐都会在有文本的实体上进行推荐，改进的主要思路是：

1. 扩展实体的文本标记。比如：标签，语义树
2. 用户的文本Profile。比如：taste，preferences,needs。

因此，基于内容的推荐算法的关键问题是建立，item的content profile和user的content profile。
对于有问题内容的推荐实体，一般的方法是利用关键词抽取技术，抽取item中最重要的或者最有信息量的一些text。
第一个任务是选择什么的文本，构建的text从来源上可以分成几个，如果来之item本身的内容，通常称为keywords；
如果来自用户的标记，通常称为tags；如果来之外部的query，通常称为intents。
第二个任务是如何在候选词里做weighting和selection。selection的方式一般是用贪心方法，选出topn weighting的词。

构建user的content profile是比较困难的。因为user本生是没有标记的，通常是通过user从前看过的item和当前看过的item做
标记。从时间的维度上，user的content profile可以分成历史和实时部分，历史部分通常是通过挖掘获取，而实时部分通常是
通过巧妙的"average"或者model-based的方法发现用户content profile, 比较出名的content-based推荐系统是[Fab][fab],
"adaptive filtering"是一种通过user的浏览记录不断提升精度的content profile构建方式

####协同过滤推荐
是大家最为熟悉的推荐算法。算法只涉及到user-item的交互矩阵，推荐方式是Heuristic-based(memory-based)方法（item-based和user-based）和
model-based的方法，后面发展的一批改进协同过滤算法的策略，比如：

1. Default Voting;
2. Inverse User Frequency;
3. Case Amplification;
4. Weighted-majority Prediction
当然其他的协同过滤算法也非常多，下次讨论协同过滤算法的时候在仔细探讨

####混合方法，主要是混合基于内容和协同过滤的方法。变种非常多，这里暂不讨论

###第二代推荐系统

1. model-based的一些变化。谈到第二代，论文提供了一些扩展，比如：model-based方法，通常是基于统计和机器学习的方法，
后面有演化出一些基于数学近似的方法，我理解的数学近似方法其实很简单，
就像我们在高中学习的展开式，或者泰勒公式等等，用无穷多的弱项组合成一个误差最小的结果。
2. 多维度的推荐。其实目前多数的推荐是单维度的，就是对user进行item的推荐，但是有些应用场景，比如：对住在北京的男性用户进行品牌推荐，
或者在妇女节给女性用户推荐优惠商品。这些场景下需要推荐从对个维度上考虑问题，所以在多维的推荐系统中需要一个受众定向的功能。
3. 多准则的推荐。一般情况下，我们即需要推荐的准确，多样性，惊喜度，时效性，覆盖率等等指标；有时候，我们需要保证推荐的推荐的品质，
比如高端的品牌推荐，不能给用户推荐一些低质量的品牌商。
4. 不打扰。很多系统为了搜集用户的兴趣，有时候会强迫用户给商品打分，这样会干扰用户的行为。
怎么在用打扰用户的情况下，搜集潜在的用户反馈；对新用户怎么增量的用户信息量最大item，也是快速构建用户profile的一种方式。

当然还有很多推荐系统应该解决的问题和扩展，
但是，就这样还不能是二代推荐系统的特征, 推荐系统的发展永远是围绕着“用户体验”来做的。

###参考文献
[fab]:https://www.ischool.utexas.edu/~i385q-dt/readings/Balabanovic_Shoham-1997-Fab.pdf "Content-based, collaborative recommendation"
