---
title: "Python"
layout: blog
link: "landing"
parent: Docs
parent_path: ''
image: python
---
These are some notes from learning and teaching Python.


## Python Paradigms
<ul>
{% assign topics = site.docs | where: "topic", "python-paradigms" | sort: 'order' %}
{%- for page in topics -%}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
{%- endfor -%}
</ul>

## Data Engineering
<ul>
{% assign topics = site.docs | where: "topic", "data-engineering" | sort: 'order' %}
{%- for page in topics -%}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
{%- endfor -%}
</ul>

## Flask
<ul>
{% assign topics = site.docs | where: "topic", "flask" | sort: 'order' %}
{%- for page in topics -%}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
{%- endfor -%}
</ul>