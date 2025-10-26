---
layout: splash
title: "👋 Welcome to Ruihan’s Log"
permalink: /
header:
  overlay_color: "#fafafa"
  overlay_filter: 0.05
  caption: ""

excerpt: "Hi, this is Ruihan. I’m documenting my learning notes on Embodied Intelligence, World Models, and Robotics.  
Stay tuned for my reflections, experiments, and readings."
feature_row:
  - title: "Latest Posts"
    excerpt: "Read my latest notes and insights."
    url: "/#posts"
---

{% include feature_row id="feature_row" %}

## 📝 Recent Posts {#posts}
{% for post in site.posts limit:5 %}
- [{{ post.title }}]({{ post.url | relative_url }})  
  <small>{{ post.date | date: "%B %d, %Y" }}</small>
{% endfor %}
