---
title: "Migrations"
layout: blog
order: 0
topic: Rails
topic_path: /docs/ruby-on-rails/index.html
---
Migrations are a way to alter the database schema over time.

## ActiveRecord Generator
Create a new scaffold
```bash
bin/rails g scaffold Post name:string title:string user:references
```

Generate migration
```bash
bin/rails g migration AddWeightToPeople
```

## Migrations
Add default value
```ruby
class AddDefaultValueToPeople < ActiveRecord::Migration[6.1]
  def change
    change_column :people, :title, :string, :default => "Mr./Ms."
  end
end
```

## Commands

| Command | Description |
| -- | -- |
| `db:migrate` | runs (single) migrations that have not run yet. |
| `db:create` | creates the database |
| `db:drop` | deletes the database |
| `db:schema:load` | creates tables and columns within the existing database following schema.rb. This will delete existing data. |
| `db:setup` | does `db:create`, `db:schema:load`, `db:seed` |
| `db:reset` | does `db:drop`, `db:setup` |
| `db:migrate:reset` | does `db:drop`, `db:create`, `db:migrate` |


## Resources
* [RailsGuides - Active Record Migrations](https://guides.rubyonrails.org/active_record_migrations.html)
* [Stack Overflow](https://stackoverflow.com/a/10302357/9080991)