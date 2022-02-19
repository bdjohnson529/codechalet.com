---
title: "Algorithms"
layout: blog
link: "landing"
topic: Algorithms
topic_path: /docs/algorithms/index.html
image: algorithms
---
{% assign pages = site.docs | sort: 'order' %}

I use [Introduction to Algorithms](https://en.wikipedia.org/wiki/Introduction_to_Algorithms), and [Cracking the Coding Interview](https://www.amazon.com/Cracking-Coding-Interview-Programming-Questions/dp/0984782850) as references.


<ul>
{%- for page in pages -%}
  {% if page.path contains "algorithms/" and page.path contains "index.md" %}
    {% unless page.path contains "algorithms/index.md" %}
      <li>
        <a href="{{ page.url | relative_url }}">
          {{ page.title | escape }}
        </a>
      </li>
    {% endunless %}
  {% endif %}
{%- endfor -%}
</ul>
