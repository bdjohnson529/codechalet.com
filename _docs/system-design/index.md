---
title: "System Design"
layout: blog
link: "landing"
topic: System Design
topic_path: /docs/system-design/index.html
image: design
---

<ul>
{% assign pages = site.docs | sort: 'order' %}
{%- for page in pages -%}
  {% if page.path contains "design/" %}
    {% unless page.path contains "design/index.md" %}
      <li>
        <a href="{{ page.url | relative_url }}">
          {{ page.title | escape }}
        </a>
      </li>
    {% endunless %}
  {% endif %}
{%- endfor -%}
</ul>