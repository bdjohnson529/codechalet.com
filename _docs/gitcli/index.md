---
title: "Git CLI"
layout: blog
link: "landing"
topic: Git CLI
topic_path: /docs/gitcli/index.html
image: git
---
{% assign pages = site.docs | sort: 'order' %}

Git is version control software which manages changes to files. These resources document usage of Git with the command line.

* [Git Commands](git-commands.html)


# Workflows
<ul>
{%- for page in pages -%}
  {% if page.path contains "gitcli/workflow" %}
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