---
title: "lab4_hw"
author: "Stephanie Tsai"
date: "February 8, 2019"
output: 
  html_document: 
    keep_md: yes
---


```r
library(tidyverse)
```

```
## -- Attaching packages ----------------------------------------------------------------- tidyverse 1.2.1 --
```

```
## v ggplot2 3.1.0     v purrr   0.3.0
## v tibble  2.0.1     v dplyr   0.7.8
## v tidyr   0.8.2     v stringr 1.3.1
## v readr   1.3.1     v forcats 0.3.0
```

```
## -- Conflicts -------------------------------------------------------------------- tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(skimr)
```



```r
life_history <- readr::read_csv("C:/Users/Stephanie T/Desktop/Master File/class_files-master/mammal_lifehistories_v2.csv")
```

```
## Parsed with column specification:
## cols(
##   order = col_character(),
##   family = col_character(),
##   Genus = col_character(),
##   species = col_character(),
##   mass = col_double(),
##   gestation = col_double(),
##   newborn = col_double(),
##   weaning = col_double(),
##   `wean mass` = col_double(),
##   AFR = col_double(),
##   `max. life` = col_double(),
##   `litter size` = col_double(),
##   `litters/year` = col_double()
## )
```

Rename some of the variables. Notice that I am replacing the old `life_history` data.

```r
life_histories <- 
  life_history %>% 
  rename( genus = Genus,
          wean_mass    = `wean mass`,
          max_life     = `max. life`,
          litter_size  = `litter size`,
          litters_yr   = `litters/year`
          )

life_histories
```

```
## # A tibble: 1,440 x 13
##    order family genus species   mass gestation newborn weaning wean_mass
##    <chr> <chr>  <chr> <chr>    <dbl>     <dbl>   <dbl>   <dbl>     <dbl>
##  1 Arti~ Antil~ Anti~ americ~ 4.54e4      8.13   3246.    3         8900
##  2 Arti~ Bovid~ Addax nasoma~ 1.82e5      9.39   5480     6.5       -999
##  3 Arti~ Bovid~ Aepy~ melamp~ 4.15e4      6.35   5093     5.63     15900
##  4 Arti~ Bovid~ Alce~ busela~ 1.50e5      7.9   10167.    6.5       -999
##  5 Arti~ Bovid~ Ammo~ clarkei 2.85e4      6.8    -999  -999         -999
##  6 Arti~ Bovid~ Ammo~ lervia  5.55e4      5.08   3810     4         -999
##  7 Arti~ Bovid~ Anti~ marsup~ 3.00e4      5.72   3910     4.04      -999
##  8 Arti~ Bovid~ Anti~ cervic~ 3.75e4      5.5    3846     2.13      -999
##  9 Arti~ Bovid~ Bison bison   4.98e5      8.93  20000    10.7     157500
## 10 Arti~ Bovid~ Bison bonasus 5.00e5      9.14  23000.    6.6       -999
## # ... with 1,430 more rows, and 4 more variables: AFR <dbl>,
## #   max_life <dbl>, litter_size <dbl>, litters_yr <dbl>
```

1. Explore the data using the method that you prefer. Below, I am using a new package called `skimr`. If you want to use this, make sure that it is installed.



```r
life_histories %>% 
  skimr::skim()
```

```
## Skim summary statistics
##  n obs: 1440 
##  n variables: 13 
## 
## -- Variable type:character -------------------------------------------------------------------------------
##  variable missing complete    n min max empty n_unique
##    family       0     1440 1440   6  15     0       96
##     genus       0     1440 1440   3  16     0      618
##     order       0     1440 1440   7  14     0       17
##   species       0     1440 1440   3  17     0     1191
## 
## -- Variable type:numeric ---------------------------------------------------------------------------------
##     variable missing complete    n      mean         sd   p0  p25     p50
##          AFR       0     1440 1440   -408.12     504.97 -999 -999    2.5 
##    gestation       0     1440 1440   -287.25     455.36 -999 -999    1.05
##  litter_size       0     1440 1440    -55.63     234.88 -999    1    2.27
##   litters_yr       0     1440 1440   -477.14     500.03 -999 -999    0.38
##         mass       0     1440 1440 383576.72 5055162.92 -999   50  403.02
##     max_life       0     1440 1440   -490.26     615.3  -999 -999 -999   
##      newborn       0     1440 1440   6703.15   90912.52 -999 -999    2.65
##    wean_mass       0     1440 1440  16048.93   5e+05    -999 -999 -999   
##      weaning       0     1440 1440   -427.17     496.71 -999 -999    0.73
##      p75          p100     hist
##    15.61     210       <U+2586><U+2581><U+2581><U+2581><U+2581><U+2581><U+2587><U+2581>
##     4.5       21.46    <U+2583><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2587>
##     3.83      14.18    <U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2587>
##     1.15       7.5     <U+2587><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2587>
##  7009.17       1.5e+08 <U+2587><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581>
##   147.25    1368       <U+2587><U+2581><U+2581><U+2583><U+2582><U+2581><U+2581><U+2581>
##    98    2250000       <U+2587><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581>
##    10          1.9e+07 <U+2587><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581>
##     2         48       <U+2586><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2587>
```

2. Run the code below. Are there any NA's in the data? Does this seem likely?

```r
life_histories %>% 
  summarize(number_nas= sum(is.na(life_history)))
```

```
## # A tibble: 1 x 1
##   number_nas
##        <int>
## 1          0
```

```r
#The summarize function states there are no NA data in the data frame, but this is highly unlikely because our previous code shows that there are -999 (usually indicates an NA from excel)
```



3. Are there any missing data (NA's) represented by different values? How much and where? In which variables do we have the most missing data? Can you think of a reason why so much data are missing in this variable?

```r
#Values used to represent NA: -999

# These values are in all the numeric data and integer data
```



```r
life_histories_na <- 
  life_histories %>%
  na_if("-999")

life_histories_na %>% 
  purrr::map_df(~ sum(is.na(.))) %>%
  gather(variable, value = "num_NA") %>%
  arrange(desc(num_NA))
```

```
## # A tibble: 13 x 2
##    variable    num_NA
##    <chr>        <int>
##  1 wean_mass     1039
##  2 max_life       841
##  3 litters_yr     689
##  4 weaning        619
##  5 AFR            607
##  6 newborn        595
##  7 gestation      418
##  8 mass            85
##  9 litter_size     84
## 10 order            0
## 11 family           0
## 12 genus            0
## 13 species          0
```

```r
# The variable with the most missing data is in wean_mass at 1039 NAs. It probably is difficult to determine exactly when an animal has entered the weaning phase, so not all animals could be weighed at the time.
```


4. Compared to the `msleep` data, we have better representation among taxa. Produce a summary that shows the number of observations by taxonomic order.

```r
taxa_summary <- life_histories_na %>% 
  group_by(order) %>% 
  summarize(n_total = n())

taxa_summary
```

```
## # A tibble: 17 x 2
##    order          n_total
##    <chr>            <int>
##  1 Artiodactyla       161
##  2 Carnivora          197
##  3 Cetacea             55
##  4 Dermoptera           2
##  5 Hyracoidea           4
##  6 Insectivora         91
##  7 Lagomorpha          42
##  8 Macroscelidea       10
##  9 Perissodactyla      15
## 10 Pholidota            7
## 11 Primates           156
## 12 Proboscidea          2
## 13 Rodentia           665
## 14 Scandentia           7
## 15 Sirenia              5
## 16 Tubulidentata        1
## 17 Xenarthra           20
```


5. Mammals have a range of life histories, including lifespan. Produce a summary of lifespan in years by order. Be sure to include the minimum, maximum, mean, standard deviation, and total n.

```r
#Adjustments to make: max lifespan to years from months
# Reference http://esapubs.org/archive/ecol/E084/093/
```
## Tidy data

```r
summary_life <- life_histories_na %>%
  mutate(yr_max_life = max_life/12) %>%
  group_by(order) %>%
  summarise(min_lifespan_yrs = min(yr_max_life, na.rm = TRUE),
   max_lifespan_yrs = max(yr_max_life, na.rm = TRUE),
   mean_lifespan_yrs = mean(yr_max_life, na.rm = TRUE),
   sd_lifespan_yrs = sd(yr_max_life, na.rm = TRUE),
   n_total = n()) 

summary_life
```

```
## # A tibble: 17 x 6
##    order min_lifespan_yrs max_lifespan_yrs mean_lifespan_y~ sd_lifespan_yrs
##    <chr>            <dbl>            <dbl>            <dbl>           <dbl>
##  1 Arti~             6.75            61               20.7            7.70 
##  2 Carn~             5               56               21.1            9.42 
##  3 Ceta~            13              114               48.8           27.7  
##  4 Derm~            17.5             17.5             17.5          NaN    
##  5 Hyra~            11               12.2             11.6            0.884
##  6 Inse~             1.17            13                3.85           2.90 
##  7 Lago~             6               18                9.02           3.85 
##  8 Macr~             3                8.75             5.69           2.39 
##  9 Peri~            21               50               35.5           10.2  
## 10 Phol~            20               20               20            NaN    
## 11 Prim~             8.83            60.5             25.7           11.0  
## 12 Prob~            70               80               75              7.07 
## 13 Rode~             1               35                6.99           5.30 
## 14 Scan~             2.67            12.4              8.86           5.38 
## 15 Sire~            12.5             73               43.2           30.3  
## 16 Tubu~            24               24               24            NaN    
## 17 Xena~             9               40               21.3            9.93 
## # ... with 1 more variable: n_total <int>
```




6. Let's look closely at gestation and newborns. Summarize the mean gestation, newborn mass, and weaning mass by order. Add a new column that shows mean gestation in years and sort in descending order.  

## Make initial summary chart

```r
#Note mass is by grams, gestation is by months
life_newBorns <- life_histories_na %>%
  select(order, gestation, newborn, wean_mass) %>%
  group_by(order) %>%
  summarise(mean_gestation_months = mean(gestation, na.rm = TRUE),
            mean_gestation_yrs = mean(gestation/12, na.rm = TRUE),
            mean_newborn_mass = mean(newborn, na.rm = TRUE),
            mean_weanmass = mean(wean_mass, na.rm = TRUE)) %>%
  arrange(desc(mean_gestation_yrs))

life_newBorns
```

```
## # A tibble: 17 x 5
##    order   mean_gestation_~ mean_gestation_~ mean_newborn_ma~ mean_weanmass
##    <chr>              <dbl>            <dbl>            <dbl>         <dbl>
##  1 Probos~            21.3            1.77           99523.        600000  
##  2 Periss~            13.0            1.09           27015.        382191. 
##  3 Cetacea            11.8            0.983         343077.       4796125  
##  4 Sirenia            10.8            0.9            22878.         67500  
##  5 Hyraco~             7.4            0.617            231.           500  
##  6 Artiod~             7.26           0.605           7082.         51025. 
##  7 Tubuli~             7.08           0.59            1734           6250  
##  8 Primat~             5.47           0.456            287.          2115. 
##  9 Xenart~             4.95           0.412            314.           420  
## 10 Carniv~             3.69           0.308           3657.         21020. 
## 11 Pholid~             3.63           0.302            276.          2006. 
## 12 Dermop~             2.75           0.229             35.9          NaN  
## 13 Macros~             1.91           0.159             24.5          104. 
## 14 Scande~             1.63           0.136             12.8          102. 
## 15 Rodent~             1.31           0.109             35.5          135. 
## 16 Lagomo~             1.18           0.0979            57.0          715. 
## 17 Insect~             1.15           0.0958             6.06          33.1
```

## Which group has the longest mean gestation? What is the common name for these mammals?
  Proboscidea has the longest mean gestation of about 1.77 years. Their common name is elephants.

## Wrap-up
Please review the learning goals and be sure to use the code here as a reference when completing the homework.

A) Work on making a repository for team data
B) Upload data
