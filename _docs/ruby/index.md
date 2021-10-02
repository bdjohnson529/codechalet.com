---
title: "Ruby"
layout: blog
link: "landing"
topic: Ruby
topic_path: /docs/ruby/index.html
image: ruby
---
{% assign pages = site.docs | sort: 'order' %}

There are many great sites out there for learning Ruby. Some of my favorites are :
* [docs.ruby-lang.org](https://docs.ruby-lang.org/en/2.4.0/)
* [The Koans](http://rubykoans.com)

## Installation
<ul>
{%- for page in pages -%}
  {% if page.path contains "ruby/installation" %}
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

## Ruby Notes
These are some of my notes from learning and practicing Ruby.

<ul>
{%- for page in pages -%}
  {% if page.path contains "ruby/ruby-syntax" %}
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


## Ruby on Rails
Tested on Rails v6.1.3, using Ruby v2.6.7.

<ul>
{%- for page in pages -%}
  {% if page.path contains "ruby/ruby-on-rails" %}
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