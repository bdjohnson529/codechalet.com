---
title:  "var, let and const"
layout: blog
order: 0
topic: Javascript
topic_path: /docs/javascript/index.html
---

Javascript ES6 was released in 2015, and introduced several new concepts to Javascript. ES6 introduced *let* and *const* object declarations, to accompany the existing *var* declaration. There are slight differences between variables declared using *var*, *let*, and *const*.

## var, let and const

**var** declarations are either globally scoped, or locally scoped within a function. Variables declared using **var** are mutable objects, meaning the value can be changed after the variable is initialized. **const** creates an immutable object, which cannot be updated. There is a slight nuance here. The **const** object itself is immutable, but its properties can be changed.

When you declare a variable in Javascript, the variable is actually initialized at the top of its scope. If the variable is scoped within a function, it is initialized at the top of the function. If the variable is scoped globally within a file, it is intiialized at the top of the file. This mechanism is called *hoisting*. **let**, **var** and **const** objects are all hoisted. When **var** objects are hoisted, they are simply initialized, but when **let** and **const** objects are hoisted, they are fully defined.

The implementation of *var* can lead to some bugs. Global and local variables can share the same name, leading to local variables overwriting the value of the global variables. *let*, however, will create two different objects when a variable is defined with the same name in two different scopes.


## Further Reading

- [Var, Let, and Const – What's the Difference?](https://www.freecodecamp.org/news/var-let-and-const-whats-the-difference/#:~:text=var%20declarations%20are%20globally%20scoped%20or%20function%20scoped%20while%20let,be%20updated%20nor%20re%2Ddeclared.)