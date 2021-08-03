---
title: "Conditionals"
layout: blog
topic: ruby-syntax
order: 0
parent: Ruby
parent_path: ruby/
---
Conditional statements evaluate as either `true` or `false`.

## Conditional statements
Ruby has neat methods like `.nil?` and `.blank?` which evaluate an object based on a condition, and return a boolean.

```ruby
if state != 'California'
  print "A different state was selected"
```

This statement can be re-written using `unless`.

```ruby
unless state == 'California'
  print "A different state was selected"
```