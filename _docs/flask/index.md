---
title: "Flask"
layout: blog
link: "landing"
excerpt: "Design patterns for Flask."
topic: Flask
topic_path: /docs/flask/index.html
image: flask
---
{% assign pages = site.docs | sort: 'order' %}

Flask is a Python framework for building web applications.

### Introduction
<ul>
{%- for page in pages -%}
  {% if page.path contains "flask/introduction" %}
    <li>
      <a href="{{ page.url | relative_url }}">
        {{ page.title | escape }}
      </a>
    </li>
  {% endif %}
{%- endfor -%}
</ul>

### Development
<ul>
{%- for page in pages -%}
  {% if page.path contains "flask/development" %}
    <li>
      <a href="{{ page.url | relative_url }}">
        {{ page.title | escape }}
      </a>
    </li>
  {% endif %}
{%- endfor -%}
</ul>

### Deployment
<ul>
{%- for page in pages -%}
  {% if page.path contains "flask/deployment" %}
    <li>
      <a href="{{ page.url | relative_url }}">
        {{ page.title | escape }}
      </a>
    </li>
  {% endif %}
{%- endfor -%}
</ul>


## Further Reading
* [External References](references.html)
