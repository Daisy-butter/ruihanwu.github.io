---
layout: default
title: "👋 Welcome to Ruihan’s Log"
permalink: /
---

<div class="home-container">
  <div class="intro-card">
    <h1 class="intro-title">👋 Welcome to Ruihan’s Log</h1>
    <p class="intro-text">
      Hi, this is Ruihan. I’m documenting my learning notes on <strong>Embodied Intelligence</strong>,
      <strong>World Models</strong>, and <strong>Robotics</strong>.
      Stay tuned for my reflections, experiments, and readings.
    </p>
  </div>

  <h2 class="recent-title">📝 Recent Posts</h2>

  <div class="post-list">
    {% for post in site.posts limit:10 %}
      <div class="post-card">
        <a href="{{ post.url | relative_url }}"><h3>{{ post.title }}</h3></a>
        <p class="post-date">{{ post.date | date: "%B %d, %Y" }}</p>
        <p class="post-excerpt">{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
      </div>
    {% endfor %}
  </div>
</div>
