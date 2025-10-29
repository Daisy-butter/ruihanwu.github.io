---
layout: post
title: "Dual System VLA Approach"
date: 2025-10-26
permalink: /dual-system-VLA/
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

Large-scale Vision-Language-Action (VLA) research has recently shifted toward *dual-system architectures*, where high-level cognition and low-level control co-exist but operate differently. A common analogy draws on the human **System-2 (cortex)** — capable of abstract reasoning, task understanding, and planning — and **System-1 (cerebellum/spinal circuit)** — responsible for fast, reactive motor control. However, the implementation varies dramatically across recent embodied AI systems.  

This blog post provides a high-level overview of these systems, focusing specifically on **how System-2 and System-1 are constructed**, **what forms the intermediate representation (IR)** between them, and **how gradients or knowledge flow across the divide**.

---

## 1️⃣ Dual-System with **implicit latent IR**
Some VLA architectures avoid exposing the intermediate representation explicitly, instead encoding planning information and task semantics in latent vectors that are consumed directly by the controller. 

### MineDreamer
MineDreamer embodies an implicit factorization: a world-model-based System-2 predicts future states and evaluates action consequences, while a System-1 executor tracks and minimizes the latent distance toward the desired goal embedding. The **Goal Q-former** distills language-conditioned semantic targets into a latent embedding space, enabling visually grounded imagination without textual dispatch during execution.

![MineDreamer](/assets/img/dual-system-vla/MineDreamer.png){: width="600" }

### MetaQueries
MetaQueries infers a latent **skill semantic embedding** from observed behavior, enabling a robot to “understand” *what* skill is being performed and reproduce it in new contexts. The planner and the controller communicate purely through the latent skill representation, capturing generalizable structure beyond explicit affordance labels or trajectories.

![MetaQueries](/assets/img/dual-system-vla/MetaQueries.png){: width="600" }

### Knowledge-Insulating VLA Models (pi0.5-KI family)
A crucial innovation in this line of work is **allowing gradients from execution to flow back** to the cognitive module, while protecting linguistic knowledge from being corrupted by noisy action supervision. Semantic adapters restrict the updates to *execution-relevant* representation dimensions — achieving beneficial bidirectional learning while preserving language/world understanding.

![KI-VLA](/assets/img/dual-system-vla/KI-VLA.png)

---

## 2️⃣ Dual-System with **explicit intermediate structure**
Other systems emphasize clearly articulated IR that reflects task structure, spatial geometry, or sub-goal semantics, typically yielding stronger interpretability and controllability.

### InternVLA-N1 / InternVLA-M1
These systems divide the brain into **a VLM planner (System-2)** and **a diffusion-based motion policy (System-1)**. Navigation (N1) employs pixel or latent goal tokens, while manipulation (M1) leverages explicit spatial grounding and operational hints. Crucially, execution is often asynchronous, enabling high-frequency control without blocking planning.

![InternVLA-N1](/assets/img/dual-system-vla/InternVLA-N1.png)

![InternVLA-M1](/assets/img/dual-system-vla/InternVLA-M1.png)

### SayCan
SayCan pioneered the modern “LLM planner → skill executor” split. A language model selects skills conditioned on *affordance Q-values*, ensuring that what the LLM suggests is physically executable. This explicit IR-based decision filter became a canonical blueprint for dual-system alignments.

![SayCan](/assets/img/dual-system-vla/SayCan.png)

### RoboDual
RoboDual takes modularity further: a **Generalist System-2** performs task reasoning and selects both skills and control modes, while **Specialist System-1** controllers are optimized for specific motion regimes. End-to-end gradient flow enables System-2 to gradually understand embodiment constraints without sacrificing structure.

![RoboDual](/assets/img/dual-system-vla/RoboDual.png)

### RoboBrain
RoboBrain enriches System-2 reasoning with **affordance perception and detailed trajectory IR**, yielding strong transparency and physical feasibility. Although still modular, it covers long-horizon manipulation more effectively by grounding the planner in scene understanding.

![RoboBrain](/assets/img/dual-system-vla/RoboBrain.png)

---

## 3️⃣ “Quasi Dual-System”: single-model **internal factorization**
Some state-of-the-art foundation models **emulate dual-system behavior inside a unified transformer**, blending reasoning, future prediction, and execution.

### VLA-R1
Trained with **SFT + GRPO**, VLA-R1 learns an internal separation between *understanding* and *execution*: SFT shapes the model’s semantic and syntactic action space, while GRPO sculpts motion quality and safety. It behaves as if a System-2 policy head supervises a System-1 motor head — but both share a single neural substrate.

![VLA-R1] (.{.{ site.baseurl }.}/assets/img/dual-system-vla/VLA-R1.png)

### UniVLA
UniVLA integrates vision-language alignment, world-model post-training, and policy learning *all within a single autoregressive model*: no explicit modular boundaries exist. Yet, its unified token space implicitly carries both System-2 knowledge and System-1 feasibility — a trend toward fully integrated cognitive-motor architectures.

![UniVLA](/assets/img/dual-system-vla/UniVLA.png)

### Gemini Robotics Series
Gemini-Robotics models can be viewed as evolving toward **a universal brain** capable of reasoning and acting through latent action tokens. Though the exact IR remains opaque, it is clear the model orchestrates planning and control jointly inside a shared transformer world-model.

![Gemini](/assets/img/dual-system-vla/Gemini.png)

### WorldVLA
A general transformer world-model is trained to predict action-conditioned future observations and then refined through policy learning. Cognition and execution are ultimately inseparable within this causal predictive substrate — embodying the long-term convergence of dual-system ideas.

![WorldVLA](/assets/img/dual-system-vla/WorldVLA.png)

---

## Closing Perspective
Across all these lines, we witness a compelling trajectory:

> Early systems established **clear dual-system decomposition**,  
> while recent models increasingly pursue **fully unified architectures**  
> — where planning and control co-evolve within a single world-model.

Yet, the **intermediate representation** remains the linchpin. Whether explicit (waypoints, affordances, spatial relations) or implicit (skill latent, future-state imagination), the IR determines how **System-2 knowledge** shapes **System-1 execution** — and how the body teaches the brain.

This unified view aims to help researchers navigate the rapidly expanding VLA landscape with clarity on the essential design choices shaping embodied intelligence.

---

<!-- 正文到这里结束。 -->
  {% endcapture %}
  {{ post_content | markdownify }}

<!-- 上面这一行强制让 Markdown 在 HTML 中被解析。 -->

<script>
</script>
