
<!-- README.md is generated from README.Rmd. Please edit that file -->

# datefixR <img src="man/figures/logo.png" align="right" width="150" />

<!-- badges: start -->

| Usage                                                                                                                                 | Release                                                                                                            | Development                                                                                                                                                                                            |
|---------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [![License: GPL-3](https://img.shields.io/badge/License-GPL3-green.svg)](https://opensource.org/licenses/GPL-3.0)                     | [![CRAN_Status_Badge](https://www.r-pkg.org/badges/version/datefixR)](https://cran.r-project.org/package=datefixR) | [![R build status](https://github.com/nathansam/datefixR/workflows/R-CMD-check/badge.svg)](https://github.com/nathansam/datefixR/actions)                                                              |
| ![R](https://img.shields.io/badge/r-%23276DC3.svg?style=for-the-badge&logo=r&logoColor=white)                                         | [![datefixR status badge](https://nathansam.r-universe.dev/badges/datefixR)](https://nathansam.r-universe.dev)     | [![codecov](https://codecov.io/gh/nathansam/datefixR/branch/main/graph/badge.svg?token=lb83myWBXt)](https://app.codecov.io/gh/nathansam/datefixR)                                                      |
| [![CRAN RStudio mirror downloads](https://cranlogs.r-pkg.org/badges/grand-total/datefixR?color=blue)](https://r-pkg.org/pkg/datefixR) | [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.5655311.svg)](https://doi.org/10.5281/zenodo.5655311)          | [![Project Status: Active – The project has reached a stable, usable state and is being actively developed.](https://www.repostatus.org/badges/latest/active.svg)](https://www.repostatus.org/#active) |

<!-- badges: end -->

`datefixR` is designed to standardize messy date data, such as dates
entered by different people via text boxes, by converting the dates to
R’s Date data type.

This package arose from my own fights with messy date data where dates
were written in many different formats e.g 01-jan-15, 2015 04 02,
10/12/2010 and more.

## Installation instructions

`datefixR` is now available on CRAN.

``` r
install.packages("datefixR")
```

The most up-to-date (hopefully) stable version of `datefixR` can be
installed via [r-universe](https://r-universe.dev/search/)

``` r
# Enable universe(s) by nathansam
options(repos = c(
  nathansam = 'https://nathansam.r-universe.dev',
  CRAN = 'https://cloud.r-project.org'))

install.packages('datefixR')
```

If you wish to live on the cutting edge of `datefixR` development, then
the development version can be installed via

``` r
if (!require("remotes")) install.packages("remotes")
remotes::install_github("nathansam/datefixR", "devel")
```

## Package vignette

`datefixR` has a “Getting Started” vignette which describes how to use
this package in more detail than this page. View the vignette by either
calling

``` r
browseVignettes("datefixR")
```

or visiting the vignette on the [package
website](https://www.constantine-cooke.com/datefixR/articles/datefixR.html)

## Usage

``` r
library(datefixR)
bad.dates <- data.frame(id = seq(5),
                        some.dates = c("02/05/92",
                                       "01-04-2020",
                                       "1996/05/01",
                                       "2020-05-01",
                                       "02-04-96"),
                        some.more.dates = c("2015",
                                            "02/05/00",
                                            "05/1990",
                                            "2012-08",
                                            "jan 2020")
                        )
fixed.df <- fix_dates(bad.dates, c("some.dates", "some.more.dates"))
knitr::kable(fixed.df)
```

|  id | some.dates | some.more.dates |
|----:|:-----------|:----------------|
|   1 | 1992-05-02 | 2015-07-01      |
|   2 | 2020-04-01 | 2000-05-02      |
|   3 | 1996-05-01 | 1990-05-01      |
|   4 | 2020-05-01 | 2012-08-01      |
|   5 | 1996-04-02 | 2020-01-01      |

By default, `datefixR` imputes missing days of the month as 01, and
missing months as 07 (July). However, this behavior can be modified via
the `day.impute` or `month.impute` arguments.

``` r
 example.df <- data.frame(example = "1994")

fix_dates(example.df, "example", month.impute = 1)
#>      example
#> 1 1994-01-01
```

Functions in `datefixR` assume day-first instead of month-first when
day, month, and year are all given (unless year is given first). However
this behavior can be modified by passing `format = "mdy"` to function
calls.

## Limitations

The package is written solely in R and seems fast enough for my current
use cases (a few hundred rows). However, I may convert the core for loop
to C++ in the future if I (or others) need it to be faster.

## Citation

If you use this package in your research, please consider citing
`datefixR`! An up-to-date citation can be obtained by running

``` r
citation("datefixR")
```
