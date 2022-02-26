---
layout: blog
title: R Functions
order: 0
topic: Bayesian Statistics
topic_path: /docs/bayesian-statistics/index.html
---
Custom R functions.


# IO

Print a density plot. Note you will need to modify `reports/` on line 2 to reflect your directory structure.
```r
print_density_plot <- function(sample, filename) {
  filepath = paste('reports/', filename, sep="")

  png(file = filepath,
      width     = 3.25,
      height    = 3.25,
      units     = "in",
      res       = 1200,
      pointsize = 4
      )

  plot(density(sample))

  # close plot
  dev.off()
}
```