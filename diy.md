---
layout: default
title: DIY Projects
---

<h1 class="post-title" style="margin-bottom: 1.5rem;">DIY Projects</h1>

{% assign diy = site.diy | sort: 'date' | reverse %}
{% if diy.size > 0 %}
<ul class="post-list">
  {% for post in diy %}
  <li class="post-item">
    <div class="post-meta">
      <span class="post-date">{{ post.date | date: "%b %d, %Y" }}</span>
      <span class="post-tag tag-diy">diy</span>
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
<div class="empty-state"><p>No DIY projects yet.</p></div>
{% endif %}
