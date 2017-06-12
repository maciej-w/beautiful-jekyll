---
layout: post
title: Linear Regression 
subtitle: the cost function from the ML course by Andrew Ng
bigimg: ../img/analog.jpg
---

### This is my personal recap on the linear regression funtion with a single parameter from Coursera 

Suppose we want to predict housing prices based on previous house prices which we have: 

1) as we have labeled data (prices) which we can use we will be building a supervised model
2) what we are trying to predict is continuous (can be 1 but 578 000 as well) it is a regression problem - if we would try to teach the model if email is spam/not spam this would be a classification model

Before we go further let me explain what we are trying to achieve - we are going to use the cost function which is:
J(\theta_0, \theta_1) = \dfrac {1}{2m} \displaystyle \sum _{i=1}^m \left ( \hat{y}_{i}- y_{i} \right)^2 = \dfrac {1}{2m} \displaystyle \sum _{i=1}^m \left (h_\theta (x_{i}) - y_{i} \right)^2

