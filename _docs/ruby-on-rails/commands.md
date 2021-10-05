---
title: "Rails Commands"
layout: blog
order: 0
topic: Rails
topic_path: /docs/ruby-on-rails/index.html
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