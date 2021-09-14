---
layout: blog
---
# Welcome to Code Chalet!

This site contains resources about different software engineering topics. To start, click a topic which interests you. Some personal favorites are the [Python](/docs/python/) tutorials and the [Git](http://localhost:4000/docs/gitcli/index.html) cheat sheets.

<br>

<div class="row">
  {% assign topics = site.docs | where: "link", "landing" | sort: "title" %}
  {% for page in topics %}
  <div class="py-2">
    <div class="col-lg-4">
      <span>
        <a href="{{ page.url | relative_url }}">
          <img src="{{ site.baseurl }}/assets/img/docs/{{ page.image }}.png" alt="Project image" width="140" height="140">
        </a>
      </span>
    </div>
  </div>
  {%- endfor -%}
</div>