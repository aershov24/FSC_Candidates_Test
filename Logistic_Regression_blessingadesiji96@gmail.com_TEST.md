# Topic: Logistic Regression

**Author**: Blessing Adesiji

**QAs Total**: 3

---

## Q: Why is _Logistic Regression_ Considered a _Linear Model_?

**Difficulty:** `Junior`

**Source:**

https://stats.stackexchange.com/questions/88603/why-is-logistic-regression-a-linear-model


**Answer:**

A model is considered linear if the **transformation of features** that is used to calculate the prediction is a **linear combination of the features**. Although Logistic Regression uses **Sigmoid function** which is a nonlinear function, the model is a generalized linear model because the outcome always depends on the sum of the **inputs and parameters**. 

i.e the logit of the estimated probability response is a linear function of the predictors parameters.

$$
\operatorname{logit}\left(p_{i}\right)=\ln \left(\frac{p_{i}}{1-p_{i}}\right)=\beta_{0}+\beta_{1} x_{1, i}+\beta_{2} x_{2, i}+\cdots+\beta_{p} x_{p, i}
$$

![Sigmoid Function](https://ai-master.gitbooks.io/logistic-regression/content/assets/sigmoid_function.png)


---

## Q: Explain the _Vectorized Implementation_ of _Logistic Regression_?

**Difficulty:** `Mid-Level`

**Source:**


* https://www.coursera.org/lecture/neural-networks-deep-learning/vectorizing-logistic-regression-moUlO
  


**Answer:**

To make predictions on training examples, Z and the sigmoid function needs to be computed as shown below for a few training examples, in this case three. 

$$
\begin{aligned}
&z^{(1)}=w^{T} x^{(1)}+b \\
&a^{(1)}=\sigma\left(z^{(1)}\right) \\
&z^{(2)}=w^{T} x^{(2)}+b \\
&a^{(2)}=\sigma\left(z^{(2)}\right) \\
&z^{(3)}=w^{T} x^{(3)}+b \\
&a^{(3)}=\sigma\left(z^{(3)}\right)
\end{aligned}
$$

The computation above is carried out M times, for M number of training examples.

### Step 1

Define a matrix X to be the training inputs, stacked together in different columns like shown below, and this is a (N<sub>x</sub> by M) matrix

$$
X=\left[\begin{array}{cccc}
:  & : & : &  : \\
:  & : & : &  : \\
x_{0} & x_{1} & x_{2} & …  x_{m} \\
:  & : & : &  : \\
:  & : & : &  : \\
\end{array}\right]
$$

### Step 2
From the matrix above, we can compute 
$$
Z=Z^{(1)} Z^{(2)} Z^{(3)} \ldots Z^{(n)}
$$ 
with one line of code. The matrix Z is a 1 by M matrix which is a row vector.

### Step 3
Using matrix multiplication 
$$
Z=W^{T} X+b
$$ 
we can be computed to obtain Z. This can be carried out using the matrix-vector product (np.dot) of NumPy. 


### Finally, 
W = (N<sub>x</sub> by 1), X is (N<sub>x</sub> by M) and b is (1 by M), multiplication and addition gives Z (1 by M).

---


## Q: Discuss the _Space Complexity Analysis_ of _Logistic Regression_ ?

**Difficulty:** `Senior`

**Source:**

https://www.analyticsvidhya.com/blog/2021/05/20-questions-to-test-your-skills-on-logistic-regression/


**Answer:**

The Space complexity analysis of Logistic Regression is the total amount of memory space used by the algorithm during **training** and **testing or runtime**.

### Training
During the training, four parameters are stored in the memory, and they are x, y, W, b 

* To store b which is a **constant parameter**, the operation requires constant space, **O(1)**. This means that the space does not grow with the size of the data on which the algorithm is operating.
* For parameter x and y, which are both matrices of dimensions (n rows by d columns), and (n rows by 1 column) respectively. The operation to store these two matrices requires **O(nd + n) space**. 
* To store W, which is a vector of d columns, the operation requires **O(d)**. 
In summary, the space complexity analysis of Logistic Regression while training is **O(nd + n + d)** in total. 

### Testing
After training the model, during the testing, W is the only parameter that needs to be stored in memory, so that other points can be classified based on the weight values.
The space needed to store W is **O(d)**, because the W is a vector of d columns in dimension. 


![Complexity Analysis](https://media.geeksforgeeks.org/wp-content/cdn-uploads/mypic.png)

