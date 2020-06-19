---
layout: default
date: 2020-06-18
author: Jason Brown
title: Blog
---

## Posts
{% for post in site.posts %}
* {{ post.date | date_to_string }} -- [{{ post.title }}]({{ post.url }})
{% endfor %}

