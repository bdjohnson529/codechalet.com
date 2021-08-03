---
title: "Ruby"
layout: blog
link: "landing"
parent: Docs
parent_path: ''
image: ruby
---
There are many great sites out there for learning Ruby. Some of my favorites are :
* [docs.ruby-lang.org](https://docs.ruby-lang.org/en/2.4.0/)
* [The Koans](http://rubykoans.com)

## Installation
<ul>
  {% assign topics = site.docs | where: "topic", "ruby-installation" %}
  {%- for page in topics -%}
  <li>
    <a href="{{ page.url | relative_url }}">{{ page.title | escape }}</a>
  </li>
  {%- endfor -%}
</ul>

## Ruby Notes
These are some of my notes from learning and practicing Ruby.

<ul>
{% assign topics = site.docs | where: "topic", "ruby-syntax" | sort: 'order' %}
{%- for page in topics -%}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
{%- endfor -%}
</ul>


## Ruby on Rails
Tested on Rails v6.1.3, using Ruby v2.6.7.

<ul>
{% assign topics = site.docs | where: "topic", "ruby-on-rails" | sort: 'order' %}
{%- for page in topics -%}
  <li>
    <a href="{{ page.url | relative_url }}">
      {{ page.title | escape }}
    </a>
  </li>
{%- endfor -%}
</ul>