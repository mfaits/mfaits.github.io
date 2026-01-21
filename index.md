---
layout: default
title: "Michelle Faits"
---

<p style="font-size: 0.85rem; font-style: italic; margin-top: 0;">
  Member of the Committee to End
  <a href="https://xkcd.com/2565/" target="_blank">SCAPDFATIAT</a>
</p>

<p style="margin-top: 1rem; font-size: 0.95rem;">
  <a href="/">Home</a> ·
  <a href="/about/">About</a> ·
  <a href="/projects/">Projects</a> ·
  <a href="/primers/">Data Science Primers</a> ·
  <a href="/links/">Links</a> ·
  <a href="/blog/">Blog</a> ·
  <a href="/subscribe/">Subscribe</a> ·
  <a href="{{ '/feed.xml' | relative_url }}">RSS</a>
</p>

---

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
</ul>
