Pickem Charts
================

``` r
library(tidyverse)
library(moderndive)
library(janitor)
library(corrr)
```

``` r
Pickem <- read_csv(here::here("2021- Pickem League Wins.csv")) %>% 
  clean_names()
```

``` r
Chris <- Pickem %>% 
  summarise(chris,week)
Jake <- Pickem %>% 
  summarise(jake,week)

ggplot() + geom_point(data=Chris,aes(x=chris, y=week), colour='red') + geom_point(alpha=.5) + geom_point(data=Jake, aes(x=jake, y=week), colour= 'blue') + geom_point(alpha=.5)
```

![](Pickem_files/figure-gfm/Comparison%20of%20Chris%20Vs%20Jake-1.png)<!-- -->

``` r
 Mean_WK <-Pickem %>% 
 rowwise() %>% 
  mutate(m=mean(c_across(2:12))) %>% 
  ungroup() %>% 
  summarise(m)
Mean_WK
```

    ## # A tibble: 18 × 1
    ##        m
    ##    <dbl>
    ##  1  7.64
    ##  2  7.73
    ##  3  7.82
    ##  4  8.55
    ##  5  8.64
    ##  6  6.64
    ##  7  6.91
    ##  8  6.73
    ##  9  6.73
    ## 10  5.45
    ## 11  6.82
    ## 12  6.82
    ## 13  6.45
    ## 14  7.82
    ## 15  6.45
    ## 16  7.36
    ## 17  6.27
    ## 18  6.36

``` r
jack <- Pickem %>% 
  summarise(jack,week)
matt <- Pickem %>% 
  summarise(matt,week)

BvM <- ggplot() + geom_point(data=jack,aes(x=jack, y=week), colour='red') + geom_point(alpha=.5) + geom_point(data=matt, aes(x=matt, y=week), colour= 'blue') + geom_point(alpha=.5)

BvM + scale_x_continuous(name="Bohr Vs Stase", breaks =c(0:16))
```

![](Pickem_files/figure-gfm/Bohr%20vs%20Stase-1.png)<!-- -->

``` r
 Corr_Mn <-Pickem %>% 
 rowwise() %>% 
  mutate(m=mean(c_across(2:12))) %>% select(2:13) %>% 
    correlate()
```

    ## Correlation computed with
    ## • Method: 'pearson'
    ## • Missing treated using: 'pairwise.complete.obs'

``` r
Corr_Mn
```

    ## # A tibble: 12 × 13
    ##    term      jack    jake     tim     mike   chris    matt  keegan      kev
    ##    <chr>    <dbl>   <dbl>   <dbl>    <dbl>   <dbl>   <dbl>   <dbl>    <dbl>
    ##  1 jack   NA       0.530   0.385   0.0990   0.0166  0.229   0.108   0.240  
    ##  2 jake    0.530  NA       0.139   0.237    0.196   0.427   0.122   0.0123 
    ##  3 tim     0.385   0.139  NA       0.338    0.425   0.126   0.0262  0.172  
    ##  4 mike    0.0990  0.237   0.338  NA        0.549   0.101  -0.408  -0.0106 
    ##  5 chris   0.0166  0.196   0.425   0.549   NA       0.318  -0.540   0.0590 
    ##  6 matt    0.229   0.427   0.126   0.101    0.318  NA      -0.140  -0.0458 
    ##  7 keegan  0.108   0.122   0.0262 -0.408   -0.540  -0.140  NA      -0.193  
    ##  8 kev     0.240   0.0123  0.172  -0.0106   0.0590 -0.0458 -0.193  NA      
    ##  9 andy   -0.0236 -0.0162 -0.300  -0.0938  -0.142  -0.382  -0.118   0.00697
    ## 10 miller -0.128  -0.170   0.0737  0.00116 -0.137  -0.163  -0.259   0.510  
    ## 11 pranav  0.246   0.597   0.123   0.433    0.305   0.530  -0.0636  0.0848 
    ## 12 haef    0.0698  0.0784  0.549   0.401    0.35    0.109  -0.176   0.171  
    ## # … with 4 more variables: andy <dbl>, miller <dbl>, pranav <dbl>, haef <dbl>
