---
layout: single
title: "Adaptive Layer-skipping in Pre-trained LLMs"
permalink: /flexidepth/
author_profile: false
---

<style>
.project-page {
  max-width: 900px;
  margin: 0 auto;
  padding: 20px;
}
.project-title {
  font-size: 2.2rem;
  font-weight: 700;
  text-align: center;
  margin-bottom: 1.5rem;
  line-height: 1.3;
}
.authors {
  text-align: center;
  font-size: 1.1rem;
  margin-bottom: 1.5rem;
  line-height: 1.6;
}
.authors a {
  color: #2c5aa0;
  text-decoration: none;
}
.authors a:hover {
  text-decoration: underline;
}
.btn-container {
  display: flex;
  justify-content: center;
  gap: 15px;
  margin: 2rem 0;
  flex-wrap: wrap;
}
.project-btn {
  display: inline-block;
  padding: 10px 24px;
  font-size: 1rem;
  font-weight: 600;
  color: #fff !important;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border: none;
  border-radius: 8px;
  text-decoration: none;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
}
.project-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4);
}
.section {
  margin: 2.5rem 0;
}
.section-title {
  font-size: 1.6rem;
  font-weight: 700;
  margin-bottom: 1rem;
  border-bottom: 2px solid #e3e5e8;
  padding-bottom: 0.5rem;
}
.abstract-text {
  font-size: 1.05rem;
  line-height: 1.8;
  text-align: justify;
  color: #333;
}
</style>

<div class="project-page">
  <h1 class="project-title">Adaptive Layer-skipping in Pre-trained LLMs</h1>
  
  <div class="authors">
    <a href="https://luoxuan-cs.github.io/">Xuan Luo</a><sup>1</sup>,
    <a href="https://victorwz.github.io/">Weizhi Wang</a><sup>1</sup>,
    <a href="https://sites.cs.ucsb.edu/~xyan/">Xifeng Yan</a><sup>1</sup>
    <br>
    <sup>1</sup>University of California, Santa Barbara
  </div>

  <div class="btn-container">
    <a class="project-btn" href="https://arxiv.org/abs/2503.23798">📄 Paper</a>
    <a class="project-btn" href="https://huggingface.co/xuan-luo/FlexiDepth-Llama-3-8B-Instruct">💻 Code</a>
    <a class="project-btn" href="https://huggingface.co/xuan-luo/FlexiDepth-Llama-3-8B-Instruct">🤖 Model</a>
    <a class="project-btn" href="https://huggingface.co/datasets/xuan-luo/FlexiPatterns-Llama-3-8B-Instruct">📊 Dataset</a>
  </div>

  <div class="section">
    <h2 class="section-title">Abstract</h2>
    <p class="abstract-text">
      Various layer-skipping methods have been proposed to accelerate token generation in large language models (LLMs). However, they have overlooked a fundamental question: How do computational demands vary across the generation of different tokens? In this work, we introduce FlexiDepth, a method that dynamically adjusts the number of Transformer layers used in text generation. By incorporating a plug-in router and adapter, FlexiDepth enables adaptive layer-skipping in LLMs without modifying their original parameters. Introducing FlexiDepth to Llama-3-8B model achieves layer skipping of 8 layers out of 32, and meanwhile maintains the full 100% benchmark performance. Experimental results with FlexiDepth demonstrate that computational demands in LLMs significantly vary based on token type. Specifically, generating repetitive tokens or fixed phrases requires fewer layers, whereas producing tokens involving computation or high uncertainty requires more layers. Interestingly, this adaptive allocation pattern aligns with human intuition. To advance research in this area, we open sourced FlexiDepth and a dataset documenting FlexiDepth's layer allocation patterns for future exploration.
    </p>
  </div>
</div> 