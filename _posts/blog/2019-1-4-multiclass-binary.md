---
layout: post
title: "Multiclass Classification and Multiple Binary Classifiers"
modified: 2019-1-4
categories: blog
excerpt:
tags: []
date: 2019-1-4
---
Placeholder  

Should we always use hierarchical softmax instead of softmax?

Pros

1. Each update only affects relevant nodes on path to the root, it's more efficient
2. It's usually better on infrequent categories when the training set is imbalanced https://stats.stackexchange.com/q/180076/95569

Cons

XOR problem for a root node
