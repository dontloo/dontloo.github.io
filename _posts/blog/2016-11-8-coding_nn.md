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
Is the networks for training and test the same? If it were in the last century, the answer might be yes. But no. 
Recently developed layers such as dropout, batch normalization behave differently in training and test. 
Sometimes people only need intermediate results of the network as feature representations. 
Sometimes intermediate results need to be shared in order to efficiently process data of non-fixed shape.

Layer behaviors can be different, network architectures can be different, 
the only thing that connects training and test is the parameters. 
So, in terms of coding, we should totally decouple the training and test networks as two different functions. 
That is to say, the training defines how to search for \\(\theta\\), the test defines how to use \\(\theta\\).

### My library
A layers is associated with its parameters and interacts with other layers, 
it can behave differently for training, test or else. 
The notion of a network is broken down into two types of functions, 
one is for optimization w.r.t some objective function (training), 
the other directly computes the output given an input (test).

TBC
### VAE example
