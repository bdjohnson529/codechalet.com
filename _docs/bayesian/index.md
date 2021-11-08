---
title: "Bayesian Statistics"
layout: blog
link: "landing"
topic: Bayesian Statistics
topic_path: /docs/bayesian/index.html
image: bayesian
---
{% assign pages = site.docs | sort: 'order' %}

Notes from learning Bayesian Statistics.

<ul>
{%- for page in pages -%}
  {% if page.path contains "bayesian" %}
    {% unless page.path contains "index" or page.path contains "/r" %}
      <li>
        <a href="{{ page.url | relative_url }}">
          {{ page.title | escape }}
        </a>
      </li>
    {% endunless %}
  {% endif %}
{%- endfor -%}
</ul>

# R
Notes from learning R.
<ul>
{%- for page in pages -%}
  {% if page.path contains "bayesian/r" %}
    <li>
      <a href="{{ page.url | relative_url }}">
        {{ page.title | escape }}
      </a>
    </li>
  {% endif %}
{%- endfor -%}
</ul>
