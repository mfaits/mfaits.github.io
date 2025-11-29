---
layout: default
title: "Michelle Faits"
---

<p style="margin-top: 1.5rem; font-size: 0.95rem;">
  <a href="/">Home</a> ·
  <a href="/about/">About</a> ·
  <a href="/projects/">Projects</a> ·
  <a href="/primers/">Data Science Primers</a> ·
  <a href="/links/">Links</a> ·
  <a href="/blog/">Blog</a>
</p>

---

<p style="margin-top: 1rem; font-size: 0.9rem;">
  <strong>Member of the Committee to End SCAPDFATIAT</strong>  
  · <a href="https://xkcd.com/2565/" target="_blank">[xkcd 2565]</a>
</p>


## Latest posts

<ul>
  {% for post in site.posts limit:5 %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <span style="color:#888; font-size:0.9em;">
        – {{ post.date | date: "%Y-%m-%d" }}
      </span>
    </li>
  {% endfor %}

  {% if site.posts == empty %}
    <li><em>No posts yet.</em></li>
  {% endif %}
</ul>
