---
title: "Inductive Solutions"
layout: blog
order: 1
topic: Recursion
topic_path: /docs/algorithms/recursion/index.html
---
Using inductive reasoning, we can calculate the bound on the time complexity of recurrences. For example, let's consider the recurrence of the [merge sort algorithm](/docs/algorithms/sorting/merge-sort.html). The worst case running time of merge sort $$ T(n) $$ is defined as follows.

$$
T(n) = 2T(n/2) + n
$$

Notice the recursion in this definition. The running time, $$ T(n) $$ is defined in terms of itself $$ T(n/2) $$. Let's take a guess at the upper bound of $$ T(n) $$.

$$
\\ T(n) = O(n \ \log n)
\\ T(n) \leq cn \ \log n
$$

If we evaluate the recurrence at the upper bound, the result will be an upper bound on $$ T(n) $$. If the result is mathematically consistent, we can accept our guess for $$ T(n) $$.

$$
\\ T(n) = 2T(n/2) + O(n)
\\ T(n) \leq 2(c \frac{n}{2} \ \log{\frac{n}{2}})  + n
\\ T(n) \leq (cn \ \log{\frac{n}{2}})  + n
\\ T(n) \leq cn \ \log{\frac{n}{2}}  + n
\\ T(n) \leq cn \ \log{n} - cn \ \log{2} + n
$$

Neglecting all but the largest term in this equation,

$$
\\ T(n) \leq cn \ \log{n}
$$

Notice we have proved our guess! This is the inductive method for solving the time complexity of a recurrence.