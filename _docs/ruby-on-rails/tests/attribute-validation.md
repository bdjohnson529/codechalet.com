---
title: "Attribute validation"
layout: blog
order: 2
topic: Rails
topic_path: /docs/ruby-on-rails/index.html
---
[ActiveRecord validations](https://guides.rubyonrails.org/active_record_validations.html) can be used to validate model attributes, before creating an instance of the model. Validations prevent bad data from entering the database. Let's say you have a person model, with a height attribute. The height attribute is specified in inches, and must be a decimal number. Using an ActiveRecord validation, you could validate the `height` attribute.
```ruby
class Person < ApplicationRecord
  validates: :height, presence: true, numericality: { only_float: true, greater_than: 0 }
```

You could write a complementary test to capture this validation.
```ruby
# test/fixtures/users.yml
one:
    name: Joe Schmoe
    height: 173

# test/models/user_test.rb
class UserTest < ActiveSupport::TestCase
  def setup
    @user = users(:one)
  end

  test 'User is valid with valid attributes' do
    assert @user.valid?
  end

  test 'User is invalid with invalid height' do
    @user.height = 'string'
    refute @user.valid?, 'Saved user without a non-numeric height'
  end
```


## References
* [How To Test Rails Models with Minitest](https://semaphoreci.com/community/tutorials/how-to-test-rails-models-with-minitest)