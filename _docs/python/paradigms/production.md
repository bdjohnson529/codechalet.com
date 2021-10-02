---
layout: blog
title:  "Cross Platform Python"
order: 1
topic: Python
topic_path: /docs/python/index.html
---
Python evolves at a rapid pace. This is one reason it is especially important to specify the version of each module, when deploying an application to production. There are also ways of writing Python which make them compatible across different versions of Python.

## Cross Platform Syntax
Python3 created f-strings. F-strings do not work on Python2. When possible, create strings in other ways. For example, when writing print statements, combine strings and variables with a comma.
```python
print("The time is ", time)
```