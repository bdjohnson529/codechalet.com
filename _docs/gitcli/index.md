---
title: "Git CLI"
layout: blog
link: "landing"
excerpt: "Command line Git cheat-sheets."
parent: Docs
parent_path: ''
image: git
---
Git is version control software which manages changes to files. These resources document usage of Git with the command line.

* [Git Commands](git-commands.html)


# Workflows
<ul>
{% assign topics = site.docs | where: "topic", "git-workflow" | sort: 'order' %}
{%- for page in topics -%}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
{%- endfor -%}
</ul>