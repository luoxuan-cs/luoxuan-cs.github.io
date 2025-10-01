---
layout: default
title: "Adaptive Layer-skipping in Pre-trained LLMs"
permalink: /flexidepth/
---

<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="description" content="FlexiDepth: Adaptive Layer-skipping in Pre-trained LLMs">
  <meta name="keywords" content="Large Language Models, Layer Skipping, Efficient Inference">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Adaptive Layer-skipping in Pre-trained LLMs</title>

  <link href="https://fonts.googleapis.com/css?family=Google+Sans|Noto+Sans|Castoro" rel="stylesheet">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/jpswalsh/academicons@1/css/academicons.min.css">
  
  <style>
    body {
      font-family: 'Noto Sans', sans-serif;
    }
    .publication-title {
      font-family: 'Google Sans', sans-serif;
    }
    .publication-authors {
      font-family: 'Google Sans', sans-serif;
    }
  </style>
</head>
<body>

<section class="hero">
  <div class="hero-body">
    <div class="container is-max-desktop">
      <div class="columns is-centered">
        <div class="column has-text-centered">
          <h1 class="title is-1 publication-title">Adaptive Layer-skipping in Pre-trained LLMs</h1>
          
          <div class="is-size-5 publication-authors">
            <span class="author-block">
              <a href="https://luoxuan-cs.github.io/">Xuan Luo</a><sup>1</sup>,&nbsp;&nbsp;
            </span> 
            <span class="author-block">
              <a href="https://victorwz.github.io/">Weizhi Wang</a><sup>1</sup>,&nbsp;&nbsp;
            </span>
            <span class="author-block">
              <a href="https://sites.cs.ucsb.edu/~xyan/">Xifeng Yan</a><sup>1</sup>&nbsp;&nbsp;
            </span>
          </div>

          <div class="is-size-5 publication-authors">
            <span class="author-block"><sup>1</sup>University of California, Santa Barbara</span>
          </div>

          <div class="column has-text-centered">
            <div class="publication-links">
              <!-- PDF Link. -->
              <span class="link-block">
                <a href="https://arxiv.org/abs/2503.23798" class="external-link button is-normal is-rounded is-dark">
                  <span class="icon">
                      <i class="fas fa-file-pdf"></i>
                  </span>
                  <span>Paper</span>
                </a>
              </span>
              <!-- Code Link. -->
              <span class="link-block">
                <a href="https://huggingface.co/xuan-luo/FlexiDepth-Llama-3-8B-Instruct" class="external-link button is-normal is-rounded is-dark">
                  <span class="icon">
                      <i class="fab fa-github"></i>
                  </span>
                  <span>Code</span>
                </a>
              </span>
              <!-- Model Link. -->
              <span class="link-block">
                <a href="https://huggingface.co/xuan-luo/FlexiDepth-Llama-3-8B-Instruct" class="external-link button is-normal is-rounded is-dark">
                  <span class="icon">
                    🤗
                  </span>
                  <span>Model</span>
                </a>
              </span>
              <!-- Dataset Link. -->
              <span class="link-block">
                <a href="https://huggingface.co/datasets/xuan-luo/FlexiPatterns-Llama-3-8B-Instruct" class="external-link button is-normal is-rounded is-dark">
                  <span class="icon">
                    🤗
                  </span>
                  <span>Dataset</span>
                </a>
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<section class="section">
  <div class="container is-max-desktop">
    <!-- Abstract. -->
    <div class="columns is-centered has-text-centered">
      <div class="column is-four-fifths">
        <h2 class="title is-3">Abstract</h2>
        <div class="content has-text-justified">
          <p>
            Various layer-skipping methods have been proposed to accelerate token generation in large language models (LLMs). However, they have overlooked a fundamental question: How do computational demands vary across the generation of different tokens? In this work, we introduce FlexiDepth, a method that dynamically adjusts the number of Transformer layers used in text generation. By incorporating a plug-in router and adapter, FlexiDepth enables adaptive layer-skipping in LLMs without modifying their original parameters. Introducing FlexiDepth to Llama-3-8B model achieves layer skipping of 8 layers out of 32, and meanwhile maintains the full 100% benchmark performance. Experimental results with FlexiDepth demonstrate that computational demands in LLMs significantly vary based on token type. Specifically, generating repetitive tokens or fixed phrases requires fewer layers, whereas producing tokens involving computation or high uncertainty requires more layers. Interestingly, this adaptive allocation pattern aligns with human intuition. To advance research in this area, we open sourced FlexiDepth and a dataset documenting FlexiDepth's layer allocation patterns for future exploration.
          </p>
        </div>
      </div>
    </div>
    <!--/ Abstract. -->
    <!-- Image -->
    <div class="columns is-centered has-text-centered">
      <div class="column is-four-fifths">
        <figure>
          <img src="/images/flexidepth/fig1.png" alt="Layer-skipping patterns">
          <figcaption class="has-text-centered is-size-5" style="margin-top: 1rem;">
            Layer-skipping patterns (Llama-3-8B-Instruct) for a language task (left) and a math task (right). The light-to-dark blue gradient represents layer usage from 16 to 32.
          </figcaption>
        </figure>
      </div>
    </div>
    <!--/ Image. -->
  </div>
</section>

</body>
</html> 