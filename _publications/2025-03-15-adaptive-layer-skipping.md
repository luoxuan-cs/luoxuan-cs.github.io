---
title: "Adaptive Layer-skipping in Pre-trained LLMs"
collection: publications
category: conferences
permalink: /publication/2025-flexidepth
excerpt: 'Xuan Luo, Weizhi Wang, Xifeng Yan<br/><details><summary>Abstract</summary>Various layer-skipping methods have been proposed to accelerate token generation in large language models (LLMs). However, they have overlooked a fundamental question: How do computational demands vary across the generation of different tokens? In this work, we introduce FlexiDepth, a method that dynamically adjusts the number of Transformer layers used in text generation. By incorporating a plug-in router and adapter, FlexiDepth enables adaptive layer-skipping in LLMs without modifying their original parameters. Introducing FlexiDepth to Llama-3-8B model achieves layer skipping of 8 layers out of 32, and meanwhile maintains the full 100% benchmark performance. Experimental results with FlexiDepth demonstrate that computational demands in LLMs significantly vary based on token type. Specifically, generating repetitive tokens or fixed phrases requires fewer layers, whereas producing tokens involving computation or high uncertainty requires more layers. Interestingly, this adaptive allocation pattern aligns with human intuition. To advance research in this area, we open sourced FlexiDepth and a dataset documenting FlexiDepth''s layer allocation patterns for future exploration.<br/><a href="https://arxiv.org/abs/2503.23798">PDF</a> | <a href="https://huggingface.co/xuan-luo/FlexiDepth-Llama-3-8B-Instruct">Code</a> | <a href="https://huggingface.co/datasets/xuan-luo/FlexiPatterns-Llama-3-8B-Instruct">Dataset</a></details>'
date: 2025-03-15
venue: 'The Conference on Language Modeling'
paperurl: 'https://arxiv.org/abs/2503.23798'
selected: true
---

Xuan Luo, Weizhi Wang, Xifeng Yan

- [PDF](https://arxiv.org/abs/2503.23798)
- [Code](https://huggingface.co/xuan-luo/FlexiDepth-Llama-3-8B-Instruct)
- [Dataset](https://huggingface.co/datasets/xuan-luo/FlexiPatterns-Llama-3-8B-Instruct)

**Venue**: COLM 25 Spotlight

### Abstract
Various layer-skipping methods have been proposed to accelerate token generation in large language models (LLMs). However, they have overlooked a fundamental question: How do computational demands vary across the generation of different tokens? In this work, we introduce FlexiDepth, a method that dynamically adjusts the number of Transformer layers used in text generation. By incorporating a plug-in router and adapter, FlexiDepth enables adaptive layer-skipping in LLMs without modifying their original parameters. Introducing FlexiDepth to Llama-3-8B model achieves layer skipping of 8 layers out of 32, and meanwhile maintains the full 100% benchmark performance. Experimental results with FlexiDepth demonstrate that computational demands in LLMs significantly vary based on token type. Specifically, generating repetitive tokens or fixed phrases requires fewer layers, whereas producing tokens involving computation or high uncertainty requires more layers. Interestingly, this adaptive allocation pattern aligns with human intuition. To advance research in this area, we open sourced FlexiDepth and a dataset documenting FlexiDepth's layer allocation patterns for future exploration. 