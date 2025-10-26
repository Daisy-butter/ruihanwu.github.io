---
layout: post
title: "RoboBrain 2.0: Embodied Intelligence with Multimodal Models"
date: 2025-10-26
permalink: /robobrain/
---

<style>
  /* ----------- 页面总体样式 ----------- */
  .post-wrapper {
    display: flex;
    flex-direction: row;
    justify-content: center;
    gap: 40px;
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem 1rem;
  }

  .post-main {
    flex: 3;
    max-width: 800px;
  }

  .post-toc {
    flex: 1;
    position: sticky;
    top: 120px;
    align-self: flex-start;
    background: var(--card);
    border-radius: 10px;
    padding: 1rem 1.2rem;
    box-shadow: 0 2px 10px rgba(0,0,0,0.05);
    height: fit-content;
  }

  .post-toc h3 {
    font-size: 1rem;
    margin-bottom: 0.8rem;
    border-bottom: 1px solid #ddd;
    padding-bottom: 0.3rem;
  }

  .post-toc ul {
    list-style: none;
    padding-left: 0;
    margin: 0;
  }

  .post-toc li {
    margin-bottom: 0.4rem;
  }

  .post-toc a {
    color: var(--subtext);
    text-decoration: none;
    font-size: 0.9rem;
  }

  .post-toc a:hover {
    color: #007acc;
  }

  /* ----------- 标题区与摘要 ----------- */
  .post-header {
    text-align: center;
    margin-bottom: 1.5rem;
  }

  .post-header h1 {
    font-size: 1.75rem;
    font-weight: 700;
    margin-bottom: 0.5rem;
  }

  .post-header .meta {
    color: #777;
    font-size: 0.85rem;
  }

  .abstract-box {
    background: var(--card);
    border-left: 4px solid #007acc;
    border-radius: 6px;
    padding: 1.2rem 1.5rem;
    margin: 1.5rem 0 2rem 0;
    font-size: 0.95rem;
    color: var(--subtext);
    box-shadow: 0 2px 6px rgba(0,0,0,.05);
  }

  /* ----------- 正文部分 ----------- */
  .post-content {
    font-size: 0.97rem;
    line-height: 1.7;
    color: var(--text);
  }

  .post-content h2 {
    margin-top: 2rem;
    margin-bottom: 1rem;
    font-size: 1.2rem;
    border-left: 3px solid #007acc;
    padding-left: 10px;
  }

  .post-content img {
    display: block;
    margin: 1.2rem auto;
    max-width: 100%;
    border-radius: 6px;
    box-shadow: 0 1px 8px rgba(0,0,0,.08);
  }

  .post-content blockquote {
    border-left: 3px solid #007acc;
    padding-left: 1rem;
    color: #555;
    font-style: italic;
    margin: 1.2rem 0;
  }

  .post-content code {
    background: #f3f3f3;
    padding: 2px 5px;
    border-radius: 4px;
    font-family: monospace;
    font-size: 0.9rem;
  }

  /* ----------- 表格 ----------- */
  .post-content table {
    border-collapse: collapse;
    width: 100%;
    margin: 1.5rem 0;
    font-size: 0.9rem;
  }

  .post-content th, .post-content td {
    border: 1px solid #ddd;
    padding: 8px 10px;
  }

  .post-content th {
    background-color: #f0f0f0;
    font-weight: 600;
  }

  .post-content tr:nth-child(even) {
    background-color: #fafafa;
  }

  .post-content tr:hover {
    background-color: #f5f5f5;
  }

  /* ----------- 页脚 ----------- */
  .post-footer {
    margin-top: 3rem;
    text-align: center;
    font-size: 0.85rem;
    color: #999;
  }

  /* 夜间模式兼容 */
  body.dark-mode .post-toc { background: #2a2a2a; }
  body.dark-mode .post-toc a { color: #ccc; }
  body.dark-mode .abstract-box { background: #2b2b2b; color: #ccc; }
  body.dark-mode .post-content th { background: #333; color: #ddd; }
</style>

<div class="post-header">
  <h1>RoboBrain 2.0: Embodied Intelligence with Multimodal Models</h1>
  <p class="meta">October 26, 2025 • Research Note</p>
</div>

<div class="post-wrapper">

  <!-- 主要内容 -->
  <div class="post-main">

    <div class="abstract-box">
      <strong>Abstract:</strong>  
      RoboBrain 2.0 integrates **visual**, **language**, and **action reasoning** within an embodied framework.  
      This post introduces the design motivation, system structure, and research outlook of RoboBrain 2.0.
    </div>

    <div class="post-content" id="post-content">

### 1. Motivation
The RoboBrain project aims to unify **perception**, **understanding**, and **interaction** into a coherent cognitive model for embodied agents.

> “An embodied agent should not just see or act — it should *understand* the causal world it interacts with.”

---

### 2. System Architecture
Below is a simplified view of the multimodal reasoning pipeline.

![Placeholder Figure](figure1.png)

**Core Components:**
- **Perceptual Frontend:** Vision-language encoder (e.g., CLIP-style)
- **World Model:** Predictive latent dynamics with physical grounding
- **Policy Module:** Flow-based decision network for embodied control

| Module | Description | Example |
|:--|:--|:--|
| Perception | Visual encoder | CLIP |
| World Model | Predictive latent dynamics | Dreamer |
| Policy | Flow-based control | MeanFlow-Q |

---

### 3. Future Directions
Potential next steps include:
- Expanding multimodal grounding to tactile and audio inputs  
- Integrating *MeanFlow policy distillation* for better stability  
- Applying RoboBrain 2.0 in **simulation-to-real transfer** experiments  

---

### References
1. BAAI. *RoboBrain 2.0: Embodied Intelligence with Multimodal World Models*, 2025.  
2. Wu, R. & Xi, H. *Explorations in Embodied Intelligence and Flow-based Learning*, Fudan University, 2025.

---

    </div>

    <div class="post-footer">
      ← <a href="{{ '/' | relative_url }}">Back to Home</a>
    </div>
  </div>

  <!-- 右侧目录 -->
  <aside class="post-toc" id="toc">
    <h3>Contents</h3>
    <ul id="toc-list"></ul>
  </aside>
</div>

<script>
  // 自动生成目录
  const tocList = document.getElementById("toc-list");
  const headers = document.querySelectorAll(".post-content h2, .post-content h3");
  headers.forEach(h => {
    const id = h.textContent.trim().replace(/\s+/g, '-').toLowerCase();
    h.id = id;
    const li = document.createElement("li");
    li.innerHTML = `<a href="#${id}">${h.textContent}</a>`;
    tocList.appendChild(li);
  });
</script>
