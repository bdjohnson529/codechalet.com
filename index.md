---
layout: blog
---
# Welcome to Code Chalet!


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