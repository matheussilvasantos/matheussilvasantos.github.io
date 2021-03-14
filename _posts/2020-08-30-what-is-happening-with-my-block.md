---
layout: post
title:  "What is Happening With my Block?"
tags: [ruby]
---

Do you know which tests are going to pass and which tests are going to fail in this test file?

```ruby
require "minitest/autorun"

class TestBlocks < Minitest::Test
  def setup
    @values = ["a", "b", "c", "d"]
  end
  
  def test_passing_a_block_with_do
    assert @values.all? do |value|
      false
    end
  end
  
  def test_passing_a_block_with_do_surround_by_parentheses
    assert(@values.all? do |value|
      false
    end)
  end
  
  def test_passing_a_block_with_braces
    assert @values.all? { |value| false }
  end
end
```

How do you do in your code base? If you do like in `test_passing_a_block_with_do` it is bad news.

`test_passing_a_block_with_do` is the only one which is going to pass, but why? I know you know, `assert` receives `@values.all? do |value|` as a block, then it thinks this block is true and that's it. If you thought that, you're almost right. Let's see what is `assert`.

```ruby
# https://github.com/seattlerb/minitest/blob/6257210b7accfeb218b4388aaa36d3d45c5c41a5/lib/minitest/assertions.rb#L178
def assert test, msg = nil
  self.assertions += 1
  unless test then
    msg ||= "Expected #{mu_pp test} to be truthy."
    msg = msg.call if Proc === msg
    raise Minitest::Assertion, msg
  end
  true
end
```

So, is `test` a `Proc`? What do you think?

After debugging this method I know that `test` is `true`. Why is it `true`? The class is `TrueClass`, so it is a proper `true`. What is happening here?

What is `msg` then? `msg` is the `Proc` then, right?

```ruby
(byebug) msg
nil
```

`msg` is `nil`. Okay, it got the default value. Where is my block then? Well, there is only one place left now.

```ruby
(byebug) yield
false
```

Ok, `false`. The block I'm passing is returning `false`, is that the reason? If I change to:

```ruby
def test_passing_a_block_with_do
  assert @values.all? do |value|
    "hello, world!"
  end
end
```

Then I have:

```ruby
(byebug) yield
"hello, world!"
```

Ahhhh, that was it.

A mindful programmer would figure that out at first saw, there is no reason to think that the whole `collection.all? do...end` is going to be a single argument. However, I think it's pretty easy to miss that, have you got it at first glance?
