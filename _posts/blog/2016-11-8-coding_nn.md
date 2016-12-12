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

### Existing Neural Network Libraries
There're many brilliant open source libraries for neural networks and deep learning. Some of them try to wrap every function they provide into an uniform interface (e.g. caffe and tensorflow), such well encapsulated libraries might be easy to use but difficult to change. As the rapid development of deep learning, it is a common need for people in the field to experiment new ideas beyond those encapsulated interfaces, and I often find that the actual interface I want is just the source code.

[Keras](https://github.com/fchollet/keras) does a great job on that, as stated as one of their guiding principles, it was developed with a focus on enabling fast experimentation. *Being able to go from idea to result with the least possible delay is key to doing good research.* Before I found keras, I wrote a library myself for such purpose, followings are some implementation notes.

### Same Network for Training and Test?
Is the same network used for both training and test? If it were in the last century, the answer might be yes. But no. 
For instance, recently developed layers such as batch normalization behave differently at training and test time, and sometimes people only need some intermediate result as feature representations for other tasks at test time. 
Here're a few examples of different architectures in training and test, [Deep Learning Face Attributes in the Wild](http://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Liu_Deep_Learning_Face_ICCV_2015_paper.pdf), [FractalNet: Ultra-Deep Neural Networks without Residuals](https://arxiv.org/abs/1605.07648).

So layer behaviors can be different, network architectures can be different, 
the only thing that connects training and test is (a subset of) the parameters. 
In terms of coding, we totally should decouple the training and test networks as two different functions,
that is to say, the training specifies how to search for the parameters, the test specifies how to use the parameters.

### Implementing a Neural Network Library
The neural network library I wrote follows the following key points, hopefully it would help sorting out the related concepts in terms of implementation.  

- The notion of a network breaks down into two types of functions, one is for optimizing an objective function w.r.t some parameters through an optimizer (training), the other computes the output for some input given the parameters (test).
- A function is defined by stacking up layers.
- A layer can have its parameter, input and output, it may behave differently for training, test or else. 
- Parameters can be shared between layers and functions.

### VAE example
