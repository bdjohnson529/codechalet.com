---
title: "RSpec"
layout: blog
order: 0
topic: Rails
topic_path: /docs/ruby-on-rails/index.html
---
Rspec is a testing framework which can be used as an alternative to the Rails-default minitest. Here are some resources to help you write rspec tests:

* [RSpec matchers](https://relishapp.com/rspec/rspec-expectations/docs/built-in-matchers)

## Installation
To install RSpec:
```bash
gem add rspec
bundle install
rails generate rspec:install
```

Install Capybara, add the following to your Gemfile:
```bash
# Gemfile
group :test do
  gem 'capybara', '>= 3.26'
end
```

RSpec will create a folder `spec` and populate some files there. To support system tests with Capybara, there are two changes you need to make. Create a new file, `spec/support/system.rb`, and modify the existing file `spec/rails_helper.rb`
```ruby
# spec/rails_helper.rb
Dir[Rails.root.join('spec', 'support', '**', '*.rb')].sort.each { |f| require f }

# spec/support/system.rb
RSpec.configure do |config|
  config.before(:each, type: :system) do
    driven_by :rack_test
  end
end
```

## Create a Spec
Now you can create a system spec! Let's write a spec which will always pass.
```ruby
# create_event_spec.rb
require "rails_helper"

RSpec.describe "example test", type: :system do
  it "sets true equal to true" do
    expect true.to be true
  end
end
```