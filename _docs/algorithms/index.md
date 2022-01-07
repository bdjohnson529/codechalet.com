---
title: "Algorithms"
layout: blog
link: "landing"
topic: Algorithms
topic_path: /docs/algorithms/index.html
image: algorithms
---
{% assign pages = site.docs | sort: 'order' %}

Common algorithms for learning and practicing computer science.


##### Sort Algorithms
<ul>
{%- for page in pages -%}
  {% if page.path contains "algorithms/sort_algorithms" %}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
  {% endif %}
{%- endfor -%}
</ul>

##### Data Structures
<ul>
{%- for page in pages -%}
  {% if page.path contains "algorithms/data_structures" %}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
  {% endif %}
{%- endfor -%}
</ul>

##### Practice Problems
<ul>
{%- for page in pages -%}
  {% if page.path contains "algorithms/problems" %}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
  {% endif %}
{%- endfor -%}
</ul>
