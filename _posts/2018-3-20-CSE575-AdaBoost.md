---
layout: post
title:  CSE 575 AdaBoost, Intuition
categories: [CSE575, boosting]
---

This post is going to share some of my own thoughts on the concept of AdaBoost. Notice it is not going to be superbly rigid, but rather I'd like build up some intuition.

First things first, there is this wonderful AdaBoost guide by some fine gentlement from CMU that you can refer to anytime: [CMU 10701 Lecture 10](https://www.cs.cmu.edu/~aarti/Class/10701/slides/Lecture10.pdf)

Next, I will go through the AdaBoost question from Homework Assignment 2 so as to demonstrate the procedure AdaBoost takes by each step. In the following demo I will show how to proceed in Iteration 1 and Iteration 2.

## A Brief Walkthrough
Recall we have the following 1-D training dataset and the sole weak classifier C. Also recall each sample is assigned with an initial weight of 0.1 .

$$

	\begin{array}{l|l|l|l|l|l|l|l|l|l|l}
		
		\hline\textbf{x} & 0 & 1 & 2 & 3  & 4  & 5  & 6 & 7 & 8 & 9  \\\hline
		\textbf{y} & 1 & 1 & 1 & -1 & -1 & -1 & 1 & 1 & 1 & -1 \\\hline 
	\end{array}
	
$$

$$
C(x)=\begin{cases}
+1\hspace{1cm}    x < \theta;\\
-1\hspace{1cm}    x \geq \theta.
\end{cases}

$$

$$
D_1 = (w_{1,1}, w_{1,2}, ... , w_{1 ,10})\\=(0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1)
$$

### Iteration t=1
(1) The initial threshold $$\theta=2.5$$, which minimizes the weighted training error, is given to you. So at such $$C_1(x)$$, we have the current optimal weak classifier as

$$
C_1(x)=\begin{cases}
+1\hspace{1cm}    x < 2.5;\\
-1\hspace{1cm}    x \geq 2.5.
\end{cases}
$$

(2) The minimal weighted training error by $$C_1(x)$$ on the dataset is 

$$\epsilon_1 = P(C_1(x_i) \neq y_i) = \sum^{N}_{i=1}w_{ti}I(C_1(x_i) \neq y_i) = 0.3$$

where I() is the [indicator function](https://en.wikipedia.org/wiki/Indicator_function).

(3) So the coefficient for $$C_1(x)$$, 

$$
\alpha_1 = \frac{1}{2} \log \frac{1-\epsilon_1}{\epsilon_1} = 0.4236
$$

(4) We now can update the samples' weights and produce $$D_2$$.

$$
D_2 = (w_{2 1}, w_{2 2}, ... , w_{2 10})\\
w_{2,i} = \frac{w_{1,i}}{Z_1} \exp(-\alpha_1 y_1 C_1(x_i)),\hspace{1cm}i=1,2,...,10 \\
D_2 = (0.07143, 0.07143, 0.07143, 0.07143, 0.07143, 0.07143, \\
0.166667, 0.166667, 0.166667, 0.07143)
$$

(5) And hence at the current step, the linearly combined classifer f is

$$
f_1(x) = \alpha_1 C_1(x) = 0.4236 C_1(x)
$$

The ensemble classifer $$sign[f_1(x)]$$ has the overall accuracy of 0.7 .

### Iteration t=2
(1) Now we have to pick the threshold on our own. Since there are 11 'cuts' to divide our training set, and after trying them all, we may find when $$8<\theta<9$$, the weighted training error is at minimum. Let's set $$\theta = 8.5$$ for convenience.

$$
C_2(x)=\begin{cases}
+1\hspace{1cm}    x < 8.5;\\
-1\hspace{1cm}    x \geq 8.5.
\end{cases}
$$

Steps (2) through (4) follow the same fashion as are in Iteration t=1. We may get the following:

$$
\epsilon_2 = P(C_2(x_i) \neq y_i) = 0.2143 \\
\alpha_2 = \frac{1}{2} \log \frac{1-\epsilon_2}{\epsilon_2} = 0.6496 \\
D_3 = (0.0455, 0.0455, 0.0455, 0.1667, 0.1667, 0.1667, \\
0.1060, 0.1060, 0.1060, 0.0455)
$$

(5) And hence at the current step, the linearly combined classifer f is now

$$
f_2(x) = \alpha_1 C_1(x) + \alpha_2 C_2(x)  = 0.4236 C_1(x) + 0.6496 C_2(x)
$$

The ensemble classifer $$sign[f_2(x)]$$ still has the overall accuracy of 0.7 .

Iterations will continue until $$sign[f_t(x)]$$ reaches 100% accuracy, which is guaranteed by the nature AdaBoost. The proof can be found either from our class slides, or from [the aforementioned CMU lecture note on Page 22](https://www.cs.cmu.edu/~aarti/Class/10701/slides/Lecture10.pdf).

## Amplifying the Misclassified

Take notice from Step (2) above, when you are updating the weights on each sample, you are equivalently doing the following selection:

$$
w_{t+1, i}=\begin{cases}
\frac{w_{t,i}}{Z_t}\exp(-\alpha_t)\hspace{1cm}    C_t(x_i) = y_i\\
\frac{w_{t,i}}{Z_t}\exp(\alpha_t)\hspace{1cm}    C_t(x_i) \neq y_i.
\end{cases}
$$

From this we can tell that the weights of the samples misclassified by $$C_t(x_i)$$ are amplified, while those of the correctly classified are shrinked. Intuitively, you may treat it as that the weights of the misclassified are now of $$\exp(2\alpha_t)$$ times importance in the following iteration.