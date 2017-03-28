---
layout: post
title: Working with arrays in Javascript
subtitle: basic functions - argh!!
bigimg: ../img/analog.jpg
---

### Recently I've been working on a project where a customer asked to sort user inputs by various rules and be able to insert future forms as well.

We've been receiving messages with json objects which were sorted before inserted to a table but there was a possibility of adding new forms at the top.

So I've devided the objects to arrays and sorted, New first, Approved second then Completed but had to somehow insert new ones at the beginning and I discovered this basic functions - always needed push and pop only!

Lovely and easily explained:

![Array Functions]({{ site.url }}../img/1pQk8.jpg)

Found this on: http://stackoverflow.com/questions/8073673/how-can-i-add-new-array-elements-at-the-beginning-of-an-array-in-javascript
