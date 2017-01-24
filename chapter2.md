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
    + `payoff`
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
  mutate(payoff = call_payoff(S = asset_price))


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
  mutate(payoff = call_payoff(S = asset_price))


# use glimpse to view the structure of DF
glimpse(DF)
```

*** =sct
```{r}
test_error()
test_object("call_payoff",
            undefined_msg = "Make sure to define `call_payoff()`",
            incorrect_msg = "Your definition of `call_payoff()` has a problem")
test_object("DF",
            undefined_msg = "Make sure to define the dataframe `DF`",
            incorrect_msg = "Your definition of `DF` has a problem")
 

success_msg("Now that we have a data frame with the values we want, e can proceed to create a plot")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:9b594565ad

## European Call Option (part 2: initializing a ggplot object)

In this exercise you will only set up the ggplot object for the plot we want to create. 



*** =instructions
* `DF` is already loaded
* Use `ls()` to verify this
* Use `glimpse()` to review the structure of `DF`
* Create `ggcall` <- `ggplot(DF, aes(x = asset_price, y = payoff))`

*** =hint
# Use ls() to verifu that `DF` is loaded
ls()

# Use glimpse() to review the stucture of `DF`
glimpse(DF)

# create gg_call
gg_call <- ggplot(data = DF, aes(x = asset_price, y = payoff)) 

*** =pre_exercise_code
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
  mutate(payoff = call_payoff(S = asset_price))
```

*** =sample_code
```{r}
# Use ls() to verify that `DF` is loaded


# Use glimpse() to review the stucture of `DF`


# create ggcall


```

*** =solution
```{r}
# Use ls() to verify that `DF` is loaded
ls()

# Use glimpse() to review the stucture of `DF`
glimpse(DF)

# create ggcall
ggcall <- ggplot(data = DF, aes(x = asset_price, y = payoff)) 

# type ggcall and see what happens
ggcall
```

*** =sct
```{r}
test_error()
test_object("ggcall",
            undefined_msg = "Make sure to define `ggcall`")
test_output_contains("ggcall")
success_msg("Good now with gg_call we can start adding geoms")
```
