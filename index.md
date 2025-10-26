---
layout: default
title: ""
permalink: /
toc: false
---

<style>
  /* ---------------- 基础结构 ---------------- */
  .skip-links, .masthead, .page__title { display: none !important; }
  .page { padding-top: 0 !important; }

  body {
    background: var(--bg);
    color: var(--text);
    line-height: 1.7;
    font-family: "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
    transition: background 0.3s ease, color 0.3s ease;
  }

  :root {
    --bg: #f7f7f7;
    --card: #ffffff;
    --text: #333333;
    --subtext: #555555;
    --shadow: rgba(0, 0, 0, 0.08);
  }

  body.dark-mode {
    --bg: #1e1e1e;
    --card: #2b2b2b;
    --text: #eaeaea;
    --subtext: #c0c0c0;
    --shadow: rgba(0, 0, 0, 0.4);
  }

  .home-wrapper {
    max-width: 900px;
    margin: 0 auto;
    padding: 48px 16px;
  }

  /* ---------------- 欢迎卡片 ---------------- */
  .intro-card {
    background: var(--card);
    border-radius: 18px;
    box-shadow: 0 4px 14px var(--shadow);
    padding: 40px 32px;
    text-align: center;
    margin-bottom: 32px;
  }
  .intro-card h1 { font-size: 2.2rem; font-weight: 700; margin: 0 0 12px; }
  .intro-card p  { font-size: 1.1rem; color: var(--subtext); }

  /* ---------------- 夜间模式按钮 ---------------- */
  .theme-toggle {
    position: fixed;
    top: 20px;
    right: 24px;
    background: var(--card);
    color: var(--text);
    border: none;
    border-radius: 50%;
    width: 44px;
    height: 44px;
    font-size: 1.2rem;
    cursor: pointer;
    box-shadow: 0 2px 6px var(--shadow);
    transition: transform 0.2s ease, box-shadow 0.3s ease;
    z-index: 1000;
  }
  .theme-toggle:hover {
    transform: translateY(-3px);
    box-shadow: 0 4px 12px var(--shadow);
  }

  /* ---------------- Recent Posts ---------------- */
  .posts-section h2 {
    text-align: center;
    font-size: 1.6rem;
    margin: 8px 0 16px;
  }

  .posts-grid {
    display: flex;
    flex-direction: column;
    gap: 16px;
  }

  .post-card {
    background: var(--card);
    border-radius: 14px;
    padding: 24px 28px;
    box-shadow: 0 2px 8px var(--shadow);
    transition: transform 0.15s ease, box-shadow 0.2s ease;
  }

  .post-card:hover {
    transform: translateY(-3px);
    box-shadow: 0 6px 14px var(--shadow);
  }

  .post-card h3 {
    margin: 0 0 6px;
    font-size: 1.3rem;
    color: var(--text);
  }

  .post-card .date {
    font-size: 0.85rem;
    color: var(--subtext);
    margin-bottom: 8px;
  }

  .post-card .excerpt {
    font-size: 0.95rem;
    color: var(--subtext);
    line-height: 1.6;
  }

  .page__footer {
    text-align: center;
    color: var(--subtext);
    font-size: 0.9rem;
    margin-top: 32px;
  }
</style>

<!-- 夜间/日间模式切换按钮 -->
<button class="theme-toggle" id="theme-toggle" aria-label="Toggle theme">🌙</button>

<script>
  // 记住用户选择
  const body = document.body;
  const btn = document.getElementById("theme-toggle");
  const storedTheme = localStorage.getItem("theme");

  if (storedTheme === "dark") {
    body.classList.add("dark-mode");
    btn.textContent = "🌞";
  }

  btn.addEventListener("click", () => {
    body.classList.toggle("dark-mode");
    const isDark = body.classList.contains("dark-mode");
    btn.textContent = isDark ? "🌞" : "🌙";
    localStorage.setItem("theme", isDark ? "dark" : "light");
  });
</script>

<div class="home-wrapper">

  <section class="intro-section">
    <div class="intro-card">
      <h1>👋 Welcome to Ruihan’s Log</h1>
      <p>
        Hi, this is <strong>Ruihan</strong> — documenting my explorations in
        <strong>Embodied Intelligence</strong>, <strong>VLA</strong>, and
        <strong>World Models</strong>.
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
