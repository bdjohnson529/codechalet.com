---
title: "Kubernetes"
layout: blog
link: "landing"
topic: Kubernetes
topic_path: /docs/kubernetes/index.html
image: kubernetes
---
{% assign pages = site.docs | sort: 'order' %}

Kubernetes uses manifests to orchestrate pods.


#### Deploy

<ul>
{%- for page in pages -%}
  {% if page.path contains "kubernetes/deploy" %}
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


#### Networking

<ul>
{%- for page in pages -%}
  {% if page.path contains "kubernetes/networking" %}
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
