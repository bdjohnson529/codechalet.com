---
title: "Terraform"
layout: blog
link: "landing"
topic: Terraform
topic_path: /docs/terraform/index.html
image: design
---
{% assign pages = site.docs | sort: 'order' %}

Terraform is an infrastructure tool which can be used to represent resources through code.

<ul>
{%- for page in pages -%}
  {% if page.path contains "docs/terraform" %}
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