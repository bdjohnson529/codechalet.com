---
layout: blog
title: R Commands
order: 0
topic: Bayesian Statistics
topic_path: /docs/bayesian/index.html
---
Common R commands.

## Dataframes
`nrows()` - count rows in dataframe `d`
```r
nrow(d)
```

### Vectors
`list()` - construct a list, evaluating elements before saving them in the list.
```r
mylist <- list(1,2,3,4,5)
```

`alist()` - construct a list without evaluating the elements.
```r
mylist <- alist( dunif(75, 0, 100) )
```
