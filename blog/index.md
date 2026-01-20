---
layout: default
title: Blog
permalink: /blog/
---

# Blog

{% for post in site.posts %}
<article style="margin: 1.25rem 0;">
  <h3 style="margin-bottom: 0.25rem;">
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
  </h3>
  <div style="color:#888; font-size:0.9em; margin-bottom: 0.5rem;">
    {{ post.date | date: "%B %-d, %Y" }}
  </div>
  <p style="margin-top: 0;">
    {{ post.excerpt | strip_html | truncatewords: 40 }}
  </p>
</article>
{% endfor %}

