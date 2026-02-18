---
layout: page
permalink: /talks/
title: Talks
description: Conference talks, workshops, and presentations.
nav: false
nav_order: 4
---

Conference talks, workshops, and live coding sessions on RAG, vector databases, multimodal AI, LLM fine-tuning, and coding agents. Want me to speak at your event? Reach out via my social links.

<style>
.video-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(360px, 1fr));
  gap: 1.25rem;
  margin-top: 2rem;
  margin-bottom: 2rem;
}

.video-card {
  background: var(--global-card-bg-color);
  border: 1px solid var(--global-divider-color);
  border-radius: 12px;
  overflow: hidden;
  transition: box-shadow 0.3s ease, transform 0.3s ease;
}

.video-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.08);
}

html[data-theme="dark"] .video-card:hover {
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.3);
}

.video-embed {
  position: relative;
  width: 100%;
  height: 0;
  padding-bottom: 56.25%;
  cursor: pointer;
  background: #0f172a;
}

.video-embed iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border: 0;
}

.video-embed .video-thumb {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: opacity 0.3s ease;
}

.video-card:hover .video-thumb {
  opacity: 0.9;
}

.video-embed .play-btn {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 64px;
  height: 44px;
  pointer-events: none;
  transition: transform 0.2s ease;
}

.video-card:hover .play-btn {
  transform: translate(-50%, -50%) scale(1.08);
}

.video-embed .play-btn svg {
  width: 100%;
  height: 100%;
  filter: drop-shadow(0 2px 8px rgba(0,0,0,0.3));
}

.video-info {
  padding: 0.875rem 1.125rem;
}

.video-title {
  font-size: 0.925rem;
  font-weight: 600;
  margin-bottom: 0.35rem;
  color: var(--global-text-color);
  line-height: 1.4;
  letter-spacing: -0.01em;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.video-meta {
  font-size: 0.8rem;
  color: var(--global-text-color-light);
  margin-bottom: 0.25rem;
}

.video-channel {
  font-size: 0.75rem;
  color: var(--global-theme-color);
  font-weight: 500;
}

@media (max-width: 768px) {
  .video-grid {
    grid-template-columns: 1fr;
    gap: 1rem;
  }
}
