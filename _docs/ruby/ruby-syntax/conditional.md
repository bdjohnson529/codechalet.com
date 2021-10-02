---
title: "Conditionals"
layout: blog
order: 0
topic: Ruby
topic_path: /docs/ruby/index.html
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