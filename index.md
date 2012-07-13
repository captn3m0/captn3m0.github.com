---
layout: default
title: CaptNemo.in
---
<div class="alert alert-info">
{% include alert.md %}
</div>

{% for post in site.posts %}
###[{{ post.title }}]({{ post.url }}) <small>{{post.date | date_to_string}}</small>
{% endfor %}
