---
title: "AWS"
layout: blog
link: "landing"
topic: AWS
topic_path: /docs/aws/index.html
image: aws
---
Notes on building in AWS. These guides assume you have [installed the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html). Verify your installation by checking the version of the `aws` package:
```bash
aws --version
```

### Compute
<ul>
{% assign pages = site.docs | sort: 'order' %}
{%- for page in pages -%}
  {% if page.path contains "aws/compute" %}
    <li>
      <a href="{{ page.url | relative_url }}">
        {{ page.title | escape }}
      </a>
    </li>
  {% endif %}
{%- endfor -%}
</ul>

### Networking
<ul>
{% assign pages = site.docs | sort: 'order' %}
{%- for page in pages -%}
  {% if page.path contains "aws/networking" %}
    <li>
      <a href="{{ page.url | relative_url }}">
        {{ page.title | escape }}
      </a>
    </li>
  {% endif %}
{%- endfor -%}
</ul>

### Designs

<ul>
{% assign pages = site.docs | sort: 'order' %}
{%- for page in pages -%}
  {% if page.path contains "aws/tutorials/index" %}
    <li>
      <a href="{{ page.url | relative_url }}">
        {{ page.title | escape }}
      </a>
    </li>
  {% endif %}
{%- endfor -%}
</ul>