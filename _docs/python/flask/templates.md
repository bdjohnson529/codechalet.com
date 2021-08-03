---
title:  "Templates and Jinja"
layout: blog
topic: flask
order: 3
parent: Python
parent_path: python/
---

Flask uses templates to render HTML pages. As defined in the [Flask documentation](https://flask.palletsprojects.com/en/1.1.x/tutorial/templates/), templates are *files that contain static data as well as placeholders for dynamic data*. The templates folder contains HTML files.

I also use the templates folder to save markdown files. Pages with a lot of writing are easy to create in Markdown. Python has a `markdown` module which can easily convert markdown to HTML. Within the Flask routing function, I use the `markdown` module to translate the file into HTML, and then insert that HTML into the template.
```python
import markdown

f = open('App/templates/blog.md', encoding="utf8")
lines = f.read()
f.close()

text = markdown.markdown(lines)
```

## Resources
Some of your resources may have different pages for different routes. Let's say you have a *Blog* resource. The URL for adding a new blog post is likely different from the URL for viewing existing blog posts. The templates for the different routes can be saved in the same folder:
```
├── blog
|  ├── new.html
|  ├── edit.html
```