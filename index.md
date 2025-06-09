---
layout: default
title: Home
---

# Welcome to My Blog

This is my personal blog where I share my thoughts, experiences, and knowledge.

## Latest Posts

<ul class="post-list">
  {% for post in site.posts %}
    <li>
      <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
      <div class="post-meta">
        {{ post.date | date: "%B %-d, %Y" }}
      </div>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul> 