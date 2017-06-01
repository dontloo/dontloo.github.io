---
layout: post
title: "Why Not Optimize the Joint Likelihood?"
modified:
categories: blog
excerpt:
tags: []
date: 2017-5-31
modified: 2017-5-31
---

Mostly when neural networks are used to build a classifier, we often optimizes the conditional likelihood 
\\(p_\theta(t|x)=\prod y_k\exp t_k \\) (or its logarithm form \\(\log p_\theta(t|x)=\sum t_k\log y_k \\)) where \\(y_k\\) is the output of the network which is guaranteed to satisfy
\\(\sum y_k=1\\) via normalization in the output layer (e.g. softmax).




