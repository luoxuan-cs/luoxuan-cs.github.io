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
          <img src="/images/dmtd/fig1.png" alt="DMTD Architecture" style="width: 70%;">
          <figcaption class="has-text-centered is-size-6" style="margin-top: 1rem;">
            Vanilla next token prediction vs. Direct Multi-Token Decoding.
          </figcaption>
        </figure>
      </div>
    </div>
    <!--/ Architecture. -->

    <!-- Scaling with Training Data. -->
    <div class="columns is-centered has-text-centered">
      <div class="column is-four-fifths">
        <h2 class="title is-3">Scaling with Training Data</h2>
        <div class="content has-text-justified">
          <p>
            We conducted scaling experiments to understand how DMTD's performance improves with increasing training data across different model sizes (0.5B, 1.5B, 3B, 7B, and 14B parameters). The results reveal a consistent decrease in cross-entropy loss as training data increases for all model sizes, with the trends approximating log-linear relationships. Our current training uses only 1.5B tokens. With large-scale continued pre-training, the performance of our method is expected to improve significantly, potentially enabling each cycle to decode more tokens efficiently.
          </p>
        </div>
        <figure>
          <img src="/images/dmtd/fig2.png" alt="Scaling Law" style="width: 60%;">
          <figcaption class="has-text-centered is-size-6" style="margin-top: 1rem;">
            Scaling law of the proposed Direct Multi-token Decoding. The x-axis represents the number of training tokens (in billions) on a logarithmic scale, while the y-axis shows the cross-entropy loss.
          </figcaption>
        </figure>
      </div>
    </div>
    <!--/ Scaling with Training Data. -->

    <!-- Results. -->
    <div class="columns is-centered has-text-centered">
      <div class="column is-four-fifths">
        <h2 class="title is-3">Results</h2>
        <div class="content has-text-justified">
          <p>
            We evaluate our method by reusing the last 8 layers of Qwen3-4B, where MTDx denotes decoding x tokens per cycle (cycle length). As shown in the figure below, our method performs well with cycle lengths up to MTD4.
          </p>
        </div>
        <figure>
          <img src="/images/dmtd/fig3.png" alt="Throughput Comparison" style="width: 80%;">
          <figcaption class="has-text-centered is-size-6" style="margin-top: 1rem;">
            Throughput (tokens per second) comparison of our method and Qwen3-4B.
          </figcaption>
        </figure>
        <figure style="margin-top: 2rem;">
          <img src="/images/dmtd/fig4.png" alt="Speedup Comparison" style="width: 80%;">
          <figcaption class="has-text-centered is-size-6" style="margin-top: 1rem;">
            Speedup comparison.
          </figcaption>
        </figure>
        <div class="content has-text-justified" style="margin-top: 2rem;">
          <p>
            Our method achieves up to 2× speedup when generating 4 tokens per cycle. <strong>Importantly, our method does not rely on speculative decoding and is orthogonal to such techniques</strong>, meaning it can potentially be combined with speculative decoding methods for further performance improvements.
          </p>
        </div>
      </div>
    </div>
    <!--/ Results. -->

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

