---
title: "Binary Search"
layout: blog
order: 6
topic: Sort
topic_path: /docs/algorithms/sorting/index.html
---
A binary search takes a sorted array, and searches by dividing the array in half. For example, take the sorted array
```
{1,5,8,9,11,13,15,19,21}
```
To search for the number 8, we could implement our own binary search. First we check in the element at the midpoint, `11`. Since `9` is less than `11`, we will take the the first half of the array, and once again divide this array in half.

The steps would look as follows
```
{1,5,8,9,11,13,15,19,21}
{1,5,8,9}
{8,9}
{9}
```

In an array with `N` elements, the worst case scenario is that we would have to continue dividing the array until we arrive at an array with one element. We can write this as a sum
```
N + ... + 4 + 2 + 1
```

The final term in the sum can be written as
```
N = 2^k
```

Notice that there are also `k` terms in the sum. The previous equation can be rewritten as
```
k = log(N)
```

Therefore, in the worst case, a binary search has a time complexity of `O log(N)`.