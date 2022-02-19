---
title: "Dynamic Programming"
layout: blog
order: 6
topic: Algorithms
topic_path: /docs/algorithms/index.html
---
{% assign pages = site.docs | sort: 'order' %}

Dynamic programming uses recursion to solve problems.

### Topics
<ul>
{%- for page in pages -%}
  {% if page.path contains "algorithms/recursion/" %}
    {% unless page.path contains "algorithms/recursion/index.md" or page.path contains "recursion/problems" %}
      <li>
        <a href="{{ page.url | relative_url }}">
          {{ page.title | escape }}
        </a>
      </li>
    {% endunless" %}
  {% endif %}
{%- endfor -%}
</ul>

### CCI - Chapter 8
Problems are taken from [Cracking the Coding Interview.](https://www.amazon.com/Cracking-Coding-Interview-Programming-Questions/dp/0984782850)

<ul>
{%- for page in pages -%}
  {% if page.path contains "algorithms/recursion/problems" %}
    <li>
      <a href="{{ page.url | relative_url }}">
        {{ page.title | escape }}
      </a>
    </li>
  {% endif %}
{%- endfor -%}
</ul>
