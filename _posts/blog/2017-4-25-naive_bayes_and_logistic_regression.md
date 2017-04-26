---
layout: post
title: "Naive Bayes and logistic regression"
modified: 2017-4-25
categories: blog
excerpt:
tags: []
date: 2017-4-25
---

### Introduction
Naive Bayes and logistic regression are two basic machine learning models that are compared frequently, 
espcially as the generative/discriminative counterpart of one another. 
However at first sight it seems these two methods are rather different. 
In naive Bayes we just count the frequencice of features and labels while in linear regression we optimize the parameters with regard to some loss function. 
If we express theses two models as probablistic graphical models, we'll see excatly how they are related.

### Graphical Models
**naive Bayes**
As shown in this figure (borrowed from [this tutorial](http://people.cs.umass.edu/~mccallum/papers/crf-tutorial.pdf) without permission),
the naive Bayes model can be expressed as a directed graph where the parent node denotes the output and the leaf nodes denote the input,
the joint probability is then 
\\[p(x, y)=p(y)\prod_n p(x_i|y).\\]

**logistic regression**
The logistic regression model can be expressed as the undirected counterpart of the naive Bayes model.
\\[\tilde{p}(x, y)=\psi(y)\prod_n\psi(x_i, y)\\]
\\[p(y|x)=\frac{1}{z(x)}\tilde{p}(x, y)\\]
\\[z(x)=\sum_y\tilde{p}(x, y).\\]

### Maximum Likelihood Estimation (MLE)
In the simplest case where both the input and output are binary values, for the naive Bayes model, 
both \\(p(y)\\) and \\(p(x_n|y)\\) can be modeled as Bernoulli distributions 
\\[p(y)=Ber(y|\theta_0)\\]
\\[p(x_i|y)=Ber(x_i|\theta_i).\\]
Then the MLE for \\(\theta\\) coould simply be solved by counting the frequencies.

For the logistic regression model, if we choose the log-linear representation with feature functions as the followings
\\[\psi(x_i, y)=\exp(w_i\phi(x_i, y))=\exp(w_i I(x_i=1, y=1))\\]
\\[\psi(y)=\exp(w_0\phi(y))=\exp(w_0 y)).\\]
Then if follows
\\[\tilde{p}(x, y=1)=\exp(\sum_n w_ix_i+w_0)\\]
\\[\tilde{p}(x, y=0)=\exp(\sum_n w_i*0+w_0*0)=1\\]
\\[p(y=1|x)=\frac{1}{z(x)}\tilde{p}(x, y=1)=\sigma(\sum_n w_ix_i+w_0)\\]
\\[p(y|x)=Ber(y|\sigma(\sum_n w_ix_i+w_0))=\sigma(\sum_n w_ix_i+w_0)^y(1-\sigma(\sum_n w_ix_i+w_0))^{(1-y)}.\\]
The MLE for \\(\w\\) can be solved by minimizing the negative log-likelihood (a.k.a the cross-entropy).



### Zero probabilities and overfitting

Essentially, a generative model is one that directly describes how
the outputs probabilistically “generate” the inputs.

not only break down the squential structre of a sentence but each token is inpendent
