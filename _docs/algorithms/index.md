---
title: "Algorithms"
layout: blog
link: "landing"
parent: Docs
parent_path: ''
image: algorithms
---
Common algorithms for learning and practicing computer science.

## Concepts
<ul>
{% assign topics = site.docs | where: "topic", "algorithm-concepts" | sort: 'order' %}
{%- for page in topics -%}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
{%- endfor -%}
</ul>

## Problems
<ul>
{% assign topics = site.docs | where: "topic", "algorithm-problems" | sort: 'order' %}
{%- for page in topics -%}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
{%- endfor -%}
</ul>