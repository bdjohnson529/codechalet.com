---
title: "Databases"
layout: blog
link: "landing"
topic: Databases
topic_path: /docs/databases/index.html
image: database
---
{% assign pages = site.docs | sort: 'order' %}

Notes from configuring and deploying databases on the Windows Subsystem for Linux.

## Postgres
<ul>
{%- for page in pages -%}
  {% if page.path contains "databases/postgres" %}
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

## Other
<ul>
{%- for page in pages -%}
  {% if page.path contains "databases" %}
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