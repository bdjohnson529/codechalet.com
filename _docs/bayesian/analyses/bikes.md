---
layout: blog
title: Bicycles and Cold Weather
order: 1
topic: Bayesian Statistics
topic_path: /docs/bayesian/index.html
---
Are people less likely to ride bicycles during a stint of cold weather? This analysis sets out to answer that question, using a data from the [Capital Bikeshare](https://www.capitalbikeshare.com/system-data) system in Washington DC. The operators of the Capital Bikeshare system publish their system data for research, and we are going to use a small sample of that data collected during 2011 and 2012. The dataset is available on the [UCI website](https://archive.ics.uci.edu/ml/datasets/bike+sharing+dataset).

The hourly datset includes 17,379 observations, representing approximately 8760 hourly observations recorded over a 2 year period. Each observation records the timestamp, normalized temperature and a count of total rental bikes. I will focus on these features to keep our model simple.

My hypothesis is that temperature can be used to predict the count of rental bikes. When the temperature increases, the count of rental bikes will also increase. This hypothesis is motivated by my own experience as a bike rider who does not particularly enjoy biking in cold weather.

## Likelihood
Let's build a linear Bayesian model to represent the relationship between our parameters. Let's define the observable parameter $$ x_i $$ as the bike count at observation $$ i $$, and $$ t_i $$ as the normalized temperature at observation $$ i $$. We will use a normal distribution to model the parameter $$ x_i $$. This is the **likelihood function** - it is the probability of the data $$ x_i $$, given the parameters $$ \mu $$ and $$ \sigma $$. 

$$
x_i \sim Normal(\mu, \sigma)
$$

The parameters $$ \mu $$ and $$ \sigma $$ are not observed, and we will need to construct a prior belief about their distribution. First, let's define $$ \mu $$ in terms of the other observable parameter, temperature. This relation is our **linear model**.

$$
\mu = \alpha + \beta t_i
$$

Now we have three unobserved parameters ($$ \alpha, \beta, \sigma$$), in addition to our two observable parameters ($$ x_i, t_i $$). Notice I did not include $$ \mu $$ in the list of unobserved parameters, because $$ \mu $$ is completely defined by the other parameters.

## Priors
Our final task is to construct a **prior distribution** for each of the unobserved parameters. This step requires some intuition, so we will think it through.

A good place to start is by thinking about extreme values. Recall the normalized temperature $$ t_i $$ ranges between 0 and 1. Let's evaluate our linear model when $$ t_i = 0 $$.

$$
\mu = \alpha + \beta (0)
\\ \mu = \alpha
$$ 

Substituting $$ \alpha $$ for $$ \mu $$ in the likelihood function for $$ x_i $$, it is clear that in this case, the distribution of bike counts is defined entirely by $$ \alpha $$. The bike count can never be negative, which means that a good prior would enforce $$ \alpha $$ to be positive. Let's take $$ \alpha $$ to be a log-normal distribution. The bike counts range from 1 to 1000, so we will specify that the log-normal distribution ranges between 0 and 100.

$$
\alpha \sim LogNormal(0,100)
$$

Let's try to understand the rate of change between normalized temperature $$ t_i $$ and bike counts $$ x_i $$. The maximum temperature ever recorded in Washington D.C. is 41 Celsius, and the minimum is -21 Celsius. This gives us a maximum range of 62 Celsius. The normalized temperature ranges from 0 to 1. One-tenth the normalized temperature range represents approximately 6.2 degrees.

Let's take a look at rate of change of our linear equation. Suppose a 6.2 degree difference resulted in 100 additional riders.

$$
\Delta x_i = \beta \Delta t_i
\\ 100 = \beta (0.1)
\\ 1000 = \beta
$$ 

We will take a more conservative estimate, and define $$ \beta $$ as a normal distribution centered around 500, with a standard deviation of 200.

$$
\beta \sim Normal(500, 200)
$$

Finally, we need to construct a prior for the variance of the likelihood function. Recall our bike counts range from 1 to 1000. If we accept that our variance lies within this range, we can construct the variance as a normal distribution with reasonable bounds.

$$
\sigma \sim Normal(0, 100)
$$


## Model
Now that we have constructed a likelihood function, and defined all our priors, we can formulate a well-defined Bayesian model. Notice that each of our parameters is defined as a stochastic distribution - this is a feature of Bayesian analyses. The only parameter which is not defined as a distribution is $$ \mu $$, and that is because $$ \mu $$ is defined in terms of other stochastic parameters.

$$
x_i \sim Normal(\mu, \sigma)
\\ \mu = \alpha + \beta t_i
\\ \alpha \sim LogNormal(0,100)
\\ \beta \sim Normal(500, 200)
\\ \sigma \sim Normal(0, 100)
$$
