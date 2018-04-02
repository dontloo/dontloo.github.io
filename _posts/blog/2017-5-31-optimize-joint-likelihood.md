---	
layout: post	
title: "Optimize the Joint Likelihood?"	
modified:	
categories: blog	
excerpt:	
tags: []	
date: 2017-5-31	
modified: 2017-5-31	
---	
	
When using neural networks to build a classifier, we often optimize the conditional likelihood 	
\\(p_\theta(t|x)=\prod y_k\exp t_k \\) (or its logarithmic form \\(\log p_\theta(t|x)=\sum t_k\log y_k \\)) where \\(y_k\\) is the output of the network which is guaranteed to be nonnegative and \\(\sum y_k=1\\) via normalization (e.g. softmax).	
	
Mostly the normalization does something like \\(y_k = \hat{y_k}/\sum \hat{y_j}\\), since we've interpreted \\(y_k\\) as 	
\\(p_\theta(t_k|x)\\), we could further formulate \\(\hat{y_k}\\) (nonnegative) as \\(p_\theta(t_k,x)=p_\theta(t_k|x)p_\theta(x)\\), then it follows \\(p_\theta(t_k|x) = \hat{y_k}/\sum \hat{y_j} = p_\theta(t_k,x)/p_\theta(x) \\), which is just the Bayes rule.	
	
So we have the joint probability defined, it seems nice to optimize the joint likelihood instead of the conditional likelihood to acquire a generative model. One problem is, the data likelihood \\(p_\theta(x)\\) (which is a factor of the joint likelihood) could be unbounded, then an MLE model will simply output a maximum value regardless of the input. Indeed it would work if we introduce some constraint to address this.
