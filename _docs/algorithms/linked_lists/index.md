---
title: "Linked Lists"
layout: blog
order: 1
topic: Algorithms
topic_path: /docs/algorithms/index.html
---
{% assign pages = site.docs | sort: 'order' %}


#### CCI - Chapter 2
Problems are taken from [Cracking the Coding Interview.](https://www.amazon.com/Cracking-Coding-Interview-Programming-Questions/dp/0984782850)

<ul>
{%- for page in pages -%}
  {% if page.path contains "linked_lists/problems/2_" %}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
  {% endif %}
{%- endfor -%}
</ul>


#### CCI - Chapter 3
Problems are taken from [Cracking the Coding Interview.](https://www.amazon.com/Cracking-Coding-Interview-Programming-Questions/dp/0984782850)

<ul>
{%- for page in pages -%}
  {% if page.path contains "linked_lists/problems/3_" %}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
  {% endif %}
{%- endfor -%}
</ul>