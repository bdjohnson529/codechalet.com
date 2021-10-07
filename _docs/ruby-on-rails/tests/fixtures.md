---
title: "Fixtures"
layout: blog
order: 1
topic: Rails
topic_path: /docs/ruby-on-rails/index.html
---
Test data is saved in the `test` database, which is defined in `config/database.yml`. Test data is defined using [`fixtures`](https://guides.rubyonrails.org/testing.html#the-low-down-on-fixtures) -- YAML files which are processed by the Rails engine. The rails engine can interpret ERB in the YAML files, a handy feature which allows us to write functions to populate the test database with lots of data.