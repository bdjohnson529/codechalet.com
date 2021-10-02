---
title: "What is data engineering?"
layout: blog
order: 0
topic: Python
topic_path: /docs/python/index.html
---
At its core, data engineering is organizing datasets so they can be consumed by software. Don't let this simple definition fool you - data engineering is a sometimes Herculean effort which can involve lots of tedious programming. Data engineering is the older, less attractive relative of data science; if you ask programmers and analysts how they would like to spend their time they will probably tell you about building machine learning models, rather than organizing massive datasets.


However, data engineering is absolutely necessary and in my opinion, is one of the greatest sources of technical value within a company. Python is a wonderful tool for data engineering - packages like Pandas and Numpy are capable of impressive dataset transformations, and Python's intuitive syntax means that programmers without much Python experience can quickly get up to speed.

This site documents some of the data engineering frameworks conceived by myself and my teammates. Our team was faced with a challenge which should be familiar to many analytics teams; we had an existing data engineering pipeline which was ingesting a massive amount of customer data, and which was also a nightmare to maintain. We refactored our existing data engineering pipeline into Python and have found the rewards to be massive - the downtime of our analytics tools has plummeted and we have increased contributions per week (measured by pull requests) by over 10X.

Our data is stored in SQL Server databases; I will share excerpts of SQL and Python code to demonstrate some key concepts. The concepts can be applied to other databases and programming languages - they are concepts fundamental to the problem of data engineering.