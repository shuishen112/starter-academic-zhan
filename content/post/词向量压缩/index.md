---
title: 词向量压缩
subtitle: 词向量压缩
date: 2021-05-20T09:28:58.349Z
draft: false
featured: true
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
\# 词向量压缩

词向量在深度学习中已经有广泛的应用，比如word2vec 和glove等。存储词向量需要大量的存储空间，比如当我们的字典有$n$个tokenS, embedding 维度为$p$时候。我们需要一个$n\times p$大小的矩阵存储空间。因此，对于深度学习任务而言，如何压缩词向量，让词向量既可以有足够的表达能力保证模型的准确性是非常有必要的。在本文中，我们介绍了几种压缩词向量的方式。Word2ket，Light RNN和Tensor Train Compression.

\## 介绍

现代深度学习方法往往依赖于词向量表示，它可以将离散的自然语言转化到一个连续的空间。对于一个字典大小为$d$的语料而言，最简单的方式就是使用one-hot表示，这样我们可以得到一个$d\times d$维度的词向量矩阵，这个空间是非常大的。word2vec和glove则将embedding的维度缩小为$p$($p\ll d$)。通常情况下，字典的大小可以到达$d=10^5$或者$10^6$,而embedding的维度可以从$p=300$到$p=1024$。我们在本文中介绍其他几种压缩词向量的方法。

\## 模型

\### word2ket

word2ket是基于量子理论而构建的。

\#### From Tensor Product Space to word2ket

两个单独的希尔伯特空间$\mathcal{V}$ 和 $\mathcal{W}$,可以通过张量积构成希尔伯特空间，这个空间定义为$\mathcal{V}\otimes\mathcal{W}$