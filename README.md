
<!-- README.md is generated from README.Rmd. Please edit that file -->

# ggfp

<!-- badges: start -->
<!-- badges: end -->

The goal of `ggfp` is to simplify the process of drawing forest plots
using ggplot2. We have packaged the main code for drawing forest plots
to form the `gg_fp()` function. `gg_fp()` has the advantage that only a
few parameters need to be provided to draw a nice forest plot. Of
course, it also has the obvious disadvantage that some of the more
fine-grained graph adjustment parameters are not available in `gg_fp()`.

## Installation

You can install the development version of ggfp like so:

``` r
# devtools::install_github('lizhiwei1994/ggfp')
```

## Example

First, we create a fake data.frame to show how to use `gg_fp()`.

``` r
library(tidyverse)
#> ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──
#> ✔ ggplot2 3.3.6     ✔ purrr   0.3.4
#> ✔ tibble  3.1.7     ✔ dplyr   1.0.9
#> ✔ tidyr   1.2.0     ✔ stringr 1.4.0
#> ✔ readr   2.1.2     ✔ forcats 0.5.1
#> ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
#> ✖ dplyr::filter() masks stats::filter()
#> ✖ dplyr::lag()    masks stats::lag()
set.seed(123)
people_name = paste('author', 1:7)
group = paste('group', 1:4)
facet = paste('facet', 1:5)

df = 
  expand.grid(people_name = people_name, 
                 group       = group,
                 facet       = facet) %>% 
  mutate(b  = rnorm(nrow(.)),
         se = rnorm(nrow(.)),
         low_95 = b - 1.96*se,
         up_95  = b + 1.96*se) %>% 
  as_tibble()
```

This is a basic example which shows you how to solve a common problem:

``` r
library(ggfp)
## basic example code

gg_fp(
  data = df,
  x_axis = people_name,
  point = b,
  low = low_95,
  up = up_95,
  group_var = group,
  facet_var = facet,
  facet_color = c(rep('white', 5)),
  group_color = c('red', 'green', 'yellow', 'orange'),
  point_shape = c(16, 16, 16, 16)
  
)
```

<img src="man/figures/README-example-1.png" width="100%" />

