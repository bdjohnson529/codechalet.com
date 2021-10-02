---
title: "Javascript"
layout: blog
link: "landing"
topic: Javascript
topic_path: /docs/javascript/index.html
image: javascript
---
{% assign pages = site.docs | sort: 'order' %}

These are my notes from learning Javascript.

<ul>
{%- for page in pages -%}
  {% if page.path contains "javascript" %}
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