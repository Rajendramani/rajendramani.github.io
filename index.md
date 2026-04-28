---
layout: default
title: Home
---

{% comment %} Combine all content types into one sorted list {% endcomment %}
{% assign all_posts = site.posts | concat: site.notes | concat: site.diy | sort: 'date' | reverse %}

{% if all_posts.size > 0 %}
<ul class="post-list">
  {% for post in all_posts %}
  <li class="post-item">
    <div class="post-meta">
      <span class="post-date">{{ post.date | date: "%b %d, %Y" }}</span>
      <span class="post-tag tag-{{ post.category | default: 'notes' }}">{{ post.category | default: "notes" }}</span>
    </div>
    <a href="{{ post.url | relative_url }}" class="post-title-link">
      <h2 class="post-title">{{ post.title }}</h2>
    </a>
    {% if post.description %}
      <p class="post-excerpt">{{ post.description }}</p>
    {% elsif post.excerpt %}
      <p class="post-excerpt">{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
    {% endif %}
  </li>
  {% endfor %}
</ul>
{% else %}
<div class="empty-state">
  <p>No posts yet. Add a Markdown file to get started!</p>
</div>
{% endif %}
