
esaj <img src="man/figures/logo.png" align="right" />
=====================================================

[![Made In Brazil](https://img.shields.io/badge/made%20in-brazil-green.svg)](http://www.abj.org.br) [![Travis-CI Build Status](https://travis-ci.org/courtsbr/esaj.svg?branch=master)](https://travis-ci.org/courtsbr/esaj) [![AppVeyor Build Status](https://ci.appveyor.com/api/projects/status/github/courtsbr/esaj?branch=master&svg=true)](https://ci.appveyor.com/project/courtsbr/esaj)

Overview
--------

The `esaj` R package is a simple interface that allows you to download multiple kinds of files from Brazil's e-SAJ (Electronic Justice Automation System) portals. With this package you can save and parse lawsuits, queries, and decisions with very simple, tidyverse compliant functions.

To install `esaj`, run the code below:

``` r
# install.packages("devtools")
devtools::install_github("courtsbr/esaj")
```

Usage
-----

### Lawsuits

Before `esaj` if you wanted to gather information about lawsuits being processed by Brazil's state-level Judiciary ("TJ" or "TJs"), you would have to go to each state's e-SAJ portal, manually input each lawsuit's ID, break a capthca, and only then download an HTML with the information you wanted; now you can simply run `download_cpopg()` or `download_cposg()`, and spend your valuable time analysing the data.

``` r
# Download trial court level from multiple states
ids <- c(
  "0123479-07.2012.8.26.0100",
  "0552486-62.2015.8.05.0001",
  "0303349-44.2014.8.24.0020")
esaj::download_cpopg(ids, "~/Desktop/")
#> [1] "/Users/user/Desktop/01234790720128260100.html"
#> [2] "/Users/user/Desktop/05524866220158050001.html"
#> [3] "/Users/user/Desktop/03033494420148240020.html"

# Download appellate level cases from São Paulo State Court of Justice 
ids <- c(
  "1001869-51.2017.8.26.0562",
  "1001214-07.2016.8.26.0565")
esaj::download_cposg(ids, "~/Desktop/")
#> [1] "/Users/user/Desktop/10018695120178260562.html"
#> [2] "/Users/user/Desktop/10012140720168260565.html"
```

For more information on how to use these functions and which TJs are implemented, please see [Downloading Lawsuits](http://courtsbr.github.io/esaj/articles/download_lawsuit.html).

### Queries

Besides downloading lawsuits (see the **Downloading Lawsuits** article), `esaj` also allows the user to download the results of a query on lawsuits. This kind of query is very useful for finding out what lawsuits contain certain words, were filed in a given period, were filed in a given court, etc.

``` r
# Download results of a simple trial level query
esaj::download_cjpg("recurso", "~/Desktop/")
#> [1] "/Users/user/Desktop/search.html"
#> [2] "/Users/user/Desktop/page1.html"

# Download results of a slightly more complex appellate level query
esaj::download_cjsg("recurso", "~/Desktop/", classes = c("1231", "1232"))
#> [1] "/Users/user/Desktop/search.html"
#> [2] "/Users/user/Desktop/page1.html"
```

For more information on how to use these functions and all their auxiliary methods (like `peek_cj*g()` and `cj*g_table()`), please see [Downloading Queries](http://courtsbr.github.io/esaj/articles/download_query.html).

### Decisions

Of all functions in the `esaj` package, `download_decision()` is probably the simplest: it downloads the PDF belonging to a decision and that's it.

``` r
# Download one decision
esaj::download_decision("10000034", "~/Desktop/")
#> [1] "/Users/user/Desktop/10000034.pdf"

# Download more than one decision
esaj::download_decision(c("10800758", "10000034"), "~/Desktop/")
#> [1] "/Users/user/Desktop/10800758.pdf"
#> [2] "/Users/user/Desktop/10000034.pdf"
```

For more information on how to use this function, please see [Downloading Decisions](http://courtsbr.github.io/esaj/articles/download_decision.html).
