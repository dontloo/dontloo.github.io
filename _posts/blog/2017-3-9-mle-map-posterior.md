---
layout: post
title: "MLE, MAP and Posterior Probability"
modified: 2017-3-9
categories: blog
excerpt:
tags: []
date: 2017-3-9
---

### MLE and MAP
One most common situation is, we have a model that could produce a probability \\( p(x|\theta) \\) for some observation \\( x \\). 
In the training phase observations are taken as the ground truth, and \\( p(x|\theta) \\) is interpreted as the likelihood function of \\( \theta \\).

We are often interested in the most probable \\( \theta \\) given the data, i.e.  \\( \theta^* = argmax_\theta p(\theta|x) \\).
Applying the Bayes' rule, \\( \theta^* = argmax_\theta p(x|\theta)p(\theta)/p(x). \\)
Since \\( p(x) \\) is independent of \\( \theta \\), it doesn't affect the outcome of the \\( argmax \\) operation, we got 
\\( \theta^* = argmax_\theta p(x|\theta)p(\theta) \\), which is known as maximum a posteriori (MAP).
If we assume a uniform (uninformative) prior \\( p(\theta) \\), if can be further reduced to just \\( \theta^* = argmax_\theta p(x|\theta) \\), which is known as maximum likelihood estimation (MLE).

### Posterior Probability
In many other cases we care more about the entire posterior distribution \\( p(\theta|x) \\) instead of a point estimation (\\( argmax \\)). These two approaches (point estimation and posterior probability) are derived from the Frequentist v.s. Bayesian approaches in Statistics.  
![bayesian](https://raw.githubusercontent.com/dontloo/dontloo.github.io/master/images/bayesian.png)  
There's very neat introduction on Coursera, [Bayesian approach to statistics](https://www.coursera.org/learn/bayesian-methods-in-machine-learning/lecture/wTqJf/bayesian-approach-to-statistics).  

The difficulty of computing the posterior often arises in computing the marginal \\( p(x) = \int p(x|\theta)p(\theta) d\theta \\), as mentioned in Pattern Recognition and Machine Learning

>  In the case of continuous variables, the required integrations may not have closed-form analytical solutions, 
while the dimensionality of the space and the complexity of the integrand may prohibit numerical integration. 
For discrete variables, the marginalizations involve summing over all possible configurations of the hidden variables, 
and though this is always possible in principle, we often find in practice that there may be exponentially many hidden states 
so that exact calculation is prohibitively expensive.

Therefore ideally we would like \\( p(\theta) \\) to be the [conjugate prior](https://en.wikipedia.org/wiki/Conjugate_prior) of the likelihood function \\( p(x|\theta) \\), so that the posterior can be solved analytically and furthermore can be used again as the prior for subsequent analyses.
For instance say the model follows \\( N(x|f(\theta), \sigma) \\), and the prior of \\( \theta \\) is also Gaussian,
then the posterior would be another Gaussian distribution if \\( f(\theta) \\) is linear.

In other cases we normally turn to approximate inference (e.g. Laplace approximation) or sampling (e.g. MCMC) 
or the combination of both for an approximation.

### Discussion
Do not be confused with the notion of the discriminative and generative models. In discriminative (\\( p(y\|x) \\)) and generative (\\( p(y, x) \\)) models, it assumes the data can be formed as \\(x\\) the input and \\(y\\) the target. While in our discussion, \\(x\\) is the data \\(\theta\\) is the parameter, how we solve for the parameters is independent of which model we choose.
