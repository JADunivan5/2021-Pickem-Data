Pickem Charts
================

``` r
library(tidyverse)
library(moderndive)
library(janitor)
```

``` r
Pickem <- read_csv(here::here("2021- Pickem League Wins.csv")) %>% 
  clean_names() %>% 
  select(-'x15':-'x27')
```

``` r
Chris <- Pickem %>% 
  summarise(chris,user)
Jake <- Pickem %>% 
  summarise(jake,user)

ggplot() + geom_point(data=Chris,aes(x=chris, y=user), colour='red') + geom_point(alpha=.5) + geom_point(data=Jake, aes(x=jake, y=user), colour= 'blue') + geom_point(alpha=.5)
```

![](Pickem_files/figure-gfm/Comparison%20of%20Chris%20Vs%20Jake-1.png)<!-- -->

``` r
 Mean_WK <-Pickem %>% 
 rowwise() %>% 
  mutate(m=mean(c_across(2:12)))
```

``` r
jack <- Pickem %>% 
  summarise(jack,user)
matt <- Pickem %>% 
  summarise(matt,user)

BvM <- ggplot() + geom_point(data=jack,aes(x=jack, y=user), colour='red') + geom_point(alpha=.5) + geom_point(data=matt, aes(x=matt, y=user), colour= 'blue') + geom_point(alpha=.5)

BvM + scale_x_continuous(name="Bohr Vs Stase", breaks =c(0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16))
```

![](Pickem_files/figure-gfm/Bohr%20vs%20Stase-1.png)<!-- -->
