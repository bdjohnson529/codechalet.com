---
title: "Chapter 4"
layout: blog
order: 3
topic: Algorithms
topic_path: /docs/algorithms/index.html
---
{% assign pages = site.docs | sort: 'order' %}

When evaluating time complexity, keep in mind the time complexity of the following operations:

* sorting an array - $$ O(n \ log \ n) $$
* iterating through an array -  $$ O(n) $$

#### Trees and Graphs
<ul>
{%- for page in pages -%}
  {% if page.path contains "problems/solutions/4_" %}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
  {% endif %}
{%- endfor -%}
</ul>