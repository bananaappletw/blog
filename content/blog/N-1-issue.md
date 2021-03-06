---
title: N+1 issue
author: bananaapple
tags:
- database
categories:
- computer science
date: 2016-12-05T14:32:00.000+00:00

---
# Introduction

比如說你現在有兩個 Database Models

一個是 Cars 另一個是 Wheels

他們的關係會是 one to many

一台車會有多個輪子

每個輪子都會有一個 column: car_id 指向一台車

那比如說我今天想要得到每台車的資訊和每台車有多少個輪子

假設資料庫裡有 **N** 台車

先搜尋所有的車 (query count: **1**)

    SELECT * FROM Cars;

在對每台車搜尋所擁有的輪子 (query count: **N**)

    SELECT * FROM Wheels WHERE car_id = ?;

總共的 Query 數是 **N+1**

那解決的方法就是

    SELECT * FROM Cars;

    SELECT * FROM Wheels;

就能把原本的 Query 數 **N+1** 縮減到 **2**

# Reference

* [stack overflow](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-issue)
* [google search](https://secure.phabricator.com/book/phabcontrib/article/n_plus_one/)