---
layout: page
title: My Novels
---
<h1>{{ site.novels }}</h1>
<ul>
  {% for post in site.novels %}
    <li><a href="{{ post.url }}">{{ post.date | date: "%B %Y" }} - {{ post.title }}</a></li>
  {% endfor %}
</ul>
