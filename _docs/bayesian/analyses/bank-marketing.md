---
layout: blog
title: Participation Likelihood
order: 2
topic: Bayesian Statistics
topic_path: /docs/bayesian/index.html
---
How can Bayes' theorem be applied to solve business problems? One application is deciding which customers to target for a business outcome. Marketing managers constantly make decisions about which customers to target. Consider this scenario.

You are the marketing manager at a large bank. The bank wants to run a marketing campaign to enroll customers in term deposits - if you're not familiar, a *term deposit* is a fixed term investment which offers a higher interest rate than the savings account. You need to enroll 500 customers for the department to hit its goal. 

It's the end of the year and your budget has almost run out. How many customers do you need to include in the marketing campaign in order to achieve 500 conversions? And perhaps more importantly, which customers should you target?

Fortunately, we have [some data](https://archive.ics.uci.edu/ml/datasets/bank+marketing). The dataset is the results of the marketing campaign which you ran earlier in the year, on a different group of customers. Your analyst compiled data from the previous marketing campaign, and included customer data which the bank maintains on its customers.

How can we predict the likelihood that each customer will sign up for a term deposit?

# Multivariate Models
The available customer information includes **age**, **education**, and the customer's **default status**. Each customer was included in last year's marketing campaign, so we also have the outcome, i.e. whether the customer enrolled in a term deposit or not.

We will use these variables to build a multivariate linear model. Let's build a model which represents  conversion rate as a linear model defined by the parameters age, education, credit and default status. First, let's define the predictive parameters:

* $$ A_i $$ - the age of customer $$ i $$
* $$ E_i $$ - highest level of education for customer $$ i $$, which we will encode as a number
* $$ D_i $$ - default status of customer $$ i $$ : has the customer defaulted on loans?

and the outcome variable:

* $$ R_i $$ - predicted conversion rate for customer $$ i $$

So far, our model looks like this:

$$
R_i \sim Normal(\mu_i, \sigma)
\\ \mu_i = \alpha + \beta_A A_i + \beta_E E_i + \beta_D D_i
$$

Before choosing the prior distribution for each of our coefficients, let's center the education variable.




# References
* [UCI Dataset](https://archive.ics.uci.edu/ml/datasets/bank+marketing) on bank marketing