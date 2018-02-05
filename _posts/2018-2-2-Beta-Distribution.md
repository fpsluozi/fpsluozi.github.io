---
layout: post
title: CSE 575 Beta Distribution In-class Exercises 
---
Below are the 3 exercise problems discussed in class regarding the Beta Distribution. Going through all of these may greatly help you with understanding important concepts, and, at least, preparing for the first midterm exam.

Exercise 1 - Derivation of conjugate distribution
---
Coin flip. Benoulli Trails. Derive that the posterior and prior of the Beta distribution are [conjugate distributions](https://en.wikipedia.org/wiki/Conjugate_prior){:target="_blank"}.

**Derivation** 

Suppose we've already known that the prior $$P(\theta) = Beta(\beta_H, \beta_T)$$ and the posterior $$P(\theta\mid D) \propto P(D \mid \theta) P(\theta)$$ . $$\theta$$ and $$D$$ denote the parameter and the observation, and $$\alpha_H$$ and $$\alpha_T$$ the numbers of heads and tails from the observation, respectively.

So for the product of the prior and the likelihood, we have

$$
P(\theta)P(D \mid \theta) = \frac{\theta^{\beta_H - 1}(1 - \theta)^{\beta_T - 1}}{B(\beta_H, \beta_T)} \theta^{\alpha_H}(1-\theta)^{\alpha_T} \\$$

$$
= \frac{1}{B(\beta_H, \beta_T)}\theta^{\alpha_H + \beta_H - 1}(1-\theta)^{\alpha_T + \beta_T - 1} \tag{1}
$$

Since $$P(\theta\mid D) \propto P(D \mid \theta) P(\theta)$$, we may use a constant $$C$$ to simplify the proportion, and thus

$$
P(\theta\mid D) = \frac{1}{C} P(D \mid \theta) P(\theta) \tag{2}
$$

Joining (1) and (2) up, and since $$B(\beta_H, \beta_T)$$ is a constant as well, we can derive that

$$
P(\theta\mid D) = \frac{1}{B(\beta_H, \beta_T)C}\theta^{\alpha_H + \beta_H - 1}(1-\theta)^{\alpha_T + \beta_T - 1} $$

$$
\sim Beta(\alpha_H + \beta_H, \alpha_T + \beta_T) \tag{3}
$$

And thus the expectation of the posterior is

$$
E[P(\theta \mid D)] = mean \space of \space Beta(\alpha_H + \beta_H, \alpha_T + \beta_T) \\
= \frac{\alpha_H + \beta_H}{\alpha_H + \beta_H + \alpha_T + \beta_T}
$$
 

Exercise 2 - Given prior and observations
---

Coin flip. Given the prior pdf $$\sim Beta(2, 3)$$, we observe 2 heads and 2 tails. What is the posterior pdf? What is the MLE $$\theta$$ and what is the MAP $$\theta$$ ?

**Direct Answers** 

Using (3), it's easy to get the posterior distribution as

$$
P(Posterior) \sim Beta(\alpha_H + \beta_H, \alpha_T + \beta_T) = Beta(2 + 2, 2 + 3) = Beta(4, 5)
$$

Recall that $$\hat{\theta}_{MLE}$$ asks for what $$\theta$$ makes observing $$D$$ the most likely. Thus

$$
\hat{\theta}_{MLE} = \underset{\theta}{\operatorname{argmax}} P(D \mid \theta) = \frac{\alpha_H}{\alpha_H + \alpha_T} \tag{4}
$$

And also recall that $$\hat{\theta}_{MAP}$$ is the most likely value in the posterior distribution (aka the peak of the pdf). So

$$
\hat{\theta}_{MAP} = \underset{\theta}{\operatorname{argmax}} P(\theta \mid D) = mode\space of\space Beta(\alpha_H + \beta_H, \alpha_T + \beta_T) 
$$

$$
= \frac{\alpha_H + \beta_H - 1}{\alpha_H + \alpha_T + \beta_H + \beta_T - 2} \tag{5}
$$

**What if...**

Now, what if we observe 20 heads and 20 tails?

Or 200 heads and 200 tails?

You may discover that $$\hat{\theta}_{MLE}$$ and $$\hat{\theta}_{MAP}$$ are converging if the observation is large enough.

Exercise 3 - Given prior and posterior
---

Given the prior $$Beta(2, 3)$$ and the posterior $$Beta(30, 40)$$, what is the observation (aka what are $$\alpha_H$$ and $$ \alpha_T$$)?

**Answer**

So we have $$\beta_H = 2$$, $$\beta_T=3$$, as well as $$\alpha_H + \beta_H = 30$$ and $$\alpha_T + \beta_T = 40$$. Now this is easy.

Some after-thoughts
---

1. The prior distribution is the experience, some model that others use to describe a phenomenon. 

2. The posterior is built upon your own observations AND the experience/prior. Technically you adjust the model in order to fit with your own findings. And that is what the posterior is all about.




