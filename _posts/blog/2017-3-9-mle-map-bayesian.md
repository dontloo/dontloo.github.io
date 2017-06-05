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
One most common situation is, we have a model that could produce a probability \\( p(x|\theta) \\) for some observation \\( x \\). 
In the training phase observations are taken as the ground truth, and \\( p(x|\theta) \\) is interpreted as the likelihood function of \\( \theta \\).

The maximum likelihood estimation (MLE) is seeking the \\( \theta \\) that maximizes the likelihood function.
If we assume a prior distribution \\( p(\theta) \\), the posterior distribution can be computed by \\( p(\theta|x)=p(x|\theta)p(\theta)/p(x) \\) according to the Bayes' theorem,
since \\( p(x) \\) is independent of \\( \theta \\), optimizing \\( p(\theta|x) \\) is equivalent to optimizing \\( p(x|\theta)p(\theta) \\),
which is known as maximum a posteriori (MAP).

### Bayesian Learning
The Bayesian learning approach is aimed at computing the entire distribution instead of doing a point estimation.
The difficulty of computing the posterior often arises in computing the denominator \\( p(x) = \int p(x|\theta)p(\theta) d\theta \\), as mentioned in Pattern Recognition and Machine Learning

>  In the case of continuous variables, the required integrations may not have closed-form analytical solutions, 
while the dimensionality of the space and the complexity of the integrand may prohibit numerical integration. 
For discrete variables, the marginalizations involve summing over all possible configurations of the hidden variables, 
and though this is always possible in principle, we often find in practice that there may be exponentially many hidden states 
so that exact calculation is prohibitively expensive.

Therefore ideally we want \\( p(\theta) \\) to be the [conjugate prior](https://en.wikipedia.org/wiki/Conjugate_prior) of the likelihood function \\( p(x|\theta) \\),
so that the posterior can be solved analytically and again can be used as the prior when the next observation comes in.
For instance say the model follows \\( N(x|f(\theta), \sigma) \\), and the prior of \\( \theta \\) is also Gaussian,
then the posterior would be another Gaussian distribution if \\( f(\theta) \\) is linear.

In other cases we normally turn to approximate inference (e.g. Laplace approximation) or sampling (e.g. MCMC) 
or the combination of both for an approximation.

### Discussion
MLE and MAP are optimization problems by definition, Bayesian Learning is not.  

Bayesian Learning is widely applicable for a whole lot of problems, estimating parameter distributions is just one of them.

Do not be confused with the notion of the discriminative and generative models. In discriminative (\\( p(y\|x) \\)) and generative (\\( p(y, x) \\)) models, it assumes the data can be formed as \\(x\\) the input and \\(y\\) the target. While in our discussion, \\(x\\) is the data \\(\theta\\) is the parameter, how we solve for the parameters is independent of which model we choose.
