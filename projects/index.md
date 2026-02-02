---
layout: default
title: Projects
permalink: /projects/
---

# Projects

{% for post in site.posts %}
  {% if post.category == "projects" %}
    <article style="margin: 2rem 0;">
      <h3 style="margin-bottom: 0.25rem;">
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      </h3>

      <div style="color:#888; font-size:0.9em; margin-bottom: 0.5rem;">
        {{ post.date | date: "%B %-d, %Y" }}
      </div>

      <p style="margin-top: 0;">
        {{ post.excerpt | strip_html | truncatewords: 45 }}
      </p>
    </article>
  {% endif %}
{% endfor %}
