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
  {% if page.path contains "bayesian/references" %}
    <li>
      <a href="{{ page.url | relative_url }}">
        {{ page.title | escape }}
      </a>
    </li>
  {% endif %}
{%- endfor -%}
</ul>

### Distributions
<ul>
{%- for page in pages -%}
  {% if page.path contains "bayesian/distributions" %}
    <li>
      <a href="{{ page.url | relative_url }}">
        {{ page.title | escape }}
      </a>
    </li>
  {% endif %}
{%- endfor -%}
</ul>

### Analyses
<ul>
{%- for page in pages -%}
  {% if page.path contains "bayesian/analyses" %}
    <li>
      <a href="{{ page.url | relative_url }}">
        {{ page.title | escape }}
      </a>
    </li>
  {% endif %}
{%- endfor -%}
</ul>
