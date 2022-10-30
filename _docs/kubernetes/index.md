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


## CKAD Notes
Notes from studying for Certified Kubernetes Application Developer exam. I used [this Udemy course](https://www.udemy.com/course/certified-kubernetes-application-developer).

<ul>
{%- for page in pages -%}
  {% if page.path contains "kubernetes/ckad" %}
    <li>
      <a href="{{ page.url | relative_url }}">
        {{ page.title | escape }}
      </a>
    </li>
  {% endif %}
{%- endfor -%}
</ul>

## Commands

<ul>
{%- for page in pages -%}
  {% if page.path contains "kubernetes/commands" %}
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


## Networking

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


## Links
* [Exposing an External IP Address to Access an Application in a Cluster](https://kubernetes.io/docs/tutorials/stateless-application/expose-external-ip-address/)