---
title: "Blocks"
layout: blog
order: 2
topic: Ruby
topic_path: /docs/ruby/index.html
---
Blocks are, well, *blocks* of code which can be passed into methods. A block can be enclosed by `do..end` or by brackets `{..}`. Blocks are often passed to iterators, to perform the same function on members of an array. Consider this code:
```ruby
[1,2,3].each do |x|
    puts x + 2
end

>> 3
>> 4
>> 5
``` 

The same code can be written by enclosing the block in brackets.
```ruby
[1,2,3].each do |x| { puts x + 2}
```

Blocks can be passed to methods. The block is evaluated within the scope of the method. In the example below, notice how the block evaluates the value of `y` which is set within the method, rather than the value which is set globally.

```ruby
def say_hello
    y = 3
    yield(y)
end

y = 10
puts say_hello { |x| x + 2 }

>> 5
```