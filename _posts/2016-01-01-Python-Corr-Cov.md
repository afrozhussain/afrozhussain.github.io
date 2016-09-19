---
layout: post
title: Implementation of Covariance and Correlation function in Python
subtitle: Let's do some Statistics
---


## Covariance

In probability theory and statistics, covariance is a measure of how much two random variables change together.
Covariance provides a measure of the strength of the correlation between two or more sets of random variates. 
The covariance for two random variates X and Y, each with sample size N, is defined by the expectation value


```python

def cov(x,y):
 
    if len(x) != len(y):
        return
         
    n = len(x)
     
    xy = [x[i]*y[i] for i in range(n)]
     
    mean_x = sum(x)/float(n)
    mean_y = sum(y)/float(n)
     
    return (sum(xy) - n*mean_x * mean_y) / float(n)
    # following code is can also be used to calculate the same result
    #return sum([(x[i]-mean_x)*(y[i]-mean_y) for i in range(n)])
 
 
x = [1,2,3,4,5,6,7,8,9 ,10]
y = [0.1, 0.2,0.3, 0.4, 0.5,0.6, 0.7,0.8,0.9,1.0]
 
print ('Covariance : ' + str(cov(x,y)) ) 

```

## Correlation 

The correlation is one of the most common and most useful statistics. A correlation is a single number that describes the degree of relationship between two variables.

The most familiar measure of dependence between two quantities is the Pearson product-moment correlation coefficient, or “Pearson’s correlation coefficient”, commonly called simply “the correlation coefficient”. It is obtained by dividing the covariance of the two variables by the product of their standard deviations.

```python
def cov(x,y):
 
    if len(x) != len(y):
        return
         
    n = len(x)
     
    xy = [x[i]*y[i] for i in range(n)]
     
    mean_x = sum(x)/float(n)
    mean_y = sum(y)/float(n)
     
    return (sum(xy) - n*mean_x * mean_y) / float(n)
    # following code is can also be used to calculate the same result
    #return sum([(x[i]-mean_x)*(y[i]-mean_y) for i in range(n)])
 
 
x = [1,2,3,4,5,6,7,8,9 ,10]
y = [0.1, 0.2,0.3, 0.4, 0.5,0.6, 0.7,0.8,0.9,1.0]
 
print ('Covariance : ' + str(cov(x,y)) ) 
 
 
def sd(x):
    if len(x) == 0:
        return 0
    n = len(x)
     
    mean_x = sum(x)/float(n)    
    variance = sum( [(x[i] - mean_x)**2 for i in range(n)])/float(n)
    return variance**0.5
     
def corr(x,y):
    if len(x) != len(y):
        return
         
    correlation = cov(x,y) / float(sd(x)*sd(y))
    return correlation
 
 
print ('Correlation of X and Y is ' + str(corr(x,y)))
```


Tags: Python, Covariance, Correlation, Statistics
