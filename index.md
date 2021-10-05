---
layout: home
---
# Welcome to Code Chalet!
This site contains resources about different software engineering topics. To start, click a topic which interests you. Some personal favorites are the [Python](/docs/python/index.html) tutorials and the [Git](/docs/gitcli/index.html) cheat sheets.


{% include navpill.html %}

<br>

<div class="row">
  {% assign topics = site.docs | where: "link", "landing" | sort: "title" %}
  {% for page in topics %}
    <div class="col-lg-4 topic" id="{{ page.topic }}">
      <span>
        <a href="{{ page.url | relative_url }}">
          <img src="{{ site.baseurl }}/assets/img/docs/{{ page.image }}.png" alt="Project image" width="140" height="140">
        </a>
      </span>
    </div>
  {% endfor %}
</div>