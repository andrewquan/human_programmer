---
layout: post
title: Namespacing
permalink: namespacing
---

### Namespacing

During the first couple of weeks as a professional Rails developer, I noticed something drastically different about the way code was being organized. It occurred to me that the applications I was working on while learning Rails were simplistic and small, thus no real need to refactor. In the real-world there can be hundreds of models where grouping all of them into a single `app/models` directory would make it almost impossible to understand. This was also conceptually disruptive in that models that are core to your application were placed alongside low-level ones.

This is where the simple act of namespacing can go a very long way to making the codebase much more digestible. I also found several positive side-effects (there is a trickle-down effect).

## Models
{% highlight ruby %}
class Book < ActiveRecord::Base
  has_many :chapters
end

class Chapter < ActiveRecord::Base
  belongs_to :book
end
{% endhighlight %}

`Book`s and `Chapter`s have an obvious relation so it makes sense to group them into a module. In this case we'll create a `Series` module.

First, create `app/models/story.rb` with the following:

{% highlight ruby %}
module Story
  def self.table_name_prefix
    'story_'
  end
end
{% endhighlight %}

This will add the proper prefix to the classes within the module.

{% highlight ruby %}
module Story
  class Book < ActiveRecord::Base
    has_many :chapters
  end
end

module Story
  class Chapter < ActiveRecord::Base
    belongs_to :book
  end
end
{% endhighlight %}

These will be placed in `app/models/story/book.rb` and `app/models/story/chapter.rb`, respectively.

It's important to note that when referencing other classes within the same module, you use just the class name without the `Story::` namespacing. However, if you're to reference it outside of the module, you need to include the namespace.

{% highlight ruby %}
class User < ActiveRecord::Base
  # incorrect way
  # NameError: uninitialized constant User::StoryBooks
  has_many :story_books

  # correct way
  has_many :story_books, classname: 'Story::Books'

  # this is also correct
  has_many :books, classname: 'Story::Books'
end
{% endhighlight %}

## Migrations
You'll need to prefix your database tables with an underscored name in order for Rails to recognize the relation.

```
$ rails generate migration create_story_books
```

{% highlight ruby %}
class CreateStoryBooks < ActiveRecord::Migration
  create_table :story_books
    # other code goes here
  end
end
{% endhighlight %}

## Routes
You'll also need to wrap your routes within the proper namespace:

{% highlight ruby %}
namespace :story do
  resources :books
end
{% endhighlight %}

The URL will look like `/story/books/1` and path helpers will look like `new_story_book_path`

## Controllers
Controller namespacing is pretty simple as well:

{% highlight ruby %}
module Story
  class BooksController < ApplicationController
    # other code goes here
  end
end
{% endhighlight %}

## Views
When rendering partials, it seems the best way is to explicitly point to where the partial is.

{% highlight ruby %}
<%= render 'story/books/bookmark', collection: @bookmarks %>
{% endhighlight %}

## Organizing Everywhere
When you start namespacing beginning from the models, it starts to make sense to organize your code in the same where everywhere else.

{% highlight ruby %}
#show examples here
{% endhighlight %}



