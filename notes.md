---
layout: default
title: Technical Notes
---

<h1 class="post-title" style="margin-bottom: 1.5rem;">Technical Notes</h1>

{% assign notes = site.notes | sort: 'date' | reverse %}

{% comment %} Collect all unique tags from notes {% endcomment %}
{% assign all_tags = "" %}
{% for post in notes %}
  {% for tag in post.tags %}
    {% assign all_tags = all_tags | append: "," | append: tag %}
  {% endfor %}
{% endfor %}
{% assign tag_array = all_tags | split: "," | uniq | sort %}

{% if notes.size > 0 %}

<!-- Tag Filter Buttons -->
<div class="filter-tabs" style="margin-bottom: 2rem;">
  <button class="filter-tab active" onclick="filterByTag('all', this)">All</button>
  {% for tag in tag_array %}
    {% if tag != "" %}
    <button class="filter-tab" onclick="filterByTag('{{ tag }}', this)">{{ tag | replace: '_', ' ' }}</button>
    {% endif %}
  {% endfor %}
</div>

<ul class="post-list">
  {% for post in notes %}
  <li class="post-item" data-tags="{% for tag in post.tags %}{{ tag }} {% endfor %}">
    <div class="post-meta">
      <span class="post-date">{{ post.date | date: "%b %d, %Y" }}</span>
      <span class="post-tag tag-notes">notes</span>
      {% for tag in post.tags %}
        <span class="post-tag" style="background: var(--tag-diy); color: var(--tag-diy-text);">{{ tag | replace: '_', ' ' }}</span>
      {% endfor %}
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

<div class="empty-state" id="no-results" style="display: none;">
  <p>No notes found for this tag.</p>
</div>

<script>
function filterByTag(tag, btn) {
  // Update active button
  document.querySelectorAll('.filter-tab').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');

  // Filter notes
  var items = document.querySelectorAll('.post-item');
  var visible = 0;
  items.forEach(function(item) {
    if (tag === 'all' || item.getAttribute('data-tags').indexOf(tag) !== -1) {
      item.style.display = '';
      visible++;
    } else {
      item.style.display = 'none';
    }
  });

  // Show/hide empty state
  document.getElementById('no-results').style.display = visible === 0 ? '' : 'none';
}
</script>

{% else %}
<div class="empty-state"><p>No notes yet.</p></div>
{% endif %}