---
layout: post
title:  CSE 575 Logistic Regression, Intuitions
categories: [CSE575, regression, machine-learning]
---

*This article is originally written in Chinese. Permission to translate has been granted by the author. The link to the orginal post is [here](http://bourneli.github.io/linear-algebra/calculus/2016/04/30/linear-algebra-12-linear-regression-matrix-calulation.html). Notice this article uses different symbols from the in-class notes, so do feel free to substitute.*

Following [the previous article](/CSE575-Derivative-Linear-Regression), we now want to take on the residual error matrix in linear regression, which composes of Least Squared Errors (LSE).

## Derivation

Let matrix $$A$$ be the hypothesis space matrix, which consists of the basis column vectors/basis functions. $$y$$ is our target, i.e. we are given instances <$$\bf{x_i}, \bf{y_i}$$>. We need to figure out an optimal weight vector $$w$$ such that the residual squared error (LSE) is minimal.

$$
\begin{equation*}
\begin{aligned}
& \underset{x}{\text{min}} && E(w) \\
& \text{s.t.} && E(w)=|Aw-y|^2
\end{aligned}
\end{equation*}
$$

We transform $$E(x)$$

$$
\begin{align}
	E(w) &= (Aw-y)^T(Aw-y) \\ 
		 &= (w^TA^T-y^T)(Aw-y) \\ 
		 &= w^TA^TAw - w^TA^Ty - y^TAw + y^Ty \\
		 &= w^TA^TAw - y^TAw - y^TAw + y^Ty \\
		 &= w^TA^TAw - 2y^TAw + y^Ty \\
\end{align}	
$$

The minimum of $$E(w)$$ is where its partial derivative equals to 0 (since $$E(w)$$ is convex). So

$$
	\frac{\partial E(w)}{\partial w} = 2A^TAw - 2A^Ty = 0
$$

The step above utilizes what we have learned from [the previous article](/CSE575-Derivative-Linear-Regression). Since $$A$$ consists of basis functions, which indicates that its columns are linearly independent, [$$A^TA$$ is invertible](https://math.stackexchange.com/questions/1840801/why-is-ata-invertible-if-a-has-independent-columns){:target="_blank"}. Hence

$$
\begin{align}
	& 2A^TAw - 2A^Ty = 0 \\
	& \Rightarrow A^TAw = A^Ty \\ 
	& \Rightarrow w = (A^TA)^{-1}A^Ty \\
\end{align}
$$

Derivation complete!
 



