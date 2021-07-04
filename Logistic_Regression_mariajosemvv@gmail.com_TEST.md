# Topic: Logistic regression
**Author**: Maria Jose Medina
**QAs Total:** 3
---
## Q: When logistic regression can be used?
**Difficulty:** `Junior`
**Source:**
[https://careerfoundry.com/en/blog/data-analytics/what-is-logistic-regression/](https://careerfoundry.com/en/blog/data-analytics/what-is-logistic-regression/)
**Answer:**
Logistic regression can be used in classification problems where the output or dependent variable is categorical or binary. However, in order to implement logistic regression correctly, the dataset must also satisfy the following properties: 

1. There should not be a high correlation between the independent variables. In other words, the predictor variables should be independent of each other. 
2. There should be a linear relationship between the logit of the outcome and each predictor variable. The logit function is given as `logit(p) = log(p/(1-p))`, where `p` is the probability of the outcome.
3. The sample size must be large. How large depends on the number of independent variables of the model. 


When all the requirements above are satisfied, logistic regression can be used. 


---

## Q: What is the difference between logistic regression and linear regression?
**Difficulty:** `Junior`
**Source:**
[https://careerfoundry.com/en/blog/data-analytics/what-is-logistic-regression/](https://careerfoundry.com/en/blog/data-analytics/what-is-logistic-regression/)
**Answer:**
- **Linear regression** determines a linear relationship between a dependent variable and one or more independent variables. In terms of output, linear regression will give you a **continuous numerical output** and it can be seen graphically as a trend line plotted amongst a set of data points.
- **Logistic regression** predicts the probability of a binary (yes/no) event occurring. Its output is categorical or **discrete**.
---
## Q: Provide a mathematical intuition of Logistic Regression
**Difficulty:** `Junior`
**Source:** 
[https://medium.com/@nikethnarasimhan/logistic-regression-an-intuitive-approach-b1ece5b13c#:~:text=Logistic regression is a statistical,many more complex extensions exist](https://medium.com/@nikethnarasimhan/logistic-regression-an-intuitive-approach-b1ece5b13c#:~:text=Logistic%20regression%20is%20a%20statistical,many%20more%20complex%20extensions%20exist).
**Answer:** 
Logistic regression can bee seen as a **transformation** from linear regression to logistic regression using the logistic function, also known as the **sigmoid function** or S(x):
$$S(x) = \frac{1}{1+e^{-x}}$$
Given the linear model: 
$$y = b_0 + b_1 \cdot x$$
If we apply the sigmoid function to the above equation it results: 
$$S(y) = \frac{1}{1+e^{-y}} = p$$
where p is the probability and it takes values between 0 and 1. If we now apply the logit function to p, it results: 
$$logit(p) = log(\frac{p}{1-p}) = b_0 + b_1 \cdot x$$
The equation above represents the logistic regression. It fits a logistic curve to set of data where the dependent variable can only take the values 0 and 1. 

The previous transformation can be illustrated in the following figure:
![](https://miro.medium.com/max/963/1*1cFchLVevekWRNRW981Krg.png)