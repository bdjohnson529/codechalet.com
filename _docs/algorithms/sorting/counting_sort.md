---
title: "Counting Sort"
layout: blog
order: 5
topic: Algorithms
topic_path: /docs/algorithms/index.html
---
Sorting algorithms take an unsorted sequence as an input, and generate a sorted sequence as an output. Counting sort works by counting the occurences of each value in the input sequence, and calculating the number of elements which are less than a given element $$ x $$. If there are 5 elements smaller than $$ x $$, then $$ x $$ belongs in the sixth position in the sorted sequence.

Counting sort works for integer arrays, where we know the maximum value.

```python
def counting_sort(A: list, k: int) -> list:
    """Sorts an unsorted array.
    """
    C = [0] * k
    B = [None] * len(A)

    for j in range(len(A)):
        C[A[j] - 1] += 1

    for i in range(1, k):
        C[i] = C[i] + C[i-1]

    j = len(A) - 1

    while(j>=0):
        B[C[A[j] - 1] - 1] = A[j]
        C[A[j] - 1] -= 1

        j -= 1

    return B
```

## Execution Time
Counting sort does not sort in place - the algorithm creates a new data structure which is not of constant size. The array `C` stores the counts of the integers, and initializing this array takes time $$ O(k) $$. The `for` loop which populates `C` iterates through all elements of the input array, and therefore takes time $$ O(n) $$. The second `for` loop, which aggregates the counts in `C`, takes time $$ O(k) $$.

The last `while` loop iterates through the elements of `A` and takes time $$ O(n) $$. The total execution time of counting sort is

$$
\\ T(n) = O(k) + O(n) + O(k) + O(n)
\\ T(n) = 2(O(k) + O(n))
$$

The number of unique elements in the sequence, `k`, is going to be less than the size of the sequence. We can create a bound on the execution time by noting that $$ k < n $$.

$$
\\ T(n) \leq 2(O(n) + O(n))
$$

Neglecting the coefficients, we can see that the execution time of counting sort is

$$
\\ T(n) \leq O(n)
$$
