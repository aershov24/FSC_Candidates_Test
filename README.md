# Welcome to MLSC Pilot Repo
Please read this document carefully before submitting your MLSC challenge

## What You Need to Do

* Fork this repository
* Carefully read the `readme.md`
* Create the `Logistic_Regression_youremail_TEST.md` file in your repo and add **3 questions and answers (QAS) relevant to Logistic Regression topic that you would ask on a real interview** if you would hire ML/DS devs for your own project. 
* Make sure you cover:
  * one simple question for Junior position, 
  * one medium difficulty question for Mid position, and 
  * one hard question for Senior position.  
We will look at this criteria when assessing your content. 

* Make sure that for all QAS you include:
  - Question Title
  - Question Description (optional) 
  - Answer + Code (if needed)
  - Link(s) to source (you don't need to write answer by yourself, just combine and research best sources that are available)
  - QA Difficulty level (entry, junior, mid, senior, expert)
* Look at the `QAS_Examples.md` file in this repo for examples of QAS Markdown file formatting. Please strictly follow these formatting conventions. That's the key to pass the challenge ;)
* Create pull request from your repo to the MLSC repo
* Send us email when you happy us to verify it

## How To Format Interview Question
All interview questions must be formated as Markdown. See the example below:

---
### Q: What are different integer data types in MySQL? How can you use unsigned integer in MySQL.

#### Difficulty Level: 
Junior

#### Source: 
https://stackoverflow.com/questions/2991405/what-is-the-difference-between-tinyint-smallint-mediumint-bigint-and-int-in-m

**Answer:**

MySQL has different INT data types with different storage requirements including **TINYINT** (1 byte) , **SMALLINT** (2 byte), **MEDIUMINT** (3 byte), **INT** (4 byte) and **BIGINT** (8 byte). All the INT types can be used as signed or unsigned. You can write UNSIGNED after data type to tell if it is unsigned. 

For example below command will create a *Student* table which can have mark as unsigned **SMALLINT** value.
```SQL
CREATE TABLE `Student`(
`name` VARCHAR(25) NOT NULL, 
`marks` SMALLINT UNSIGNED);
```

---

## Where To Find ML Interview Questions

## Good and Bad Interview Questions

