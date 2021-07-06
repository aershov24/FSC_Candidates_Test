# Topic: Logistic Regression
**Author:** Uzal Chhetri\
**QAs Total:** 4

## Q: What is the difference between *linear regression* and *logistic regression*?
**Difficulty:** `Junior` \
**Sources:** \
https://en.wikipedia.org/wiki/Linear_regression \
https://machinelearningmastery.com/logistic-regression-for-machine-learning/

**Answer:**

* **Linear regression** models two variables by fitting a *linear equation* to the observed data. 

![linear function](https://ernesto.net/wp-content/uploads/2021/05/simple.png) \
Figure shows a linear function.

* **Logistic regression** models the variables using *logistic functions* (also called sigmoid function) to plot the probabilities between `0` and `1`. 

![sigmoid function](https://machinelearningmastery.com/wp-content/uploads/2016/03/Logistic-Function.png) \
Figure shows a sigmoid function.

## Q: Why can't a *linear regression* be used instead of *logistic regression*?
**Difficulty:** `Junior`\
**Sources:**\
https://stats.stackexchange.com/questions/124818/logistic-regression-error-term-and-its-distribution \
https://pages.pomona.edu/~jsh04747/Student%20Theses/KalyanChadalavada18.pdf \
https://machinelearningmastery.com/logistic-regression-for-machine-learning/

**Answer:**

* It is required for the independent and dependent variables to be **linear** for linear regression models, but the independent and dependent variables are **not** required to have a linear relationship in logistic functions.

* The **linear regression** models assume that the error terms are *normally distributed* (bell-shaped graph) whereas there is *no error terms* in **logistic regression** because it is assumed to follow a *Bernoulli distribution*.

![linear error](https://qph.fs.quoracdn.net/main-qimg-426f562fb3bdf0e65f22844b916ac29a.webp) \
Figure shows the error terms normally distributed in linear regression. 

* **Linear regression** has a *continuous output*. **Logistic regression** does *not* have a continuous output, rather the output is a probability between `0` and `1`. A linear regression may have an output that can go beyond `0` and `1`.

## Q: Compare *SVM* and *logistic regression* in handling outliers.
**Difficulty:** `Mid` \
**Sources:**\
https://scialert.net/fulltext/?doi=jas.2011.26.35 \
https://www.researchgate.net/publication/4202393_Weighted_support_vector_machine_for_data_classification 

**Answer:**

* For **logistic regression**, outliers can have an *unusually large effect* on the estimate of logistic regression coefficients. It will find a linear boundary if it exists to accomodate the outliers. To solve the problem of outliers, sometimes a sigmoid function is used in logistic regression.

* For **SVM**, outliers can make the decision boundary to deviate severely from the optimal hyperplane. One way for SVM to get around the problem is to intrduce *slack variables*. There is a penalty involved with using slack variables, and how SVM handles outliers depends on how this penalty is imposed.

## Q: How can we avoid over-fitting in logistic regression models?
**Difficulty:** `Senior` \
**Sources:**\
https://medium.com/analytics-vidhya/interview-questions-on-logistic-regression-1ebd1666bbbd \
https://towardsdatascience.com/l1-and-l2-regularization-methods-ce25e7fc831c \
https://towardsdatascience.com/the-basics-logistic-regression-and-regularization-828b0d2d206c

**Details:** Explain the different techniques.

**Answer:**

**Regularization techniques** can be used to avoid over-fitting in regression models.

Two types of regularization techniques used for logistic regression models are *Lasso Regularization, and Ridge Regularization*. Ridge and Lasso allow the regularization ('shrinking') of coefficients. This reduces the *variance* in the model which contributes to the model not overfitting on the data. Ridge and Lasso add penalty values to the loss function as shown below:

1. **Lasso regression** adds the absolute value of the magnitude of coefficient as penalty term to the loss function as can be seen in the equation below: 

$$Loss = Error(y, \hat y) + \lambda \sum_{i=1}^N \lvert w_i \rvert$$

The second term added to the loss function is a penalty term whose size depends on the *total magnitude of all the coefficients*. Lambda is a *tuning parameter* that adjusts how large a penalty there will be.

2. **Ridge** regression adds *squared magnitude* of all the coefficients as penalty term to the loss function as can be seen in the equation below:

$$Loss = Error(y, \hat y) + \lambda \sum_{i=1}^N w_i^2$$

The extra penalty term in this case disincentivizes including extra features. There is a balancing act between the increasing of a coefficient and the corresponding increase to the overall variance of the model. 

The Ridge and Lasso act as their own feature selector where features which don't drive the predictive power of the regression see their coefficients pushed down, while more predictive features see higher coefficients despite the added penalty.
