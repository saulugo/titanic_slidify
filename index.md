---
title       : The Titanic Passengers Survival Prediction App
subtitle    : Machine Learning App
author      : Saul Lugo
job         : Student at Developing Data Products Class
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Historical Background

The sinking of the Titanic on April 15th 1912, was one of the worst passenger ship accidents of moderm history. The sinking killed 1502 out of 2224 passengers and crew. One of the reasons that led to such 
a loss of people's life was that there were not enough lifeboats on board. Also, some people relate that passengers in the first class had priority to access the lifeboats over passengers in the third class.

If you saw the movie "Titanic" (and assuming that the movie tells the truth), you might realize
that conditions like passenger traveling in 1st or 3rd class, passenger being a woman, a man or a
children, passenger traveling alone or with relatives and other conditions had an impact in the survival chances of people.

--- 

## About the App

This App was built using a Machine Learning algorithm. The objective was that the algorithm were
able to predict if a person would survive the Titanic sinking depending on the following variables:

1. Traveling Class (1st, 2nd and 3rd class, being 1st of most expensive ticket and 3rd the cheapest)
2. Passenger Gender (Sex: male or female)
3. Passenger Age
4. Passenger traveling with family or relative or traveling alone

The objective is to provide a tool for the user to analyze how these variables impact the survival
chances of a person traveling on the Titanic.

---

## The Machine Learning Algorithm

The algorithm used for the prediction was a Regression Tree, specifically a RPART (Recursive 
Partitioning and Regression Trees). The library "rpart" in R was used for the algorithm.
 
### The Prediction Algorithm

The following code load the train dataset, prepare it and then builds the prediction model:


```r
library(rpart)
```

```
## Warning: package 'rpart' was built under R version 3.1.3
```

```r
set.seed(1234)
train <- read.csv('train.csv')
```

```
## Warning in file(file, "rt"): cannot open file 'train.csv': No such file or
## directory
```

```
## Error in file(file, "rt"): cannot open the connection
```

```r
train$Survived <- as.factor(train$Survived)
```

```
## Error in is.factor(x): object 'train' not found
```

```r
train$family <- ifelse(train$SibSp>0 | train$Parch>0,1,0)
```

```
## Error in ifelse(train$SibSp > 0 | train$Parch > 0, 1, 0): object 'train' not found
```

```r
train$family <- as.factor(train$family)
```

```
## Error in is.factor(x): object 'train' not found
```

```r
train$Pclass <- as.factor(train$Pclass)
```

```
## Error in is.factor(x): object 'train' not found
```

```r
mod <- rpart(Survived ~ Pclass + Sex + Age + family,data=train)
```

```
## Error in is.data.frame(data): object 'train' not found
```

```r
print(mod)
```

```
## Error in print(mod): object 'mod' not found
```

---

## The Dataset

The dataset used was the train dataset provided in the [Kaggle's Competition for predicting the
survival chances of passengers in the Titanic](https://www.kaggle.com/c/titanic/data)

### Results

You can see the app at [https://saulugo.shinyapps.io/titanic/](https://saulugo.shinyapps.io/titanic/)

After you set the input variables values you must click on submit to see the survival prediction.

You can also see the App code in my github account:
[https://github.com/saulugo/titanic](https://github.com/saulugo/titanic)

Feel free to fork it!

Enjoy!
