---
layout: home
---
# Welcome to Code Chalet!
This site is a library for different software engineering topics. To start, click a topic which interests you.

<br>


<div class="row">
  <div class="col">

  {% for category in site.data.settings %}
  <h3>{{ category[0] }}</h3>

  <ul>
    {% for topic in category[1] %}
    {% assign path = topic | downcase | replace: " ", "-" %}
    <li>
        <a href="{{ site.baseurl }}/docs/{{ topic | downcase | replace: ' ', '-'' }}/index.html">
          {{ topic }}
        </a>
    </li>
    {% endfor %}
  </ul>

  {% endfor %}

  </div>

  <div class="col">
    <img src="{{ site.baseurl }}/assets/img/tree.jpg" alt="Ski Mountain">
  </div>
</div>


<br><br>
<p>
  <a href='https://www.freepik.com/vectors/plant-silhouette' target="_blank">
    Sketch from rawpixel.com.
  </a>
</p>