---
layout: post
title: "MLE, MAP and Bayesian Learning"
modified: 2017-3-9
categories: blog
excerpt:
tags: []
date: 2017-3-9
---

### MLE and MAP
One most common situation is, we build a model that could produce a probability \\( p(x|\theta) \\) for some observation \\( x \\). 
The observations are taken as the ground truth in the training phase, and \\( p(x|\theta) \\) is interpreted as the likelihood function of \\( \theta \\).

The maximum likelihood estimation (MLE) is seeking the \\( \theta \\) that maximizes the likelihood function \\( p(x|\theta) \\).
If we assume a prior distribution \\( p(\theta) \\), the posterior distribution can be computed by \\( p(\theta|x)=p(x|\theta)p(\theta)/p(x) \\) according to the Bayes' theorem,
since \\( p(x) \\) is independent of \\( \theta \\), optimizing \\( p(\theta|x) \\) is equivalent to optimizing \\( p(x|\theta)p(\theta) \\),
which is known as maximum a posteriori (MAP).

### Bayesian Learning
While the Bayesian learning approach is aimed at computing the whole posterior distribution instead of doing a point estimation.
The difficulty of computing the posterior often arises in computing the denominator \\( p(x) = \int p(x|\theta)p(\theta) d\theta )\\, 
as mentioned in Pattern Recognition and Machine Learning

>  In the case of continuous variables, the required integrations may not have closed-form analytical solutions, 
while the dimensionality of the space and the complexity of the integrand may prohibit numerical integration. 
For discrete variables, the marginalizations involve summing over all possible configurations of the hidden variables, 
and though this is always possible in principle, we often find in practice that there may be exponentially many hidden states 
so that exact calculation is prohibitively expensive.

Therefore ideally we want \\( p(\theta) \\) to be the [conjugate prior](https://en.wikipedia.org/wiki/Conjugate_prior) of the likelihood function \\( p(x|\theta) \\),
so that the posterior can be solved analytically and angain can be used as the prior when the next observation comes in.
Otherwise we would rely on approximate inference (e.g. Laplace approximation) or sampling (e.g. MCMC) 
or the combination of both (e.g. auto-encoding variational Bayes) for an approximation.

### Discussion
MLE and MAP are optimization problems, Bayesian Learning is not.
