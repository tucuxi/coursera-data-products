---
title       : Predicting Miles Per Gallon
subtitle    : Homework Assignment of Developing Data Products
author      : tucuxi
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
---

## Overview

Fuel consumption of cars is getting more and more important. A commonly used
measure for fuel consumption is **Miles Per Gallon** (MPG).

Using R and Shiny, we build a web application for predicting
MPG from basic car specification data.

The presentation is organized as follows:

1. Data set
2. Linear model for predicting miles per gallon
3. Shiny application

--- 

## Data Set



We use the **mtcars** data set from package **datasets**. It contains data
extracted from the 1974 Motor Trend US magazine for 32 cars.

Row  | Variable    | Description
---- | ----------- | -------------------
1    | mpg         | Miles/(US) gallon
2    | cyl         | Number of cylinders
3    | disp        | Displacement (cu.in.)
4    | hp          | Gross horsepower
5    | drat        | Rear axle ratio
6    | wt          | Weight (lb/1000)
7    | qsec	       | 1/4 mile time
8    | vs	       | V/S
9    | am	       | Transmission (0 = automatic, 1 = manual)
10   | gear	       | Number of forward gears
11   | carb	       | Number of carburetors

---

## Linear Model for Predicting Miles Per Gallon

We build a linear model for mpg with two predictors:
weight (wt) and number of cylinders (cyl).


```
## 
## Call:
## lm(formula = mpg ~ wt + factor(cyl), data = mtcars)
## 
## Coefficients:
##  (Intercept)            wt  factor(cyl)6  factor(cyl)8  
##        33.99         -3.21         -4.26         -6.07
```

This model has statistically significant P-values (< 0.05):


```r
summary(lm)$coefficients[, 4]
```

```
##  (Intercept)           wt factor(cyl)6 factor(cyl)8 
##    6.257e-17    2.130e-04    4.718e-03    9.992e-04
```

---

## Shiny Application

The [web application](http://tucuxi.shinyapps.io/data_products) allows
the user to enter number of cylinders and weight. It displays a figure
representing the linear model and highlights the predicted mpg value.

At the heart of the application is the prediction of the mpg value. This
is done with the linear model and the predict() function.

For instance, with 6 cylinders and a weight of 3,500 lbs:


```r
predict(lm, data.frame(cyl = 6, wt = 3.5))
```

```
##     1 
## 18.52
```