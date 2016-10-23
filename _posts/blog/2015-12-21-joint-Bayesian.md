---
layout: post
title: "Notes on Joint Bayesian Verification"
modified:
categories: blog
excerpt:
tags: []
date: 2015-12-21
modified: 2015-12-21
---

The followings are some detailed derivatation of the formulars in the paper 
[Bayesian Face Revisited: A Joint Formulation](https://www.microsoft.com/en-us/research/publication/bayesian-face-revisited-a-joint-formulation/).  

### Background
\\[x=\mu+\epsilon\\]
where \\(\mu\\) and \\(\epsilon\\) follow two independent Gaussians \\(N(0,S_\mu)\\) and \\(N(0,S_\epsilon)\\).
The covariance matrices of \\(p(x_1,x_2|H_I)\\) and \\(p(x_1,x_2|H_E)\\) are given by
\\[\Sigma_I=\[ \begin{matrix} 
  S_{\mu}+S_{\epsilon} & S_{\mu} \\\\
  S_{\mu} & S_{\mu}+S_{\epsilon} \end{matrix} \],\\]
\\[\Sigma_E=\[ \begin{matrix} 
  S_{\mu}+S_{\epsilon} & 0 \\\
  0 & S_{\mu}+S_{\epsilon} \end{matrix} \].\\]

### Eq.4  
\\[r(x_1,x_2)=\log\frac{p(x_1,x_2|H_I)}{p(x_1,x_2|H_E)}=x_1^TAx_1+x_2^TAx_2-2x_1^TGx_2+const,\\]
where
\\[A=(S_\mu+S_\epsilon)^{-1}-(F+G),\\]
\\[\[ \begin{matrix} 
  F+G & G\\
  G & F+G 
\end{matrix} \]
=
\[ \begin{matrix} 
  S_{\mu}+S_{\epsilon} & S_{\mu}\\
  S_{\mu} & S_{\mu}+S_{\epsilon} 
\end{matrix} \]^{-1}.\\]
**Derivatation**
\\[p(x_1,x_2|H_I)=\frac{1}{norm}exp(-\frac{1}{2}
\[ \begin{matrix} 
  x_1^T & x_2^T
\end{matrix} \] 
\Sigma_I^{-1}
\[ \begin{matrix} 
  x_1 \\ x_2
\end{matrix} \]),\\]
where
\\[\[ \begin{matrix} 
  x_1^T & x_2^T
\end{matrix} \] 
\Sigma_I^{-1}
\[ \begin{matrix} 
  x_1 \\ x_2
\end{matrix} \]
=
\[ \begin{matrix} 
  x_1 & x_2
\end{matrix} \] 
\[ \begin{matrix} 
  F+G & G\\
  G & F+G 
\end{matrix} \]
\[ \begin{matrix} 
  x_1 \\ x_2
\end{matrix} \]
=
x_1^TAx_1+x_2^TAx_2-2x_1^TGx_2\\]

\\[\[ \begin{matrix} 
  x_1^T & x_2^T
\end{matrix} \] 
\Sigma_E^{-1}
\[ \begin{matrix} 
  x_1 \\ x_2
\end{matrix} \]
=
\[ \begin{matrix} 
  x_1 & x_2
\end{matrix} \] 
\[ \begin{matrix} 
  (S_{\mu}+S_{\epsilon})^{-1} & 0\\
  0 & (S_{\mu}+S_{\epsilon})^{-1}
\end{matrix} \]
\[ \begin{matrix} 
  x_1 \\ x_2
\end{matrix} \]
=
x_1^T(S_{\mu}+S_{\epsilon})^{-1}x_1+x_2^T(S_{\mu}+S_{\epsilon})^{-1}x_2\\]
\\[\therefore r(x_1,x_2)=\log\frac{p(x_1,x_2|H_I)}{p(x_1,x_2|H_E)}=x_1^T((S_\mu+S_\epsilon)^{-1}-(F+G))x_1+x_2^T((S_\mu+S_\epsilon)^{-1}-(F+G))x_2-2x_1^TGx_2+const=x_1^TAx_1+x_2^TAx_2-2x_1^TGx_2+const\\]

### Eq.8
