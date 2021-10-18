---
title: "AWS"
layout: blog
link: "landing"
topic: AWS
topic_path: /docs/aws/index.html
image: aws
---
{% assign pages = site.docs | sort: 'order' %}

Deploy static websites on AWS, it's cheap! Combined with some serverless concepts, and it is possible to create a powerful ecommerce website.

<ul>
{%- for page in pages -%}
  {% if page.path contains "aws" %}
    {% unless page.path contains "index.md" or page.path contains "references.md" or page.path contains "sample-authorization-function" %}
      <li>
        <a href="{{ page.url | relative_url }}">
          {{ page.title | escape }}
        </a>
      </li>
    {% endunless %}
  {% endif %}
{%- endfor -%}
</ul>