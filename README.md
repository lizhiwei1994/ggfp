
<!-- README.md is generated from README.Rmd. Please edit that file -->

# ggfp: Easy way to draw a forest plot (fp) with ggplot2(gg)

[![lifecycle](https://img.shields.io/badge/lifecycle-experimental-%23fd8008.svg)](https://lifecycle.r-lib.org/articles/stages.html)
[![install with
devtools](https://img.shields.io/badge/install%20with-devtools-brightgreen.svg)](https://cran.r-project.org/web/packages/devtools/index.html)
[![issues](https://img.shields.io/github/issues/lizhiwei1994/ggfp.svg)](https://github.com/lizhiwei1994/ggfp/issues)

## :bar_chart: Overview

The goal of `ggfp` is to simplify the process of drawing forest plots
using ggplot2. We have packaged the main code for drawing forest plots
to form the `gg_fp()` function. `gg_fp()` has the advantage that only a
few parameters need to be provided to draw a nice forest plot. Of
course, it also has the obvious disadvantage that some of the more
fine-grained graph adjustment parameters are not available in `gg_fp()`.

## :arrow_double_down: Installation

You can install the development version of ggfp like so:

``` r
devtools::install_github('lizhiwei1994/ggfp)
```

## :beginner: Usage

First, we create a fake data.frame to show how to use `gg_fp()`.

``` r
library(tidyverse)
#> ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──
#> ✔ ggplot2 3.3.6      ✔ purrr   0.3.4 
#> ✔ tibble  3.1.7      ✔ dplyr   1.0.10
#> ✔ tidyr   1.2.1      ✔ stringr 1.4.1 
#> ✔ readr   2.1.2      ✔ forcats 0.5.1
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

You can change the facet strip color by giving color name to
`facet_color`.

``` r
gg_fp(
  data = df,
  x_axis = people_name,
  point = b,
  low = low_95,
  up = up_95,
  group_var = group,
  facet_var = facet,
  facet_color = c('blue', 'red', 'purple', 'blue', 'red'),
  group_color = c('red', 'green', 'yellow', 'orange'),
  point_shape = c(16, 16, 16, 16)
  
)
```

<img src="man/figures/README-change facet color-1.png" width="100%" />

In that case, don’t forget to commit and push the resulting figure
files, so they display on GitHub and CRAN.

## :page_with_curl: About Author

Zhiwei Li (<lizhiwei@ccmu.edu.cn>)

Department of Epidemiology and Health Statistics

School of Public Health, Capital Medical University

No.10 Xitoutiao, Youanmen Wai Street

Beijing, 100069
