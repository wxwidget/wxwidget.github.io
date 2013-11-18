##冷启动问题的解决

冷启动问题的分类：

1. 用户冷启动（新用户来了）；
2. 物品冷启动（新物品来了）；
3. 系统冷启动（整个推荐系统都是新的，也可以认为，它和“用户冷启动”的区别是，所有用户对系统冷启动来讲都是新用户，都面临冷启动问题）

冷启动是稀疏数据问题一种特殊形态。用户跟系统的交互非常少，导致可以利用的数据比较小,也很难为用户建立Profile和兴趣,因此会导致一般的推荐算法失效。

冷启动问题的解决方案：说白了，就是尽可能利用信息给用户一个可以接受的物品列表，最常见的就是热门排行。

有的是根据冷启动问题分类来的，有的是从解决方案（能利用用户什么类型信息）来的。

####启发式方法

    Linear combination of regression and CF models
    Filterbot Add user features as psuedo users and do collaborative filtering
    Hybrid approaches Use content based to fill up entries, then use CF

http://grouplens.org/papers/pdf/filterbot-CSCW98.pdf

####Matrix Factorization
Good performance on Netflix (Koren, 2009)

####Model-based approaches

- Bilinear random-effects model (probabilistic matrix factorization)
- Good on Netflix data [Ruslan et al ICML, 2009]
- Add feature-based regression to matrix factorization 
  (Agarwal and Chen, 2009)
- Add topic discovery (from textual items) to matrix factorization 
  (Agarwal and Chen, 2009; Chun and Blei, 2011)

