---
title: "Algorithms"
layout: blog
link: "landing"
topic: Algorithms
topic_path: /docs/algorithms/index.html
image: algorithms
---
{% assign pages = site.docs | sort: 'order' %}

Algorithms for learning and practicing computer science. I use [Introduction to Algorithms](https://en.wikipedia.org/wiki/Introduction_to_Algorithms), by Cormen, as a reference.


##### Mathematics
<ul>
{%- for page in pages -%}
  {% if page.path contains "algorithms/mathematics" %}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
  {% endif %}
{%- endfor -%}
</ul>

##### Sort
<ul>
{%- for page in pages -%}
  {% if page.path contains "algorithms/sort" %}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
  {% endif %}
{%- endfor -%}
</ul>

##### Search
<ul>
{%- for page in pages -%}
  {% if page.path contains "algorithms/search" %}
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
