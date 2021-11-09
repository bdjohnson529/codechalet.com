---
layout: blog
title: Normal Distribution
order: 0
topic: Bayesian Statistics
topic_path: /docs/bayesian/index.html
---
The normal distribution is capable of representing many different process models. Any measurement with noise will tend towards a normal distribution, because of the cumulative effects of the fluccuations. For example, if you are trying to measure the postition of the stars in the sky, you will tend to have fewer measurements with extreme errors, and more measurements with errors of smaller magnitude.

Parameters with normal distributions can be represented like so, where $$ \mu $$ is the mean and $$ \sigma $$ is the variance.

$$  X \sim \mathcal{N}(\mu,\,\sigma) $$

Mathematically, the equation for the normal probability density function is 

$$
f(x) = \frac{1}{\sigma\sqrt{2\pi}} 
\exp\left( -\frac{1}{2}\left(\frac{x-\mu}{\sigma}\right)^{\!2}\,\right)
$$

Let's substitute $$ \beta $$ for the factor multiplying $$ e $$.

$$
f(x) = \beta e ^ {\left( -\frac{1}{2}\left(\frac{x-\mu}{\sigma}\right)^{\!2}\,\right)}
$$

Multiplying out the quadratic in the exponent, we get

$$
f(x) = \beta e ^ {\left( - \frac{x^2 -  2x\mu + \mu^2 }{ 2 \sigma^2} \right)}
$$
