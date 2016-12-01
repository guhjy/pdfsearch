# pdfsearch

[![Build Status](https://travis-ci.org/lebebr01/pdfsearch.svg?branch=master)](https://travis-ci.org/lebebr01/pdfsearch)
[![codecov.io](https://codecov.io/github/lebebr01/pdfsearch/coverage.svg?branch=master)](https://codecov.io/github/lebebr01/pdfsearch?branch=master)

This package defines a few useful functions for keyword searching using the [pdftools](https://github.com/ropensci/pdftools)  package developed by [rOpenSci](https://ropensci.org/).

To install use devtools:

```r
devtools::install_github('lebebr01/pdfsearch')
```

## Basic Usage
There are currently two functions in this package. The first `keyword_search` takes a single pdf and searches for keywords from the pdf. The second `directory_search` does the same search over a directory of pdfs.

## Examples
The package comes with two pdf files from [arXiv](https://arxiv.org/) to use as test cases. Below is an example of using the `keyword_search` function.

```r
library(pdfsearch)
file <- system.file('pdf', '1501.00450.pdf', package = 'pdfsearch')

result <- keyword_search(file, 
            keyword = c('repeated measures', 'mixed effects'),
            path = TRUE)
head(result)
```

```
## # A tibble: 6 � 4
##             keyword page_num line_num line_text
##               <chr>    <int>    <int>    <list>
## 1 repeated measures        1       24 <chr [1]>
## 2 repeated measures        2       57 <chr [1]>
## 3 repeated measures        2      108 <chr [1]>
## 4 repeated measures        2      110 <chr [1]>
## 5 repeated measures        2      125 <chr [1]>
## 6 repeated measures        6      444 <chr [1]>
```

### Surrounding lines of text 
It may be useful to extract not just the line of text that the keyword is found in, but also surrounding text to have additional context when looking at the keyword results. This can be added by using the argument `surround_lines` as follows:

```r
file <- system.file('pdf', '1501.00450.pdf', package = 'pdfsearch')

result <- keyword_search(file, 
            keyword = c('repeated measures', 'mixed effects'),
            path = TRUE, surround_lines = 1)
head(result)
```

```
## # A tibble: 6 � 4
##             keyword page_num line_num line_text
##               <chr>    <int>    <int>    <list>
## 1 repeated measures        1       24 <chr [3]>
## 2 repeated measures        2       57 <chr [3]>
## 3 repeated measures        2      108 <chr [3]>
## 4 repeated measures        2      110 <chr [3]>
## 5 repeated measures        2      125 <chr [3]>
## 6 repeated measures        6      444 <chr [3]>
```
