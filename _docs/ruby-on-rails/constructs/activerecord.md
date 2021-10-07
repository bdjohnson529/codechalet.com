---
title: "Active Record Finders"
layout: blog
order: 7
topic: Rails
topic_path: /docs/ruby-on-rails/index.html
---
These are some [Active Record](https://guides.rubyonrails.org/active_record_basics.html) Finder methods which I find helpful.

<b>Assign attributes</b>
```ruby
cat = Cat.new(name: "Simba")
cat.assign_attributes(name: "Nala")
```

<b>Select attributes as a list.</b>
```ruby
Cat.pluck(:name)
Cat.all.map { |x| x.name }
```

<b>Get column names</b>
```ruby
Cat.column_names
```

<b>Join with another table</b>
```ruby
Cat.joins(:owners)
```

<b>Select ambiguous column from joined table</b>
```ruby
Cat.joins(:owners)
   .select("owners.id")
   .map { |x| x.id }
```