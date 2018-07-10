---	
layout: post	
title: "Model the Joint Likelihood?"	
modified:	
categories: blog	
excerpt:	
tags: []	
date: 2017-5-31	
modified: 2017-5-31	
---	
	
When building a classifier, we often optimize the conditional log-likelihood \\(\log p_\theta(t|x)=\log Multi(t|y(x), N=1) = \sum t_k\log y_k \\) w.r.t some parameter \\(theta\\), where \\(x\\) is the input, \\(t\\) is the target and \\(y\\) is the output of the classifier (network) which is guaranteed to be nonnegative and \\(\sum y_k=1\\) via normalization (e.g. softmax).	
	
Mostly the normalization does something like \\(y_k = \hat{y_k}/\sum \hat{y_j}\\), following the multinomial model we can interpret each \\(y_k\\) as \\(p_\theta(t_k|x)\\), we could further interpret \\(\hat{y_k}\\) (nonnegative) as \\(p_\theta(t_k,x)\\), then it follows \\(p_\theta(t_k|x) = \hat{y_k}/\sum \hat{y_j} = p_\theta(t_k,x)/p_\theta(x) \\), which is just the Bayes rule.	
	
So we have the joint probability defined, it seems we can directly read off \\(\sum \hat{y_j}\\) as the input data likelihood \\(p_\theta(x)\\). However one problem is, \\(p_\theta(x)\\) could be just any distribution (say very high for one input and very low for another and vice versa), as long as \\(p_\theta(t_k,x)\\) is of the same scale, the loss won't be so different. Indeed it would be meaningful if we introduce some assumptions to \\(p_\theta(x)\\).

For instance, say we let \\(p_\theta(x)\\) be a Gaussian mixture model, then \\(p_\theta(t_k|x)\\) is just the "responsibility" of the \\(k\\)th mixture component.
TBC
