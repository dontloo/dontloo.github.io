---
layout: post
title: "Notes on Coding Neural Networks"
modified: 2016-11-8
categories: blog
excerpt:
tags: []
date: 2016-11-8
---

This post talks about feedforward neural networks (FFNNs), but the ideas should be applicable to recurrent networks as well.

Network training is to optimize a loss function \\( E(y(x\| \theta), t) \\) of parameter \\( \theta \\), where \\( x \\) is the data \\( t \\) is the label, \\( y(x\| \theta) \\) is the output of the network. 

### Same Network for Training and Test?
Is the same network used for both training and test? If it were in the last century, the answer might be yes. But no. 
For instance, recently developed layers such as batch normalization behave differently at training and test time, and sometimes people only need some intermediate result as feature representations for other tasks at test time. 
Here're a few examples of different architectures in training and test, [Deep Learning Face Attributes in the Wild](http://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Liu_Deep_Learning_Face_ICCV_2015_paper.pdf), [FractalNet: Ultra-Deep Neural Networks without Residuals](https://arxiv.org/abs/1605.07648).

So layer behaviors can be different, network architectures can be different, 
the only thing that connects training and test is (a subset of) the parameters. 
In terms of coding, we totally should decouple the training and test networks as two different functions,
that is to say, the training defines how to search for \\( \theta \\), the test defines how to use \\( \theta \\).

### Implementing Neural Networks
I wrote a neural network library myself following the following key points, and hopefully it would help sorting out the related concepts in terms of implementation.  
- The notion of a network is broken down into two types of functions, 
one is for optimizing an objective function w.r.t some parameters through an optimizer (training), 
the other computes the output for some input given the parameters (test).
- A function is defined by stacking up layers.
- A layer can have its parameter, input and output, it may behave differently for training, test or else. 
- Parameters can be shared between layers and functions.

### VAE example
