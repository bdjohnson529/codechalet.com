---
title: "Serverless email notification system"
layout: blog
topic: AWS
topic_path: /docs/aws/index.html
image: aws
---
This guide explains how to build an email notification system for a static website, using serverless resources such **Lambda** and **API Gateway**.

<ul>
{% assign pages = site.docs | sort: 'order' %}
{%- for page in pages -%}
  {% if page.path contains "aws/tutorials" %}
    {% unless page.path contains "index.md" or page.path contains "html-forms" or page.path contains "sample-authorization-function" %}
      <li>
        <a href="{{ page.url | relative_url }}">
          {{ page.title | escape }}
        </a>
      </li>
    {% endunless %}
  {% endif %}
{%- endfor -%}
</ul>