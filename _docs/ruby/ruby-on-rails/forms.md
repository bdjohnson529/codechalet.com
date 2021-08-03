---
title: "Forms"
layout: blog
topic: ruby-on-rails
order: 6
parent: Ruby
parent_path: ruby/
---
Websites use HTML forms to collect user input. Forms are composed of different input elements, such as `text`, `radio` and `submit`. For example, to gather a user's name and email, you can use a form:

```html
<form action="/users/">
  <input type="text">
  <input type="submit">
</form>
```

Forms are associated with an HTTP request. In Rails, the request is handled by the controller. In the example above, when the user clicks submit, the site will make a POST request to `/users/`, with the data contained in the form.

