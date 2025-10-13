---
layout: default
title: "Direct Multi-Token Decoding"
permalink: /dmtd/
---

<html>
<head>
  <meta charset="utf-8">
  <meta name="description" content="Direct Multi-Token Decoding: Efficient Inference for Large Language Models">
  <meta name="keywords" content="Large Language Models, Multi-Token Decoding, Efficient Inference">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Direct Multi-Token Decoding</title>

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
    .container.is-max-desktop {
      max-width: 1152px; /* 960px * 1.2 = 1152px */
    }
    .content p {
      font-size: 1.15rem;
    }
    figcaption {
      font-size: 0.9rem !important; /* Smaller than is-size-6 */
    }
  </style>
</head>
<body>

<section class="hero">
  <div class="hero-body">
    <div class="container is-max-desktop">
      <div class="columns is-centered">
        <div class="column has-text-centered">
          <h1 class="title is-1 publication-title">Direct Multi-Token Decoding</h1>
          
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
                <a href="/images/dmtd/DMTD_arxiv.pdf" class="external-link button is-normal is-rounded is-dark">
                  <span class="icon">
                      <i class="fas fa-file-pdf"></i>
                  </span>
                  <span>Paper</span>
                </a>
              </span>
              <!-- Code Link. -->
              <span class="link-block">
                <a href="https://github.com/luoxuan-cs/Direct-Multitoken-Decoding" class="external-link button is-normal is-rounded is-dark">
                  <span class="icon">
                      <i class="fab fa-github"></i>
                  </span>
                  <span>Code</span>
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
            Decoder-only transformers have become the standard architecture for large language models (LLMs) due to their strong  performance. Recent studies suggest that, in pre-trained LLMs, early, middle, and late layers may serve distinct roles: Early layers focus on understanding the input context, middle layers handle task-specific processing, and late layers convert abstract representations into output tokens.  We hypothesize that once representations have been processed by the early and middle layers, the resulting hidden states may encapsulate sufficient information to support the generation of multiple tokens using only the late layers, eliminating the need to repeatedly traverse the early and middle layers. We refer to this inference paradigm as Direct Multi-Token Decoding (DMTD). Unlike speculative decoding, our method introduces no additional parameters, auxiliary routines, or post-generation verification. Despite being trained on a limited dataset, a fine-tuned DMTD Qwen3-4B model has already demonstrated promising results, achieving up to a 2× speedup with only minor performance loss. Moreover, as shown in our scaling analysis, its performance is expected to further improve with larger training datasets.
          </p>
        </div>
      </div>
    </div>
    <!--/ Abstract. -->

    <!-- Main Idea. -->
    <div class="columns is-centered has-text-centered">
      <div class="column is-four-fifths">
        <h2 class="title is-3">Main Idea</h2>
        <div class="content has-text-justified">
          <p>
            In our previous work <a href="/flexidepth/">FlexiDepth</a>, we discovered that pre-trained large language models contain redundancy, as many layers can be skipped without affecting performance. However, these layer-skipping patterns are irregular and difficult to provide acceleration in memory-bound scenarios. DMTD repurposes this redundancy into a regular pattern by cyclically reusing the late layers to efficiently generate multiple tokens. <strong>Importantly, DMTD introduces no additional parameters, auxiliary routines, or post-generation verification like speculative decoding.</strong>
          </p>
        </div>
      </div>
    </div>
    <!--/ Main Idea. -->

    <!-- Architecture. -->
    <div class="columns is-centered has-text-centered">
      <div class="column is-four-fifths">
        <h2 class="title is-3">Architecture</h2>
        <div class="content has-text-justified">
          <p>
            Unlike the vanilla decoder-only transformer that generates tokens one by one through full forward passes, the proposed DMTD operates in fixed multi-token cycles. Figure 1 (right) demonstrates the generation pipeline of DMTD in a single cycle. DMTD performs only one full forward pass at the beginning of the cycle and then reuses the later layers to decode multiple tokens consecutively. This cycle-based setting transforms the irregular computational redundancies observed in pre-trained LLMs into a fixed periodical pattern for efficient decoding.
          </p>
        </div>
        <figure>
          <img src="/images/dmtd/fig1.png" alt="DMTD Architecture" style="width: 100%;">
          <figcaption class="has-text-centered is-size-6" style="margin-top: 1rem;">
            Figure 1: Vanilla next token prediction vs. Direct Multi-Token Decoding.
          </figcaption>
        </figure>
      </div>
    </div>
    <!--/ Architecture. -->

    <!-- Placeholder for future content -->
    <div class="columns is-centered has-text-centered">
      <div class="column is-four-fifths">
        <div class="content has-text-justified">
          <p style="text-align: center; font-style: italic; margin-top: 2rem;">
            More content coming soon...
          </p>
        </div>
      </div>
    </div>
    <!--/ Placeholder -->
  </div>
</section>

</body>
</html>

