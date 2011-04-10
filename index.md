---
layout: default
title: captn3m0.github.com
---
{% for post in site.posts %}
  * [{{ post.title }}]({{ post.url }})
{% endfor %}
