---
title: "Lab 1 Homework"
author: "Stephanie Tsai"
date: "Winter 2019"
output:
  html_document:
    keep_md: yes
    theme: spacelab
---
#Arithmatic

```r
(5 - 3) * 2
```

```
## [1] 4
```

```r
(8/2) **2
```

```
## [1] 16
```

##Gambler Problems

3. You have decided to use your new analytical powers in R to become a professional gambler. Here are your winnings and losses this week.
a. Build a new vector called `days` for the days of the week (Monday through Friday). 


```r
blackjack <- c(140, -20, 70, -120, 240)
roulette <- c(60, 50, 120, -300, 10)
days <- c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday")
```

##Assign days to data to label
We will use `days` to name the elements in the poker and roulette vectors.

```r
#Apply names of days to blackjack and roulette
names(blackjack) <- days
names(roulette) <- days
```

##Calculating Sums
b. Calculate how much you won or lost in blackjack over the week.

```r
total_blackjack <- sum(blackjack)
total_blackjack #prints blackjack total
```

```
## [1] 310
```


```r
total_roulette <- sum(roulette)
  total_roulette
```

```
## [1] -60
```

#Total week
Build a `total_week` vector to show how much you lost or won on each day over the week. Which days seem lucky or unlucky for you?

```r
total_week <- blackjack + roulette
  total_week
```

```
##    Monday   Tuesday Wednesday  Thursday    Friday 
##       200        30       190      -420       250
```

```r
#Friday seems lucky and Thursday seems unlucky
```


#Choose blackjack or roulette
e. Should you stick to blackjack or roulette? Write a program that verifies this below.

```r
#Establish possible outcomes
winner_blackjack <- total_blackjack > total_roulette
winner_roulette <- total_roulette > total_blackjack


#Returns True or False
winner_blackjack
```

```
## [1] TRUE
```

```r
winner_roulette
```

```
## [1] FALSE
```

