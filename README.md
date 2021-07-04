# Welcome to MLSC Candidate Repo

Please read this document carefully before submitting your MLSC candidate challenge

# What You Need to Do

* Fork this repository
* Carefully read the `readme.md`
* Create the `Logistic_Regression_youremail_TEST.md` file in the forked repo and add **3 questions and answers (QAS) relevant to Logistic Regression topic that you would ask on a real interview** if you would hire ML/DS devs for your own project
* Make sure you add:
  * one **Junior** question for Junior position
  * one **Medium** difficulty question for Mid position, and
  * one **Senior** question for Senior position.  

* Make sure that for all QA you'll include:
  * Question Title
  * Question Description (optional)
  * Answer + Code (if needed) + Math expressions (if needed)
  * Link(s) to sources (you don't need to write answer by yourself, just combine and research best sources that are available)
  * QA Difficulty Level (`entry`, `junior`, `mid`, `senior`, `expert`)
* Look at the `QAS_Examples.md` file in this repo for examples of QAS Markdown file formatting. Please strictly follow these formatting conventions. That's the key to pass the challenge ;)
* Create pull request from your repo to the MLSC Candidate repo
* Send us email when you happy us to verify it

# How To Choose Good Interview Question

When choosing the good interview question use several simple tactics:

* The QA should not be too **broad**, like 
  * 🚫 `What is Machine Learning?`
* The QA should be **opened** and spark rather a conversation with a candidate than test his/her/their specific knowledge. Compare:
  * 🚫 `Explain Clustering` 
  * ✅ `When would you use Clustering vs Classification?`  
* Keep answer **short** and **succinct**. If you feel your answer is growing in size and covering different topics - split it!
* Avoid very specific highly practical questions like
  * 🚫 `How to install pandas?` - we wont accept that type of questions
* Don't submit questions related to personal candidate experience. That questions are valid for an interview but don't fit to the format of MLSC like
  *  🚫 `Have you ever worked with Tensorflow?`
  *  🚫 `Describe your experience building ML models on your previous job?`
* Don't submit behavioral questions like:
  * 🚫 `Describe your strengths and weakness` and so on
* Use that that types of questions:
  * ✅ `When to use X vs Y?`
  * ✅ `Why would you use X?`
  * ✅ `Compare X vs Y for solving Z`
  * ✅ `What types of X for you know?`
  * ✅ `Are there any problems when using X for solving Z?`
  * ✅ `Name some advantages of using X vs Y for solving Z?`
  * ✅ `Explain X to 5 yo/your grandparents`
  * ✅ `What is example of Y in real life?`
  * ✅ `Provide an intuitive explanation of X`
* The best **rule of thumb** to follow is
  * ✅ question yourself would you ask this question to someone on a real ML interview? If answer is Yes - go for it!

# Where To Find ML/DS Interview Questions

Remember, **you don't need to write the interview questions and answer by yourself** unless you are 100% sure your can provide the best most brilliant answer to the question you're asking. You task is to research the best sources that are available in the Internet (blog posts, books, videos, tutorials), combine and convert that knowledge to answer.

⚠️ **Warning**: Don't use information from the websites with bad english grammar and poor QAs quality like:
* geekforgeeks.com
* onlineinterviewquestions.com
* etc...

There are a list of quality resources you can do you research on:

* towardsdatascience.com
* www.mathsisfun.com
* ml-cheatsheet.readthedocs.io
* en.wikipedia.org
* stats.stackexchange.com
* datascience.stackexchange.com
* becominghuman.ai
* lionbridge.ai
* machinelearningmastery.com
* scikit-learn.org
* blog.paperspace.com
* blogs.oracle.com
* statisticsbyjim.com
* www.datatechnotes.com
* etc ...

💡 **Hint**: Don't blindly copy all answers from one source for one topic. Try to find at least 2-3 source of information for the question and choose the best explanation.

💡**Hint**: Search Github for Machine Learning interview questions repos that other people did. Usually they  already formatted as Markdown and can get you great amount of QAS for the topic

💡**Hint**: When exploring some topic look at the `Table of Content` to get a sense on what subtopics you can cover

# How To Format Interview Question

All interview questions must be formatted using those rules:

* use only **Markdown** ([Github flavour](https://guides.github.com/features/mastering-markdown/))
* use [Katex](https://katex.org/docs/supported.html) for inclusion of math expressions
* **Do** include images, graphs and math into your answers when needed to explain some concepts
* **Do** use and reformat original source of answer using **lists** for better readability

See some examples of QA formatting below. Note how to format **list**, **code**, **file names**, **terms**, **links**, QA **difficulties**, **math expressions** and so on:

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

## Q: What is the difference between _Cost Function_ vs _Gradient Descent_?

**Difficulty**: `Junior`

**Source:**

https://towardsdatascience.com/5-ways-to-detect-outliers-that-every-data-scientist-should-know-python-code-70a54335a623

**Answer:**
*   A **Cost Function** is something we want to minimize. For example, our cost function might be the sum of squared errors over the training set like:

$$J(\theta_0,\theta_1)=\frac{1}{2m}\sum\limits_{i=1}^m (h_{\theta}(x^{(i)})-y^{(i)})^2$$

*  **Gradient Descent** is a method for finding the minimum of a function of multiple variables.

# Useful Tools To Use

There are some good tools that can help you along the way

## Markdown Extractors & Chrome Extensions

* [Copycat](https://chrome.google.com/webstore/detail/copycat/jdjbiojkklnaeoanimopafmnmhldejbg) Chrome/Brave Extension
* [HTML to Markdown Converter](https://mixmark-io.github.io/turndown/)

## Markdown Editors

* VS Code + Markdown Extensions
* StackEdit.io
* [Dllinger.io](https://dillinger.io/)

## VS Extensions

* Markdown All In One
* Markdown Preview Enhanced
* Markdownlint

# What's Next?

Once we got your file we will verify the results and circle back to you in no time. Then we schedule a Slack call and talk about your first MLSC project :)