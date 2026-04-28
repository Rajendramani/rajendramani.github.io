---
layout: default
title: Technical Notes
---

<h1 class="post-title" style="margin-bottom: 1.5rem;">Technical Notes</h1>

{% assign notes = site.notes | sort: 'date' | reverse %}
{% if notes.size > 0 %}
<ul class="post-list">
  {% for post in notes %}
  <li class="post-item">
    <div class="post-meta">
      <span class="post-date">{{ post.date | date: "%b %d, %Y" }}</span>
      <span class="post-tag tag-notes">notes</span>
    </div>
    <a href="{{ post.url | relative_url }}" class="post-title-link">
      <h2 class="post-title">{{ post.title }}</h2>
    </a>
    {% if post.description %}
      <p class="post-excerpt">{{ post.description }}</p>
    {% endif %}
  </li>
  {% endfor %}
</ul>
{% else %}
<div class="empty-state"><p>No notes yet.</p></div>
{% endif %}
