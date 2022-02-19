---
title: "Dynamic Programming"
layout: blog
order: 6
topic: Algorithms
topic_path: /docs/algorithms/index.html
---
Dynamic programming uses recursion to solve problems.

<ul>
{%- for page in pages -%}
  {% if page.path contains "algorithms/recursion/" %}
    {% unless page.path contains "algorithms/recursion/index.md" %}
      <li>
        <a href="{{ page.url | relative_url }}">
          {{ page.title | escape }}
        </a>
      </li>
    {% endunless" %}
  {% endif %}
{%- endfor -%}
</ul>