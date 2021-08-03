---
title: "Active Record"
layout: blog
topic: ruby-on-rails
order: 7
parent: Ruby
parent_path: ruby/
---
[RailsGuides](https://guides.rubyonrails.org/active_record_basics.html) has a great explanation of Active Record. These are some Active Record methods which I find helpful.

## Methods
Assign attributes to a model instance
```ruby
cat = Cat.new(name: "Simba")
cat.assign_attributes(name: "Nala")
print cat.name

>> Nala
```