---
layout: default
title: m.igrs.jp
---
<h1><a href="http://m.igrs.jp/">{{ page.title }}</a></h1>
<h2>Posts</h2>

<ul class="posts">
{% for post in site.posts limit:30 %}
<li><span class="date">{{ post.date | date:"%Y-%m-%d" }}</span> <a href="{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
</ul>
