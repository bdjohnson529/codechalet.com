---
title: "Dynamic Arrays"
layout: blog
order: 1
topic: Algorithms
topic_path: /docs/algorithms/index.html
---
What is the time complexity of adding an element to a dynamic array? A dynamic array allocates space based on the number of elements in the array. Each time the array reaches capacity, the array contents are copied to a new array with twice as many elements.

The array might be initialized with 2 bytes. Once two bytes are added to the array, the array size will double to four bytes. Once the array reaches capacity again, these 4 bytes will be copied over to a new array, allocated with 8 bytes.

After adding `X` elements to the array, the array will have made copies of itself a certain number of times. If you add up the copies which are made during each resizing, you would get the following sum
```
1 + 2 + 4 + 8 + 16 ... X
```
The sum can be rewritten
```
X + X/2 + X/4 + X/8 + ... + 1
```
This sum converges to `2X`. Adding `X` elements to the array would take roughly `2X` time. We are usually only concerned with the order of the polynomial, and this algorithm has a time complexity of `O(X)`.