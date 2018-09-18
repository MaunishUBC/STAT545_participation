---
title: 'cm005: `dplyr` Exercise'
output:
  html_document:
    keep_md: true
---

**Optional, but recommended startup**:

Change the file output to both html and md _documents_ (not notebook).

# Intro to `dplyr` syntax

1. Load the `gapminder` and `tidyverse` packages. Hint: `suppressPackageStartupMessages()`!
    - This loads `dplyr`, too.
2. `knit` the document. 


```r
library(gapminder)
```

```
## Warning: package 'gapminder' was built under R version 3.3.2
```

```r
library(tidyverse)
```

```
## Warning: package 'tidyverse' was built under R version 3.3.2
```

```
## Loading tidyverse: ggplot2
## Loading tidyverse: tibble
## Loading tidyverse: tidyr
## Loading tidyverse: readr
## Loading tidyverse: purrr
## Loading tidyverse: dplyr
```

```
## Warning: package 'ggplot2' was built under R version 3.3.2
```

```
## Warning: package 'tibble' was built under R version 3.3.2
```

```
## Warning: package 'tidyr' was built under R version 3.3.2
```

```
## Warning: package 'readr' was built under R version 3.3.2
```

```
## Warning: package 'dplyr' was built under R version 3.3.2
```

```
## Conflicts with tidy packages ----------------------------------------------
```

```
## filter(): dplyr, stats
## lag():    dplyr, stats
```


## `select()`

1. Make a data frame containing the columns `year`, `lifeExp`, `country` from the gapminder data, in that order.

```r
select(gapminder, year, lifeExp, country)
```

```
## # A tibble: 1,704 x 3
##     year lifeExp     country
##    <int>   <dbl>      <fctr>
##  1  1952  28.801 Afghanistan
##  2  1957  30.332 Afghanistan
##  3  1962  31.997 Afghanistan
##  4  1967  34.020 Afghanistan
##  5  1972  36.088 Afghanistan
##  6  1977  38.438 Afghanistan
##  7  1982  39.854 Afghanistan
##  8  1987  40.822 Afghanistan
##  9  1992  41.674 Afghanistan
## 10  1997  41.763 Afghanistan
## # ... with 1,694 more rows
```

2. Select all variables, from `country` to `lifeExp`. 

```r
select(gapminder, country:lifeExp)
```

```
## # A tibble: 1,704 x 4
##        country continent  year lifeExp
##         <fctr>    <fctr> <int>   <dbl>
##  1 Afghanistan      Asia  1952  28.801
##  2 Afghanistan      Asia  1957  30.332
##  3 Afghanistan      Asia  1962  31.997
##  4 Afghanistan      Asia  1967  34.020
##  5 Afghanistan      Asia  1972  36.088
##  6 Afghanistan      Asia  1977  38.438
##  7 Afghanistan      Asia  1982  39.854
##  8 Afghanistan      Asia  1987  40.822
##  9 Afghanistan      Asia  1992  41.674
## 10 Afghanistan      Asia  1997  41.763
## # ... with 1,694 more rows
```


3. Select all variables, except `lifeExp`.

```r
select(gapminder, -lifeExp) # The minus sign is to deselect a particular column
```

```
## # A tibble: 1,704 x 5
##        country continent  year      pop gdpPercap
##         <fctr>    <fctr> <int>    <int>     <dbl>
##  1 Afghanistan      Asia  1952  8425333  779.4453
##  2 Afghanistan      Asia  1957  9240934  820.8530
##  3 Afghanistan      Asia  1962 10267083  853.1007
##  4 Afghanistan      Asia  1967 11537966  836.1971
##  5 Afghanistan      Asia  1972 13079460  739.9811
##  6 Afghanistan      Asia  1977 14880372  786.1134
##  7 Afghanistan      Asia  1982 12881816  978.0114
##  8 Afghanistan      Asia  1987 13867957  852.3959
##  9 Afghanistan      Asia  1992 16317921  649.3414
## 10 Afghanistan      Asia  1997 22227415  635.3414
## # ... with 1,694 more rows
```


4. Put `continent` first. Hint: use the `everything()` function.

```r
select(gapminder, continent, year, everything()) # everything preserves the order without 
```

```
## # A tibble: 1,704 x 6
##    continent  year     country lifeExp      pop gdpPercap
##       <fctr> <int>      <fctr>   <dbl>    <int>     <dbl>
##  1      Asia  1952 Afghanistan  28.801  8425333  779.4453
##  2      Asia  1957 Afghanistan  30.332  9240934  820.8530
##  3      Asia  1962 Afghanistan  31.997 10267083  853.1007
##  4      Asia  1967 Afghanistan  34.020 11537966  836.1971
##  5      Asia  1972 Afghanistan  36.088 13079460  739.9811
##  6      Asia  1977 Afghanistan  38.438 14880372  786.1134
##  7      Asia  1982 Afghanistan  39.854 12881816  978.0114
##  8      Asia  1987 Afghanistan  40.822 13867957  852.3959
##  9      Asia  1992 Afghanistan  41.674 16317921  649.3414
## 10      Asia  1997 Afghanistan  41.763 22227415  635.3414
## # ... with 1,694 more rows
```

5. Rename `continent` to `cont`.

```r
rename(gapminder, cont=continent)
```

```
## # A tibble: 1,704 x 6
##        country   cont  year lifeExp      pop gdpPercap
##         <fctr> <fctr> <int>   <dbl>    <int>     <dbl>
##  1 Afghanistan   Asia  1952  28.801  8425333  779.4453
##  2 Afghanistan   Asia  1957  30.332  9240934  820.8530
##  3 Afghanistan   Asia  1962  31.997 10267083  853.1007
##  4 Afghanistan   Asia  1967  34.020 11537966  836.1971
##  5 Afghanistan   Asia  1972  36.088 13079460  739.9811
##  6 Afghanistan   Asia  1977  38.438 14880372  786.1134
##  7 Afghanistan   Asia  1982  39.854 12881816  978.0114
##  8 Afghanistan   Asia  1987  40.822 13867957  852.3959
##  9 Afghanistan   Asia  1992  41.674 16317921  649.3414
## 10 Afghanistan   Asia  1997  41.763 22227415  635.3414
## # ... with 1,694 more rows
```

## `arrange()`

1. Order by year.

```r
arrange(gapminder, year)
```

```
## Warning: package 'bindrcpp' was built under R version 3.3.2
```

```
## # A tibble: 1,704 x 6
##        country continent  year lifeExp      pop  gdpPercap
##         <fctr>    <fctr> <int>   <dbl>    <int>      <dbl>
##  1 Afghanistan      Asia  1952  28.801  8425333   779.4453
##  2     Albania    Europe  1952  55.230  1282697  1601.0561
##  3     Algeria    Africa  1952  43.077  9279525  2449.0082
##  4      Angola    Africa  1952  30.015  4232095  3520.6103
##  5   Argentina  Americas  1952  62.485 17876956  5911.3151
##  6   Australia   Oceania  1952  69.120  8691212 10039.5956
##  7     Austria    Europe  1952  66.800  6927772  6137.0765
##  8     Bahrain      Asia  1952  50.939   120447  9867.0848
##  9  Bangladesh      Asia  1952  37.484 46886859   684.2442
## 10     Belgium    Europe  1952  68.000  8730405  8343.1051
## # ... with 1,694 more rows
```

2. Order by year, in descending order.

```r
arrange(gapminder, desc(lifeExp)) # desc is used for descending order
```

```
## # A tibble: 1,704 x 6
##             country continent  year lifeExp       pop gdpPercap
##              <fctr>    <fctr> <int>   <dbl>     <int>     <dbl>
##  1            Japan      Asia  2007  82.603 127467972  31656.07
##  2 Hong Kong, China      Asia  2007  82.208   6980412  39724.98
##  3            Japan      Asia  2002  82.000 127065841  28604.59
##  4          Iceland    Europe  2007  81.757    301931  36180.79
##  5      Switzerland    Europe  2007  81.701   7554661  37506.42
##  6 Hong Kong, China      Asia  2002  81.495   6762476  30209.02
##  7        Australia   Oceania  2007  81.235  20434176  34435.37
##  8            Spain    Europe  2007  80.941  40448191  28821.06
##  9           Sweden    Europe  2007  80.884   9031088  33859.75
## 10           Israel      Asia  2007  80.745   6426679  25523.28
## # ... with 1,694 more rows
```

3. Order by year, then by life expectancy.

```r
arrange(gapminder, year, lifeExp)
```

```
## # A tibble: 1,704 x 6
##          country continent  year lifeExp     pop gdpPercap
##           <fctr>    <fctr> <int>   <dbl>   <int>     <dbl>
##  1   Afghanistan      Asia  1952  28.801 8425333  779.4453
##  2        Gambia    Africa  1952  30.000  284320  485.2307
##  3        Angola    Africa  1952  30.015 4232095 3520.6103
##  4  Sierra Leone    Africa  1952  30.331 2143249  879.7877
##  5    Mozambique    Africa  1952  31.286 6446316  468.5260
##  6  Burkina Faso    Africa  1952  31.975 4469979  543.2552
##  7 Guinea-Bissau    Africa  1952  32.500  580653  299.8503
##  8   Yemen, Rep.      Asia  1952  32.548 4963829  781.7176
##  9       Somalia    Africa  1952  32.978 2526994 1135.7498
## 10        Guinea    Africa  1952  33.609 2664249  510.1965
## # ... with 1,694 more rows
```

## Piping, `%>%`

Note: think of `%>%` as the word "then"!

1. Combine `select()` Task 1 with `arrange()` Task 3.

select 1. Make a data frame containing the columns `year`, `lifeExp`, `country` from the gapminder data, in that order.
arrange 3. Order by year, then by life expectancy.


```r
gapminder %>% 
  select(year, lifeExp, country) %>% 
  arrange(year, lifeExp)
```

```
## # A tibble: 1,704 x 3
##     year lifeExp       country
##    <int>   <dbl>        <fctr>
##  1  1952  28.801   Afghanistan
##  2  1952  30.000        Gambia
##  3  1952  30.015        Angola
##  4  1952  30.331  Sierra Leone
##  5  1952  31.286    Mozambique
##  6  1952  31.975  Burkina Faso
##  7  1952  32.500 Guinea-Bissau
##  8  1952  32.548   Yemen, Rep.
##  9  1952  32.978       Somalia
## 10  1952  33.609        Guinea
## # ... with 1,694 more rows
```

How to pipe input in a differnt variable
dat %>%  f(a=3, b=.)
Now the value will go into b


```r
gapminder %>%
  filter(pop > 100000000)
```

```
## # A tibble: 77 x 6
##       country continent  year lifeExp       pop gdpPercap
##        <fctr>    <fctr> <int>   <dbl>     <int>     <dbl>
##  1 Bangladesh      Asia  1987  52.819 103764241  751.9794
##  2 Bangladesh      Asia  1992  56.018 113704579  837.8102
##  3 Bangladesh      Asia  1997  59.412 123315288  972.7700
##  4 Bangladesh      Asia  2002  62.013 135656790 1136.3904
##  5 Bangladesh      Asia  2007  64.062 150448339 1391.2538
##  6     Brazil  Americas  1972  59.504 100840058 4985.7115
##  7     Brazil  Americas  1977  61.489 114313951 6660.1187
##  8     Brazil  Americas  1982  63.336 128962939 7030.8359
##  9     Brazil  Americas  1987  65.205 142938076 7807.0958
## 10     Brazil  Americas  1992  67.057 155975974 6950.2830
## # ... with 67 more rows
```

## `filter()`

1. Only take data with population greater than 100 million.

2. Of those, only take data from Asia.

## git stuff (Optional)

Knit, commit, push!

# Break/Challenge: metaprogramming

Here's an activity for you to do during the break, in case you're all caught up. It should help you understand metaprogramming a bit more.

Suppose you're the instructor of an R programming course. You write an assignment question to evaluate whether students can write an `if` statement, for which an answer to the question looks something like this:

```
my_commute <- 60
if (my_commute > 30) {
    print("That's a long commute!")
} else {
    print("That's a short commute.")
}
```

Your task is to use metaprogramming to check whether a response (like the one above) works and contains an `if` statement. You should roughly follow these steps, using [adv-r: expressions](https://adv-r.hadley.nz/expressions.html) as a resource (especially Section 18.1).

1. Wrap the above block of code in the `expr()` function from the `rlang` package.
2. Use the `eval()` function to execute the code, to see if the code runs.
3. Use the `as.character()` function to check whether this response contains an `if` statement.

# Relational/Comparison and Logical Operators in R

1. Find all entries of Canada and Algeria occuring in the '60s. 

2. Find all entries of Canada, and entries of Algeria occuring in the '60s. 
3. Find all entries _not_ including Canada and Algeria.

# Bonus Exercises

If there's time remaining, we'll practice with these three exercises. I'll give you 1 minute for each, then we'll go over the answer.

1. Take all countries in Europe that have a GDP per capita greater than 10000, and select all variables except `gdpPercap`. (Hint: use `-`).

2. Take the first three columns, and extract the names.

3. Of the `iris` data frame, take all columns that start with the word "Petal". 
    - Hint: take a look at the "Select helpers" documentation by running the following code: `?tidyselect::select_helpers`.
    - Exercise from [r-exercises](https://www.r-exercises.com/2017/10/19/dplyr-basic-functions-exercises/).
