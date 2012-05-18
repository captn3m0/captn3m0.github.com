---
layout: default
title: CaptNemo.in
---
<div class="alert alert-info">
  IIT-JEE 2012 Results Listing is now available <a href="/projects/iitjee">here</a>
</div>

{% for post in site.posts %}
###[{{ post.title }}]({{ post.url }}) <small>{{post.date | date_to_string}}</small>
{% endfor %}
