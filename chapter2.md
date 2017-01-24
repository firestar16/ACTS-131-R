---
title       : Using ggplot2 for ACTS 121
description : This lab is about learning to use ggplot2 for graphics in ACTS 121
--- type:NormalExercise lang:r xp:100 skills:1 key:66550becfc
## European Call Option (part 1)

A European call option on stock index $S$ has strike price $K = 40$ and will expire at time $T$.  In this series of exercises you will learn how
to use ggplot2 to create an attractive graph of the option's payoff at expiration.  The graphs you learn to create can be included in your Rmarkdown files or power point presentation slides.  In part 1 of this series you will set up the payoff function and create a data frame that will be used for plotting.



*** =instructions
* Load the `dplyr` and `ggplot2` packages
* Define the option call option payoff function as `call_payoff()`
* `call_payoff()` should have two arguements:
    + $S$, the stock price at expiration
    + $K$, the strike price (default = 40)
* Create a dataframe DF with two columns
    + `asset_price`, stock prices from 0 to 80 by 5
    + `derivative_payoff`, `call_payoff(S= asset_price)`
* Use `glimpse` to review the structure of DF


*** =hint
```{r}
# Load the dplyr and ggplot2 packages
library(dplyr)
library(ggplot2)

# Define call_payoff
call_payoff <- 
  # compute a european call option payoff
  function(S,K = 40){
  (K <= S) * (S - K)}

# Create dataframe DF
DF <- data_frame(asset_price = seq(from = 0, to = 80, by = 5))

DF <- DF %>%
  mutate(derivative_payoff = call_payoff(S = asset_price))


# use glimpse to view the structure of DF
glimpse(DF)

*** =pre_exercise_code
```{r}


```

*** =sample_code
```{r}
# Load the dplyr and ggplot2 packages


# Define call_payoff


# Create dataframe DF


# use glimpse to view the structure of DF


```

*** =solution
```{r}
# Load the dplyr and ggplot2 packages
library(dplyr)
library(ggplot2)

# Define call_payoff
call_payoff <- 
  # compute a european call option payoff
  function(S,K = 40){
  (K <= S) * (S - K)}

# Create dataframe DF
DF <- data_frame(asset_price = seq(from = 0, to = 80, by = 5))

DF <- DF %>%
  mutate(derivative_payoff = call_payoff(S = asset_price))


# use glimpse to view the structure of DF
glimpse(DF)
```

*** =sct
```{r}

```
