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
    .dmtd-scroll {
      overflow-x: auto;
      margin: 1.5rem 0;
    }
    .dmtd-loop-diagram {
      display: block;
      width: 100%;
      min-width: 640px;
    }
    .dmtd-results-table {
      width: 100%;
      border-collapse: collapse;
      font-variant-numeric: tabular-nums;
      white-space: nowrap;
    }
    .dmtd-results-table caption {
      caption-side: bottom;
      white-space: normal;
      text-align: center;
      font-size: 0.9rem;
      padding-top: 1rem;
    }
    .dmtd-results-table th,
    .dmtd-results-table td {
      padding: 0.65rem 0.7rem;
      text-align: center;
    }
    .dmtd-results-table thead {
      border-top: 2px solid currentColor;
      border-bottom: 1px solid currentColor;
    }
    .dmtd-results-table tbody {
      border-bottom: 2px solid currentColor;
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
                <a href="https://openreview.net/pdf?id=gdo9Cv6rL3" class="external-link button is-normal is-rounded is-dark">
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
              <!-- Model Link. -->
              <span class="link-block">
                <a href="https://huggingface.co/xuan-luo/DMTD-Qwen3-4B" class="external-link button is-normal is-rounded is-dark">
                  <span class="icon">
                    🤗
                  </span>
                  <span>Model</span>
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
            Recent studies suggest that pre-trained large language models (LLMs) might develop distinct functional roles across their layers: early layers focus on understanding the input context, middle layers handle task-specific processing, and late layers map abstract representations to output tokens. Inspired by the intuition that humans can produce an extended sequence of speech from a single act of reading and thinking, we hypothesize that a single pass through the early and middle layers could provide sufficient information to support the decoding of multiple future tokens. Accordingly, we propose Direct Multi-Token Decoding (DMTD), which performs only one full forward pass for every <i>n</i> tokens and reuses the late layers to decode multiple subsequent tokens. Unlike speculative decoding, our method introduces no additional computation, auxiliary routines, or post-generation verification. With minimal training overhead, a Qwen3-4B model finetuned with DMTD achieves up to a 2.15× speedup with marginal performance loss, and our scaling analysis indicates that its performance could be further improved with larger-scale training.
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
          <p>
            DMTD is also compatible with speculative decoding. Since a DMTD model can generate several tokens in one cycle, it can serve as its own fast drafter and then verify the drafted tokens with the full DMTD model. We provide a <a href="https://huggingface.co/xuan-luo/DMTD-Qwen3-4B">DMTD Qwen3-4B model</a> with several decoding variants, including DMTD, DMTD with speculative decoding, tree speculative decoding, and Medusa-style tree speculative decoding.
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

    <!-- Connection to Looped Transformers. -->
    <div class="columns is-centered has-text-centered">
      <div class="column is-four-fifths">
        <h2 class="title is-3">Connection to Looped Transformers</h2>
        <div class="content has-text-justified">
          <p>
            <a href="https://arxiv.org/abs/2502.05171">Looped Transformers</a> increase computational depth by repeatedly refining hidden states before predicting the next token. DMTD explores a complementary direction: one full-depth pass supports several successive token predictions through the late layers, with missing early- and middle-layer KV entries refilled at cycle boundaries. Both perspectives relax the fixed coupling between full-depth processing and token generation. This suggests a future direction: jointly adapting how much latent computation to perform and how many tokens to generate between full-depth updates.
          </p>
        </div>
        <figure>
          <div class="dmtd-scroll" tabindex="0" role="region" aria-label="Looped Transformers, DMTD, and adaptive computation schematic">
            <img class="dmtd-loop-diagram" src="/images/dmtd/looped-transformers.svg" alt="Looped Transformers: loop n times in latent space before one token. DMTD: one full-depth pass supports n successive tokens through the late layers, averaging 1/n full-depth passes per token, with KV refill at cycle boundaries. Adaptive, a future direction: jointly vary latent computation and the number of tokens between full-depth updates.">
          </div>
          <figcaption>
            Complementary ways to allocate computation. “Loop 1/n times” denotes the average full-depth update frequency per token in DMTD; late-layer decoding still occurs for every token. Adaptive computation is a proposed future direction.
          </figcaption>
        </figure>
      </div>
    </div>
    <!--/ Connection to Looped Transformers. -->

    <!-- Scaling with Training Data. -->
    <div class="columns is-centered has-text-centered">
      <div class="column is-four-fifths">
        <h2 class="title is-3">Scaling with Training Data</h2>
        <div class="content has-text-justified">
          <p>
            We conducted scaling experiments to understand how DMTD's performance improves with increasing training data across different model sizes (0.5B, 1.5B, 3B, 7B, and 14B parameters). The results reveal a consistent decrease in cross-entropy loss as training data increases for all model sizes, with the trends approximating log-linear relationships. Our current training uses only 1.5B tokens with a 4K context length. With large-scale continued pre-training, the performance of our method is expected to further improve, potentially enabling each cycle to decode more tokens efficiently. Training with longer contexts and reinforcement learning (RL) may also help further improve performance; these remain directions for future exploration.
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
            We evaluate our method by reusing the last 8 layers of Qwen3-4B, where C&tau; denotes a decoding cycle of &tau; tokens. Across six benchmarks, C2 and C3 achieve 100.9% and 99.4% of the vanilla model's overall performance, respectively, while C4 retains 95.9%. Extending the cycle to C6 reduces overall performance to 81.7%, illustrating the trade-off between cycle length and prediction quality.
          </p>
        </div>
        <div class="dmtd-scroll" tabindex="0" role="region" aria-label="Benchmark results by decoding cycle length">
          <table class="dmtd-results-table">
            <caption>Table 1: The influence of different cycle lengths. C&tau; denotes a decoding cycle of &tau; tokens. The overall score reflects the average relative performance compared to the vanilla Qwen3-4B.</caption>
            <thead>
              <tr><th scope="col">Model</th><th scope="col">ARC-E</th><th scope="col">ARC-C</th><th scope="col">WinoGrande</th><th scope="col">GSM8K</th><th scope="col">CoQA</th><th scope="col">MBPP+</th><th scope="col">Overall</th></tr>
            </thead>
            <tbody>
              <tr><th scope="row">Vanilla</th><td>0.934</td><td>0.922</td><td>0.657</td><td>0.907</td><td>0.805</td><td>0.669</td><td>100.0%</td></tr>
              <tr><th scope="row">C2</th><td>0.930</td><td>0.897</td><td>0.701</td><td>0.901</td><td>0.798</td><td>0.693</td><td>100.9%</td></tr>
              <tr><th scope="row">C3</th><td>0.921</td><td>0.886</td><td>0.673</td><td>0.889</td><td>0.780</td><td>0.698</td><td>99.4%</td></tr>
              <tr><th scope="row">C4</th><td>0.916</td><td>0.881</td><td>0.652</td><td>0.866</td><td>0.749</td><td>0.627</td><td>95.9%</td></tr>
              <tr><th scope="row">C6</th><td>0.872</td><td>0.801</td><td>0.601</td><td>0.500</td><td>0.672</td><td>0.536</td><td>81.7%</td></tr>
            </tbody>
          </table>
        </div>
        <div class="content has-text-justified" style="margin-top: 2rem;">
          <p>
            Our method achieves up to 2.15× speedup when generating 4 tokens per cycle (C4), while retaining 95.9% of the vanilla model's overall benchmark performance. DMTD does not rely on speculative decoding, but it is orthogonal and complementary to speculative decoding techniques. The plain DMTD results shown here can therefore be further combined with self-speculative variants implemented in the released model.
          </p>
        </div>
        <figure style="margin-top: 2rem;">
          <img src="/images/dmtd/fig4.png" alt="Speedup Comparison" style="width: 80%;">
          <figcaption class="has-text-centered is-size-6" style="margin-top: 1rem;">
            Speedup over vanilla Qwen3-4B across batch sizes. MTD2, MTD3, and MTD4 in the plot correspond to C2, C3, and C4 in Table 1.
          </figcaption>
        </figure>
      </div>
    </div>
    <!--/ Results. -->
  </div>
</section>

</body>
</html>
