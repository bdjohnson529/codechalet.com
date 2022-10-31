---
title: "Analytics"
layout: blog
link: "landing"
topic: Analytics Engineering
topic_path: /docs/analytics-engineering/index.html
image: analytics
---
{% assign pages = site.docs | sort: 'order' %}

Notes from building analytics platforms.

### Data Engineering
<ul>
{%- for page in pages -%}
  {% if page.path contains "analytics-engineering/data-engineering" %}
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
  {% if page.path contains "analytics-engineering/databricks" %}
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
  {% if page.path contains "analytics-engineering/airflow" %}
    <li>
      <a href="{{ page.url | relative_url }}">
        {{ page.title | escape }}
      </a>
    </li>
  {% endif %}
{%- endfor -%}
</ul>