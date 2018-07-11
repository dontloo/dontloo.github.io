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
	
When building a classifier, we often optimize the conditional log-likelihood \\(\log p_\theta(t\|x)=\log Multi(t\|y(x), n=1) = \sum t_k\log y_k \\) w.r.t some parameter \\(\theta\\), where \\(x\\) is the input, \\(t\\) is the target and \\(y\\) is the output of the classifier (network) which is guaranteed to be nonnegative and \\(\sum y_k=1\\) via normalization (e.g. softmax).	
	
Mostly the normalization does something like \\(y_k = \hat{y_k}/\sum \hat{y_j}\\), following the multinomial model we can interpret each \\(y_k\\) as \\(p_\theta(t_k\|x)\\), we could further interpret \\(\hat{y_k}\\) (nonnegative) as \\(p_\theta(t_k,x)\\), then it follows \\(p_\theta(t_k\|x) = \hat{y_k}/\sum \hat{y_j} = p_\theta(t_k,x)/p_\theta(x) \\), which is just the Bayes rule.	
	
So we have the joint probability defined, it seems we can directly read off \\(\sum \hat{y_j}\\) as the marginal likelihood \\(p_\theta(x)\\). However the problem is, \\(p_\theta(x)\\) could be just any distribution (say very high for one input and very low for another and vice versa), as long as the corresponding \\(p_\theta(t_k,x)\\) is of the same scale, the loss won't be so different. Indeed it can be a meaningful distribution if we introduce some assumptions to \\(p_\theta(x)\\).

For instance, say we let \\(p_\theta(x)\\) be a Gaussian mixture model, then \\(p_\theta(t_k\|x)\\) is just the "responsibility" of the \\(k\\)th mixture component. If we optimize \\(p_\theta(t_k\|x)\\) directly, we have the same issue, a data point can be far away from any component while still having the correct conditional likelihood. To obtain a meaningful marginal distribution, we can add \\(p_\theta(x)\\) to the loss, which will then become the joint log-likelihood \\(\log p_\theta(x,t) = \log p_\theta(t\|x) + \log p_\theta(x)\\).

Then it reminds me of the [Google FaceNet](https://www.cv-foundation.org/openaccess/content_cvpr_2015/ext/1A_089_ext.pdf), which basically minimizes the distance between data points in the same category and maximizes the distance between data points from different categories. This is equivalent to minimizing the variance within each Gaussian mixture component while maximizing the distance between component centers. Thus we can set the loss to be \\(\log p_\theta(x\|t) - dist(\theta)\\). There're many way to implement \\(dist(\theta)\\), one obvious way is to compute the distance between every pair of data and add them together. Or as mentioned in this paper [(A Structured Self-attentive Sentence Embedding)](https://arxiv.org/pdf/1703.03130.pdf), we can use \\(-\left\|cov(\theta)-I\right\|^2\\) to set the covariance matrix of component centers close to the identity matrix. However this will also lead to redundant components when the number of components is larger than the dimension of data.
