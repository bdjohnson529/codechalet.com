---
title: "Windows"
layout: blog
link: "landing"
topic: Windows
topic_path: /docs/windows/index.html
image: windows
---
{% assign pages = site.docs | sort: 'order' %}

Notes from configuring Windows for software development.

## Windows
* [Windows context menu](context-menu.html)
* [Resource logging](resource-logging.html)
* [Netsh Commands](netsh-commands.html)

## Windows Subsystem for Linux
* [Introduction](wsl.html)
* [SSH Keys](ssh-keys.html)
* [Sublime](wsl-sublime.html)


## Sublime
<ul>
{%- for page in pages -%}
  {% if page.path contains "windows/sublime" %}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
  {% endif %}
{%- endfor -%}
</ul>
