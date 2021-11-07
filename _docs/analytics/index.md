---
title: "Analytics"
layout: blog
link: "landing"
topic: Analytics
topic_path: /docs/analytics/index.html
image: analytics
---
{% assign pages = site.docs | sort: 'order' %}

Notes from building analytics platforms.

### Data Engineering
<ul>
{%- for page in pages -%}
  {% if page.path contains "analytics/data-engineering" %}
    <li>
      <a href="{{ page.url | relative_url }}">
        {{ page.title | escape }}
      </a>
    </li>
  {% endif %}
{%- endfor -%}
</ul>

### Databricks
<ul>
{%- for page in pages -%}
  {% if page.path contains "analytics/databricks" %}
    <li>
      <a href="{{ page.url | relative_url }}">
        {{ page.title | escape }}
      </a>
    </li>
  {% endif %}
{%- endfor -%}
</ul>

### Airflow
<ul>
{%- for page in pages -%}
  {% if page.path contains "analytics/airflow" %}
    <li>
      <a href="{{ page.url | relative_url }}">
        {{ page.title | escape }}
      </a>
    </li>
  {% endif %}
{%- endfor -%}
</ul>