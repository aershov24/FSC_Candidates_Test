![](https://user-images.githubusercontent.com/13550565/152297029-160a235d-81f0-4cbb-99cd-d9603e3bb191.png)

# Welcome to FullStack.Cafe Candidates Repo

Please read this document carefully before submitting your FSC candidate challenge.

# What Do You Need to Do?

* Carefully read the `README.md`
* **Fork** this repository
* Create the `RUST_youremail.md` Markdown file in the forked repo and add **`3` questions and answers (QAS) relevant to _Rust Programming Language topic_ that you would ask on a real interview** if you would hire a Rust Developer for your own project. All content must be formatted as Markdown (see examples below).
* Make sure you'll add:
  * one **Junior** question for **Junior** position
  * one **Medium** difficulty question for **Mid** position, and
  * one **Senior** question for **Senior** position

* Make sure that for all QAs you'll include:
  * Question **Title**
  * Question **Description** (optional)
  * **Answer** (required) + `Code` (if needed)
  * Link(s) to **Source**s (you don't need to write answer by yourself, just combine and research best sources that are available)
  * QA **Difficulty** Level. Use that Difficulty enum: [`entry`, `junior`, `mid`, `senior`, `expert`]
* Look at the `QAS_Examples.md` file in this repo for examples of QAS file formatting in Markdown. Use this file as a template for your submission. Please strictly follow these formatting conventions. This is **the key** to pass the challenge ;)
* Create a [pull request](https://docs.github.com/en/github/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork) from your repo into the FSC Candidates repo. Name the PR as `RUST | youremail`. PRs with different names will be rejected.
* Send us email or DM us on UpWork when you happy us to verify it

# How To Choose/Write Good Interview Questions

When choosing a good interview question follow these rules:

* The QA should not be too **broad** or too **obvious/trivial**, like:
  * 🚫 `What is Rust?`
* The QA should be **opened** and invite the candidate for a conversation rather than strictly test his/her/their specific knowledge. Compare:
  * 🚫 What is `enum` in Rust?
  * ✅ Provide an example when you would use `enum` in Rust 
  * ✅ What does the `static` keyword mean? Can you _override_ `private` or `static` method in Rust?
* Keep the answers **short**, **succinct** and **informative**. If you feel your answer is growing in size and covers different topics the split it!
* Avoid  highly practical questions like
  * 🚫 How to install Rust? - we won't accept that type of questions
* Don't submit questions related to a personal candidate experience. These questions are valid on an interview but won't fit to the format of FSC like:
  *  🚫 Have you ever worked with `Borsch` in Rust?
  *  🚫 Describe your experience building `SPL Tokens` using Rust on your previous job?
* Don't submit behavioral questions like:
  * 🚫 Describe your strengths and weakness, and so on
* Use that that types of questions:
  * ✅ `When to use X vs Y?`
  * ✅ `Why would you use X?`
  * ✅ `Compare X vs Y for solving Z`
  * ✅ `What types of X do you know?`
  * ✅ `Are there any problems when using X for solving Z?`
  * ✅ `Name some advantages of using X vs Y for solving Z?`
  * ✅ `Explain X to 5 yo/your grandparents`
  * ✅ `What is example of Y in real life?`
  * ✅ `Provide an intuitive explanation of X`
* The best **rule of thumb** to follow is
  * ✅ ask yourself would you use this question on a real developer/software engineer interview? If answer is "Yes" then go for it!

# Where To Find/Source Good Interview Questions

Remember, **you don't need to reinvent an interview question and the answer by yourself**. Your task is to research the best sources that are available on the Internet (blog posts, books, videos, tutorials), _combine_, _convert_ and (sometimes) _reformat_ that existing knowledge into the answer.

There is just a fraction of quality resources you can do you research on:

* stackoverflow.com - 💡 **Hint**: sort questions by Score (or Votes) in search
* github repositories (with many stars, not forks)
* gitbooks.io
* hackernoon.com
* hackr.io
* codeburst.io
* freecodecamp.org
* medium.com
* dev.com
* dzone.com
* docs.oracle.com
* docs.docker.com
* developers.google.com
* dart.dev
* brilliant.org
* blogs.msdn.microsoft.com
* blog.logrocket.com
* atlassian.com
* coderbyte.com
* etc...

💡 **Hint**: Don't blindly copy all answers from one source for the same topic. Try to find at least 2-3 source of the information and choose the best explanation **you like most**.

💡**Hint**: Search Github for programming interview questions repos that other people did. Usually they already formatted as Markdown and can get you great amount of QAS for the topic

💡**Hint**: When research on some topic look at the `Table of Content` in your favorite programming book to get a sense on what subtopics you can cover. Most of the Coursera and Udemy courses will work too!

# Resources to AVOID

⚠️ **Warning**: Don't use/copy information from the websites with bad grammar and poor QAs quality. We won't accept QAs that will be copied from poor quality resources and will reject your submission. You can recognize these sites by deficient crappy design, low quality images, tons of ads, lack of code formatting and code samples and  _no attribution to the sources of the answer_ like:

* onlineinterviewquestions.com
* geekforgeeks.com
* career.guru99.com
* educba.com
* edureka.co
* a4academics.com
* etc ...

# How To Format Interview Questions + QAS Examples

All interview questions must be formatted using those rules:

* use ONLY **Markdown** ([Github flavour](https://guides.github.com/features/mastering-markdown/))
* **Do** include images (include them as Markdown links) into your answers if they help to explain concepts you cover
* **Do** use and reformat original source of answer using **lists**, _italic_ and **bold** for better readability
* **Do** include formatting in the QA title
* **Do** format the code (see samples)

See some examples of QA formatting below. Note how to format **list**, **code**, **file names**, **terms**, **links**, QA **difficulties**, **images** and so on. To see more QA formatting examples go to [www.fullstack.cafe](www.fullstack.cafe) and explore our QAs library.

---

## Q: Why to use `lock` statement in C#?

**Difficulty:** `Junior`

**Source:**

https://stackoverflow.com/questions/6029804/how-does-lock-work-exactly

**Details**:

Provide some code example.

**Answer:**

The `lock` keyword ensures that one thread _does not enter a critical section of code_ while another thread is in the critical section. If another thread tries to enter a locked code, it will wait, block, until the object is released.

The `lock` keyword calls [`Enter`](http://msdn.microsoft.com/en-us/library/system.threading.monitor.enter.aspx) at the start of the block and [`Exit`](http://msdn.microsoft.com/en-us/library/system.threading.monitor.exit.aspx) at the end of the block. `lock` keyword actually handles [`Monitor`](http://msdn.microsoft.com/en-us/library/System.Threading.Monitor%28v=vs.110%29.aspx) class at back end.

For example:

```cs
private static readonly Object obj = new Object();

lock (obj)
{
  // critical section
}
```

---

## Q: What is the difference between `INNER JOIN` and `OUTER JOIN`?

**Difficulty**: `Junior`

**Source:**

https://github.com/chetansomani/SQL-Interview-Questions

**Answer:**

Assuming you're joining on columns with no duplicates, which is a very common case:

* An `INNER JOIN` of A and B gives the result of A intersect B, i.e. the inner part of a **Venn diagram** intersection.
* An `OUTER JOIN` of A and B gives the results of A union B, i.e. the outer parts of a **Venn diagram** union.
* A `LEFT OUTER JOIN` will give all rows in A, plus any common rows in B.
* A `RIGHT OUTER JOIN` will give all rows in B, plus any common rows in A.
* A `FULL OUTER JOIN` will give you the `union` of A and B, i.e. all the rows in A and all the rows in B. If something in A doesn't have a corresponding datum in B, then the B portion is null, and vice versa.

Consider:

![](https://i.stack.imgur.com/1UKp7.png)

# How We Asses Your Work

Look at this list of criteria that we will keep in mind when assessing your submission:

* _Variety_ and _Quality of Sources_ you have used. We hard stop and reject your candidacy if you copy/source QAs from one source or sources mentioned to AVOID
* _Markdown Formatting_ Quality - don't blindly copy answer, **RE**format it to increase _readability_, for example:
  * Use paragraphs and new lines to visually separate different parts of the answer
  * Use **bold** for terms and acronyms
  * Use **lists** to visually separate different concepts especially if they presented in one long sentence in the source
  * Use _italic_ to stress attention on critical/important _idea_ or _concepts_ or _hints_ for a reader
  * Use _italic_ in QA Title for terms and acronyms
  * Use `code` for numbers: `123`, percentages: `68%`, `file_names.md` and code `<html/>` in your answers
  * Don't write long QA _Titles_. Move additional information, problem statement or following questions to QA _Details_
* _Inclusion of Images_ is very important
* Add context for QA when needed in _Details_ section (aka _Let's say we need to deploy backend on 5000 nodes simultaneously..._)
* If you reference to some image in the answer make sure you reference it by its _visible_ ID (A, B, C, ... 1, 2, 3 and etc.)

# Useful Tools to Try

There are some awesome tools that will greatly help you along the way of content creation for FSC:

## Markdown Extractors & Chrome Extensions

* [Copycat](https://chrome.google.com/webstore/detail/copycat/jdjbiojkklnaeoanimopafmnmhldejbg) Chrome/Brave Extension
* [HTML to Markdown Converter](https://mixmark-io.github.io/turndown/)

## Markdown Editors

* VS Code + Markdown Extensions - recommended
* StackEdit.io
* [Dllinger.io](https://dillinger.io/)

## VS Extensions

* Markdown All In One
* Markdown Preview Enhanced
* Markdownlint

# I'm In! What's Next?

Great! Once getting your pull request we'll verify the content and circle back to you in no time. Then we schedule a Google Meet call and discuss your first FSC topic to work on :)
