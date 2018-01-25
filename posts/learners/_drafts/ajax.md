---
layout: post
title: Ajax
permalink: ajax
---

### Ajax

Ajax isn't a technology on its own, but rather a collection of technologies that work together to help create user friendly web interfaces. What this means is that JavaScript allows a web page to update just parts of a page instead of getting the entire page from the server.

Rails comes with built-in support for Ajax so it makes it very easy to implement into your Rails project.

### Unobtrusive JavaScript
The standard way now is to separate JavaScript from HTML. This separation of concerns helps in the long run when you have to make identical changes across multiple web pages. It also keeps your code DRY.

Rails is also able to minimize and concatenate your JavaScript, and also download it on the first page load then cache it for subsequent page loads.

