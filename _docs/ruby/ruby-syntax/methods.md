---
title: "Methods"
layout: blog
order: 3
topic: Ruby
topic_path: /docs/ruby/index.html
---
Ruby methods are similar to functions in other programming languages. Method names need to start with a lower case letter so that the Ruby interpreter parses them correctly.

Methods are defined between an opening `def` statement and a closing `end` statement. Methods accept arguments, contained within parentheses. Methods also need to be defined, before they are invoked.
```ruby
def add_numbers(x, y)
    x + y
end

puts add_numbers(1,2)

>> 3
```

Ruby methods have an implicit return value, equal to the final method instruction. An explicit `return` statement can also be used to return one or more values. The Ruby parser will prioritize the explicit value over the implicit value.
```ruby
def reverse_numbers(x, y)
    return y, x
end

print reverse_numbers(1,2)

>> [1,2]
```

Arguments can be passed to Ruby methods by separating the arguments and the method with a space.
```ruby
puts add_numbers 1, 2
```


This functionality breaks down when you include additional statements after the method. For example, a ternary statement cannot be used after calling a function method with a space.
This functionality breaks down when you are using more complicated statements, like ternary statements.
```ruby
item = 'orange'
fruits = ['orange', 'grapefruit', 'apple']

x = fruits.include? item ? 'You picked a fruit' : 'You did not pick a fruit'

puts x
```

In the example above, the argument `item` should be passed to the method `include?` using parentheses.
```ruby
x = fruits.include?(item) ? 'You picked a fruit' : 'You did not pick a fruit'
```
