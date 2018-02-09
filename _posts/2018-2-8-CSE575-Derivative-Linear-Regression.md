---
layout: post
title:  CSE 575 Scalar-by-vector Derivatives Used in Linear Regression
categories: [CSE575,linear-algebra,calculus]
---

*This article is originally written in Chinese. Permission to translate has been granted by the author. The link to the orginal post is [here](http://bourneli.github.io/linear-algebra/calculus/2016/04/28/linear-algebra-11-derivate-of-linear-regression.html).*

In linear regreesion, we may encounter scalar-by-vector derivatives when calculating the residual error. This article is going to talk about two derivatives: $$\frac{\partial x^TAx}{\partial x}$$ and $$\frac{\partial b^TAx}{\partial x}$$。

## Scalar-by-vector Derivative

$$f(x_1,\cdots,x_n)$$ is a differentiable multivariable function, denoted as $$f(x)$$. We also have $$x=(x_1,\cdots,x_n)^T$$. The derivative of $$f$$ over $$x$$ is defined as the following n-dimension vector:

$$
\nabla f = \frac{\partial f(x)}{\partial x} 
		 = \begin{bmatrix}
				\frac{\partial f(x)}{\partial x_1} \\	
				\vdots \\
				\frac{\partial f(x)}{\partial x_n} \\
		   \end{bmatrix} \qquad (1)
$$

which is a column vector composed of $$f(x)$$'s partial derivatives.

## Derivative of $$x^TAx$$

Let $$A=\begin{bmatrix}c_1 & \cdots & c_n \end{bmatrix}=\begin{bmatrix}r_1 & \cdots & r_n \end{bmatrix}^T$$, where $$c_i$$ is the column vectors of $$A$$, and $$r_i$$ the row vectors of $$A$$. According to $$(1)$$, the question is now

$$
	f(x) = x^TAx = \sum_{i=1}^n{x_ix^Tc_i} = \sum_{i=1}^n{\sum_{j=1}^n{x_ix_jc_{ij}}}
$$

We take the partial derivative $$\frac{\partial f(x)}{\partial x_k}$$. Only the terms where $$i=k$$ or $$j=k$$ stay, since all the others are treated as constants.

$$
	\frac{\partial f(x)}{\partial x_k} = \sum_{j=1}^n{c_{kj}x_j} + \sum_{i=1}^n{c_{ik}x_i} 
	                                   = r_k^Tx + c_k^Tx = (r_k^T + c_k^T)x \qquad (2)
$$

Bring (2) into (1) and we can solve


$$
\nabla f = \frac{\partial (x^TAx)}{\partial x} 
		 = \begin{bmatrix}
				(r_1^T + c_1^T)x \\
				\vdots \\
				(r_n^T + c_n^T)x \\
		   \end{bmatrix}
		  = \left( \begin{bmatrix} r_1^T \\ \vdots \\ r_n^T \end{bmatrix} + 
			\begin{bmatrix} c_1^T \\ \vdots \\ c_n^T \end{bmatrix} \right) x
		  = (A + A^T)x  \qquad(3)
$$

Derivation complete!



## Derivative of $$b^TAx$$

Let $$A=\begin{bmatrix} a_1 && \cdots && a_n\end{bmatrix}$$ and we define $$f(x)$$ as

$$
	f(x) = b^TAx = b^T\sum_{i=1}^n{a_ix_i}=\sum_{i=1}^n{b^Ta_ix_i}
$$

Take the partial derivative and we have

$$
	\frac{\partial (b^TAx)}{\partial x_k} = b^Ta_k \qquad (4)
$$

Bring (4) into (1)

$$
	\nabla f = \frac{\partial (b^TAx)}{\partial x} 
			 = \begin{bmatrix} b^Ta_1 \\ \vdots \\ b^Ta_n \end{bmatrix}
			 = \begin{bmatrix} a_1^Tb \\ \vdots \\ a_n^Tb \end{bmatrix}
			 = \begin{bmatrix} a_1^T \\ \vdots \\ a_n^T \end{bmatrix} b 
			 = A^Tb
$$

Derivation complete!

## What's Next

Now knowing all of above, let's take on [the residual error matrix](/CSE575-Derivative-Linear-Regression-Matrix).
 



