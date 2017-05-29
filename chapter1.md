---
title       : Integration using R
description : This lab is about integrating one and two variable functions using R
attachments :
  



--- type:NormalExercise lang:r xp:100 skills:1 key:0d76418123
## SOA Exam P #34
The lifetime of a machine part has a continuous distribution on the
interval $(0, 40)$ with probability density function $f(x)$, where $f(x)$ is
proportional to $(10 + x)^{−2}$ on the interval. Calculate the probability
that the lifetime of the machine part is less than 6.

To answer this question, use the following property of density functions

$$\int\limits_{-\infty}^{+\infty} f(x) \ dx=1$$

to solve for the constant $c$ such that 
$$
f(x) = 
\begin{cases}
\dfrac{c}{(x+10)^2} &, \ 0 < x < 40 \\\
&  \\\
0 &, \ \text{otherwise} \\\
\end{cases}
$$
After that calculate the probability as 
$$ P[X<6] = \int\limits_{0}^{6} f(x) \ dx $$


*** =instructions
* Load the `stats` package
* Solve for the constant $c$
* Define the density function $f(x)$
* Compute the probability, $P[X <6]$
* Assign your answer to `prob_x`
* Disply the value of `prob_x`

*** =hint
`library(stats)`


`c <- 1 / integrate(function(x){(10+x)^{-2}}, lower = 0, upper = 40)$value`


`f <- function(x){(0 <x & x < 40) * c / (10 + x)^2}`


`prob_x <- integrate(f = f, lower =0, upper = 6)$value`


`prob_x`

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# Load the stats package


# Solve for the value of c


# Define the density function f


# Compute P[X<6] assign to prob_x


# Display the value of prob_x
```

*** =solution
```{r}
# Load the stats package
library(stats)

# Solve for the value of c
(c <- 1 / integrate(function(x){(10+x)^{-2}}, lower = 0, upper = 40)$value)

# Define the density function f
f <- function(x){(0 <x & x < 40) * c / (10 + x)^2}

# Compute P[X<6] assign to prob_x
prob_x <- integrate(f = f, lower =0, upper = 6)$value

# Display the value of prob_x
prob_x
```

*** =sct
```{r}
test_error()
test_object("c",
            undefined_msg = "Make sure to define the density c",
            incorrect_msg = "Your definition of c has a problem")
test_object("f",
            undefined_msg = "Make sure to define the density f(x, y)",
            incorrect_msg = "Your definition of f has a problem")
test_object("prob_x",
            undefined_msg = "Make sure define prob_x",
            incorrect_msg = "your value of prob_x is incorrect")  
test_output_contains("prob_x")
success_msg("Outstanding!")
```




--- type:NormalExercise lang:r xp:100 skills:1 key:ace2599d9b
##SOA Exam P #45
Let $X$ be a continuous random variable with density function
$$
f(x) = \begin{cases}
\dfrac{\vert x\vert}{10} &, \ \ -2 < x < 4 \\\
& \\\
0 &, \ \ \text{otherwise} \\\
\end{cases}
$$
Calculate the expected value of $X$.


*** =instructions

- Assign the density function of $X$ to `f`
- Use `integrate` with appropriate arguements to calculate the expected value of $X$
- Assign your answer to `expected_value`

*** =hint
Did you use `integrate()` with arguements `f = function(x){x*f(x)}`,`lower = -2`, and `upper = 4`? Did you define the density using
`f <- function(x){(-2 < x & x < 4) * abs(x) / 10}`?  Did you only select the numerical result of `integrate`?  Did you assign the expected value to `expected_value` and print the result to the console? 

*** =pre_exercise_code
```{r}


```

*** =sample_code
```{r}
# Load the stats package


# Assign the density function of X to f


# Use integrate to calculate the expected value of X.  Assign to expected_value


# Display expected_value



```

*** =solution
```{r}
# Load the stats package
library(stats)

# Assign the density function of X to f
f <- function(x){(-2 < x & x < 4) * abs(x) / 10}

# Use integrate to calculate the expected value of X.  Assign to expected_value
expected_value <- integrate(f = function(x){x * f(x)}, lower = -2, upper = 4)$value

# Display expected_value
expected_value
```

*** =sct
```{r}
test_error()
test_object("f",
            undefined_msg = "Did you define the density function as f?",
            incorrect_msg = "Did you correctly define the density function of X?")
test_object("expected_value",
            undefined_msg = "Did you assign the expected value to expected_value?",
            incorrect_msg = "Did you correctly compute E[X]?")
test_output_contains(expected_value,
                     times = 1,
                     incorrect_msg = "Did you print out expected_value?")
success_msg("Good job! You can solve exam P problems using R")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:5bcf4a8e2e
## SOA Exam P #55
An insurance company's monthly claims are modeled by a continuous, positive random variable $X$ whose probability density function is proportional to $(1+x)^{-4}$, for $\ 0    <  \  x   <  \infty$.  Calculate the company's expected monthly claims.


*** =instructions

* Solve for the constant of proportionality, `c`.  
* Assign the probability density function of $X$ to `f`
* Calculate $E[X]$ using `integrate()`

*** =hint
- Did you integrate $(1+x)^{-4}$ over the interval $(0, \infty)$ and assign the value to `c`?


- Did you compute $\displaystyle{E[X] = \int\limits_0^{\infty} x f(x) \ dx}$?

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# load the stats package


# Calculate the contant of proportionality and assign this value to c


# Assign the density function of X to f


# Calculate the expected value of X and save as expected_value


# Display expected_value

```

*** =solution
```{r}
# load the stats package
library(stats)

# Calculate the contant of proportinality and assign this value to c
(c <- 1 / integrate(function(x) (1 + x) ^{-4}, lower = 0, upper = Inf)$value)


# Assign the density function of X to f
f <- function(x){c / (1 + x)^4}


# Calculate the expected value of X and save as expected_value
expected_value <- integrate(function(x){x * f(x)}, lower = 0,  upper = Inf)$value

# Display expected_value
expected_value
```

*** =sct
```{r}
test_error()
test_object("c",
            undefined_msg = "Did you define the constant c?",
            incorrect_msg = "Did you correctly calculate the value of c?")

test_object("f",
            undefined_msg = "Did you define the density function as f?",
            incorrect_msg = "Did you correctly define the density function of X using the value of c?")
test_object("expected_value",
            undefined_msg = "Did you assign the expected value to expected_value?",
            incorrect_msg = "Your answer for E[X] is wrong")
test_output_contains(expected_value,
                     times = 1,
                     incorrect_msg = "Did you print out expected_value?")
success_msg("Good job! You are getting really good at this!")
```




--- type:NormalExercise lang:r xp:100 skills:1 key:b2434ee5d2
## SOA Exam P #157

Let $X$ be a continuous random variable with density function

$$
f(x) = 
\begin{cases}
\dfrac{p-1}{x^p} &, \ 1 < x \\\
& \\\
0 &, \ \text{otherwise} \\\
\end{cases}
$$

Calculate the value of $p$ such that $E[X] = 2$



*** =instructions
* load the stats package

* Define a density function $f(x,p)$ as `f`

* Note that for $E[X]$ to be defined, $2 < p$

* Define an expected value function $ex(p) = \displaystyle{\int\limits_1^{\infty} x \cdot f(x,p) \ dx}$

* Estimate a solution to the equation $ex(p) = 2$ using `which.min()`

* Remember that $2 < p$ 

*** =hint
- Load both the stats package
- Define `f` a a function of  $x$ and $p$
- Use `integrate()` to define `ex(p)` 
- Vectorize `ex`
- Estimate a solution to the equation ex(p) = 2 using `which.min()`
- Save your answer as p_answer
- Print p_answer

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# load the stats package


# Define the density function f


# Use f to define an expected value function ex


# Vectorize ex


# Estimate a solution to the equation ex(p) = 2 and save as p_answer


# Print p_answer to the console


```

*** =solution
```{r}
# load the stats package
library(stats)


# Define the density function f
f <- function(x, p){(1 < x) * (p - 1) / x ^ p}

# Use f to define an expected value function e
ex <- function(p){integrate(function(x){x * f(x, p)}, lower = 1, upper = Inf)$value}

# Vectorize ex
ex <- Vectorize(ex)

# Estimate a solution to the equation e(p) = 2 and save as p_answer
p_vals   <- seq(from = 2.01,  to = 5, by = 0.001)
values   <- ex(p_vals) 
index    <- which.min(abs(values - 2))
p_answer <- p_vals[index]

# Print p_answer to the console
p_answer
```

*** =sct
```{r}
test_error()
test_object("f",
            undefined_msg = "Make sure to define the density f(x,p)",
            incorrect_msg = "Did you correctly define f(x,p)?")
test_object("ex",
            undefined_msg = "Did you assign the expected value function ex",
            incorrect_msg = "Your definition of for ex is wrong")
test_output_contains(p_answer,
                     times = 1,
                     incorrect_msg = "Did you print out p_answer")
success_msg("Good job! You are awesome at this!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:4b21b3e7f4
## SOA Exam P # 178

The proportion $X$ of yearly dental claims that exceed 200 is a random variable with probability density function

$$f(x) = 
\begin{cases}
60x^3(1-x)^2 &, \ 0 < x < 1 \\\
& \\\
0 & , \ \text{otherwise} \\\
\end{cases}
$$

Calculate $Var[X/(1-X)]$



*** =instructions
- the stats package is already loaded

- Define the density function as `f`

- Define `g` as $X / (X-1)$

- Compute $E[g(X)]$ and save as `ex_g1`

- Compute $E[g(X)]^2$ and save as `ex_g2`

- Solve for $V[g(X)]$ and save as `var_g`

*** =hint
* Make sure to define the density function as `f` and $X/ (X-1)$ as `g`
* When you use `integrate`make sure to select the `value` using `$`

*** =pre_exercise_code
```{r}
library(stats)
```

*** =sample_code
```{r}
# define the density function as f


# define g = X / (X - 1)


# Compute E[g(X)].  Save as ex_g1


# Compute E[g(X) ^ 2]. Save as ex_g2


# Solve for V[g(X)].  Save as var_g

```

*** =solution
```{r}
# define the density function as f
f <- function(x){(0 < x & x < 1) * 60 * x ^ 3 * (1 - x) ^ 2}

# define g = X / (X - 1)
g <- function(x){x / (x-1)}

# Compute E[g(X)].  Save as ex_g1
(ex_g1 <- integrate(f = function(x){g(x)*f(x)}, lower = 0, upper = 1)$value)

# Compute E[g(X) ^ 2]. Save as ex_g2
(ex_g2 <- integrate(f = function(x){g(x)^2 * f(x)}, lower = 0, upper = 1)$value)

# Solve for V[g(X)].  Save as var_g
(var_g = ex_g2 - (ex_g1) ^ 2)
```

*** =sct
```{r}
test_error()
test_object("f",
            undefined_msg = "Make sure to define the density f(x)",
            incorrect_msg = "Your definition of f has a problem")
test_object("g",
            undefined_msg = "Make sure to define g(x)",
            incorrect_msg = "Your definition of g has a problem")
test_object("ex_g1",
            undefined_msg = "Did you assign the expected value of g to ex_g1",
            incorrect_msg = "Your definition of for ex_g1 is incorrect")
test_object("ex_g2",
            undefined_msg = "Did you assign the expected value of g^2 to ex_g2",
            incorrect_msg = "Your definition of for ex_g2 is incorrect")
test_object("var_g",
            undefined_msg = "Did you assign the variance of X/(X-1) to var_g",
            incorrect_msg = "Your calculation of var_g is wrong")
success_msg("Awesome!! You are learning more and more about this.")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:f8b44f897f
## SOA Exam P #33
The loss due to a fire in a commercial building is modeled by a random variable $X$ with density function

$$
f(x) = 
\begin{cases}
0.005(20 - x) &, \ 0 < x < 20 \\\
& \\\
0 &, \ \text{otherwise} \\\
\end{cases}
$$

Given that a fire loss exceed 8, calculate the probability that it exceeds 16.


*** =instructions
* load the stats package
* 
* Assign the density function of $X$ to `f`

* Calculate $P[8 < X]$.  Assign to `prob_A`

* Define the conditional density function `f_A`

* Compute the conditional probability $P[X > 16 | X > 8]$.  Assign to `cond_prob`

*** =hint

`library(stats)`


`f <-` 

`function(x){(0 < x & x < 20)*0.005*(20-x)}`


`(prob_A <-` 

`integrate(f, lower = 8, upper =20)$value) `


`f_A <-` 

`function(x){f(x)*(8 < x)/prob_A}`


`(cond_prob <-` 

`integrate(f_A,lower = 16,upper = 20)$value)`

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# load the stats package


# assign the density of X to f


# Calculate P[8 < X].  Assign to prob_A


# Define the conditional density f_A


# Compute the conditional probability P[X>16 | X > 8].  Assign to cond_prob

```

*** =solution
```{r}
# load the stats package
library(stats)

# assign the density of X to f
f <- function(x){(0 < x & x < 20) * 0.005 * (20 - x)}

# Calculate P[8 < X].  Assign to prob_A
(prob_A <- integrate(f, lower = 8, upper =20)$value) 

# Define the conditional density f_A
f_A <- function(x){f(x) * (8 < x) / prob_A}

# Compute the conditional expected value.  Assign to cond_prob
(cond_prob <- integrate(f_A, lower = 16, upper = 20)$value)

```

*** =sct
```{r}
test_error()
test_object("f",
            undefined_msg = "Make sure to define the density f(x)",
            incorrect_msg = "Your definition of f has a problem")
test_object("prob_A",
            undefined_msg = "Make sure define prob_A",
            incorrect_msg = "the value of prob_A is incorrect")
test_object("f_A",
            undefined_msg = "Did you assign the conditional density function to f_A?",
            incorrect_msg = "Is your definition of f_A correct?")
test_object("cond_prob",
            undefined_msg = "Did you assign the conditional probability to cond_prob?",
            incorrect_msg = "the value of cond_prob is incorrect")
success_msg("Cool!, you can even solve conditional probability questions using `integrate()`")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:c96f044016
## SOA Exam P # 121
Let $X$ represent the age of an insured automobile involved in an accident.
Let $Y$ represent the length of time the owner has insured the
automobile at the time of the accident. $X$ and $Y$ have joint probability
density function

$$f(x,y) = 
\begin{cases}
& \\\
\dfrac{1}{64} \left(10 - xy^2 \right ) &, \ 2 \leq x \leq 10, \ 0 \leq y \leq 1 \\\
 &  \\\
0 &, \ \text{otherwise} \\\
& \\\
\end{cases}
$$

Calculate the expected age of an insured automobile involved in an
accident.


*** =instructions
* Load the `stats` package
* `iterated_integral()` is already loaded
* Define the joint density function `f(x, y)`
* Calculate the expected value, $E[X]$
* Use the formula
$$E[X] = \displaystyle{\int\int x f(x,y) \ dx dy}$$

*** =hint

`library(stats)`

`f <- function(x, y){`

$\ \ $  `(2 <= x & x <= 10) *`

$\ \ $ `(0 <= y & y <= 1) *` 

$\ \ $ `(1 / 64) * (10 - x * y ^ 2)}`
  
`expected_value_x <-` 

`iterated_integral(`

- `f = function(x,y){x * f(x,y)},` 

- `xl = function(y){2},` 

- `xu = function(y){10},`

- `yl = function(x){0},`

- `yu = function(x){1},`

- `dx = 1)`
    
`expected_value_x`


*** =pre_exercise_code
```{r}
iterated_integral <- function(f , xl, xu, yl, yu, dx){
  # computes the iterated integral of f over the region defined by 
  # xl < x < xu and yl < y < yu
  # Args:
  #   f : the integrand as a function of x and y
  #   xl: lower bound for x, as a function of y 
  #   xu: upper bound for x, as a function of y
  #   yl: lower bound for y, as a function of x
  #   yu: upper bound for y, as a function of x
  #   dx: 1 means integrate x first (on the inside) and then y
  #   f : the integrand as a function of x and y
  #
  # Returns: the iterated integral of f over the region defined by xl, xu, yl, and yu
  if (dx == 1){ 
      integrate(function(y)
      {sapply(y, function(y)
      {integrate(function(x){f(x,y)}, lower = xl(y), upper=xu(y))$value})},
      lower = yl(x), upper = yu(x))
  } else {
      integrate(function(x)
      {sapply(x, function(x)
      {integrate(function(y){f(x,y)}, lower = yl(x), upper=yu(x))$value})},
      lower = xl(y), upper = xu(y))}
}

```

*** =sample_code
```{r}
# load the stats package


# define the density function f

  
# Calculate E[X] and assign to expected_value_x

    
# print out expected_value_x


```

*** =solution
```{r}
# load the stats package
library(stats)

# define the density function f
f <- 
  function(x, y){
  (2 <= x & x <= 10) * (0 <= y & y <= 1) * (1 / 64) * (10 - x * y ^ 2)}
  
# Calculate E[X] and assign to expected_value_x
expected_value_x <- 
  iterated_integral(
    f = function(x,y){x * f(x,y)}, 
    xl = function(y){2}, 
    xu = function(y){10},
    yl = function(x){0},
    yu = function(x){1},
    dx = 1)
    
# print out expected_value_x
expected_value_x


```

*** =sct
```{r}
test_error()
test_object("f",
            undefined_msg = "Make sure to define the density f(x, y)",
            incorrect_msg = "Your definition of f has a problem")
test_object("expected_value_x",
            undefined_msg = "Make sure define expeted_value_x",
            incorrect_msg = "you value for E[X] is incorrect")
success_msg("Perfect!, Now you can compute iterated integrals using R!!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:4872a61ca1
## SOA Exam P # 77

A device runs until either of two components fails, at which point the device stops running.  The joint density function of the lifetimes of the two components, both measured in hours, is

$$
\begin{eqnarray}
f(x,y) & = & 
\begin{cases}
\dfrac{x+y}{8}&, \  \ 0 < x < 2, \ \ 0 < y < 2 \\\
& \\\
0 &, \ \  \text{otherwise}\\\
\end{cases}\\\
\end{eqnarray}
$$

Calculate the probability that the device fails during its first hour of operation.

*** =instructions
* Load the `stats` package
* `compute_Iterated_Integral()` is already loaded
* Define the joint density function `f(x, y)`
* Define a function `r(x)` for the region of integration
* Calculate $P[\min\\{X, Y\\} \leq 1]$ assign to prob_hour

*** =hint

`library(stats)`


`f <- function(x, y){`

`(0 < x & x < 2)*(0 < y & y < 2)*(x + y) / 8}`


`r <- function(x, y){`

`(0<x & x<2)*(0 < y & y < 2)*(x < 1 | y < 1)}`


`prob_hour <- `

`compute_Iterated_Integral(`

-  `f  = function(x, y){r(x,y) * f(x,y)},`
-  `xl = function(y){0},`
-  `xu = function(y){2},`
-  `yl = function(x){0},`
-  `yu = function(x){2},`
-  `dx = 1)`
    

`prob_hour`

*** =pre_exercise_code
```{r}
compute_Iterated_Integral <- function(f , xl, xu, yl, yu, dx){
  # computes the iterated integral of f over the region defined by 
  # xl < x < xu and yl < y < yu
  # Args:
  #   f : the integrand as a function of x and y
  #   xl: lower bound for x, as a function of y 
  #   xu: upper bound for x, as a function of y
  #   yl: lower bound for y, as a function of x
  #   yu: upper bound for y, as a function of x
  #   dx: 1 means integrate x first (on the inside) and then y
  #   f : the integrand as a function of x and y
  #
  # Returns: the iterated integral of f over the region defined by xl, xu, yl, and yu
  if (dx == 1){ 
      integrate(function(y)
      {sapply(y, function(y)
      {integrate(function(x){f(x,y)}, lower = xl(y), upper=xu(y))$value})},
      lower = yl(x), upper = yu(x))
  } else {
      integrate(function(x)
      {sapply(x, function(x)
      {integrate(function(y){f(x,y)}, lower = yl(x), upper=yu(x))$value})},
      lower = xl(y), upper = xu(y))}
}
```

*** =sample_code
```{r}
# load the stats package


# define the joint density function


# define r(x,y) corresponding to the region of integration


# compute P[min{X,Y} <=1] and assign to prob_hour


# print out prob_hour

```

*** =solution
```{r}
# load the stats package
library(stats)

# define the joint density function
f <- function(x, y){(0 < x & x < 2) * (0 < y & y < 2) * (x + y) / 8}

# define r(x,y) corresponding to the region of integration
r <- function(x, y){(0 < x & x < 2) * (0 < y & y < 2) * (x < 1 | y < 1)}

# compute P[min{X,Y} <=1] and assign to prob_hour
prob_hour <- 
  compute_Iterated_Integral(
    f  = function(x, y){r(x,y) * f(x,y)},
    xl = function(y){0},
    xu = function(y){2},
    yl = function(x){0},
    yu = function(x){2},
    dx = 1)
    
# print out prob_hour
prob_hour
```

*** =sct
```{r}
test_error()
test_object("f",
            undefined_msg = "Make sure to define the density f(x, y)",
            incorrect_msg = "Your definition of f has a problem")
test_object("r",
            undefined_msg = "Make sure define r(x,y)",
            incorrect_msg = "you definition of r is incorrect")
test_object("prob_hour",
            undefined_msg = "Make sure define prob_hour",
            incorrect_msg = "your value of prob_hour is incorrect")            
success_msg("Perfect!, Another example of computing iterated integrals using R!!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:15503309e8
## SOA Exam P #117

A company is reviewing tornado damage claims under a farm insurance policy.  Let $X$ be the portion of a claim representing damage to the house and let $Y$ be the portion of the same claim representing damage to the rest of the property.  The joint density of function of $X$ and $Y$ is

$$
\begin{eqnarray}
f(x,y) & = & \begin{cases}
6[1-(x+y)] &, \ 0 < x,\ 0 < y,\ x + y < 1\\\
& \\\
0 &, \ \text{otherwise}\\\
\end{cases}
\end{eqnarray}
$$

Calculate the probability that the portion of a claim representing damage to the house is less than 0.2.

*** =instructions
`compute_Iterated_Integral is already loaded

Use `ls()` to verify this

load the `stats` package

Assign the joint density to `f`

Compute $P[X < 0.2]$

Assign the probabiity to `prob_house_0.2`

*** =hint

`library(stats)`


`f <-`

`function(x,y){`

`(0 < x & 0 < y)*(x < 1-y)*6*(1-(x+y))}`


`prob_house_0.2 <-`

`compute_Iterated_Integral(`

- `xl = function(y){0},`
- `xu = function(y){0.2},`
- `yl = function(x){0},`
- `yu = function(x){1-x},`
- `f  = f,`
- `dx = 2)`
  
`prob_house_0.2`


*** =pre_exercise_code
```{r}
compute_Iterated_Integral <- function(f , xl, xu, yl, yu, dx){
  # computes the iterated integral of f over the region defined by 
  # xl < x < xu and yl < y < yu
  # Args:
  #   f : the integrand as a function of x and y
  #   xl: lower bound for x, as a function of y 
  #   xu: upper bound for x, as a function of y
  #   yl: lower bound for y, as a function of x
  #   yu: upper bound for y, as a function of x
  #   dx: 1 means integrate x first (on the inside) and then y
  #   f : the integrand as a function of x and y
  #
  # Returns: the iterated integral of f over the region defined by xl, xu, yl, and yu
  if (dx == 1){ 
      integrate(function(y)
      {sapply(y, function(y)
      {integrate(function(x){f(x,y)}, lower = xl(y), upper=xu(y))$value})},
      lower = yl(x), upper = yu(x))
  } else {
      integrate(function(x)
      {sapply(x, function(x)
      {integrate(function(y){f(x,y)}, lower = yl(x), upper=yu(x))$value})},
      lower = xl(y), upper = xu(y))}
}
```

*** =sample_code
```{r}
# use ls() to see that compute_Iterated_Integral is already defined


# load the stats package


# define the joint probability density function


# compute P[X < 0.2] assign to prob_house_0.2

  
# display prob_house_0.2


```

*** =solution
```{r}
# use ls() to see that compute_Iterated_Integral is already defined
ls()

# load the stats package
library(stats)

# define the joint probability density function
f <- function(x,y){(0 < x & 0 < y)*(x < 1-y)*6*(1-(x+y))}

# compute P[X < 0.2] assign to prob_house_0.2
prob_house_0.2 <- 
  compute_Iterated_Integral(
  xl = function(y){0},
  xu = function(y){0.2},
  yl = function(x){0},
  yu = function(x){1-x},
  f  = f,
  dx = 2)
  
# display prob_house_0.2
prob_house_0.2



```

*** =sct
```{r}
test_error()
test_object("f",
            undefined_msg = "Make sure to define the density f(x, y)",
            incorrect_msg = "Your definition of f has a problem")
test_object("prob_house_0.2",
            undefined_msg = "Make sure define prob_house_0.2",
            incorrect_msg = "your value of prob_house_0.2 is incorrect")            
success_msg("Ecellent!, an example of computing iterated integrals over non-rectangular regions!!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:1b8af88c71
## SOA Exam P #90  

An insurance company sells two types of auto insurance policies: Basic and Deluxe. The time until the next Basic Policy claim is an exponential random variable with mean two days. The time until the next Deluxe Policy claim is an independent exponential random variable with mean three days. Calculate the probability that the next claim will be a Deluxe Policy claim.

Since $X$ and $Y$ are independent the joint density function is $f(x,y) = f(x)f(y)$

$$
\begin{eqnarray}
f(x,y) & = & 
\begin{cases}
\dfrac{1}{6}e^{-x/2}e^{-y/3} &,\  0 < x \ \text{ and } \ 0 < y \\\
& \\\
0 &, \ \text{ otherwise } \\\
\end{cases}\\
\end{eqnarray}
$$

In this question we want to compute the probability $P[Y < X]$. 



*** =instructions
load the `stats` package

use`ls()` to check for `compute_Iterated_Integral`

define the joint density function as `f`

use integration to compute $P[Y<X]$

assign your answer to `prob_xy`

*** =hint

`library(stats)`

`ls()`

`f <- function(x,y){`

`(0 < x)*(0 < y)*(1/6)*exp(-x/2)*exp(-y/3)}`


`prob_xy <- compute_Iterated_Integral(`

-  `xu = function(y){Inf},`

-  `xl = function(y){0},`

-  `yu = function(x){x},`

-  `yl = function(x){0},`

-  `dx = 2)`
  

`prob_xy`

*** =pre_exercise_code
```{r}
compute_Iterated_Integral <- function(f , xl, xu, yl, yu, dx){
  # computes the iterated integral of f over the region defined by 
  # xl < x < xu and yl < y < yu
  # Args:
  #   f : the integrand as a function of x and y
  #   xl: lower bound for x, as a function of y 
  #   xu: upper bound for x, as a function of y
  #   yl: lower bound for y, as a function of x
  #   yu: upper bound for y, as a function of x
  #   dx: 1 means integrate x first (on the inside) and then y
  #   f : the integrand as a function of x and y
  #
  # Returns: the iterated integral of f over the region defined by xl, xu, yl, and yu
  if (dx == 1){ 
      integrate(function(y)
      {sapply(y, function(y)
      {integrate(function(x){f(x,y)}, lower = xl(y), upper=xu(y))$value})},
      lower = yl(x), upper = yu(x))
  } else {
      integrate(function(x)
      {sapply(x, function(x)
      {integrate(function(y){f(x,y)}, lower = yl(x), upper=yu(x))$value})},
      lower = xl(y), upper = xu(y))}
}
```

*** =sample_code
```{r}
# load the stats package


# use ls() to check for compute_Iterated_Integral


# define the joint density function f


# compute P[Y < X] and assign to prob_xy

  
# display the answer

```

*** =solution
```{r}
# load the stats package
library(stats)

# use ls() to check for compute_Iterated_Integral

# define the joint density function f
f <- function(x,y){(0 < x)*(0 < y)*(1/6)*exp(-x/2)*exp(-y/3)}

# compute P[Y < X] and assign to prob_xy
prob_xy <- compute_Iterated_Integral(
  f  = f,
  xu = function(y){Inf},
  xl = function(y){0},
  yu = function(x){x},
  yl = function(x){0},
  dx = 2)
  
# display the answer
prob_xy



```

*** =sct
```{r}
test_error()
test_object("f",
            undefined_msg = "Make sure to define the density f(x, y)",
            incorrect_msg = "Your definition of f has a problem")
test_object("prob_xy",
            undefined_msg = "Make sure define prob_xy",
            incorrect_msg = "your value of prob_xy is incorrect")  
test_output_contains("prob_xy")
success_msg("Ecellent!, an example of computing iterated integrals with infinite integration limits!!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:eed5e04419
## SOA Exam P #91
An insurance company insures a large number of drivers. Let $X$ be
the random variable representing the company’s losses under collision
insurance, and let $Y$ represent the company’s losses under liability insurance.
$X$ and $Y$ have joint density function

$$
f(x,y) =
\begin{cases}
\dfrac{2x+2-y}{4} &,\ 0 <x <1, \ 0 < y < 2  \\\
&   \\\
0 &,  \ \text{otherwise} \\\
\end{cases}
$$

Calculate the probability that the total company loss is at least 1.


*** =instructions
* load the `stats` package


* use `ls()` to check for `compute_Iterated_Integral`


* define the joint density function `f`


* compute $P[X + Y > 1]$ and assign to `prob_xy`

  
* display the answer

*** =hint
`library(stats)`


`ls()`


`f <- function(x,y){`

`(0 < x & x < 1) * (0 < y & y < 2) * (2 * x + 2 - y) / 4}`


`prob_xy <- compute_Iterated_Integral(`

-  `f  = f,`

-  `dx = 2,`

-  `xl = function(y){0},`

-  `xu = function(y){1},`

-  `yl = function(x){1-x},`

-  `yu = function(x){2})`
  

`prob_xy`

*** =pre_exercise_code
```{r}
compute_Iterated_Integral <- function(f , xl, xu, yl, yu, dx){
  # computes the iterated integral of f over the region defined by 
  # xl < x < xu and yl < y < yu
  # Args:
  #   f : the integrand as a function of x and y
  #   xl: lower bound for x, as a function of y 
  #   xu: upper bound for x, as a function of y
  #   yl: lower bound for y, as a function of x
  #   yu: upper bound for y, as a function of x
  #   dx: 1 means integrate x first (on the inside) and then y
  #   f : the integrand as a function of x and y
  #
  # Returns: the iterated integral of f over the region defined by xl, xu, yl, and yu
  if (dx == 1){ 
      integrate(function(y)
      {sapply(y, function(y)
      {integrate(function(x){f(x,y)}, lower = xl(y), upper=xu(y))$value})},
      lower = yl(x), upper = yu(x))
  } else {
      integrate(function(x)
      {sapply(x, function(x)
      {integrate(function(y){f(x,y)}, lower = yl(x), upper=yu(x))$value})},
      lower = xl(y), upper = xu(y))}
}
```

*** =sample_code
```{r}
# load the stats package


# use ls() to check for compute_Iterated_Integral


# define the joint density function f


# compute P[X + Y > 1] and assign to prob_xy

  
# display the answer

```

*** =solution
```{r}
# load the stats package
library(stats)

# use ls() to check for compute_Iterated_Integral
ls()

# define the joint density function f
f <- function(x,y){
  (0 < x & x < 1) * (0 < y & y < 2) * (2 * x + 2 - y) / 4}

# compute P[X + Y > 1] and assign to prob_xy
prob_xy <- compute_Iterated_Integral(
  f  = f,
  dx = 2,
  xl = function(y){0},
  xu = function(y){1},
  yl = function(x){1-x},
  yu = function(x){2})
  
# display the answer
prob_xy
```

*** =sct
```{r}
test_error()
test_object("f",
            undefined_msg = "Make sure to define the density f(x, y)",
            incorrect_msg = "Your definition of f has a problem")
test_object("prob_xy",
            undefined_msg = "Make sure define prob_xy",
            incorrect_msg = "your value of prob_xy is incorrect")  
test_output_contains("prob_xy")
success_msg("Outstanding!")
```
