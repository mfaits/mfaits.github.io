---
layout: default
title: "Michelle Faits"
---

## Sections

- [About](/about/)
- [Projects](/projects/)
- [Data Science Primers](/primers/)
- [Links](/links/)
- [Blog](/blog/)

## Latest posts

<ul>
  {% for post in site.posts limit:3 %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <span style="color:#888; font-size:0.9em;">
        – {{ post.date | date: "%Y-%m-%d" }}
      </span>
    </li>
  {% endfor %}
</ul>
