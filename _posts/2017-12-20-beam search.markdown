---
layout:     post
title:      "greedy decoding和beam search"
date:       2017-12-20 12:00:00
author:     "ZhY"
header-img: "img/post-bg-basic.jpg"
header-mask: 0.3
catalog:    true
tags:
    - nlp
---

## greedy decoding和beam search

greedy decoding == beam search(size=1)

beam search:

beam search只在test时候需要。训练时候知道正确答案，因此不需要使用这个搜索方式。

test时候，假设词表大小为3，内容为a,b,c。beam size是2

decoder解码的时候：

1.生成第一个词的时候，选择概率最大的2个词，假设为a,c，那么当前序列就是a,c

2.生成第二个词的时候，我们将当前序列a和c，分别与词表中所有词进行组合，得到的序列aa ab ac ca cb cc，然后从其中选择2个得分最高的，作为当前序列

3.后面不断重复该过程，直到遇到EOS为止。最终输出2个得分最高的序列


greedy decoding即为beam size等于1的beam search



