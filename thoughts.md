---
layout: default
title: Thoughts
---

<h1 class="post-title" style="margin-bottom: 1.5rem;">Thoughts</h1>

{% assign thoughts = site.posts | where: "category", "thoughts" | sort: 'date' | reverse %}
{% if thoughts.size > 0 %}
<ul class="post-list">
  {% for post in thoughts %}
  <li class="post-item">
    <div class="post-meta">
      <span class="post-date">{{ post.date | date: "%b %d, %Y" }}</span>
      <span class="post-tag tag-thoughts">thoughts</span>
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
<div class="empty-state"><p>No thoughts yet.</p></div>
{% endif %}
