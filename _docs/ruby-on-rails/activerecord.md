---
title: "Active Record"
layout: blog
order: 7
topic: Ruby
topic_path: /docs/ruby/index.html
---
[RailsGuides](https://guides.rubyonrails.org/active_record_basics.html) has a great explanation of Active Record. These are some Active Record methods which I find helpful.

<b>Assign attributes</b>
```ruby
cat = Cat.new(name: "Simba")
cat.assign_attributes(name: "Nala")
print cat.name

>> Nala
```

<b>Select attributes as a list.</b>
```ruby
Cat.pluck(:name)
Cat.all.map { |x| x.name }

>> ["Nala"]
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