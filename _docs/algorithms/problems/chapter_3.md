---
title: "Chapter 3"
layout: blog
order: 1
topic: Algorithms
topic_path: /docs/algorithms/index.html
---
{% assign pages = site.docs | sort: 'order' %}

When evaluating time complexity, keep in mind the time complexity of the following operations:

* sorting an array - $$ O(n \ log \ n) $$
* iterating through an array -  $$ O(n) $$

#### Stacks and Queues
<ul>
{%- for page in pages -%}
  {% if page.path contains "problems/solutions/3_" %}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
  {% endif %}
{%- endfor -%}
</ul>