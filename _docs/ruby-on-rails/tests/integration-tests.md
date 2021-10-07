---
title: "Integration tests"
layout: blog
order: 1
topic: Rails
topic_path: /docs/ruby-on-rails/index.html
---
Integration tests can test for user flows. For example, you can write a test to initiate an HTTP request to the server, and minitest can verify the response code. The list of status codes in Ruby [can be found here.](https://rubydoc.info/github/rack/rack/master/Rack/Utils#HTTP_STATUS_CODES-constant)
```ruby
class UserLoginTest < ActionDispatch::IntegrationTest
  test 'Omniauth login flow' do
      post user_google_oauth2_omniauth_authorize_path
      assert_response :ok
    end
  end
end
```