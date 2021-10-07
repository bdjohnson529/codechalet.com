---
title: "RSpec and Capybara"
layout: blog
order: 0
topic: Rails
topic_path: /docs/ruby-on-rails/index.html
---
Rspec and Capybara are testing frameworks which can be used in Rails.

To install RSpec:
```bash
gem add rspec
bundle install
rails generate rspec:install
```

Install Capybara, add the following to your Gemfile:
```bash
# Gemfile

group :test do
  gem 'capybara', '>= 3.26'
end
```