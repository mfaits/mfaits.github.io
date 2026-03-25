---
title: Home
layout: single
author_profile: false
classes: wide
---

*Member of the Committee to End [SCAPDFATIAT](https://xkcd.com/2565/).*

## Latest posts

<ul>
  {% for post in site.posts limit:4 %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <span style="color:#777;">– {{ post.date | date: "%Y-%m-%d" }}</span>
    </li>
  {% endfor %}
</ul>
