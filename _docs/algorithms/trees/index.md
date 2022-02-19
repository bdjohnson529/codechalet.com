---
title: "Trees and Graphs"
layout: blog
order: 2
topic: Algorithms
topic_path: /docs/algorithms/index.html
---
{% assign pages = site.docs | sort: 'order' %}

More on trees, graphs and traversals.

<ul>
{%- for page in pages -%}
  {% if page.path contains "trees/traversals/" %}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
  {% endif %}
{%- endfor -%}
</ul>


#### CCI - Chapter 4
Practice problems taken from [Cracking the Coding Interview.](https://www.amazon.com/Cracking-Coding-Interview-Programming-Questions/dp/0984782850)

<ul>
{%- for page in pages -%}
  {% if page.path contains "trees/problems/" %}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
  {% endif %}
{%- endfor -%}
</ul>