---
title: "Rails Commands"
layout: blog
topic: ruby-on-rails
order: 0
parent: Ruby
parent_path: ruby/
---
The following is a list of Rails commands which I've found helpful. Commmands can be entered in the rails console, which can be accessed at
```bash
bin/rails c
```

# Commands
View all path helpers
```bash
puts Rails.application.routes.named_routes.helper_names.sort
```