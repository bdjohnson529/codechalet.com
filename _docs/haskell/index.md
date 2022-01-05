---
title: "Haskell"
layout: blog
link: "landing"
topic: Haskell
topic_path: /docs/haskell/index.html
image: haskell
---
{% assign pages = site.docs | sort: 'order' %}

Notes from learning Haskell.

# Guides
<ul>
{%- for page in pages -%}
  {% if page.path contains "haskell/guides" %}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
  {% endif %}
{%- endfor -%}
</ul>
