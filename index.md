---
layout: default
title: ""
permalink: /
toc: false
---

<style>
  /* 让首页干净：隐藏顶部跳转链接和站点 masthead（全站效果） */
  .skip-links, .masthead, .page__title { display: none !important; }
  /* 去掉默认顶部空白 */
  .page { padding-top: 0 !important; }

  /* 背景与字体 */
  body { background: #f7f7f7; color: #333; line-height: 1.7; }
  .home-wrapper { max-width: 900px; margin: 0 auto; padding: 48px 16px; }

  /* 欢迎卡片（居中、白底、圆角阴影） */
  .intro-card {
    background: #fff; border-radius: 18px;
    box-shadow: 0 4px 14px rgba(0,0,0,.08);
    padding: 40px 32px; text-align: center; margin-bottom: 32px;
  }
  .intro-card h1 { font-size: 2.2rem; font-weight: 700; margin: 0 0 12px; }
  .intro-card p  { font-size: 1.1rem; color: #555; }

  /* “Recent Posts” 标题 */
  .posts-section h2 { text-align: center; font-size: 1.6rem; margin: 8px 0 16px; }

  /* 文章卡片：白底、圆角、阴影、悬浮提升 */
  .posts-grid { display: flex; flex-direction: column; gap: 16px; }
  .post-card {
    background: #fff; border-radius: 14px; padding: 24px 28px;
    box-shadow: 0 2px 8px rgba(0,0,0,.06);
    transition: transform .15s ease, box-shadow .2s ease;
  }
  .post-card:hover { transform: translateY(-3px); box-shadow: 0 6px 14px rgba(0,0,0,.10); }
  .post-card h3 { margin: 0 0 6px; font-size: 1.25rem; color: #333; }
  .post-card .date { font-size: .85rem; color: #888; margin: 0 0 8px; }
  .post-card .excerpt { font-size: .95rem; color: #555; line-height: 1.6; }

  /* 可选：页脚更简洁 */
  .page__footer { text-align: center; color: #777; font-size: .9rem; margin-top: 32px; }
</style>

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
      {% for post in site.posts limit: 10 %}
        <article class="post-card">
          <a href="{{ post.url | relative_url }}">
            <h3>{{ post.title }}</h3>
            <p class="date">{{ post.date | date: "%B %d, %Y" }}</p>
            <p class="excerpt">{{ post.excerpt | strip_html | default: post.content | strip_html | truncatewords: 28 }}</p>
          </a>
        </article>
      {% endfor %}
    </div>
  </section>

</div>
