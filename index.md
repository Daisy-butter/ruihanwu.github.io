---
layout: default
title: "Ruihan’s Log"
permalink: /
---

<div class="home-wrapper">

  <section class="intro-section">
    <div class="intro-card">
      <h1>👋 Welcome to Ruihan’s Log</h1>
      <p>
        Hi, this is <strong>Ruihan</strong> — documenting my explorations in
        <strong>Embodied Intelligence</strong>, <strong>World Models</strong>, and
        <strong>Robotics Learning</strong>.
      </p>
    </div>
  </section>

  <section class="posts-section">
    <h2>📝 Recent Posts</h2>
    <div class="posts-grid">
      {% for post in site.posts limit:6 %}
      <article class="post-card">
        <a href="{{ post.url | relative_url }}">
          <h3>{{ post.title }}</h3>
          <p class="date">{{ post.date | date: "%B %d, %Y" }}</p>
          <p class="excerpt">{{ post.excerpt | strip_html | truncatewords: 25 }}</p>
        </a>
      </article>
      {% endfor %}
    </div>
  </section>

</div>
