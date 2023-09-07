---
layout: page
title: My Novels
---
<h1>Hello</h1>

{% for tag in site.tags %}
  {% if tag[0] | contains: 'novel-' %}
    {% assign novel_info = tag[0] | split: '-' %}
    {% assign novel_name = novel_info[1] %}
    {% assign chapter_name = novel_info[2] %}
    {% if novel_name != '' %}
      <h3>{{ novel_name }}</h3>
      <ul>
        {% for post in tag[1] | sort: "date" %}
          <li><a href="{{ post.url }}">{{ post.date | date: "%B %Y" }} - {{ chapter_name }}</a></li>
        {% endfor %}
      </ul>
    {% endif %}
  {% endif %}
{% endfor %}
