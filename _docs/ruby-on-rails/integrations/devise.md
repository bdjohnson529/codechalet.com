---
title: "Devise"
layout: blog
order: 3
topic: Rails
topic_path: /docs/ruby-on-rails/index.html
---
Devise is an authentication solution which can be used to provide login and logout functionality for your users. This tutorial will explain how to create a Rails app from scratch, with Devise authentication.

## Let's begin
Start by creating a new Rails application. I will name my app `blog`, however, feel free to name yours as you wish. Make sure you have Ruby, SQLite3, Node.js, Yarn and Rails installed. You can verify these installations using the following commands.
```bash
ruby --version
sqlite3 --version
node --version
yarn --version
rails --version
```

Once you have verified the installation of the prerequisites, create a new Rails app.
```bash
rails new blog
```

Verify that your app is working by starting the Rails server.
```bash
bin/rails s
```

## Do Some Modeling
Our simple app will need one model to work properly, a User. The User is the entity which will login and logout from our app. Generate the User model using the Rails generator.
```bash
bin/rails g model User first_name:string last_name:string
```

A file will be created, named `app/models/user.rb`. Rails will also generate a migration. Let's run that migration.
```bash
bin/rails g db:migrate
```

The migration will create a table in the `sqlite3` database. You can view that table by loading the database
```bash
sqlite3 db/development.sqlite3
```

In the Sqlite3 intepreter, enter the following command
```bash
>> .tables
```

Voila! There is a users table.

## Integrate Devise
Now we can integrate Devise. Add the following to your `Gemfile`:
```bash
gem 'devise'
```

Install the Gem using `bundle install`. Now run the Devise generator:
```bash
bin/rails g devise:install
```

The generator will provide a set of instructions to your console. The first thing we need to do is add an option to `config/environments/development.rb`.
```ruby
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
```

The Devise generator will also have created a migration for us. Let's run that migration using the command `bin/rails db:migrate`.

## Get it Under Control
Next, let's create a `home` controller, and an associated route in `config/routes.rb`. Create a new file and save it to `app/controllers/home_controller.rb`. Notice the `authenticate_user!` method which we are specifying at the top of the controller. By doing this, we are ensuring that the user needs to be logged in to view the content.
```ruby
# app/controllers/home_controller.rb

class HomeController < ApplicationController
  before_action :authenticate_user!

  def index
    render "home/index"
  end
end
```

We will also need to create an associated view, `app/views/home/index.html.erb`. Let's populate this file with the following content. Notice the ERB tag, which is going to pull a variable from our controller into the view. In this case, I want to pull the `current_user` so that we can verify in the view that there is a current_user selected.
```ruby
<h1>Welcome to My Amazing Website!</h1>

<%= current_user %>
```

Finally, let's add notices to our `app/views/layouts/application.html.erb`. Notice I abbreviated the middle of the file to keep this article short. Don't delete anything from your file, just copy the two lines with `notice` and `alert`.
```html
<html>
  ...
  <body>
    <p class="notice"><%= notice %></p>
    <p class="alert"><%= alert %></p>

    <%= yield %>
  </body>
</html>
```

## Look at the View
Finally, let's use Devise to generate some login and signup views!
```bash
bin/rails g devise:views
```

Launch the server and enjoy your new app!
```bash
bin/rails s
```