---
layout: post
title: "Notes on Coding Neural Networks"
modified:
categories: blog
excerpt:
tags: []
date: 2016-11-8
---

This post talks about feedforward neural networks (FFNNs), but the ideas should be applicable to recurrent networks as well.

Network training is to optimize a loss function \\(E(y(x|\theta), t)\\) of parameter \\(\theta\\), where \\(x\\) is the data \\(t\\) is the label, \\\\(y(x|\theta)\\) is the output of the network. 

### Same network for training and test?
Is the same network used for both training and test? If it were in the last century, the answer might be yes. But no. 
Recently developed techniques such as dropout, batch normalization behave differently in training and test. 
In many cases people only need the intermediate result as feature representations for other tasks at test time. 
There're a few examples of different networks used for training and test, [Deep Learning Face Attributes in the Wild](http://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Liu_Deep_Learning_Face_ICCV_2015_paper.pdf), [https://arxiv.org/abs/1605.07648](https://arxiv.org/abs/1605.07648).

So layer behaviors can be different, network architectures can be different, 
the only thing that connects training and test is the parameters. 
In terms of coding, we totally should decouple the training and test networks as two different functions,
that is to say, the training defines how to search for \\(\theta\\), the test defines how to use \\(\theta\\).

### My library
A layers is associated with its parameters and interacts with other layers, 
it can behave differently for training, test or else. 
The notion of a network is broken down into two types of functions, 
one is for optimization w.r.t some objective function (training), 
the other directly computes the output given an input (test).

TBC
### VAE example
