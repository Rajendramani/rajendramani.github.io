---
layout: default
title: Home
---

{% comment %} Combine all content types into one sorted list {% endcomment %}
{% assign all_posts = site.posts | concat: site.notes | concat: site.diy | sort: 'date' | reverse %}

{% comment %} Collect all unique tags {% endcomment %}
{% assign all_tags = "" %}
{% for post in all_posts %}
  {% for tag in post.tags %}
    {% assign all_tags = all_tags | append: "," | append: tag %}
  {% endfor %}
{% endfor %}
{% assign tag_array = all_tags | split: "," | uniq | sort %}

{% if all_posts.size > 0 %}

<!-- Tag Filter Buttons -->
<div class="filter-tabs" style="margin-bottom: 2rem;">
  <button class="filter-tab active" onclick="filterByTag('all', this)">All</button>
  {% for tag in tag_array %}
    {% if tag != "" %}
    <button class="filter-tab" onclick="filterByTag('{{ tag }}', this)">{{ tag | replace: '_', ' ' }}</button>
    {% endif %}
  {% endfor %}
</div>

<ul class="post-list" id="post-list">
  {% for post in all_posts %}
  <li class="post-item" data-tags="{% for tag in post.tags %}{{ tag }} {% endfor %}">
    <div class="post-meta">
      <span class="post-date">{{ post.date | date: "%b %d, %Y" }}</span>
      <span class="post-tag tag-{{ post.category | default: 'notes' }}">{{ post.category | default: "notes" }}</span>
      {% for tag in post.tags %}
        <span class="post-tag" style="background: var(--tag-diy); color: var(--tag-diy-text);">{{ tag | replace: '_', ' ' }}</span>
      {% endfor %}
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

<div class="empty-state" id="no-results" style="display: none;">
  <p>No posts found for this tag.</p>
</div>

<!-- Pagination -->
<div id="pagination" style="display: flex; align-items: center; justify-content: center; gap: 1rem; margin-top: 2.5rem; padding-top: 1.5rem; border-top: 1px solid var(--border);">
  <button id="prev-btn" onclick="changePage(-1)" style="padding: 0.4rem 1rem; border-radius: 100px; font-size: 0.85rem; font-weight: 500; color: var(--text-secondary); background: transparent; border: 1px solid var(--border); cursor: pointer; transition: all 0.2s;">← Prev</button>
  <span id="page-info" style="font-family: 'IBM Plex Mono', monospace; font-size: 0.8rem; color: var(--text-muted);"></span>
  <button id="next-btn" onclick="changePage(1)" style="padding: 0.4rem 1rem; border-radius: 100px; font-size: 0.85rem; font-weight: 500; color: var(--text-secondary); background: transparent; border: 1px solid var(--border); cursor: pointer; transition: all 0.2s;">Next →</button>
</div>

<script>
var POSTS_PER_PAGE = 5;
var currentPage = 1;
var currentTag = 'all';

function getFilteredItems() {
  var items = Array.from(document.querySelectorAll('.post-item'));
  if (currentTag === 'all') return items;
  return items.filter(function(item) {
    return item.getAttribute('data-tags').indexOf(currentTag) !== -1;
  });
}

function renderPage() {
  var allItems = Array.from(document.querySelectorAll('.post-item'));
  var filtered = getFilteredItems();
  var totalPages = Math.max(1, Math.ceil(filtered.length / POSTS_PER_PAGE));

  if (currentPage > totalPages) currentPage = totalPages;

  var start = (currentPage - 1) * POSTS_PER_PAGE;
  var end = start + POSTS_PER_PAGE;

  // Hide all first
  allItems.forEach(function(item) { item.style.display = 'none'; });

  // Show only current page items
  filtered.forEach(function(item, i) {
    if (i >= start && i < end) {
      item.style.display = '';
    }
  });

  // Empty state
  document.getElementById('no-results').style.display = filtered.length === 0 ? '' : 'none';

  // Pagination controls
  var pagination = document.getElementById('pagination');
  if (filtered.length <= POSTS_PER_PAGE) {
    pagination.style.display = 'none';
  } else {
    pagination.style.display = 'flex';
    document.getElementById('page-info').textContent = currentPage + ' / ' + totalPages;
    document.getElementById('prev-btn').disabled = currentPage <= 1;
    document.getElementById('prev-btn').style.opacity = currentPage <= 1 ? '0.4' : '1';
    document.getElementById('next-btn').disabled = currentPage >= totalPages;
    document.getElementById('next-btn').style.opacity = currentPage >= totalPages ? '0.4' : '1';
  }
}

function filterByTag(tag, btn) {
  currentTag = tag;
  currentPage = 1;

  document.querySelectorAll('.filter-tab').forEach(function(b) { b.classList.remove('active'); });
  btn.classList.add('active');

  renderPage();
}

function changePage(direction) {
  var filtered = getFilteredItems();
  var totalPages = Math.ceil(filtered.length / POSTS_PER_PAGE);
  var newPage = currentPage + direction;
  if (newPage >= 1 && newPage <= totalPages) {
    currentPage = newPage;
    renderPage();
    window.scrollTo({ top: 0, behavior: 'smooth' });
  }
}

// Initial render
renderPage();
</script>

{% else %}
<div class="empty-state">
  <p>No posts yet. Add a Markdown file to get started!</p>
</div>
{% endif %}