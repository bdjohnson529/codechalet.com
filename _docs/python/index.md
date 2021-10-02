---
title: "Python"
layout: blog
link: "landing"
topic: Python
topic_path: /docs/python/index.html
image: python
---
{% assign pages = site.docs | sort: 'order' %}

These are some notes from learning and teaching Python.


## Python Paradigms
<ul>
{%- for page in pages -%}
  {% if page.path contains "python/paradigms" %}
    {% unless page.path contains "index.md" %}
      <li>
        <a href="{{ page.url | relative_url }}">
          {{ page.title | escape }}
        </a>
      </li>
    {% endunless %}
  {% endif %}
{%- endfor -%}
</ul>

## Data Engineering
<ul>
{%- for page in pages -%}
  {% if page.path contains "python/data-engineering" %}
    {% unless page.path contains "index.md" %}
      <li>
        <a href="{{ page.url | relative_url }}">
          {{ page.title | escape }}
        </a>
      </li>
    {% endunless %}
  {% endif %}
{%- endfor -%}
</ul>

## Flask
<ul>
{%- for page in pages -%}
  {% if page.path contains "python/flask" %}
    {% unless page.path contains "index.md" %}
      <li>
        <a href="{{ page.url | relative_url }}">
          {{ page.title | escape }}
        </a>
      </li>
    {% endunless %}
  {% endif %}
{%- endfor -%}
</ul>