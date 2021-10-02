---
title: "Strings"
layout: blog
order: 4
topic: Ruby
topic_path: /docs/ruby/index.html
---
Strings in Ruby are specified the same way as they are in Python. A string is enclosed by either single or double quotes.
```ruby
puts "my string"
```

Regular expressions are defined in the [Regexp class](https://docs.ruby-lang.org/en/2.4.0/Regexp.html). The `=~` operator can be used to search a regular expression in a string. The operator matches the regex against the string, and returns the character index of the starting character in the regular expression.
```ruby
pattern = /orange/
string = "I eat lots of oranges"

puts pattern =~ string

>>14
```