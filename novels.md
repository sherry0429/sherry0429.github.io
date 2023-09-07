---
layout: page
title: My Novels
---

{% assign novels = site.tags | where_exp: "tag", "tag[0] | split: '-' | first == 'novel'" %}
{% assign novels_grouped = novels | group_by: "tag[0] | split: '-' | last" %}

{% for novel_group in novels_grouped %}
  <h3>{{ novel_group.name }}</h3>
  <ul>
    {% assign chapters = novel_group.items | sort: "date" %}
    {% for chapter in chapters %}
      <li><a href="{{ chapter.url }}">{{ chapter.date | date: "%B %Y" }} - {{ chapter.tag[0] | split: '-' | last }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}
