---
layout: blog
title: R Commands
order: 0
topic: Bayesian Statistics
topic_path: /docs/bayesian/index.html
---
Common R commands.

`typeof()`
: Type of object
```r
typeof(d)
```

<br>
# Dataframes
`nrows()`
: Count rows in dataframe `d`
```r
nrow(d)
```

<br>
# Vectors
`list()`
: Construct a list, evaluating elements before saving them in the list.
```r
mylist <- list(1,2,3,4,5)
```

`alist()`
: Construct a list without evaluating the elements.
```r
mylist <- alist( dunif(75, 0, 100) )
```

`c()`
: Combine values into a vector.
```r
> c(1,2,3,4,5)
[1] 1 2 3 4 5
```

<br>
# Distributions
`dnorm(x, 1, 1)`
: Gives the value of the normal pdf at `x`

<br>
# RStudio
`rm(list = ls() )`
: Remove all data from the global environment.