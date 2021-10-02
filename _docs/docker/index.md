---
title: "Docker"
layout: blog
link: "landing"
topic: Docker
topic_path: /docs/docker/index.html
image: docker
---
{% assign pages = site.docs | sort: 'order' %}

Docker generates an image of our app, making it easier to deploy. Tested with Docker installed on WSL2.

<ul>
{%- for page in pages -%}
  {% if page.path contains "docker" %}
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


## External Resources
* [Docker connection refused](https://pythonspeed.com/articles/docker-connection-refused/)