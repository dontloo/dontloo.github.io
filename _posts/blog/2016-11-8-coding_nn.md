---
layout: post
title: "Notes on Coding Neural Networks"
modified:
categories: blog
excerpt:
tags: []
date: 2016-11-8
---

This post talks about ffnns, but it should be generaly applicable to rnns too.

### Is the same network being used for both training and test?
If it were in the last century, the answer might be yes. But no. 
Recent network architectures such as dropout, batch normalization yield different behaviors for training and test. 
Sometimes people only need intermediate results of the network as feature representations. 
Sometimes intermediate results need to be shared in order to efficiently process data of non-fixed shape.


The layer behaviors can be different, the network architectures can be different, 
the only thing that connects the training and test is the parameter. 
So, in terms of coding, we should totally decouple the training and test networks as two different functions. 
That is to say, the training defines how to search for \\(\theta\\), the test defines how to apply \\(\theta\\).

### My libaray
A layers is associated with its parameters and interacts with other layers, 
it has different types of behaviors (for training, test or else). 
The notion of a network is broken down into two types of funtions, 
one is for optimization w.r.t some objective funtion (training), 
the other simply computes the output.

