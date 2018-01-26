---
layout: post
title: The `super` Method
permalink: super-method
tags:
---

The `super` method is *super* simple and helpful. It calls a parent method of the same name and use the same argument(s) provided to the child method.

```
class Foo
  def baz(str)
    p str + ' from the parent class'
  end
end

class Bar < Foo
  def baz(str)
    super
    p str + ' from the child class'
  end
end

Bar.new.baz('Hello')
"Hello from the parent class"
"Hello from the child class"
=> "Hello from the child class"
# need to figure out what the return value is in different scenarios
```

If there is no method of the same name in the parent class, you'll get a NoMethodError

You can stack them deep so `super` can also be used in a grandchild class

If you use `super()` instead, it won't pass any arguments to the parent class. You can pass as many arguments as needed into `super()` so that it works with the parent method. Syntax is important here because Rails will throw an exception if the parent method gets the wrong number of arguments.
