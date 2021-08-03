---
title: "Procs"
layout: blog
topic: ruby-syntax
order: 2
parent: Ruby
parent_path: ruby/
---
A proc is another encapsulation of code. Procs are assigned a variable name, and in this way are similar to methods. Blocks, on the other hand, are not assigned a variable name. You could define a Proc at the top of your file and call it later, but you could not do this with a Block.

In the example below, `make_upper` is a proc. Lambdas are a specific type of proc. Procs can be invoked using the `call` method.
```ruby
make_upper = lambda { |n| n.upcase }

puts make_upper.call("test")

>> TEST
```

To pass a proc into a method, the proc needs to be converted into a block. Methods accept blocks as arguments, but not procs. In the example below, the ampersand prefix converts the `make_upper` proc into a block.
```ruby
def say_hello
    yield("test")
end

make_upper = lambda { |n| n.upcase }

puts say_hello(&make_upper)

>> TEST
```

Notice in the example above that `say_hello` accepts a block, and the `yield` line passes the argument into the block, within the `say_hello` method. The block is evaluated within this method. The following code will not work, because the proc is being evaluated before it is passed into the method.

```ruby
def say_hello
    yield
end

make_upper = lambda { |n| n.upcase }

puts say_hello(make_upper.call("test"))
```

The proc evaluates to a string, which is then passed into the `say_hello` method as an argument. However, when this method is executed, `yield`  expects a block to be passed into the method. Since there is no block, the Ruby interpreter will throw an error.