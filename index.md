---
title       : Body Mass Index
subtitle    : Developing Data Products from Coursera and Johns Hopkins University
author      : 
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
---

## About the data

We analyze the Chicken Weight data from `datasets` package. The Chicken Weight data frame has 578 rows and 4 columns from an experiment on the effect of diet on early growth of chickens. It examplified the importance of the Body Max Index (BMI).

1. Weight - a numeric vector giving the body weight of the chicken (gm)
2. Time - a numeric vector giving the number of days since birth when the measurement was made
3. Chick - an ordered factor with levels 18 < ... < 48 giving a unique identifier for the chicken. The ordering of the levels groups chicken on the same diet together and orders them according to their final weight (lightest to heaviest) within diet.
4. Diet - a factor with levels 1, ..., 4 indicating which experimental diet the chicken received.


```
  weight Time Chick Diet
1     42    0     1    1
2     51    2     1    1
3     59    4     1    1
4     64    6     1    1
5     76    8     1    1
6     93   10     1    1
```

--- .class #id

## Pre processing

Using `data.table` package, first we remove those chicken, which do not have full data (21 time steps). Later we summarize the `weight` column across each `Time` and `Diet` column.

```r
cw <- data.table(ChickWeight)
tmp <- cw[,max(Time),by=Chick]
tmp <- tmp[which(V1==21)]
cw <- cw[Chick %in% tmp$Chick]
cw <- cw[,list(wt=mean(weight),time=Time),by=c('Diet','Time')]
```

--- .class #id

## Visualization

Two type of visualizations - *boxplot* & *line plot* are supported by the shiny application. This is controlled by a radio button. For each of the type, the data can be plotted for different diet types as shown here:

![plot of chunk unnamed-chunk-3](assets/fig/unnamed-chunk-3.png) 

--- .class #id

## Conclusion

Help documentation is provided in a separate tab. It describes the data set. The usage of the Body Mass Index application is also briefly described in this tab.

It is seen from both the charts that certain diet types have significant effect on weight gained by chickens. Therefore, it is for our best to check our weight and BMI regularly for a healthy life. We can ajust our activity level and food intake to control our BMI.




