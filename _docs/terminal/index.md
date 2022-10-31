---
title: "Terminal"
layout: blog
link: "landing"
topic: Terminal
topic_path: /docs/terminal/index.html
image: git
---
{% assign pages = site.docs | sort: 'order' %}

The terminal is the most direct way of interacting with a computer.

<ul>
{%- for page in pages -%}
  {% if page.path contains "terminal/config" %}
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