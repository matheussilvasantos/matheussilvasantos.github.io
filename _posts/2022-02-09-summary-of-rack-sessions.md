---
layout: post
title:  "Summary of Rack Sessions With Cookies and Pool"
tags: [ruby]
---

This is a Rack application:

```ruby
run -> (env) do
  [200, {}, ["hello friend"]]
end

```

This is a Rack application using sessions:

```ruby
use Rack::Session::Pool, secret: SecureRandom.uuid
run -> (env) do
  count = env["rack.session"][:count] ||= 1
  env["rack.session"][:count] += 1
  [
    200,
    {},
    [
      (["hello friend"] * count).join(", ")
    ]
  ]
end
```

`Rack::Session::Pool` isn't the only option. You can use `Rack::Session::Cookie` instead.

Be aware! `Rack::Session::Pool` stores sessions in an instance variable. Therefore, it resets if you restart the server, it won't work by default if you have a load balancer, and similar situations.

`Rack::Session::Cookie` does marshalling and store sessions in cookies, so you will have persistent sessions at the price of marshalling. However, marshaling has it's performance costs, and you lost flexibility with what you can put in sessions.¹ Also, storing in cookies means you will increase the amount of data in your requests.

If you decide to use `Rack::Session::Pool` in your application, be cautious with how you include the middleware in your application. The following application wouldn't work, for example:

```ruby
app = Rack::Builder.new do
  use Rack::Session::Pool, secret: SecureRandom.uuid
  run -> (env) do
    count = env["rack.session"][:count] ||= 1
    env["rack.session"][:count] += 1
    [
      200,
      {},
      [
        (["hello friend"] * count).join(", ")
      ]
    ]
  end
end
run app
```

The code ends up calling `to_app` on `app` for every request, which causes a new instance of `Rack::Session::Pool` for every request - since it tracks sessions by an instance variable it won't be able to track sessions: just calling `Rack::Builder.app` instead of `Rack::Builder.new` would make it work:

From [lib/rack/builder.rb:118](https://github.com/rack/rack/blob/main/lib/rack/builder.rb#L118):
```ruby
# Create a new Rack::Builder instance and return the Rack application
# generated from it.
def self.app(default_app = nil, &block)
  self.new(default_app, &block).to_app
end
```


<hr>

1. [Using `Rack::Session::Pool` over `Rack::Session::Cookie`](https://stackoverflow.com/questions/13573968/using-racksessionpool-over-racksessioncookie).
