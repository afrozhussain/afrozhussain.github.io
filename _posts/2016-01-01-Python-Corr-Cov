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

# -*- coding: utf-8 -*-
"""
Implementing Covariance in Python
Created on Mon Jan 11 20:28:20 2016
 
@author: SyedAfroz
"""
 
 
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
