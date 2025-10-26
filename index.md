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
    line-height: 1.65;
    font-family: "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
    font-size: 15px;
    transition: background 0.3s ease, color 0.3s ease;
  }

  :root {
    --bg: #f7f7f7;
    --card: #ffffff;
    --text: #2d2d2d;
    --subtext: #555555;
    --shadow: rgba(0, 0, 0, 0.08);
  }

  body.dark-mode {
    --bg: #1e1e1e;
    --card: #2b2b2b;
    --text: #eaeaea;
    --subtext: #bdbdbd;
    --shadow: rgba(0, 0, 0, 0.4);
  }

  .home-wrapper {
    max-width: 900px;
    margin: 0 auto;
    padding: 48px 16px;
  }

  /* ---------------- 欢迎区（学术化样式） ---------------- */
  .intro-card {
    text-align: center;
    padding: 60px 32px 30px;
    margin-bottom: 20px;
    background: transparent;
  }
  .intro-card h1 {
    font-size: 1.9rem;
    font-weight: 700;
    letter-spacing: 0.3px;
    color: var(--text);
    margin-bottom: 14px;
  }
  .intro-card p {
    font-size: 1rem;
    color: var(--subtext);
    line-height: 1.7;
    max-width: 720px;
    margin: 0 auto;
  }
  .intro-card em {
    color: var(--text);
    font-style: normal;
    font-weight: 500;
  }

  /* ---------------- 夜间模式按钮 ---------------- */
  .theme-toggle {
    position: fixed;
    top: 20px;
    right: 24px;
    background: var(--card);
    color: var(--text);
    border: none;
    border-radius: 50%;
    width: 40px;
    height: 40px;
    font-size: 1rem;
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
    font-size: 1.3rem;
    letter-spacing: 0.3px;
    color: var(--text);
    margin: 32px 0 18px;
  }

  .posts-grid {
    display: flex;
    flex-direction: column;
    gap: 14px;
  }

  .post-card {
    background: var(--card);
    border-radius: 10px;
    padding: 20px 24px;
    box-shadow: 0 1px 6px var(--shadow);
    transition: transform 0.15s ease, box-shadow 0.2s ease;
  }

  .post-card:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 10px var(--shadow);
  }

  .post-card h3 {
    margin: 0 0 5px;
    font-size: 1.1rem;
    color: var(--text);
    font-weight: 600;
  }

  .post-card a {
    text-decoration: none;
    color: var(--text);
  }

  .post-card a:hover h3 {
    color: var(--text);
  }

  .post-card .date {
    font-size: 0.82rem;
    color: var(--subtext);
    margin-bottom: 6px;
  }

  .post-card .excerpt {
    font-size: 0.9rem;
    color: var(--subtext);
    line-height: 1.6;
  }

  .page__footer {
    text-align: center;
    color: var(--subtext);
    font-size: 0.85rem;
    margin-top: 36px;
  }
</style>

<!-- 夜间/日间模式切换按钮 -->
<button class="theme-toggle" id="theme-toggle" aria-label="Toggle theme">🌙</button>

<script>
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
        <em>Exploring the intersection of Embodied Intelligence, World Models, and Robotics Learning.</em><br>
      </p>
    </div>
  </section>

  <section class="posts-section">
    <h2>Recent Posts</h2>
    <div class="posts-grid">
    {% for post in site.data.posts %}
        <article class="post-card">
            <a href="{{ post.url | absolute_url }}">
            <h3>{{ post.title }}</h3>
            <p class="date">{{ post.date | date: "%B %d, %Y" }}</p>
            <p class="excerpt">{{ post.excerpt }}</p>
            </a>
        </article>
    {% endfor %}

    </div>
  </section>

</div>
