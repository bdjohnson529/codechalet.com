---
title: "Integration tests"
layout: blog
order: 1
topic: Rails
topic_path: /docs/ruby-on-rails/index.html
---
Integration tests use Capybara to interact with the DOM of the webpage. A typical integration test might be testing user sign. This guide describes how to write integration tests with RSpec, Capybara and FactoryBot.

The setup for fixtures will be similar because the test does not modify any of the generated data.

## Factories
First you will need to create some factories to generate user data. Let's write a factory to generate a set of users.
```ruby
# /spec/factories/user.rb

FactoryBot.define do
  factory :user do
    first_name { "Jordan" }
    last_name { "McChicken" }
    sequence(:email) { |n| "test-#{n.to_s.rjust(3, "0")}@fake.com" }
    password { "password" }
  end
end
```

We want our test to know as little about our code implementation as possible. One way to write a system test would be to load the DOM with the login view, enter our user's login information, and click the submit button. Let's do that.

## Write the Test
Let's make a list of the sequence of events in our test.
* visit the login screen
* enter email in the `<input>` element
* enter password in the `<input>` element
* submit the form

Our expected outcome is the user logs in, and receives the next view in the UX sequence. Let's say that after the login page, we want the user to see a "Welcome" page. We can verify this by searching for the text "Welcome" in the DOM.
```ruby
# /spec/system/user_login_spec.rb

require "rails_helper"

RSpec.describe "user can log in", type: :system do
  let(:user) { FactoryBot.create(:user) }

  it "with email and password" do
    visit root_path
    fill_in "user_email", :with => user.email
    fill_in "user_password", :with => user.password
    click_button "submit"

    expect(page).to have_text("Welcome")
  end
end

```

Well done! You have written your first integration test. Time to celebrate!