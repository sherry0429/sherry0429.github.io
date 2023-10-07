---
layout: page
title: Blog Archive
---
<ul>
  {% for post in site.novels %}
    <li><a href="{{ post.url }}">{{ post.date | date: "%B %Y" }} - {{ post.title }}</a></li>
  {% endfor %}
</ul>
