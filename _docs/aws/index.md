---
title: "Go Serverless"
layout: blog
link: "landing"
topic: AWS
topic_path: /docs/aws/index.html
image: aws
---

<br>

## It's cheap!

<br>
With a serverless architecture, you only pay for the resources you use. Go serverless and save money!




## Serverless Architectures

<ul>
{% assign pages = site.docs | sort: 'order' %}
{%- for page in pages -%}
  {% if page.path contains "aws/tutorials/index" %}
    <li>
      <a href="{{ page.url | relative_url }}">
        {{ page.title | escape }}
      </a>
    </li>
  {% endif %}
{%- endfor -%}
</ul>