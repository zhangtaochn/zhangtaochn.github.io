---
layout:     post
title:      "BOW与TF-IDF模型原理介绍"
subtitle:   "statistic model"
date:       2019-05-11 13:19:10 +0800
author:     "ZHANG Tao"
header-img: "img/post-bow&tfidf-2019-05-11-statistic-model.jpg"
tags:
- nlp
- bow
- tf-idf
- machine learning
- statistic model

---

<script type="text/javascript" async src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML"> </script>

### Bag-of-words model

[Bag-of-words model](https://en.wikipedia.org/w/index.php?title=Bag-of-words_model&oldid=525730564) $$^{[1]}$$(BOW) 是一种文本表征模型，常用与自然语言处理与信息检索领域。

模型的大致思路为首先构建一个词袋字典。

例如：

```
John likes to watch movies. Mary likes too.
John also likes to watch football games.
```

我们可以构建一个词典：

```
{"John": 1, "likes": 2, "to": 3, "watch": 4, "movies": 5, "also": 6, "football": 7, "games": 8, "Mary": 9, "too": 10}
```

如此，我们可以对于两段文本进行表征：

```
[1, 2, 1, 1, 1, 0, 0, 0, 1, 1]
[1, 1, 1, 1, 0, 1, 1, 1, 0, 0]
```

数字代表该词在文本当中出现的频次。经过该种方法处理后的文本失去了词本身的顺序关系。

### TF-IDF

TF-IDF（term frequency–inverse document frequency）$$^{[2,3]}$$是一种自然语言处理与信息检索领域常用的算法。TF意思是词频(Term Frequency)，IDF意思是逆文本频率指数(Inverse Document Frequency)。

TF-IDF属于是一种统计模型，该算法模型的目标在于面对大量的文本数据时，如何通过算法得到能够代表每一篇文章的关键词汇，以通过关键词汇来代表该篇文章。

基于我们的理解能够代表一篇文章的词汇即核心词应该满足的条件为：①、该词汇在所有的文档当中出现的次数尽可能少；②、同时在该篇文章当中出现的频次尽可能高。满足以上两个特征的词汇即为核心词。

TF-IDF公式为：

$$tf_{i,j} = \frac{n_{i,j}}{\sum_{k}n_{k,j}}$$

频次：单篇文本当中频次计算方法

$$idf_i = lg\frac{|D|}{|\{j:t_i \in d_j\}|}$$

逆向文件频率：&#124;D&#124;代表语料库文件综述，idf值表示文件总数除以出现过该词汇的文件数，并对其以10为底取对数得到idf值。

$$tfidf = tf_{i,j} * idf_{i}$$

TF-IDF值为两者的乘积。通过公式我们也可以得到只有单篇文本当中出现的频次高而总的语料库出现的文档数少对应的TF-IDF值才会更大。

### Reference:

[1] [wikipedia: Bag-of-words model](<https://en.wikipedia.org/w/index.php?title=Bag-of-words_model&oldid=525730564>)

[2] [百度百科: tf-idf](<https://baike.baidu.com/item/tf-idf/8816134?fr=aladdin>)

[3] [wikipedia: tf-idf]([https://en.wikipedia.org/wiki/Tf%E2%80%93idf](https://en.wikipedia.org/wiki/Tf–idf))

