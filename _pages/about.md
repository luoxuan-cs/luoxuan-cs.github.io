---
permalink: /
title: "Xuan Luo (罗炫)"
author_profile: true
---

Xuan Luo (罗炫)

I am a PhD student at UC Santa Barbara. My current research is mainly about efficient large language models and applications of generative models.

- github: https://github.com/luoxuan-cs
- huggingface: https://huggingface.co/xuan-luo
- google scholar: https://scholar.google.com/citations?user=z5pKzAcAAAAJ&hl

## Selected publications

<div class="pubs">
  <div class="pub-year">2025</div>
  <div class="pub-item">
    <div class="pub-title"><a href="/publication/2025-flexidepth">Adaptive Layer-skipping in Pre-trained LLMs</a></div>
    <div class="pub-authors">Xuan Luo, Weizhi Wang, Xifeng Yan</div>
    <div class="pub-venue">The Conference on Language Modeling, 2025</div>
    <div class="pub-oral">Oral Presentation</div>
    <div class="pub-buttons">
      <span class="btn-popover">
        <a class="btn-tag" href="#" onclick="return false;">ABSTRACT</a>
        <div class="popover">
          Various layer-skipping methods have been proposed to accelerate token generation in large language models (LLMs). However, they have overlooked a fundamental question: How do computational demands vary across the generation of different tokens? In this work, we introduce FlexiDepth, a method that dynamically adjusts the number of Transformer layers used in text generation. By incorporating a plug-in router and adapter, FlexiDepth enables adaptive layer-skipping in LLMs without modifying their original parameters. Introducing FlexiDepth to Llama-3-8B model achieves layer skipping of 8 layers out of 32, and meanwhile maintains the full 100% benchmark performance. Experimental results with FlexiDepth demonstrate that computational demands in LLMs significantly vary based on token type. Specifically, generating repetitive tokens or fixed phrases requires fewer layers, whereas producing tokens involving computation or high uncertainty requires more layers. Interestingly, this adaptive allocation pattern aligns with human intuition. To advance research in this area, we open sourced FlexiDepth and a dataset documenting FlexiDepth's layer allocation patterns for future exploration.
        </div>
      </span>
      <a class="btn-tag" href="https://arxiv.org/abs/2503.23798">PDF</a>
      <a class="btn-tag" href="https://huggingface.co/xuan-luo/FlexiDepth-Llama-3-8B-Instruct">CODE</a>
      <a class="btn-tag" href="https://huggingface.co/datasets/xuan-luo/FlexiPatterns-Llama-3-8B-Instruct">DATASET</a>
      <a class="btn-tag" href="/publication/2025-flexidepth">WEBSITE</a>
    </div>
  </div>
  <div class="pub-item">
    <div class="pub-title"><a href="/publication/2025-diffskip">DiffSkip: Differential Layer Skipping in Large Language Models</a></div>
    <div class="pub-authors">Xuan Luo, Weizhi Wang, Xifeng Yan</div>
    <div class="pub-venue">Findings of the Association for Computational Linguistics, 2025</div>
    <div class="pub-buttons">
      <span class="btn-popover">
        <a class="btn-tag" href="#" onclick="return false;">ABSTRACT</a>
        <div class="popover">
          Existing Large Language Models (LLMs) enforce uniform computation across all tokens. We analyze the correlation between the input-output difference of self-attention block and Feed-Forward Network (FFN) within the same transformer layer, and find that these two differential vectors are highly correlated. Thus, we propose to dynamically skip the FFN blocks based on the self-attention difference and introduce Diffential Layer Skipping (DiffSkip) to show that LLMs are inherently dynamic-depth models, capable of adjusting computational depth when generating different tokens. DiffSkip employs a lightweight router module to dynamically skip a set of FFN blocks in LLMs and only requires efficient fine-tuning while keeping the whole LLM frozen. Experimental results demonstrate that DiffSkip effectively enables dynamic FFN skipping in decoder-only language models, even in continuous token generation tasks where many layer-skipping methods struggle.
        </div>
      </span>
      <a class="btn-tag" href="https://aclanthology.org/2025.findings-acl.377.pdf">PDF</a>
      <a class="btn-tag" href="https://huggingface.co/xuan-luo/DiffSkip-Llama-3-8B-Instruct">CODE</a>
    </div>
  </div>
</div>
