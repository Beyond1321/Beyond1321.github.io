# Chapter 1 Data Mining

## 1.1 什么是数据挖掘

### 机器学习和数据挖掘对比

+ 机器学习相比数据挖掘，可解释性较差。
+ 当挖掘的目标明确时，机器学习竞争力较差。

### 数据建模

+ 总结数据
  + 比如谷歌的网页排名
  + 比如数据聚合的思想 （水井 伦敦霍乱）
+ 提取数据的主要特征
  + frequent itemset 频繁项集 （购物篮问题 寻找购物篮中 经常出现的商品组合）
  + similarity item 相似项 （比如亚马逊商店，将商品推荐给相似的顾客）

## 1.2 数据挖掘的统计限制

### 举例：TIA项目 

total information awareness

收集各种信息，分析预防恐怖分子，后因隐私问题被终止。

### Bonferroni准则

数据量大时，会出现一些不寻常的特征看起来很重要，但并不。

`Bonferroni principal`  在一些随机产生的数据中，很难找到想要的结果。比如从一堆随机数据中分析找到一些恐怖分子。可能得到的是许多根本不是恐怖分子的结果。

## 1.3 Things Useful to Know

### 词的重要性

+ 比如文章分类，停词 `stop word`，比如`the and`会被先去掉。

+ 文章中出现次数少的词更重要，但不是所有这样的词都重要。

#### TF-IDF

N篇文章，判断词的重要性。TF-IDF Term Frequency times Inverse Document Frequency

计算方式如下：
$$
TF_{ij}=\frac{f_{ij}}{max_kf_{kj}}
$$

$$
IDF_i=log_2(N/n_i)
$$
$TF_{ij}$ 表示第

