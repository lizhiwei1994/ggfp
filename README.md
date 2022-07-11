
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
# devtools::install_github('lizhiwei1994/ggfp)
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

What is special about using `README.Rmd` instead of just `README.md`?
You can include R chunks like so:

``` r
summary(cars)
#>      speed           dist       
#>  Min.   : 4.0   Min.   :  2.00  
#>  1st Qu.:12.0   1st Qu.: 26.00  
#>  Median :15.0   Median : 36.00  
#>  Mean   :15.4   Mean   : 42.98  
#>  3rd Qu.:19.0   3rd Qu.: 56.00  
#>  Max.   :25.0   Max.   :120.00
```

You’ll still need to render `README.Rmd` regularly, to keep `README.md`
up-to-date. `devtools::build_readme()` is handy for this. You could also
use GitHub Actions to re-render `README.Rmd` every time you push. An
example workflow can be found here:
<https://github.com/r-lib/actions/tree/v1/examples>.

You can also embed plots, for example:

<img src="man/figures/README-pressure-1.png" width="100%" />

In that case, don’t forget to commit and push the resulting figure
files, so they display on GitHub and CRAN.
