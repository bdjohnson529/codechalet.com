---
layout: blog
title: Binomial Distribution
order: 0
topic: Bayesian Statistics
topic_path: /docs/bayesian/index.html
---
The binomial distribution measures the number of successes in an experiment which has two possible outcomes. Flipping a coin is a binomial experiment - the experiment can produce one of two values, H or T. We can define the two outcomes as *success* and *failure*, depending on the context. Mathematically, the probability of `X` successes, given a likelihood `p` and number of experiments `x` can be expressed like so:

$$ P(x,n,p) = {n \choose x} p^x (1-p)^{(n-x)} $$

The binomial distribution assumes independence between each experiment. Let's plot `P(x)`, for 7 coin flips. In this case `x` represents the number of successes in our experiment. We can use `P(x)` to compute the probability of each outcome - in this case, there are only 7 possible outcomes. First, initialize an array to represent the discrete values of `x`.

```r
x <- 0:100
```

Now, compute the array of probabilities for each outcome.
```r
y <- dbinom(x, size=100, prob=0.5)
```

Plot `x` against `y` to see the probability density function.
```r
plot(x, y, type='h')
```

<img src="{{ site.baseurl }}/assets/img/docs/bayesian/dbinom.png"
     alt="Binomial distribution"
     width=500px
     height="100%">

Note the pdf is *normalized*, if you add up each `P(x)`, the values will sum to 1. The binomial distribution can be used to define the *likelihood* of an outcome. The likelihood is used to update the prior, in Bayesian statistics.

## Weighted Coin Flip
Let's do a simple Bayesian analysis of a weighted coin flip. For the purposes of the experiment, suppose you are having dinner with your friends, and one of your friends brings a coin. Your friend suggests a game - she will flip a coin 100 times, and the person who predicts the number of heads most accurately wins.

### Prior
This particular friend is known to be shady. You suspect that the coin is not a fair coin. You suspect the coin is weighted, but you don't have a good reason to suspect it is weighted towards heads rather than tails. The *prior* is therefore a uniform distribution - each of the probabilities has an equal likelihood of being true.

```r
x <- seq( from=0 , to=1 , length.out=1000 )
prior <- rep( 1 , 1000 )
plot(x, prior)
```

<img src="{{ site.baseurl }}/assets/img/docs/bayesian/uniform-dist.png"
     alt="Uniform distribution"
     width=500px
     height="100%">

### Likelihood
Your friend flips the coin, and out of 100 coin flips, 77 are heads. This is the experiment data, and we can use it to update the prior. In Bayesian analyis, we use the experiment data to compute the likelihood of each prior prediction. Essentially, we are using data to update our model of the world.

Let's use a grid analysis to perform a numerical analysis. First, instantiate a vector with 1000 evenly-spaced values between 0 and 1, to represent the probability `p` of the coin landing on heads. Then, compute the *likelihood* of that value of `p`, using the binomial density function. Note in the code below that since we pass a vector into `dbinom()`, the result is also computed as a vector.

```r
p_grid <- seq( from=0 , to=1 , length.out=1000 )
likelihood <- dbinom( 77 , size=100 , prob=p_grid )
```

<img src="{{ site.baseurl }}/assets/img/docs/bayesian/likelihood.png"
     alt="Likelihood"
     width=500px
     height="100%">

### Posterior
Now we can compute the *posterior* distribution. In Bayesian analysis, the *posterior distribution* is the *prior distribution* multiplied by the *likelihood* of the data. Since the prior is a uniform distribution, our posterior will be identical to our likelihood function.

```r
posterior <- likelihood * prior
plot(x, posterior)
```

<img src="{{ site.baseurl }}/assets/img/docs/bayesian/posterior.png"
     alt="Posterior"
     width=500px
     height="100%">

### Sampling the Posterior
In our case, the posterior distribution has an analytic solution (at this point the posterior can be represented by the binomial probability density function, since the posterior was formed by multiplying a uniform prior and the likelihood). However, in more complex Bayesian models, the posterior does not have a simple solution. It can be computatationally expensive to even calculate the posterior distribution. In this case we can approximate the posterior distribution by sampling it.

Let's take 10,000 samples from the posterior distribution. We are sampling the values of the parameter `p`, which represents the probability that the coin will land on heads. Recall the vector `p_grid` represents 1000 discrete parameter values, and the vector `posterior` represents the plausability of each parameter value.

```r
samples <- sample( p_grid , prob=posterior , size=1e4 , replace=TRUE )
hist(samples)
```

Each value in the `samples` vector is one of the discrete parameter values specified in `p_grid`. Let's create a histogram of the samples drawn from the posterior distribution.

<img src="{{ site.baseurl }}/assets/img/docs/bayesian/samples-hist.png"
     alt="Samples Histogram"
     width=500px
     height="100%">

### Interpreting the Model
The posterior distribution gives us the likelihood of different parameter values. If we were to predict the results of the next 100 coin flips, we could use the posterior distribution to select a parameter value to use in our calculations. In this simple experiment, the most likely parameter value is 0.77, as the posterior distribution is entirely formed by the data (recall the prior was a uniform distribution).

There are definite limitations to our model. The model assumes independence between events, but we know that the physical world is deterministic and a past flip of the coin could influence future coin flips. In his book *Statistical Rethinking*, Richard McElreath points out that physical events are deterministic and therefore past events can influence future events. This could inspire a debate on free will but for our purposes, suffice it to say that the assumption of independence is questionable.

The prior distribution could also be improved. Physics makes it extremely unlikely that the coin would have a 99% probability of landing on heads. Extreme parameter values are unlikely, but our prior distribution treats 0.99 and 0.70 as equally plausible.

The next time your friend wants to play the game, you can use your posterior distribution to make a prediction! After the game, you can use the new experiment data to update the model. The current posterior would become your new prior, and it can be updated using new experiment data.