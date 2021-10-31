---
layout: blog
title:  "Unit Testing"
order: 0
topic: Python
topic_path: /docs/python/index.html
---
Python has its own [unit testing framework](https://docs.python.org/3/library/unittest.html), consisting of [assertions](https://docs.python.org/3/library/unittest.html#assert-methods) which can be used to test the validity of Python code. The basic unit of testing, a test case, is a section of code which is executed and returns a value. The return value of the test case is evaluated against an expected value; if the return value equals the expected value, the test case passes. However, if the return value differs from the expected value, the test case fails.