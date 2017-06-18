---
layout: post
title: "LogSoftMax"
modified:
categories: blog
excerpt:
tags: []
date: 2017-6-18
modified: 2017-6-18
---

For a neural network classifier with cross-entropy loss and softmax in the output layer,
if follows \\(\log p_\theta(t|x)=\sum t_k\log y_k = \sum t_k\log \frac{\exp(a_k)}{\sum\exp(a_j)}\\),
where \\(y_k\\) is the output of the neural network and \\(a_k\\) the activation of the output layer.

In practice, many popular frameworks will instead make \\(a_k\\) the output of the network and move softmax into the loss function.
Because if the loss function can further be derived as 
\\(\log p_\theta(t|x) = \sum t_k\log \frac{\exp(a_k)}{\sum\exp(a_j)} = \sum t_k (a_k - \log\sum\exp(a_j))\\),
where \\(\log\sum\exp\\) can be implemented as [LogSumExp](https://en.wikipedia.org/wiki/LogSumExp) to prevent numerical under/overflow.
On the other hand if we explicitly compute the results of \\(y_k\\), we'll often need to clip the value to avoid *Nan*s,
which will also lead to inaccurate gradients.
