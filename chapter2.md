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






--- type:NormalExercise lang:r xp:100 skills:1 key:fb5065fc71


## European Call Option (part 2: initializing a ggplot object)

In this exercise you will only set up the ggplot object for the plot we want to create. 



*** =instructions
* `DF` is already loaded
* Use `ls()` to verify this
* Use `glimpse()` to review the structure of `DF`
* Create `ggcall` <- `ggplot(DF, aes(x = asset_price, y = payoff))`

*** =hint

* `ls()`

* `glimpse(DF)`

* `gg_call` <- 

    `ggplot(data = DF, aes(x = asset_price, y = payoff))` 

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

success_msg("Good now with ggcall we can start adding geoms.  Notice that ggcall only sets up the axis, gridlines, etc.  If we want to add points, lines, or regions we need to add geoms to the ggplot object.")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:1ba590597c

## European Call Option (part 3: adding a points geom)

Lets add points to the ggplot object using `geom_point()`


*** =instructions
* load `dplyr` and `ggplot2`
* `ggcall` is  already defined
* add `geom_point()` to `ggcall` 
  + `col  = 'red'`
  + `pch  = 18,`
  + `size = 3`

*** =hint
- `library(dplyr)`
- `library(ggplot2)`

- `ggcall + `
    `geom_point(col  = 'red',`
               `pch  = 18,`
               `size = 3)`

*** =pre_exercise_code
```{r}
library(dplyr)
library(ggplot2)

call_payoff <- 
  # compute a european call option payoff
  function(S,K = 40){
  (K <= S) * (S - K)}


DF <- data_frame(asset_price = seq(from = 0, to = 80, by = 5))

DF <- DF %>%
  mutate(payoff = call_payoff(S = asset_price))

ggcall <- ggplot(data = DF, aes(x = asset_price, y = payoff)) 
```

*** =sample_code
```{r}
# load dplyr and ggplot2


# add points to ggcall using geom_point()


```

*** =solution
```{r}
# load dplyr and ggplot2
library(dplyr)
library(ggplot2)


# add points to ggcall using geom_point()
ggcall + 
  geom_point(col  = 'red',
             pch  = 18,
             size = 3)

```

*** =sct
```{r}
test_error()
success_msg("Good! Next we will connect the dots using `geom_line()`")
```




--- type:NormalExercise lang:r xp:100 skills:1 key:a08fdcf916
## Adding lines

Lets add points to the ggplot object using `geom_line()`. The R script on the right already contains the code from
the prvious exercise.  You can also see the plot that was generated.  In this exercise we will add a lines geom using 
`geom_line()`


*** =instructions
* review the code and graph on the right
* copy and paset the code where indicated 
* add `geom_line(col = 'red')`
* look at the new graph


*** =hint
* `ggcall + `
*  `geom_point(col  = 'red',`
*             `pch  = 18,`
*             `size = 3) +`
*  `geom_line(col = 'red')`

*** =pre_exercise_code
```{r}
library(dplyr)
library(ggplot2)

call_payoff <- 
  # compute a european call option payoff
  function(S,K = 40){
  (K <= S) * (S - K)}


DF <- data_frame(asset_price = seq(from = 0, to = 80, by = 5))

DF <- DF %>%
  mutate(payoff = call_payoff(S = asset_price))

ggcall <- ggplot(data = DF, aes(x = asset_price, y = payoff)) 

ggcall + 
  geom_point(col  = 'red',
             pch  = 18,
             size = 3)
```

*** =sample_code
```{r}
# Previous code

library(dplyr)
library(ggplot2)

call_payoff <- 
  # compute a european call option payoff
  function(S,K = 40){
  (K <= S) * (S - K)}


DF <- data_frame(asset_price = seq(from = 0, to = 80, by = 5))

DF <- DF %>%
  mutate(payoff = call_payoff(S = asset_price))

ggcall <- ggplot(data = DF, aes(x = asset_price, y = payoff)) 

# Copy the below here

ggcall + 
  geom_point(col  = 'red',
             pch  = 18,
             size = 3)
             
# Paste and add geom_line()

```

*** =solution
```{r}
# Previous code

library(dplyr)
library(ggplot2)

call_payoff <- 
  # compute a european call option payoff
  function(S,K = 40){
  (K <= S) * (S - K)}


DF <- data_frame(asset_price = seq(from = 0, to = 80, by = 5))

DF <- DF %>%
  mutate(payoff = call_payoff(S = asset_price))

ggcall <- ggplot(data = DF, aes(x = asset_price, y = payoff)) 

# Copy the below here

ggcall + 
  geom_point(col  = 'red',
             pch  = 18,
             size = 3)
             
# Paste and add geom_line()
ggcall + 
  geom_point(col  = 'red',
             pch  = 18,
             size = 3) +
  geom_line(col = 'red')
```

*** =sct
```{r}
test_error()
success_msg("Nice!, Now let's try to change the y limits of the graph")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:ff0e29e754
## Changing the Y- Axis Limits

The graph is starting to look better, but what if we want to change the $y$ axis limits to include values below 0?
You can use the `ylim()` function to achieve this 


*** =instructions
* the dplyr and ggplot2 packages are already loaded in your workspace
* the graph from the prvious exercise is shown on the right
* add a `ylim()` to make the graph symmetric about $y=0$

*** =hint
* `ggcall + `
*  `geom_point(col  = 'red',`
*             `pch  = 18,`
*             `size = 3) +`
*  `geom_line(col = 'red') +`
*  `ylim(-40, 40)`
*** =pre_exercise_code
```{r}
library(dplyr)
library(ggplot2)

call_payoff <- 
  # compute a european call option payoff
  function(S,K = 40){
  (K <= S) * (S - K)}


DF <- data_frame(asset_price = seq(from = 0, to = 80, by = 5))

DF <- DF %>%
  mutate(payoff = call_payoff(S = asset_price))

ggcall <- ggplot(data = DF, aes(x = asset_price, y = payoff)) 
ggcall + 
  geom_point(col  = 'red',
             pch  = 18,
             size = 3) +
  geom_line(col = 'red')
```

*** =sample_code
```{r}
# ggplot2 is already loaded

# previous exercise
ggcall + 
  geom_point(col  = 'red',
             pch  = 18,
             size = 3) +
  geom_line(col = 'red')
  
# copy, paste,  and add ylim() to make the graph symmetric about y = 0
```

*** =solution
```{r}
# ggplot2 is already loaded

# previous exercise
ggcall + 
  geom_point(col  = 'red',
             pch  = 18,
             size = 3) +
  geom_line(col = 'red')
  
# copy, paste,  and add ylim() to make the graph symmetric about y = 0
ggcall + 
  geom_point(col  = 'red',
             pch  = 18,
             size = 3) +
  geom_line(col = 'red') +
  ylim(-40, 40)
```

*** =sct
```{r}
test_error()
success_msg("Well Done!, now lets adjust the aspect ratio to be 1")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:ee0a25a212
## Changing the Aspect Ratio

The units of both axes are dollars.  It is therefore a good idea to set the aspect ratio to 1.  To make this happen in ggplot2, we can use the `coord_fixed()` function



*** =instructions
* the previous exercises code is available in your work space
* review the plot from before
* notice that the aspect ratio is not 1
* add `coord_fixed(ratio = 1)` to adjust the aspect ratio
* review the new plot and notice the different aspect ratio 

*** =hint
* `ggcall +` 
*  `geom_point(col  = 'red',`
*             `pch  = 18,`
*             `size = 3) +`
*  `geom_line(col = 'red') +`
*  `ylim(-40, 40) +`
*  `coord_fixed(ratio = 1)`

*** =pre_exercise_code
```{r}
library(dplyr)
library(ggplot2)

call_payoff <- 
  # compute a european call option payoff
  function(S,K = 40){
  (K <= S) * (S - K)}


DF <- data_frame(asset_price = seq(from = 0, to = 80, by = 5))

DF <- DF %>%
  mutate(payoff = call_payoff(S = asset_price))

ggcall <- ggplot(data = DF, aes(x = asset_price, y = payoff)) 
ggcall + 
  geom_point(col  = 'red',
             pch  = 18,
             size = 3) +
  geom_line(col = 'red') +
  ylim(-40, 40)
```

*** =sample_code
```{r}
# add coord_fixed() with the appropriate argument to the code below
ggcall + 
  geom_point(col  = 'red',
             pch  = 18,
             size = 3) +
  geom_line(col = 'red') +
  ylim(-40, 40)

```

*** =solution
```{r}
# add coord_fixed() with the appropriate argument to the code below
ggcall + 
  geom_point(col  = 'red',
             pch  = 18,
             size = 3) +
  geom_line(col = 'red') +
  ylim(-40, 40) +
  coord_fixed(ratio = 1)
```

*** =sct
```{r}
test_error()
success_msg("Good!, now lets try to add a title to the plot")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:13e197f4a1
## Adding a Title to the Plot

You can add a title to the graph using `ggtitle()`.  Adjusting the color, size, font, etc will come later when you learn about `themes()`


*** =instructions
* the previous plot is shown on the right
* add a title to your plot 
* add `ggtitle("Call Option Payoff")
* review the new graph to see the difference

*** =hint
* `ggcall +` 
* `geom_point(col  = 'red',`
*             `pch  = 18,`
*             `size = 3) +`
*  `geom_line(col = 'red') +`
*  `ylim(-40, 40) +`
*  `coord_fixed(ratio = 1) +`
*  `ggtitle("Call Option Payoff")`

*** =pre_exercise_code
```{r}
library(dplyr)
library(ggplot2)

call_payoff <- 
  # compute a european call option payoff
  function(S,K = 40){
  (K <= S) * (S - K)}


DF <- data_frame(asset_price = seq(from = 0, to = 80, by = 5))

DF <- DF %>%
  mutate(payoff = call_payoff(S = asset_price))

ggcall <- ggplot(data = DF, aes(x = asset_price, y = payoff)) 
ggcall + 
  geom_point(col  = 'red',
             pch  = 18,
             size = 3) +
  geom_line(col = 'red') +
  ylim(-40, 40) +
  coord_fixed(ratio = 1)
```

*** =sample_code
```{r}
# add coord_fixed() with the appropriate argument to the code below
ggcall + 
  geom_point(col  = 'red',
             pch  = 18,
             size = 3) +
  geom_line(col = 'red') +
  ylim(-40, 40) +
  coord_fixed(ratio = 1)
```

*** =solution
```{r}
# add coord_fixed() with the appropriate argument to the code below
ggcall + 
  geom_point(col  = 'red',
             pch  = 18,
             size = 3) +
  geom_line(col = 'red') +
  ylim(-40, 40) +
  coord_fixed(ratio = 1) +
  ggtitle("Call Option Payoff")
```

*** =sct
```{r}
test_error()
success_msg("Awesome!, Next we will change the axes labels")
```
