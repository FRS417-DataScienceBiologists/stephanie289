---
title: "lab3_hw"
author: "Stephanie Tsai"
date: "February 1, 2019"
output: 
  html_document: 
    keep_md: yes
---

```r
library(tidyverse)
```

```
## -- Attaching packages ------------------------------------------------------------------------------------------- tidyverse 1.2.1 --
```

```
## v ggplot2 3.1.0     v purrr   0.2.5
## v tibble  1.4.2     v dplyr   0.7.8
## v tidyr   0.8.2     v stringr 1.3.1
## v readr   1.3.1     v forcats 0.3.0
```

```
## -- Conflicts ---------------------------------------------------------------------------------------------- tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```


```r
getwd()
```

```
## [1] "C:/Users/Stephanie T/Desktop/FRS_417/stephanie289"
```

##Loading the data

```r
fisheries <- readr::read_csv(file = "C:/Users/Stephanie T/Desktop/class_files-master/class_files-master/FAO_1950to2012_111914.csv") 
```

```
## Warning: Duplicated column names deduplicated: 'Species (ISSCAAP group)'
## => 'Species (ISSCAAP group)_1' [4], 'Species (ASFIS species)' => 'Species
## (ASFIS species)_1' [5], 'Species (ASFIS species)' => 'Species (ASFIS
## species)_2' [6]
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   `Species (ISSCAAP group)` = col_double(),
##   `Fishing area (FAO major fishing area)` = col_double()
## )
```

```
## See spec(...) for full column specifications.
```

1. Do you see any potential problems with the column names? Does the error message now make more sense?  
*Column names are duplicated so R manipulated them to unique names*

```r
#Column names that are the same risk being considered the same even when the data is supposed to be different. R is trying to fix this by relabeling them as an unique, separate column.
```
# Viewing available data

```r
glimpse(fisheries)
```

```
## Observations: 17,692
## Variables: 71
## $ `Country (Country)`                     <chr> "Albania", "Albania", ...
## $ `Species (ASFIS species)`               <chr> "Angelsharks, sand dev...
## $ `Species (ISSCAAP group)`               <dbl> 38, 36, 37, 45, 32, 37...
## $ `Species (ISSCAAP group)_1`             <chr> "Sharks, rays, chimaer...
## $ `Species (ASFIS species)_1`             <chr> "10903XXXXX", "1750100...
## $ `Species (ASFIS species)_2`             <chr> "Squatinidae", "Sarda ...
## $ `Fishing area (FAO major fishing area)` <dbl> 37, 37, 37, 37, 37, 37...
## $ `Measure (Measure)`                     <chr> "Quantity (tonnes)", "...
## $ `1950`                                  <chr> "...", "...", "...", "...
## $ `1951`                                  <chr> "...", "...", "...", "...
## $ `1952`                                  <chr> "...", "...", "...", "...
## $ `1953`                                  <chr> "...", "...", "...", "...
## $ `1954`                                  <chr> "...", "...", "...", "...
## $ `1955`                                  <chr> "...", "...", "...", "...
## $ `1956`                                  <chr> "...", "...", "...", "...
## $ `1957`                                  <chr> "...", "...", "...", "...
## $ `1958`                                  <chr> "...", "...", "...", "...
## $ `1959`                                  <chr> "...", "...", "...", "...
## $ `1960`                                  <chr> "...", "...", "...", "...
## $ `1961`                                  <chr> "...", "...", "...", "...
## $ `1962`                                  <chr> "...", "...", "...", "...
## $ `1963`                                  <chr> "...", "...", "...", "...
## $ `1964`                                  <chr> "...", "...", "...", "...
## $ `1965`                                  <chr> "...", "...", "...", "...
## $ `1966`                                  <chr> "...", "...", "...", "...
## $ `1967`                                  <chr> "...", "...", "...", "...
## $ `1968`                                  <chr> "...", "...", "...", "...
## $ `1969`                                  <chr> "...", "...", "...", "...
## $ `1970`                                  <chr> "...", "...", "...", "...
## $ `1971`                                  <chr> "...", "...", "...", "...
## $ `1972`                                  <chr> "...", "...", "...", "...
## $ `1973`                                  <chr> "...", "...", "...", "...
## $ `1974`                                  <chr> "...", "...", "...", "...
## $ `1975`                                  <chr> "...", "...", "...", "...
## $ `1976`                                  <chr> "...", "...", "...", "...
## $ `1977`                                  <chr> "...", "...", "...", "...
## $ `1978`                                  <chr> "...", "...", "...", "...
## $ `1979`                                  <chr> "...", "...", "...", "...
## $ `1980`                                  <chr> "...", "...", "...", "...
## $ `1981`                                  <chr> "...", "...", "...", "...
## $ `1982`                                  <chr> "...", "...", "...", "...
## $ `1983`                                  <chr> "...", "...", "...", "...
## $ `1984`                                  <chr> "...", "...", "...", "...
## $ `1985`                                  <chr> "...", "...", "...", "...
## $ `1986`                                  <chr> "...", "...", "...", "...
## $ `1987`                                  <chr> "...", "...", "...", "...
## $ `1988`                                  <chr> "...", "...", "...", "...
## $ `1989`                                  <chr> "...", "...", "...", "...
## $ `1990`                                  <chr> "...", "...", "...", "...
## $ `1991`                                  <chr> "...", "...", "...", "...
## $ `1992`                                  <chr> "...", "...", "...", "...
## $ `1993`                                  <chr> "...", "...", "...", "...
## $ `1994`                                  <chr> "...", "...", "...", "...
## $ `1995`                                  <chr> "0 0", "1", "...", "0 ...
## $ `1996`                                  <chr> "53", "2", "...", "3",...
## $ `1997`                                  <chr> "20", "0 0", "...", "0...
## $ `1998`                                  <chr> "31", "12", "...", "-"...
## $ `1999`                                  <chr> "30", "30", "...", "-"...
## $ `2000`                                  <chr> "30", "25", "2", "-", ...
## $ `2001`                                  <chr> "16", "30", "...", "-"...
## $ `2002`                                  <chr> "79", "24", "...", "34...
## $ `2003`                                  <chr> "1", "4", "...", "22",...
## $ `2004`                                  <chr> "4", "2", "2", "15", "...
## $ `2005`                                  <chr> "68", "23", "4", "12",...
## $ `2006`                                  <chr> "55", "30", "7", "18",...
## $ `2007`                                  <chr> "12", "19", "...", ".....
## $ `2008`                                  <chr> "23", "27", "...", ".....
## $ `2009`                                  <chr> "14", "21", "...", ".....
## $ `2010`                                  <chr> "78", "23", "7", "..."...
## $ `2011`                                  <chr> "12", "12", "...", ".....
## $ `2012`                                  <chr> "5", "5", "...", "..."...
```
## Viewing data and Renaming
2. The `make.names()` command is helpful when there are issues with column names. Notice that although the names are still cumbersome, much of the problemtatic syntax is removed.

```r
names(fisheries) = make.names(names(fisheries), unique=T) #changes the column names
names(fisheries)
```

```
##  [1] "Country..Country."                    
##  [2] "Species..ASFIS.species."              
##  [3] "Species..ISSCAAP.group."              
##  [4] "Species..ISSCAAP.group._1"            
##  [5] "Species..ASFIS.species._1"            
##  [6] "Species..ASFIS.species._2"            
##  [7] "Fishing.area..FAO.major.fishing.area."
##  [8] "Measure..Measure."                    
##  [9] "X1950"                                
## [10] "X1951"                                
## [11] "X1952"                                
## [12] "X1953"                                
## [13] "X1954"                                
## [14] "X1955"                                
## [15] "X1956"                                
## [16] "X1957"                                
## [17] "X1958"                                
## [18] "X1959"                                
## [19] "X1960"                                
## [20] "X1961"                                
## [21] "X1962"                                
## [22] "X1963"                                
## [23] "X1964"                                
## [24] "X1965"                                
## [25] "X1966"                                
## [26] "X1967"                                
## [27] "X1968"                                
## [28] "X1969"                                
## [29] "X1970"                                
## [30] "X1971"                                
## [31] "X1972"                                
## [32] "X1973"                                
## [33] "X1974"                                
## [34] "X1975"                                
## [35] "X1976"                                
## [36] "X1977"                                
## [37] "X1978"                                
## [38] "X1979"                                
## [39] "X1980"                                
## [40] "X1981"                                
## [41] "X1982"                                
## [42] "X1983"                                
## [43] "X1984"                                
## [44] "X1985"                                
## [45] "X1986"                                
## [46] "X1987"                                
## [47] "X1988"                                
## [48] "X1989"                                
## [49] "X1990"                                
## [50] "X1991"                                
## [51] "X1992"                                
## [52] "X1993"                                
## [53] "X1994"                                
## [54] "X1995"                                
## [55] "X1996"                                
## [56] "X1997"                                
## [57] "X1998"                                
## [58] "X1999"                                
## [59] "X2000"                                
## [60] "X2001"                                
## [61] "X2002"                                
## [62] "X2003"                                
## [63] "X2004"                                
## [64] "X2005"                                
## [65] "X2006"                                
## [66] "X2007"                                
## [67] "X2008"                                
## [68] "X2009"                                
## [69] "X2010"                                
## [70] "X2011"                                
## [71] "X2012"
```

```r
#using make.names() takes the fisheries columns and check if the name is unique and an acceptable name. If not, R will change it to an accepted notation.

#In this case, R changed numeric dates into characters leading with X and removed paranthesis
```


3. Let's rename the columns. Use `rename()` to adjust the names as follows. Double check to make sure the rename worked correctly. Make sure to replace the old fisheries object with a new one so you can keep the column names.
+ country     = Country..Country.  
+ commname    = Species..ASFIS.species.  
+ sciname     = Species..ASFIS.species._2  
+ spcode      = Species..ASFIS.species._1  
+ spgroup     = Species..ISSCAAP.group.  
+ spgroupname = Species..ISSCAAP.group._1  
+ region      = Fishing.area..FAO.major.fishing.area.  
+ unit        = Measure..Measure.  


```r
fisheries_2 <- fisheries %>%
  dplyr::rename(
     country     = Country..Country. , 
 commname    = Species..ASFIS.species.  ,
 sciname     = Species..ASFIS.species._2  ,
 spcode      = Species..ASFIS.species._1  ,
 spgroup     = Species..ISSCAAP.group.  ,
 spgroupname = Species..ISSCAAP.group._1 , 
 region      = Fishing.area..FAO.major.fishing.area.  ,
 unit        = Measure..Measure.
  )

fisheries_2
```

```
## # A tibble: 17,692 x 71
##    country commname spgroup spgroupname spcode sciname region unit  X1950
##    <chr>   <chr>      <dbl> <chr>       <chr>  <chr>    <dbl> <chr> <chr>
##  1 Albania Angelsh~      38 Sharks, ra~ 10903~ Squati~     37 Quan~ ...  
##  2 Albania Atlanti~      36 Tunas, bon~ 17501~ Sarda ~     37 Quan~ ...  
##  3 Albania Barracu~      37 Miscellane~ 17710~ Sphyra~     37 Quan~ ...  
##  4 Albania Blue an~      45 Shrimps, p~ 22802~ Ariste~     37 Quan~ ...  
##  5 Albania Blue wh~      32 Cods, hake~ 14804~ Microm~     37 Quan~ ...  
##  6 Albania Bluefish      37 Miscellane~ 17020~ Pomato~     37 Quan~ ...  
##  7 Albania Bogue         33 Miscellane~ 17039~ Boops ~     37 Quan~ ...  
##  8 Albania Caramot~      45 Shrimps, p~ 22801~ Penaeu~     37 Quan~ ...  
##  9 Albania Catshar~      38 Sharks, ra~ 10801~ Scylio~     37 Quan~ ...  
## 10 Albania Common ~      57 Squids, cu~ 32102~ Sepia ~     37 Quan~ ...  
## # ... with 17,682 more rows, and 62 more variables: X1951 <chr>,
## #   X1952 <chr>, X1953 <chr>, X1954 <chr>, X1955 <chr>, X1956 <chr>,
## #   X1957 <chr>, X1958 <chr>, X1959 <chr>, X1960 <chr>, X1961 <chr>,
## #   X1962 <chr>, X1963 <chr>, X1964 <chr>, X1965 <chr>, X1966 <chr>,
## #   X1967 <chr>, X1968 <chr>, X1969 <chr>, X1970 <chr>, X1971 <chr>,
## #   X1972 <chr>, X1973 <chr>, X1974 <chr>, X1975 <chr>, X1976 <chr>,
## #   X1977 <chr>, X1978 <chr>, X1979 <chr>, X1980 <chr>, X1981 <chr>,
## #   X1982 <chr>, X1983 <chr>, X1984 <chr>, X1985 <chr>, X1986 <chr>,
## #   X1987 <chr>, X1988 <chr>, X1989 <chr>, X1990 <chr>, X1991 <chr>,
## #   X1992 <chr>, X1993 <chr>, X1994 <chr>, X1995 <chr>, X1996 <chr>,
## #   X1997 <chr>, X1998 <chr>, X1999 <chr>, X2000 <chr>, X2001 <chr>,
## #   X2002 <chr>, X2003 <chr>, X2004 <chr>, X2005 <chr>, X2006 <chr>,
## #   X2007 <chr>, X2008 <chr>, X2009 <chr>, X2010 <chr>, X2011 <chr>,
## #   X2012 <chr>
```

## Evaluating Tidyness
4. Are these data tidy? Why or why not, and, how do you know?


```r
# The data is organized in a way that makes sense to a person looking at it, but not for R. All the data points will still be read as vectors rather than being specifically grouped to match with its appropriate label. Each year variable does not have a defined observation linked to it, so the numbers associated to year will be read columnarly by R.
```




## Tidy data with gather()

5. We need to tidy the data using `gather()`. The code below will not run because it is commented (#) out. I have added a bit of code that will prevent you from needing to type in each year from 1950-2012 but you need to complete the remainder `QQQ` and remove the `#`.

```r
fisheries_tidy <- 
  fisheries_2 %>% 
  gather(num_range('X',1950:2012), key= "year", value= "catch")

fisheries_tidy
```

```
## # A tibble: 1,114,596 x 10
##    country commname spgroup spgroupname spcode sciname region unit  year 
##    <chr>   <chr>      <dbl> <chr>       <chr>  <chr>    <dbl> <chr> <chr>
##  1 Albania Angelsh~      38 Sharks, ra~ 10903~ Squati~     37 Quan~ X1950
##  2 Albania Atlanti~      36 Tunas, bon~ 17501~ Sarda ~     37 Quan~ X1950
##  3 Albania Barracu~      37 Miscellane~ 17710~ Sphyra~     37 Quan~ X1950
##  4 Albania Blue an~      45 Shrimps, p~ 22802~ Ariste~     37 Quan~ X1950
##  5 Albania Blue wh~      32 Cods, hake~ 14804~ Microm~     37 Quan~ X1950
##  6 Albania Bluefish      37 Miscellane~ 17020~ Pomato~     37 Quan~ X1950
##  7 Albania Bogue         33 Miscellane~ 17039~ Boops ~     37 Quan~ X1950
##  8 Albania Caramot~      45 Shrimps, p~ 22801~ Penaeu~     37 Quan~ X1950
##  9 Albania Catshar~      38 Sharks, ra~ 10801~ Scylio~     37 Quan~ X1950
## 10 Albania Common ~      57 Squids, cu~ 32102~ Sepia ~     37 Quan~ X1950
## # ... with 1,114,586 more rows, and 1 more variable: catch <chr>
```

6. Use `glimpse()` to look at the categories of the variables. Pay particular attention to `year` and `catch`. What do you notice?  


```r
glimpse(fisheries_tidy)
```

```
## Observations: 1,114,596
## Variables: 10
## $ country     <chr> "Albania", "Albania", "Albania", "Albania", "Alban...
## $ commname    <chr> "Angelsharks, sand devils nei", "Atlantic bonito",...
## $ spgroup     <dbl> 38, 36, 37, 45, 32, 37, 33, 45, 38, 57, 33, 57, 31...
## $ spgroupname <chr> "Sharks, rays, chimaeras", "Tunas, bonitos, billfi...
## $ spcode      <chr> "10903XXXXX", "1750100101", "17710001XX", "2280203...
## $ sciname     <chr> "Squatinidae", "Sarda sarda", "Sphyraena spp", "Ar...
## $ region      <dbl> 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, 37...
## $ unit        <chr> "Quantity (tonnes)", "Quantity (tonnes)", "Quantit...
## $ year        <chr> "X1950", "X1950", "X1950", "X1950", "X1950", "X195...
## $ catch       <chr> "...", "...", "...", "...", "...", "...", "...", "...
```


```r
# The year and catch are represented by characters. We would expect them to be numbers. The catch variable has a lot of missing data.
```



7. From question 6 you should see that there are a lot of entries that are missing. In R, these are referred to as NA's but they can be coded in different ways by the scientists in a given study. In order to make the data tidy, we need to deal with them. As a preview to our next lab, run the following code by removing the `#`. It removes the 'X' from the years and changes the `catch` column from a character into a numeric. This forces the blank entries to become NAs. The error "NAs introduced by coercion" indicates their replacement.

```r
fisheries_tidy <- 
  fisheries_tidy %>% 
  mutate(
    year= as.numeric(str_replace(year, 'X', '')), #remove the X from year
    catch= as.numeric(str_replace(catch, c(' F','...','-'), replacement = '')) #replace character strings with NA
    )
```

```
## Warning in evalq(as.numeric(str_replace(catch, c(" F", "...", "-"),
## replacement = "")), : NAs introduced by coercion
```

```r
fisheries_tidy
```

```
## # A tibble: 1,114,596 x 10
##    country commname spgroup spgroupname spcode sciname region unit   year
##    <chr>   <chr>      <dbl> <chr>       <chr>  <chr>    <dbl> <chr> <dbl>
##  1 Albania Angelsh~      38 Sharks, ra~ 10903~ Squati~     37 Quan~  1950
##  2 Albania Atlanti~      36 Tunas, bon~ 17501~ Sarda ~     37 Quan~  1950
##  3 Albania Barracu~      37 Miscellane~ 17710~ Sphyra~     37 Quan~  1950
##  4 Albania Blue an~      45 Shrimps, p~ 22802~ Ariste~     37 Quan~  1950
##  5 Albania Blue wh~      32 Cods, hake~ 14804~ Microm~     37 Quan~  1950
##  6 Albania Bluefish      37 Miscellane~ 17020~ Pomato~     37 Quan~  1950
##  7 Albania Bogue         33 Miscellane~ 17039~ Boops ~     37 Quan~  1950
##  8 Albania Caramot~      45 Shrimps, p~ 22801~ Penaeu~     37 Quan~  1950
##  9 Albania Catshar~      38 Sharks, ra~ 10801~ Scylio~     37 Quan~  1950
## 10 Albania Common ~      57 Squids, cu~ 32102~ Sepia ~     37 Quan~  1950
## # ... with 1,114,586 more rows, and 1 more variable: catch <dbl>
```

8. Are the data tidy? Why?  


```r
# The data is more tidy than before because now R knows that the year column contains numeric years and it is paired to the catch column as one variable to one data point.
```


9. You are a fisheries scientist studying cephalopod catch during 2008-2012. Identify the top five consumers (by country) of cephalopods (don't worry about species for now). Restrict the data frame only to our variables of interest.

##Restrict year to 2008-2012

```r
year_narrow <- fisheries_tidy %>%
  select(country, year, spgroupname,commname, catch) %>%
  filter(year > 2008 & year < 2012 | year == 2008 |year == 2012)

year_narrow
```

```
## # A tibble: 88,460 x 5
##    country  year spgroupname                 commname                 catch
##    <chr>   <dbl> <chr>                       <chr>                    <dbl>
##  1 Albania  2008 Sharks, rays, chimaeras     Angelsharks, sand devil~    23
##  2 Albania  2008 Tunas, bonitos, billfishes  Atlantic bonito             27
##  3 Albania  2008 Miscellaneous pelagic fish~ Barracudas nei              NA
##  4 Albania  2008 Shrimps, prawns             Blue and red shrimp         NA
##  5 Albania  2008 Cods, hakes, haddocks       Blue whiting(=Poutassou)    NA
##  6 Albania  2008 Miscellaneous pelagic fish~ Bluefish                    NA
##  7 Albania  2008 Miscellaneous coastal fish~ Bogue                       NA
##  8 Albania  2008 Shrimps, prawns             Caramote prawn              23
##  9 Albania  2008 Sharks, rays, chimaeras     Catsharks, nursehounds ~    NA
## 10 Albania  2008 Squids, cuttlefishes, octo~ Common cuttlefish           62
## # ... with 88,450 more rows
```

##Who consumes cephalopods?

```r
cephalopod_consumption <- year_narrow %>%
  filter(spgroupname == "Squids, cuttlefishes, octopuses") %>%
  filter(catch >= 1)
  
cephalopod_consumption
```

```
## # A tibble: 1,480 x 5
##    country        year spgroupname                  commname          catch
##    <chr>         <dbl> <chr>                        <chr>             <dbl>
##  1 Albania        2008 Squids, cuttlefishes, octop~ Common cuttlefish    62
##  2 Albania        2008 Squids, cuttlefishes, octop~ Common octopus       82
##  3 Albania        2008 Squids, cuttlefishes, octop~ Common squids nei   107
##  4 Algeria        2008 Squids, cuttlefishes, octop~ Cephalopods nei      29
##  5 Algeria        2008 Squids, cuttlefishes, octop~ Common cuttlefish   449
##  6 Algeria        2008 Squids, cuttlefishes, octop~ Common squids nei   236
##  7 Algeria        2008 Squids, cuttlefishes, octop~ Octopuses, etc. ~   895
##  8 American Sam~  2008 Squids, cuttlefishes, octop~ Octopuses, etc. ~     1
##  9 Angola         2008 Squids, cuttlefishes, octop~ Octopuses, etc. ~     6
## 10 Angola         2008 Squids, cuttlefishes, octop~ Various squids n~    65
## # ... with 1,470 more rows
```
##Gathering countries

```r
#Calculates based on the mean and max catch of cephalopods per country out of all their years

top_consumers <- cephalopod_consumption %>%
  group_by(country) %>%
  summarize(max_Catch = max(catch),
            mean_Catch = mean(catch)) %>%
  arrange(desc(mean_Catch)) #arranged by the average cephalopod catch

top_consumers
```

```
## # A tibble: 122 x 3
##    country                  max_Catch mean_Catch
##    <chr>                        <dbl>      <dbl>
##  1 Viet Nam                    260000    260000 
##  2 China                       462981    103090.
##  3 Peru                        533414     90453.
##  4 Chile                       200428     39719.
##  5 Japan                       242262     37861.
##  6 India                        82456     30827 
##  7 Argentina                    94984     21280.
##  8 Taiwan Province of China    208641     17936.
##  9 Indonesia                   116991     17373.
## 10 Philippines                  57223     12749.
## # ... with 112 more rows
```
##The top 5 consumers of cephalopods are Vietnam, China, Peru, Chile, and Japan.


10. Let's be more specific. Who consumes the most `Common cuttlefish`? Store this as a new object `cuttle`.


```r
cuttle <- year_narrow %>%
  filter(commname == "Common cuttlefish") %>%
  group_by(country) %>%
  summarize(max_Catch = max(catch),
            mean_Catch = mean(catch)) %>%
  arrange(desc(mean_Catch)) #arranged by the average cephalopod catch
  
cuttle
```

```
## # A tibble: 17 x 3
##    country         max_Catch mean_Catch
##    <chr>               <dbl>      <dbl>
##  1 Tunisia              7717     4585. 
##  2 France              13217     3626. 
##  3 Turkey               1502     1065. 
##  4 Spain                1685      971  
##  5 Portugal             2027      530. 
##  6 Albania               126      100. 
##  7 Croatia               169       93.2
##  8 Malta                  36       24.8
##  9 Slovenia               15       11.2
## 10 Channel Islands         7        4  
## 11 Algeria                NA       NA  
## 12 Belgium                NA       NA  
## 13 Cyprus                 NA       NA  
## 14 Greece                 NA       NA  
## 15 Israel                 NA       NA  
## 16 Libya                  NA       NA  
## 17 Netherlands            NA       NA
```

##Tunisia consumes the most Common Cuttlefish.

