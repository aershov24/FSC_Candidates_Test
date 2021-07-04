# Topic: Anomalies Detection

**Author**: Alex Smith

**QAs Total**: 3

---

## Q: Explain how to use _Standard Deviation_ for _Anomalies Detection_?

**Difficulty:** `Junior`

**Source:**

https://towardsdatascience.com/5-ways-to-detect-outliers-that-every-data-scientist-should-know-python-code-70a54335a623

**Answer:**

In statistics, if a **data distribution** is approximately **normal** then:
* about **68%** of the data values lie within **one standard deviation** of the mean and 
* about **95%** are within **two standard deviations**, and 
* about **99.7%** lie within **three standard deviations**:

![](https://miro.medium.com/max/1400/1*rV7rq7F_uB5gwjzzGJ9VqA.png)

Therefore, if you have any data point that is more than 3 times the standard deviation, then those points are very likely to be **anomalous** or **outliers**.

---

## Q: How to use _one-class SVM_ for _Anomalies Detections_?

**Difficulty:** `Junior`

**Source:**

https://towardsdatascience.com/5-ways-to-detect-outliers-that-every-data-scientist-should-know-python-code-70a54335a623

**Answer:**

Naturally, **SVM** is used in solving multi-class classification problems.

However, **SVM** is also increasingly being used in **one class problem**, where all data belong to a single class. In this case, the algorithm is trained to learn what is “normal”, so that when a new data is shown the algorithm can identify whether it should belong to the group or not. If not, the new data is labeled as out of ordinary or anomaly.

When modeling one class, the algorithm captures the **density** of the majority class and classifies examples on the *extremes of the density* function as *outliers*. This modification of SVM is referred to as **One-Class SVM**.

![](https://1.bp.blogspot.com/-6eNEzd8LnCs/Xoq8wdXGUiI/AAAAAAAAAug/Nktkh8E-8eEXfW4XX-BMhVxhc_2AY0AQQCPcBGAYYCw/s400/one_class_svm_result2.JPG)

---
## Q: What is the difference between _Cost Function_ vs _Gradient Descent_?

**Difficulty**: `Junior`

**Source:**

https://towardsdatascience.com/5-ways-to-detect-outliers-that-every-data-scientist-should-know-python-code-70a54335a623

**Answer:**
*   A **Cost Function** is something we want to minimize. For example, our cost function might be the sum of squared errors over the training set like:

$$J(\theta_0,\theta_1)=\frac{1}{2m}\sum\limits_{i=1}^m (h_{\theta}(x^{(i)})-y^{(i)})^2$$

*  **Gradient Descent** is a method for finding the minimum of a function of multiple variables.