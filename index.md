---
layout: default
title: m.igrs.jp
---
<h1><a href="http://m.igrs.jp/">{{ page.title }}</a></h1>
<h2>Posts</h2>

<ul class="posts">
{% for post in site.posts limit:30 %}
<li><span>{{ post.date | date_to_string }}</span>&raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
</ul>

<div id="contacts">
Masato Igarashi <a href="http://github.com/migrs">github</a> / <a href="http://twitter.com/migrs">twitter</a> / <a href="http://facebook.com/migrs">facebook</a> / <a href="http://www.linkedin.com/in/migrs">linkedin</a>
</div>
