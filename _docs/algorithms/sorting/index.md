---
title: "Sort and Search"
layout: blog
order: 4
topic: Algorithms
topic_path: /docs/algorithms/index.html
---
{% assign pages = site.docs | sort: 'order' %}

Sorting and searching algorithms.

<ul>
{%- for page in pages -%}
  {% if page.path contains "algorithms/sorting/" %}
    {% unless page.path contains "algorithms/sorting/index.md" %}
      <li>
        <a href="{{ page.url | relative_url }}">
          {{ page.title | escape }}
        </a>
      </li>
    {% endunless" %}
  {% endif %}
{%- endfor -%}
</ul>