---
layout: home
---
# Welcome to Code Chalet!
This site contains resources about different technical topics. To start, click a topic which interests you.

<br>


{% for category in site.data.settings %}
  <h3>{{ category[0] }}</h3>

  <ul>
    {% for topic in category[1] %}
    {% assign path = topic | downcase | replace: " ", "-" %}
    <li>
        <a href="{{ site.baseurl }}/docs/{{ topic | downcase | replace: ' ', '-'' }}">
          {{ topic }}
        </a>
    </li>
    {% endfor %}
  </ul>

{% endfor %}
