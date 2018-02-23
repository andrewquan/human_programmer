---
layout: post
title: Memoization
permalink: memoization
tags:
---

Memoization is a technique that can be used to speed up accessor methods

The first time I encountered memoization was through this common pattern I see everywhere nowadays
def current_user
  @current_user ||= User.find(session[:user_id]}
end

Another way to write the above is
def current_user
  @current_user = @current_user || User.find(session[:user_id])
end

So if the instance variable is already set, then it'll just use that value. If it's not set, it'll perform whatever calculation or query it needs to in order to set the instance variable. Because it is so commonly used in Rails, the shorthand version was thus created. (reference to deprecated Memoization module?)

Multi-line use
