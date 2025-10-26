---
layout: post
title: "Non-E2E VLA models"
date: 2025-10-26
permalink: /non-e2e-VLA/
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

<!-- 在这里插入markdownify开关 -->
    {% capture post_content %}

<!-- 这里开始markdown正文。 -->

In this post I survey a growing class of **non-end-to-end Vision-Language-Action (VLA)** systems. These architectures deliberately decouple high-level cognition (vision + language → plan) from low-level control (plan → motion/trajectory), introducing structured intermediate representations (IR). Two prominent paradigms — exemplified by RoboBrain and Gemini Robotics 1.5 — highlight divergent design choices in how cognition and execution are connected, and provide a useful lens for surveying broader work.

---

## 1. Why go “non-E2E” in VLA?  
End-to-end VLA systems — inputting raw vision + language and directly emitting motor commands — are appealing in their simplicity, but pose significant difficulties:  
- **Lack of modular interpretability**: it is difficult to trace “why” a robot chose a certain motion.  
- **Poor error recovery or replanning**: when mid-task states drift, end-to-end systems struggle to adapt.  
- **Limited cross-embodiment generalization**: monolithic policies often over-fit to one robot morphology.  
By contrast, non-end-to-end designs split the pipeline and insert intermediate representations (IR), enabling clearer division of labour, easier debugging, plug-in modules and better generalisation.

---

## 2. A taxonomy of non-E2E VLA systems  
I organise the space along two key dimensions:  
1. **Cognition vs Execution**: Are planning and control implemented in separate modules?  
2. **Intermediate Representation (IR) complexity**: Does the system produce a simple label (e.g., subtask tag), a structured task graph, or a full trajectory/code-plan?  

| Class | Description | IR type | Example systems |
|:--|-------------|---------|----------------|
| **B1** – Planner + Controller (Minimal IR) | High-level module produces a subtask or skill label, passed to a pre-scripted controller. | Skill label / textual sub-goal | SayCan-style systems |
| **B2** – Planner + Structured IR + Controller | Adds explicit structured IR (subtask sequence, affordance graph, waypoints) bridging planning and control. | Task graph, affordance map, waypoint trajectory | RoboBrain |
| **B3** – Multi-system / Hybrid (Strong IR + some end-to-end) | Strong cognition and strong execution, with latent/action-token IR, cross-embodiment transfer, multi-robot policy. | Code plan, motion transfer tokens, latent action token sequence | Gemini Robotics 1.5 |

---

## 3. Positioning RoboBrain vs Gemini Robotics 1.5  
### 3.1 RoboBrain  
RoboBrain is a recently published system that explicitly decomposes robotic manipulation into **Planning → Affordance Perception → Trajectory Prediction**, addressing key missing capabilities in large multimodal language models when applied to robotics.
- IR: detailed affordance annotations + end-effector trajectories drawn from a heterogeneous dataset (ShareRobot) designed for long-horizon manipulation tasks.
- Category: **B2 (structured IR)**  
- Strengths: Clear modular separation, rich IR, strong interpretability and debug-ability.  
- Limitations: Requires manual annotation of affordance/trajectory data; control execution still relies on traditional modules / cannot necessarily generalize to completely unseen morphologies without adaptation.

### 3.2 Gemini Robotics 1.5  
While fewer peer-review publications are publicly available (some sources via media coverage), Gemini Robotics 1.5 from Google DeepMind is emblematic of a “strong IR + hybrid” architecture. 
- IR: internal reasoning traces (chain-of-thought style), motion-transfer tokens, unified across multiple robot morphologies and tasks.  
- Category: **B3 (high IR + hybrid)**  
- Strengths: Zero-shot cross-robot generalisation; “think before act” paradigm; potential for multi-embodiment reuse.  
- Limitations: System complexity is very high, intermediate modules are less transparent; high compute/training cost; details still emerging.

---

## 4. Broader related work  
Beyond the two “anchor” systems above, there is a wider ecosystem of non-E2E VLA and modular embodied systems. Below are some representative works and design angles to watch.

### 4.1 Modular pipelines with affordance/skill labels  
- Systems such as **“Do As I Can, Not As I Say”** (2022/23) decompose tasks into language-level instructions and a fixed skill set, producing affordance scores and selecting from predefined skills.  
- These belong broadly to **B1** category: minimal IR (skill labels) and rely heavily on pre-scripted controllers.

### 4.2 Structured IR systems (task graphs, waypoints)  
- Many recent works adopt task graph generation, 3D scene graph understanding, affordance region prediction and waypoint sequences.  
- For instance, the survey “A Survey on Vision-Language-Action Models for Embodied AI” (2025) provides a taxonomy and identifies clear separation of planner vs control modules.  
- This class aligns with **B2**: richer IR, structured bridging of cognition and control.

### 4.3 Hybrid / multi-embodiment systems  
- Emerging research emphasises cross-morphology generalisation, action-tokenisation, latent plan representations, motion transfer.  
- Surveys like “Large VLM-based Vision-Language-Action Models for Robotic Manipulation: A Survey” (2025) highlight the hierarchical (planning/execution) vs monolithic dichotomy and emphasise explicit IR decoupling.   
- Such systems map directly into **B3**: strong IR, modular planning, and high-level generalisation.

### 4.4 Efficiency & deployment oriented work  
- More recently, “Efficient Vision-Language-Action Models for Embodied Manipulation: A Systematic Survey” (2025) deals with latency, model size, edge-deployment constraints in VLA systems.   
- Even within modular designs, there is an increasing focus on efficiency (compression, lower memory, faster inference) and real-world deployment rather than just benchmark performance.

---

## 5. Implications for your research  
From your vantage — building VLA systems with modularity, interpretability, and scalability — the taxonomy suggests several design decisions:

- **Decide your IR granularity**: Will you stop at subtask labels (B1), or go as far as trajectory/code plans (B2/B3)?  
- **Select your modular cut**: Where will you split cognition vs execution? A clean planning module enables reuse across robots.  
- **Consider data annotation cost**: More structured IR (affordance/trajectory) improves performance but increases annotation and dataset cost.  
- **Balance generality vs cost**: Hybrid systems (B3) offer best generalisation across embodiments but at high infrastructure/training cost.  
- **Ensure error-handling and replanning**: Modular systems allow mid-task corrections and transparent monitoring; end-to-end monoliths struggle in dynamic environments.  
- **Consider deployment constraints**: Efficiency, real-time control and physical robot constraints (latency, actuation bandwidth, safety) require attention especially if targeting real-world robot systems.

---

## 6. Conclusion  
Non-end-to-end VLA architectures are emerging as a pragmatic middle way between fully monolithic control and purely symbolic planning. By injecting structured intermediate representations and decoupling cognition from execution, these systems gain interpretability, modularity, and improved generalisation. Understanding where systems like RoboBrain and Gemini Robotics 1.5 lie in this spectrum helps clarify design trade-offs and provides a roadmap for your own system architecture.

---

## References  
- Ji Y, Tan H, Shi J, et al. *RoboBrain: A Unified Brain Model for Robotic Manipulation from Abstract to Concrete*. CVPR 2025. 
- Shao R, Li W, Zhang L, et al. *Large VLM-based Vision-Language-Action Models for Robotic Manipulation: A Survey*. 2025. 
- Guan W, Hu Q, Li A, Cheng J. *Efficient Vision-Language-Action Models for Embodied Manipulation: A Systematic Survey*. 2025. 
- Sui X, Tian D, Sun Q, et al. *From Grounding to Manipulation: Case Studies of Foundation Model Integration in Embodied Robotic Systems*. 2025. 



<!-- 正文到这里结束。 -->
    {% endcapture %}
    {{ post_content | markdownify }}
<!-- 上面这一行强制让 Markdown 在 HTML 中被解析。 -->

<script>
</script>
