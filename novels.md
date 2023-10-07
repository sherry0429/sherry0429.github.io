---
layout: page
title: My Novels
---
<h1>Hello</h1>
{% raw %}
{% assign novels = site.tags | where_exp: "tag", "tag[0] | contains: 'novel-'" %}
{% if novels.size > 0 %}
  {% for tag in novels %}
    {% assign novel_info = tag[0] | split: '-' %}
    {% assign novel_name = novel_info[1] %}
    {% assign chapter_name = novel_info[2] %}
    
    {% if novel_name != empty %}
      <h3>{{ novel_name }}</h3>
      <ul>
        {% for post in tag[1] | sort: "date" %}
          <li><a href="{{ post.url }}">{{ post.date | date: "%B %Y" }} - {{ chapter_name }}</a></li>
        {% endfor %}
      </ul>
    {% endif %}
  {% endfor %}
{% endif %}
{% endraw %}






