---
layout: page
title: My Novels - 逆旅
---
<ul>
  {% for post in site.novels %}
    <li><a href="{{ post.url }}">{{ post.date | date: "%B %Y" }} - {{ post.title }}</a></li>
  {% endfor %}
</ul>
