---
layout: page
permalink: /writing/
title: Writing
description: Technical articles and insights on AI, machine learning, and reinforcement learning.
nav: true
nav_order: 3
---

Technical deep dives and practical guides on RAG, vector databases, embeddings, LLM fine-tuning, and multimodal AI. 
<style>
.blog-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
  gap: 1.25rem;
  margin-top: 2rem;
  margin-bottom: 2rem;
}

.blog-card {
  background: var(--global-card-bg-color);
  border: 1px solid var(--global-divider-color);
  border-radius: 12px;
  overflow: hidden;
  transition: box-shadow 0.3s ease, transform 0.3s ease;
  height: fit-content;
}

.blog-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.08);
}

html[data-theme="dark"] .blog-card:hover {
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.3);
}

.blog-content {
  padding: 1.25rem 1.5rem;
}

.blog-title {
  font-size: 1.05rem;
  font-weight: 600;
  margin-bottom: 0.4rem;
  color: var(--global-text-color);
  line-height: 1.4;
  letter-spacing: -0.01em;
}

.blog-title a {
  color: inherit;
  text-decoration: none;
  transition: color 0.2s ease;
}

.blog-title a:hover {
  color: var(--global-theme-color);
}

.blog-description {
  font-size: 0.875rem;
  color: var(--global-text-color-light);
  margin-bottom: 1rem;
  line-height: 1.6;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.blog-meta {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 0.75rem;
  border-top: 1px solid var(--global-divider-color);
}

.blog-date {
  font-size: 0.8rem;
  color: var(--global-text-color-light);
  font-variant-numeric: tabular-nums;
}

.blog-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
}

.blog-tag {
  background: rgba(8, 145, 178, 0.1);
  color: var(--global-theme-color);
  padding: 0.15rem 0.55rem;
  border-radius: 6px;
  font-size: 0.7rem;
  font-weight: 500;
  letter-spacing: 0.01em;
}

html[data-theme="dark"] .blog-tag {
  background: rgba(34, 211, 238, 0.1);
}

.external-link-icon {
  display: inline-block;
  margin-left: 0.35rem;
  font-size: 0.75rem;
  opacity: 0.5;
  transition: opacity 0.2s ease;
}

.blog-title a:hover .external-link-icon {
  opacity: 1;
}

.external-tag {
  color: white;
  padding: 0.15rem 0.55rem;
  border-radius: 6px;
  font-size: 0.7rem;
  font-weight: 500;
  letter-spacing: 0.01em;
}

.external-tag.weaviate {
  background: #0d9488;
}

.external-tag.together {
  background: #6366f1;
}

@media (max-width: 768px) {
  .blog-grid {
    grid-template-columns: 1fr;
    gap: 1rem;
  }
}
</style>

{% comment %}
Get all posts from external data sources
Display them in chronological order (newest first)
{% endcomment %}

{% assign weaviate_posts = site.data.weaviate_posts.weaviate_posts %}
{% assign external_posts = site.data.weaviate_posts.external_posts %}

{% comment %} Create a combined array manually sorted by date {% endcomment %}
{% assign all_posts_with_dates = "" | split: "" %}

{% comment %} Add external posts (Together AI, etc.) with their dates for sorting {% endcomment %}
{% for post in external_posts %}
{% assign date_string = post.date | date: "%Y%m%d" %}
{% assign post_with_sort = post.title | prepend: date_string | append: "|external|" | append: forloop.index0 %}
{% assign all_posts_with_dates = all_posts_with_dates | push: post_with_sort %}
{% endfor %}

{% comment %} Add Weaviate posts with their dates for sorting {% endcomment %}
{% for post in weaviate_posts %}
{% assign date_string = post.date | date: "%Y%m%d" %}
{% assign post_with_sort = post.title | prepend: date_string | append: "|weaviate|" | append: forloop.index0 %}
{% assign all_posts_with_dates = all_posts_with_dates | push: post_with_sort %}
{% endfor %}

{% assign sorted_post_refs = all_posts_with_dates | sort | reverse %}

<div class="blog-grid">
{% for post_ref in sorted_post_refs %}
  {% assign ref_parts = post_ref | split: "|" %}
  {% assign post_type = ref_parts[1] %}
  {% assign post_index = ref_parts[2] | plus: 0 %}
  
  {% if post_type == "external" %}
    {% assign current_post = external_posts[post_index] %}
  {% else %}
    {% assign current_post = weaviate_posts[post_index] %}
  {% endif %}
  
  <div class="blog-card">
    <div class="blog-content">
      <h3 class="blog-title">
        <a href="{{ current_post.url }}" target="_blank">{{ current_post.title }}<span class="external-link-icon">↗</span></a>
      </h3>
      <p class="blog-description">
        {{ current_post.description }}
      </p>
      <div class="blog-meta">
        <span class="blog-date">{{ current_post.date | date: "%B %d, %Y" }}</span>
        <div class="blog-tags">
          {% if current_post.source == "Weaviate" %}
            <span class="external-tag weaviate">{{ current_post.source }}</span>
          {% else %}
            <span class="external-tag together">{{ current_post.source }}</span>
          {% endif %}
          {% for tag in current_post.tags limit: 2 %}
            <span class="blog-tag">{{ tag }}</span>
          {% endfor %}
        </div>
      </div>
    </div>
  </div>
{% endfor %}
</div>
