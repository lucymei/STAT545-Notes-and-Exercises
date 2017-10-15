# Untitled
---
title: "cm009 Notes and Exercises: Table Joins"
date: '2017-10-03'
output: github_document
---


```r
suppressPackageStartupMessages(library(dplyr))
suppressPackageStartupMessages(library(gapminder))
library(tidyverse)
```

```
## Loading tidyverse: ggplot2
## Loading tidyverse: tibble
## Loading tidyverse: tidyr
## Loading tidyverse: readr
## Loading tidyverse: purrr
```

```
## Conflicts with tidy packages ----------------------------------------------
```

```
## filter(): dplyr, stats
## lag():    dplyr, stats
```


After going through the `dplyr` [vignette](https://cran.r-project.org/web/packages/dplyr/vignettes/two-table.html) on "two-table verbs", we'll work on the following exercises.
# how to join two data frames
1. Mutating joins - adding new coloums from new data frame
2. Filtering joins - take original table and subset it
3. Set operations - take two tables with the same variables, intersection, unions, set difference, etc.


```r
# library("nycflights13")
# flights2 <- flights %>% select(year:day, hour, origin, dest, tailnum, carrier)

# flights2 %>% 
  #left_join(airlines)
# finds common variables in both data frames and match up to map the names
# if the name is not found, it will keep rows in the original one, and also keep things that are not found

# inner join - only combine things in common
# outer join - keep rows from both data sets


# coloum a - 0, 1, 2; column val1 - 15, 13, 101
# coloum a - 0,3,2; name - canada, Indian, China

# left join (x,y) - keep everything in x, try to match against y
# Since both data set has column a, but not name, this will generate a new coloum called "name", to add the things that match to column a, and anything that is not matched will return "NA"
# return, column a - 0,1,2; column val1 - 15, 13, 101; name - Canada, NA, China
# if there is a duplicate on the first column, it will return one more column stating the match for the second one


# inner join
# return, column a -


# outer join
# return, column a - 0,1,2,3; val1 - 15,12,101,NA; name - Canada, NA, China, India
```


Consider the following areas of countries, in hectares:


```r
(areas <- data.frame(country=c("Canada", "United States", "India", "Vatican City"),
                     area=c(998.5*10^6, 983.4*10^6, 328.7*10^6, 44)) %>% 
     as.tbl)
```

```
## # A tibble: 4 x 2
##         country      area
##          <fctr>     <dbl>
## 1        Canada 998500000
## 2 United States 983400000
## 3         India 328700000
## 4  Vatican City        44
```


1. To the `gapminder` dataset, add an `area` variable using the `areas` tibble. Be sure to preserve all the rows of the original `gapminder` dataset.

```r
left_join(gapminder, areas)
```

```
## Joining, by = "country"
```

```
## Warning: Column `country` joining factors with different levels, coercing
## to character vector
```

```
## # A tibble: 1,704 x 7
##        country continent  year lifeExp      pop gdpPercap  area
##          <chr>    <fctr> <int>   <dbl>    <int>     <dbl> <dbl>
##  1 Afghanistan      Asia  1952  28.801  8425333  779.4453    NA
##  2 Afghanistan      Asia  1957  30.332  9240934  820.8530    NA
##  3 Afghanistan      Asia  1962  31.997 10267083  853.1007    NA
##  4 Afghanistan      Asia  1967  34.020 11537966  836.1971    NA
##  5 Afghanistan      Asia  1972  36.088 13079460  739.9811    NA
##  6 Afghanistan      Asia  1977  38.438 14880372  786.1134    NA
##  7 Afghanistan      Asia  1982  39.854 12881816  978.0114    NA
##  8 Afghanistan      Asia  1987  40.822 13867957  852.3959    NA
##  9 Afghanistan      Asia  1992  41.674 16317921  649.3414    NA
## 10 Afghanistan      Asia  1997  41.763 22227415  635.3414    NA
## # ... with 1,694 more rows
```


2. To the `gapminder` dataset, add an `area` variable using the `areas` tibble, but only keeping obervations for which areas are available. 

```r
inner_join(gapminder, areas)
```

```
## Joining, by = "country"
```

```
## Warning: Column `country` joining factors with different levels, coercing
## to character vector
```

```
## # A tibble: 36 x 7
##    country continent  year lifeExp      pop gdpPercap      area
##      <chr>    <fctr> <int>   <dbl>    <int>     <dbl>     <dbl>
##  1  Canada  Americas  1952   68.75 14785584  11367.16 998500000
##  2  Canada  Americas  1957   69.96 17010154  12489.95 998500000
##  3  Canada  Americas  1962   71.30 18985849  13462.49 998500000
##  4  Canada  Americas  1967   72.13 20819767  16076.59 998500000
##  5  Canada  Americas  1972   72.88 22284500  18970.57 998500000
##  6  Canada  Americas  1977   74.21 23796400  22090.88 998500000
##  7  Canada  Americas  1982   75.76 25201900  22898.79 998500000
##  8  Canada  Americas  1987   76.86 26549700  26626.52 998500000
##  9  Canada  Americas  1992   77.95 28523502  26342.88 998500000
## 10  Canada  Americas  1997   78.61 30305843  28954.93 998500000
## # ... with 26 more rows
```



3. Use a `_join` function to output the rows in `areas` corresponding to countries that _are not_ found in the `gapminder` dataset. 

```r
anti_join(areas, gapminder)
```

```
## Joining, by = "country"
```

```
## Warning: Column `country` joining factors with different levels, coercing
## to character vector
```

```
## # A tibble: 1 x 2
##        country  area
##         <fctr> <dbl>
## 1 Vatican City    44
```



4. Use a `_join` function to output the rows in `areas` corresponding to countries that _are_ found in the `gapminder` dataset. 

```r
semi_join(areas, gapminder)
```

```
## Joining, by = "country"
```

```
## Warning: Column `country` joining factors with different levels, coercing
## to character vector
```

```
## # A tibble: 3 x 2
##         country      area
##          <fctr>     <dbl>
## 1        Canada 998500000
## 2 United States 983400000
## 3         India 328700000
```



5. Construct a tibble that joins `gapminder` and `areas`, so that all rows found in each original tibble are also found in the final tibble. 

```r
full_join(areas, gapminder)
```

```
## Joining, by = "country"
```

```
## Warning: Column `country` joining factors with different levels, coercing
## to character vector
```

```
## # A tibble: 1,705 x 7
##    country      area continent  year lifeExp      pop gdpPercap
##      <chr>     <dbl>    <fctr> <int>   <dbl>    <int>     <dbl>
##  1  Canada 998500000  Americas  1952   68.75 14785584  11367.16
##  2  Canada 998500000  Americas  1957   69.96 17010154  12489.95
##  3  Canada 998500000  Americas  1962   71.30 18985849  13462.49
##  4  Canada 998500000  Americas  1967   72.13 20819767  16076.59
##  5  Canada 998500000  Americas  1972   72.88 22284500  18970.57
##  6  Canada 998500000  Americas  1977   74.21 23796400  22090.88
##  7  Canada 998500000  Americas  1982   75.76 25201900  22898.79
##  8  Canada 998500000  Americas  1987   76.86 26549700  26626.52
##  9  Canada 998500000  Americas  1992   77.95 28523502  26342.88
## 10  Canada 998500000  Americas  1997   78.61 30305843  28954.93
## # ... with 1,695 more rows
```



6. Subset the `gapminder` dataset to have countries that are only found in the `areas` data frame. 

```r
semi_join(gapminder, areas)
```

```
## Joining, by = "country"
```

```
## Warning: Column `country` joining factors with different levels, coercing
## to character vector
```

```
## # A tibble: 36 x 6
##    country continent  year lifeExp      pop gdpPercap
##     <fctr>    <fctr> <int>   <dbl>    <int>     <dbl>
##  1  Canada  Americas  1952   68.75 14785584  11367.16
##  2  Canada  Americas  1957   69.96 17010154  12489.95
##  3  Canada  Americas  1962   71.30 18985849  13462.49
##  4  Canada  Americas  1967   72.13 20819767  16076.59
##  5  Canada  Americas  1972   72.88 22284500  18970.57
##  6  Canada  Americas  1977   74.21 23796400  22090.88
##  7  Canada  Americas  1982   75.76 25201900  22898.79
##  8  Canada  Americas  1987   76.86 26549700  26626.52
##  9  Canada  Americas  1992   77.95 28523502  26342.88
## 10  Canada  Americas  1997   78.61 30305843  28954.93
## # ... with 26 more rows
```


7. Subset the `gapminder` dataset to have countries that are _not_ found in the `areas` data frame. 

```r
anti_join(gapminder, areas)
```

```
## Joining, by = "country"
```

```
## Warning: Column `country` joining factors with different levels, coercing
## to character vector
```

```
## # A tibble: 1,668 x 6
##        country continent  year lifeExp      pop gdpPercap
##         <fctr>    <fctr> <int>   <dbl>    <int>     <dbl>
##  1 Afghanistan      Asia  1952  28.801  8425333  779.4453
##  2 Afghanistan      Asia  1957  30.332  9240934  820.8530
##  3 Afghanistan      Asia  1962  31.997 10267083  853.1007
##  4 Afghanistan      Asia  1967  34.020 11537966  836.1971
##  5 Afghanistan      Asia  1972  36.088 13079460  739.9811
##  6 Afghanistan      Asia  1977  38.438 14880372  786.1134
##  7 Afghanistan      Asia  1982  39.854 12881816  978.0114
##  8 Afghanistan      Asia  1987  40.822 13867957  852.3959
##  9 Afghanistan      Asia  1992  41.674 16317921  649.3414
## 10 Afghanistan      Asia  1997  41.763 22227415  635.3414
## # ... with 1,658 more rows
```

