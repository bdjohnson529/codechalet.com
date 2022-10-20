---
title: "Kubernetes"
layout: blog
link: "landing"
topic: Kubernetes
topic_path: /docs/kubernetes/index.html
image: kubernetes
---
{% assign pages = site.docs | sort: 'order' %}

Kubernetes uses manifests to define the docker application.

<ul>
{%- for page in pages -%}
  {% if page.path contains "docs/kubernetes" %}
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


## Links
* [Exposing an External IP Address to Access an Application in a Cluster](https://kubernetes.io/docs/tutorials/stateless-application/expose-external-ip-address/)