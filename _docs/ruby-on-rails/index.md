---
title: "Ruby on Rails"
layout: blog
link: "landing"
topic: Ruby on Rails
topic_path: /docs/ruby-on-rails/index.html
image: rails
---
{% assign pages = site.docs | sort: 'order' %}

Tested on Rails v6.1.3, using Ruby v2.6.7.

<ul>
{%- for page in pages -%}
  {% if page.path contains "ruby-on-rails" %}
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