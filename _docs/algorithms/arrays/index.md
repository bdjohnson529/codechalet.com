---
title: "Arrays and Strings"
layout: blog
order: 0
topic: Algorithms
topic_path: /docs/algorithms/index.html
---
{% assign pages = site.docs | sort: 'order' %}

One type of problem asks that you to reduce the array or string into a smaller set or a single value. Another type of problem asks that you compare two strings or arrays. Remember that an array or string is represented mathematically as a set, and most problems are asking you to reduce that set into a smaller set (or a single value.)

When evaluating time complexity, keep in mind the time complexity of the following operations:

* sorting an array - $$ O(n \ log \ n) $$
* iterating through an array -  $$ O(n) $$

#### CCI - Chapter 1
Problems are taken from [Cracking the Coding Interview.](https://www.amazon.com/Cracking-Coding-Interview-Programming-Questions/dp/0984782850)

<ul>
{%- for page in pages -%}
  {% if page.path contains "arrays/problems/" %}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
  {% endif %}
{%- endfor -%}
</ul>