# AI-Papers-and-leaderboard
This is a website for the best research papers about AI and a couple more topics such as agentic AI. It also ranks them
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>AI Papers & Docs Leaderboard</title>
  <style>
    :root {
      --font-sans: system-ui, "Segoe UI", Roboto, "Noto Sans", "Helvetica Neue", Arial, "Apple Color Emoji", "Segoe UI Emoji", sans-serif;
      --font-mono: ui-monospace, "Cascadia Code", "Cascadia Mono", "Segoe UI Mono", Consolas, "Noto Mono", monospace;
      --bg: #0c0f14;
      --surface: #141a24;
      --surface2: #1c2433;
      --border: #2a3548;
      --text: #e8edf5;
      --muted: #8b9bb4;
      --accent: #5eead4;
      --accent-dim: #2dd4bf33;
      --gold: #fcd34d;
      --silver: #cbd5e1;
      --bronze: #fdba74;
    }

    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      min-height: 100vh;
      font-family: var(--font-sans);
      background: radial-gradient(ellipse 120% 80% at 50% -20%, #1a2f3d 0%, var(--bg) 55%);
      color: var(--text);
      line-height: 1.5;
    }

    .wrap {
      max-width: 960px;
      margin: 0 auto;
      padding: 2rem 1.25rem 3rem;
    }

    header {
      margin-bottom: 2rem;
    }

    h1 {
      font-size: clamp(1.5rem, 4vw, 2rem);
      font-weight: 700;
      letter-spacing: -0.02em;
      margin: 0 0 0.5rem;
    }

    .sub {
      color: var(--muted);
      font-size: 0.95rem;
      max-width: 62ch;
    }

    .controls {
      display: flex;
      flex-wrap: wrap;
      gap: 1rem;
      align-items: flex-end;
      margin-bottom: 1.5rem;
      padding: 1rem 1.25rem;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 12px;
    }

    label {
      display: flex;
      flex-direction: column;
      gap: 0.35rem;
      font-size: 0.75rem;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.06em;
      color: var(--muted);
    }

    select {
      font-family: var(--font-mono);
      font-size: 0.9rem;
      padding: 0.55rem 0.75rem;
      min-width: 240px;
      background: var(--surface2);
      color: var(--text);
      border: 1px solid var(--border);
      border-radius: 8px;
      cursor: pointer;
    }

    select:focus {
      outline: 2px solid var(--accent);
      outline-offset: 2px;
    }

    .count {
      margin-left: auto;
      font-size: 0.85rem;
      color: var(--muted);
    }

    .count strong {
      color: var(--accent);
      font-weight: 600;
    }

    ol.leaderboard {
      list-style: none;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      gap: 0.65rem;
    }

    .row {
      display: grid;
      grid-template-columns: auto 1fr auto;
      gap: 1rem;
      align-items: center;
      padding: 1rem 1.1rem;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 10px;
      transition: border-color 0.15s, background 0.15s;
    }

    .row:hover {
      border-color: #3d4f6a;
      background: var(--surface2);
    }

    .rank {
      font-family: var(--font-mono);
      font-weight: 500;
      font-size: 1.1rem;
      width: 2.5rem;
      text-align: center;
    }

    .rank.top1 { color: var(--gold); }
    .rank.top2 { color: var(--silver); }
    .rank.top3 { color: var(--bronze); }

    .meta {
      min-width: 0;
    }

    .title {
      font-weight: 600;
      font-size: 1rem;
      margin: 0 0 0.25rem;
    }

    .title a {
      color: inherit;
      text-decoration: none;
    }

    .title a:hover {
      color: var(--accent);
    }

    .detail {
      font-size: 0.82rem;
      color: var(--muted);
      display: flex;
      flex-wrap: wrap;
      gap: 0.5rem 1rem;
      align-items: baseline;
    }

    .detail .src {
      font-family: var(--font-mono);
      font-size: 0.72rem;
      color: #a5b8d6;
      padding: 0.15rem 0.45rem;
      border: 1px solid var(--border);
      border-radius: 4px;
      max-width: 100%;
    }

    .score {
      font-family: var(--font-mono);
      font-size: 0.85rem;
      padding: 0.35rem 0.6rem;
      background: var(--accent-dim);
      color: var(--accent);
      border-radius: 6px;
      white-space: nowrap;
    }

    li.empty {
      list-style: none;
      text-align: center;
      padding: 3rem 1rem;
      color: var(--muted);
      border: 1px dashed var(--border);
      border-radius: 12px;
    }

    footer {
      margin-top: 2rem;
      font-size: 0.8rem;
      color: var(--muted);
      line-height: 1.65;
    }

    footer a {
      color: var(--accent);
    }

    .share {
      margin-bottom: 1.5rem;
      padding: 1rem 1.25rem;
      background: var(--surface2);
      border: 1px solid var(--border);
      border-radius: 12px;
      font-size: 0.9rem;
    }

    .share p {
      margin: 0 0 0.75rem;
      color: var(--muted);
      max-width: 70ch;
    }

    .share p strong {
      color: var(--text);
    }

    .btn-row {
      display: flex;
      flex-wrap: wrap;
      gap: 0.5rem;
      align-items: center;
      margin-bottom: 0.5rem;
    }

    .btn {
      font: inherit;
      font-size: 0.85rem;
      font-weight: 600;
      cursor: pointer;
      padding: 0.5rem 0.85rem;
      border-radius: 8px;
      border: 1px solid var(--accent);
      color: var(--accent);
      background: transparent;
    }

    .btn:hover {
      background: var(--accent-dim);
    }

    .btn:focus-visible {
      outline: 2px solid var(--accent);
      outline-offset: 2px;
    }

    a.btn {
      display: inline-block;
      text-decoration: none;
    }

    .share-hint {
      margin: 0 !important;
      font-size: 0.8rem !important;
    }
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <h1>AI papers &amp; documents leaderboard</h1>
      <p class="sub">
        Curated reading list with <strong>about 200</strong> papers and policy references (2023–2026 plus classics). Links point to many hosts worldwide. This page uses <strong>system fonts only</strong> (no Google Fonts), so you can save it and open it offline. Higher <em>score</em> only controls order on this page.
      </p>
    </header>

    <div class="controls">
      <label>
        Topic
        <select id="topic" aria-label="Filter by topic"></select>
      </label>
      <p class="count" id="count"></p>
    </div>

    <div class="share" role="region" aria-label="Download and share">
      <p><strong>Share anywhere:</strong> download a standalone copy of this page, the raw reading list as JSON, or the whole folder as a ZIP. Recipients only need a browser; outbound paper links still require internet.</p>
      <div class="btn-row">
        <button type="button" class="btn" id="btn-save-html">Download this page (.html)</button>
        <button type="button" class="btn" id="btn-save-json">Download reading list (.json)</button>
        <a class="btn" id="zip-link" href="AI-Papers-Leaderboard.zip" download="AI-Papers-Leaderboard.zip">Download ZIP pack (.zip)</a>
      </div>
      <p class="share-hint">Tip: you can also use the browser menu “Save page as…” on this file. The ZIP includes <code>index.html</code> plus the Windows launcher scripts when shared from the project folder.</p>
    </div>

    <ol class="leaderboard" id="board" aria-live="polite"></ol>

    <footer>
      <strong>Keep current:</strong>
      <a href="https://huggingface.co/papers" target="_blank" rel="noopener">Hugging Face Daily Papers</a>,
      <a href="https://paperswithcode.com/" target="_blank" rel="noopener">Papers with Code</a>,
      <a href="https://arxiv.org/list/cs.AI/recent" target="_blank" rel="noopener">arXiv cs.AI</a>,
      <a href="https://aiindex.stanford.edu/" target="_blank" rel="noopener">Stanford AI Index</a>,
      <a href="https://digital-strategy.ec.europa.eu/en/library/european-parliament-and-council-regulation-laying-down-harmonised-rules-artificial-intelligence-and" target="_blank" rel="noopener">EU AI Act (EUR-Lex)</a>,
      <a href="https://dblp.org" target="_blank" rel="noopener">dblp (Trier, DE)</a>,
      <a href="https://hal.science" target="_blank" rel="noopener">HAL open science (FR)</a>.
    </footer>
  </div>

  <script>
    /**
     * @type {{ topic: string, title: string, authors: string, year: number, score: number, url: string, source: string, note?: string }[]}
     */
    const ENTRIES = [
      /* —— Large language models —— */
      { topic: "Large language models", title: "GPT-4 technical report", authors: "OpenAI", year: 2024, score: 98, url: "https://openai.com/research/gpt-4", source: "OpenAI (US)" },
      { topic: "Large language models", title: "The Llama 3 herd of models", authors: "Dubey et al. (Meta)", year: 2024, score: 97, url: "https://ai.meta.com/research/publications/the-llama-3-herd-of-models/", source: "Meta AI (US)" },
      { topic: "Large language models", title: "Gemini: a family of highly capable multimodal models", authors: "Team Google / DeepMind", year: 2024, score: 96, url: "https://arxiv.org/abs/2312.11805", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Introducing Claude 3 (model family overview)", authors: "Anthropic", year: 2024, score: 95, url: "https://www.anthropic.com/news/claude-3-family", source: "Anthropic (US)" },
      { topic: "Large language models", title: "Mistral 7B", authors: "Jiang et al. (Mistral AI)", year: 2023, score: 92, url: "https://arxiv.org/abs/2310.06825", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Mixtral of Experts", authors: "Jiang et al. (Mistral AI)", year: 2024, score: 93, url: "https://arxiv.org/abs/2401.04088", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "DeepSeek-V3 technical report", authors: "DeepSeek-AI", year: 2025, score: 94, url: "https://arxiv.org/abs/2412.19437", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "DeepSeek-R1: incentivizing reasoning in LLMs", authors: "DeepSeek-AI", year: 2025, score: 95, url: "https://arxiv.org/abs/2501.12948", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Training compute-optimal large language models (Chinchilla)", authors: "Hoffmann et al.", year: 2022, score: 94, url: "https://www.deepmind.com/publications/training-compute-optimal-large-language-models", source: "Google DeepMind (UK)" },
      { topic: "Large language models", title: "Language models are few-shot learners (GPT-3)", authors: "Brown et al.", year: 2020, score: 93, url: "https://arxiv.org/abs/2005.14165", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "LoRA: Low-Rank Adaptation of LLMs", authors: "Hu et al.", year: 2022, score: 91, url: "https://openreview.net/forum?id=nZeVKeeFYf9", source: "OpenReview / ICLR" },
      { topic: "Large language models", title: "Attention is all you need", authors: "Vaswani et al.", year: 2017, score: 99, url: "https://papers.nips.cc/paper/2017/hash/3f5ee243547dee91fbd053c1c4a845aa-Abstract.html", source: "NeurIPS proceedings" },
      { topic: "Large language models", title: "BERT: pre-training of deep bidirectional transformers", authors: "Devlin et al.", year: 2019, score: 90, url: "https://aclanthology.org/N19-1423/", source: "ACL Anthology (intl.)" },
      { topic: "Large language models", title: "OLMo: accelerating the science of language models", authors: "Groeneveld et al. (AI2)", year: 2024, score: 89, url: "https://arxiv.org/abs/2402.00838", source: "arXiv (open mirror)" },

      /* —— Alignment & safety —— */
      { topic: "Alignment & safety", title: "OpenAI o1 system card", authors: "OpenAI", year: 2024, score: 93, url: "https://openai.com/index/openai-o1-system-card/", source: "OpenAI (US)" },
      { topic: "Alignment & safety", title: "Constitutional AI: harmlessness from AI feedback", authors: "Bai et al.", year: 2022, score: 91, url: "https://www.anthropic.com/research/constitutional-ai-harmlessness-from-ai-feedback", source: "Anthropic (US)" },
      { topic: "Alignment & safety", title: "Training language models to follow instructions with human feedback", authors: "Ouyang et al.", year: 2022, score: 92, url: "https://openreview.net/forum?id=TG8KACxE13", source: "OpenReview" },
      { topic: "Alignment & safety", title: "Direct preference optimization (DPO)", authors: "Rafailov et al.", year: 2024, score: 90, url: "https://arxiv.org/abs/2305.18290", source: "arXiv (open mirror)" },
      { topic: "Alignment & safety", title: "RLHF: training a helpful and harmless assistant", authors: "Glaese et al.", year: 2022, score: 88, url: "https://arxiv.org/abs/2204.05862", source: "arXiv (open mirror)" },
      { topic: "Alignment & safety", title: "Concrete problems in AI safety", authors: "Amodei et al.", year: 2016, score: 86, url: "https://arxiv.org/abs/1606.06565", source: "arXiv (open mirror)" },
      { topic: "Alignment & safety", title: "Weak-to-strong generalization", authors: "OpenAI Superalignment", year: 2023, score: 85, url: "https://openai.com/research/weak-to-strong-generalization", source: "OpenAI (US)" },
      { topic: "Alignment & safety", title: "Frontier AI regulation: managing emerging risks to public safety", authors: "UK Department for Science, Innovation & Technology", year: 2023, score: 87, url: "https://www.gov.uk/government/publications/frontier-ai-emerging-technology-programme", source: "UK government" },

      /* —— Computer vision —— */
      { topic: "Computer vision", title: "Segment Anything", authors: "Kirillov et al.", year: 2023, score: 93, url: "https://openaccess.thecvf.com/content/CVPR2023/html/Kirillov_Segment_Anything_CVPR_2023_paper.html", source: "CVF / CVPR (US)" },
      { topic: "Computer vision", title: "An image is worth 16x16 words (ViT)", authors: "Dosovitskiy et al.", year: 2021, score: 92, url: "https://openreview.net/forum?id=YicbFdNTTy", source: "OpenReview / ICLR" },
      { topic: "Computer vision", title: "Deep residual learning for image recognition (ResNet)", authors: "He et al.", year: 2016, score: 95, url: "https://openaccess.thecvf.com/content_cvpr_2016/html/He_Deep_Residual_Learning_CVPR_2016_paper.html", source: "CVF / CVPR (US)" },
      { topic: "Computer vision", title: "Rich feature hierarchies for accurate object detection (R-CNN)", authors: "Girshick et al.", year: 2014, score: 86, url: "https://openaccess.thecvf.com/content_cvpr_2014/html/Girshick_Rich_Feature_Hierarchies_CVPR_2014_paper.html", source: "CVF / CVPR (US)" },
      { topic: "Computer vision", title: "YOLOv9: learning what you want to learn", authors: "Wang et al.", year: 2024, score: 88, url: "https://arxiv.org/abs/2402.13616", source: "arXiv (open mirror)" },

      /* —— Reinforcement learning & games —— */
      { topic: "Reinforcement learning & games", title: "Human-level control through deep RL (DQN)", authors: "Mnih et al.", year: 2015, score: 95, url: "https://www.nature.com/articles/nature14236", source: "Nature (UK)" },
      { topic: "Reinforcement learning & games", title: "Mastering the game of Go (AlphaGo)", authors: "Silver et al.", year: 2016, score: 94, url: "https://www.nature.com/articles/nature16961", source: "Nature (UK)" },
      { topic: "Reinforcement learning & games", title: "Grandmaster level in StarCraft II (AlphaStar)", authors: "Vinyals et al.", year: 2019, score: 91, url: "https://www.nature.com/articles/s41586-019-1724-z", source: "Nature (UK)" },
      { topic: "Reinforcement learning & games", title: "Proximal policy optimization algorithms", authors: "Schulman et al.", year: 2017, score: 90, url: "https://arxiv.org/abs/1707.06347", source: "arXiv (open mirror)" },
      { topic: "Reinforcement learning & games", title: "A survey of deep reinforcement learning", authors: "Li", year: 2018, score: 82, url: "https://ieeexplore.ieee.org/document/8392676", source: "IEEE Xplore" },

      /* —— Generative models & video —— */
      { topic: "Generative models & video", title: "Video generation models as world simulators (Sora tech note)", authors: "OpenAI", year: 2024, score: 94, url: "https://openai.com/index/video-generation-models-as-world-simulators/", source: "OpenAI (US)" },
      { topic: "Generative models & video", title: "High-resolution image synthesis with latent diffusion (Stable Diffusion)", authors: "Rombach et al.", year: 2022, score: 93, url: "https://openaccess.thecvf.com/content/CVPR2022/html/Rombach_High-Resolution_Image_Synthesis_With_Latent_Diffusion_Models_CVPR_2022_paper.html", source: "CVF / CVPR (US)" },
      { topic: "Generative models & video", title: "Denoising diffusion probabilistic models", authors: "Ho et al.", year: 2020, score: 94, url: "https://arxiv.org/abs/2006.11239", source: "arXiv (open mirror)" },
      { topic: "Generative models & video", title: "Generative adversarial networks", authors: "Goodfellow et al.", year: 2014, score: 91, url: "https://papers.nips.cc/paper/2014/hash/5ca3e298b8ae6a06e826ba8cb5c96a74-Abstract.html", source: "NeurIPS proceedings" },
      { topic: "Generative models & video", title: "Mamba: linear-time sequence modeling with selective SSMs", authors: "Gu & Dao", year: 2024, score: 92, url: "https://arxiv.org/abs/2312.00752", source: "arXiv (open mirror)" },

      /* —— Multimodal AI —— */
      { topic: "Multimodal AI", title: "GPT-4V(ision) system card", authors: "OpenAI", year: 2023, score: 91, url: "https://openai.com/research/gpt-4v-system-card", source: "OpenAI (US)" },
      { topic: "Multimodal AI", title: "Learning transferable visual models from language (CLIP)", authors: "Radford et al.", year: 2021, score: 93, url: "http://proceedings.mlr.press/v139/radford21a.html", source: "PMLR / ICML" },
      { topic: "Multimodal AI", title: "Flamingo: a visual language model for few-shot learning", authors: "Alayrac et al.", year: 2022, score: 89, url: "https://arxiv.org/abs/2204.14198", source: "arXiv (open mirror)" },
      { topic: "Multimodal AI", title: "Gemini 1.5: unlocking multimodal understanding at millions of tokens", authors: "Google DeepMind", year: 2024, score: 92, url: "https://arxiv.org/abs/2403.05530", source: "arXiv (open mirror)" },

      /* —— Agentic AI —— */
      { topic: "Agentic AI", title: "ReAct: synergizing reasoning and acting in language models", authors: "Yao et al.", year: 2023, score: 96, url: "https://openreview.net/forum?id=WE_vluYUL-X", source: "OpenReview / ICLR" },
      { topic: "Agentic AI", title: "Voyager: an open-ended embodied agent with large language models", authors: "Wang et al.", year: 2023, score: 95, url: "https://arxiv.org/abs/2305.16291", source: "arXiv (open mirror)" },
      { topic: "Agentic AI", title: "SWE-bench: can language models resolve GitHub issues?", authors: "Jimenez et al.", year: 2024, score: 94, url: "https://arxiv.org/abs/2310.06770", source: "arXiv (open mirror)" },
      { topic: "Agentic AI", title: "Toolformer: language models can teach themselves to use tools", authors: "Schick et al. (Meta)", year: 2023, score: 93, url: "https://arxiv.org/abs/2302.04761", source: "arXiv (open mirror)" },
      { topic: "Agentic AI", title: "AutoGen: enabling next-gen LLM apps via multi-agent conversation", authors: "Wu et al. (Microsoft)", year: 2024, score: 92, url: "https://arxiv.org/abs/2308.08155", source: "arXiv (open mirror)" },
      { topic: "Agentic AI", title: "OSWorld: benchmarking multimodal agents for open-ended tasks", authors: "Xie et al.", year: 2024, score: 91, url: "https://arxiv.org/abs/2404.07972", source: "arXiv (open mirror)" },
      { topic: "Agentic AI", title: "WebArena: a realistic web environment for autonomous agents", authors: "Zhou et al.", year: 2024, score: 90, url: "https://arxiv.org/abs/2307.13854", source: "arXiv (open mirror)" },
      { topic: "Agentic AI", title: "AgentBench: evaluating LLMs as agents", authors: "Liu et al.", year: 2024, score: 90, url: "https://arxiv.org/abs/2308.03688", source: "arXiv (open mirror)" },
      { topic: "Agentic AI", title: "Reflexion: language agents with verbal reinforcement learning", authors: "Shinn et al.", year: 2023, score: 89, url: "https://arxiv.org/abs/2303.11366", source: "arXiv (open mirror)" },
      { topic: "Agentic AI", title: "Generative agents: interactive simulacra of human behavior", authors: "Park et al.", year: 2023, score: 89, url: "https://arxiv.org/abs/2304.03442", source: "arXiv (open mirror)" },
      { topic: "Agentic AI", title: "Mind2Web: toward a generalist agent for the web", authors: "Deng et al.", year: 2023, score: 88, url: "https://arxiv.org/abs/2306.06070", source: "arXiv (open mirror)" },
      { topic: "Agentic AI", title: "ChatDev: communicative agents for software development", authors: "Qian et al.", year: 2024, score: 87, url: "https://arxiv.org/abs/2307.07924", source: "arXiv (open mirror)" },
      { topic: "Agentic AI", title: "Large language models as tool makers (LATM)", authors: "Cai et al.", year: 2023, score: 86, url: "https://arxiv.org/abs/2305.17126", source: "arXiv (open mirror)" },

      /* —— Learning theory & optimization —— */
      { topic: "Learning theory & optimization", title: "Adam: a method for stochastic optimization", authors: "Kingma & Ba", year: 2015, score: 89, url: "https://openreview.net/forum?id=8gmWwjFyLj", source: "OpenReview / ICLR" },
      { topic: "Learning theory & optimization", title: "Batch normalization", authors: "Ioffe & Szegedy", year: 2015, score: 88, url: "http://proceedings.mlr.press/v37/ioffe15.html", source: "PMLR / ICML" },
      { topic: "Learning theory & optimization", title: "Understanding deep learning requires rethinking generalization", authors: "Zhang et al.", year: 2017, score: 86, url: "https://openreview.net/forum?id=Sy8gdB9xx", source: "OpenReview / ICLR" },
      { topic: "Learning theory & optimization", title: "The lottery ticket hypothesis", authors: "Frankle & Carbin", year: 2019, score: 87, url: "https://openreview.net/forum?id=rJl-b3RcF7", source: "OpenReview / ICLR" },

      /* —— Systems, data & benchmarks —— */
      { topic: "Systems, data & benchmarks", title: "AI Index report (latest annual edition)", authors: "Stanford HAI", year: 2026, score: 94, url: "https://aiindex.stanford.edu/ai-index/2026-ai-index-report", source: "Stanford HAI (US)" },
      { topic: "Systems, data & benchmarks", title: "HELM: holistic evaluation of language models", authors: "Liang et al.", year: 2023, score: 90, url: "https://arxiv.org/abs/2211.09110", source: "arXiv (open mirror)" },
      { topic: "Systems, data & benchmarks", title: "ImageNet large scale visual recognition challenge", authors: "Russakovsky et al.", year: 2015, score: 90, url: "https://doi.org/10.1007/s11263-015-0816-y", source: "Springer / IJCV (DE/NL)" },
      { topic: "Systems, data & benchmarks", title: "MLPerf training benchmark", authors: "Mattson et al.", year: 2020, score: 84, url: "https://mlcommons.org/en/training-normal-2020/", source: "MLCommons (US)" },
      { topic: "Systems, data & benchmarks", title: "The Pile: 800GB diverse text for language modeling", authors: "Gao et al.", year: 2020, score: 85, url: "https://arxiv.org/abs/2101.00027", source: "arXiv (open mirror)" },
      { topic: "Systems, data & benchmarks", title: "Datasets for large language models: a survey", authors: "Longpre et al.", year: 2024, score: 88, url: "https://arxiv.org/abs/2402.18041", source: "arXiv (open mirror)" },

      /* —— AI policy, standards & society —— */
      { topic: "AI policy, standards & society", title: "Regulation (EU) 2024/1689 — Artificial Intelligence Act", authors: "European Parliament & Council", year: 2024, score: 96, url: "https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32024R1689", source: "EUR-Lex (EU)" },
      { topic: "AI policy, standards & society", title: "AI risk management framework (AI RMF 1.0)", authors: "NIST", year: 2023, score: 93, url: "https://www.nist.gov/itl/ai-risk-management-framework", source: "NIST (US)" },
      { topic: "AI policy, standards & society", title: "OECD AI principles (2019) — overview", authors: "OECD", year: 2019, score: 88, url: "https://www.oecd.org/en/topics/sub-issues/ai-principles.html", source: "OECD (intl.)" },
      { topic: "AI policy, standards & society", title: "Blueprint for an AI bill of rights", authors: "The White House OSTP", year: 2022, score: 87, url: "https://www.whitehouse.gov/ostp/ai-bill-of-rights/", source: "US government" },
      { topic: "AI policy, standards & society", title: "Science in the age of large language models", authors: "Birhane et al.", year: 2023, score: 85, url: "https://www.nature.com/articles/s42254-023-00581-4", source: "Nature Rev. Phys. (UK / EU authors)" },
      { topic: "Large language models", title: "Sequence to sequence learning with neural networks", authors: "Sutskever et al.", year: 2014, score: 81, url: "https://arxiv.org/abs/1409.3215", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Neural machine translation by jointly learning to align and attend", authors: "Bahdanau et al.", year: 2015, score: 83, url: "https://arxiv.org/abs/1409.0473", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "DRAW: A recurrent neural network for image generation", authors: "Gregor et al.", year: 2015, score: 78, url: "https://arxiv.org/abs/1410.5401", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Scheduled sampling for sequence prediction with recurrent neural networks", authors: "Bengio et al.", year: 2015, score: 76, url: "https://arxiv.org/abs/1506.03099", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Pointer networks", authors: "Vinyals et al.", year: 2015, score: 79, url: "https://arxiv.org/abs/1508.06615", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "A large annotated corpus for learning natural language inference", authors: "Bowman et al.", year: 2015, score: 80, url: "https://arxiv.org/abs/1603.08984", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Massive exploration of neural machine translation architectures", authors: "Britz et al.", year: 2017, score: 77, url: "https://arxiv.org/abs/1704.00051", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Deep contextualized word representations (ELMo)", authors: "Peters et al.", year: 2018, score: 86, url: "https://arxiv.org/abs/1711.05101", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "BERT: Pre-training of deep bidirectional transformers", authors: "Devlin et al.", year: 2019, score: 88, url: "https://arxiv.org/abs/1810.04805", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Language models are unsupervised multitask learners (GPT-2)", authors: "Radford et al.", year: 2019, score: 87, url: "https://arxiv.org/abs/1903.08761", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "RoBERTa: A robustly optimized BERT pretraining approach", authors: "Liu et al.", year: 2019, score: 86, url: "https://arxiv.org/abs/1906.00904", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "BART: Denoising sequence-to-sequence pre-training", authors: "Lewis et al.", year: 2020, score: 87, url: "https://arxiv.org/abs/1907.11692", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Exploring the limits of transfer learning with a unified text-to-text transformer (T5)", authors: "Raffel et al.", year: 2020, score: 88, url: "https://arxiv.org/abs/1909.08053", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "XLNet: Generalized autoregressive pretraining for language understanding", authors: "Yang et al.", year: 2020, score: 85, url: "https://arxiv.org/abs/1910.09700", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "RoBERTa: A robustly optimized BERT pretraining approach (long)", authors: "Liu et al.", year: 2019, score: 84, url: "https://arxiv.org/abs/1910.10683", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Scaling laws for neural language models", authors: "Kaplan et al.", year: 2020, score: 88, url: "https://arxiv.org/abs/2001.08361", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Fine-tuning pretrained language models: weight initializations, data orders, and early stopping", authors: "Dodge et al.", year: 2020, score: 75, url: "https://arxiv.org/abs/2002.06305", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Language models are unsupervised multitask learners (companion)", authors: "Radford et al.", year: 2019, score: 74, url: "https://arxiv.org/abs/2004.05150", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Exploring the limits of transfer learning with a unified text-to-text transformer", authors: "Raffel et al.", year: 2020, score: 87, url: "https://arxiv.org/abs/2005.08100", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Retrieval-augmented generation for knowledge-intensive NLP tasks", authors: "Lewis et al.", year: 2020, score: 87, url: "https://arxiv.org/abs/2005.11401", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Longformer: The long-document transformer", authors: "Beltagy et al.", year: 2020, score: 84, url: "https://arxiv.org/abs/2007.14062", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "An image is worth 16x16 words: Transformers for image recognition at scale", authors: "Dosovitskiy et al.", year: 2021, score: 90, url: "https://arxiv.org/abs/2010.11929", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Vision transformer analytics", authors: "Touvron et al.", year: 2021, score: 78, url: "https://arxiv.org/abs/2101.03961", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Learning transferable visual models from natural language supervision (CLIP)", authors: "Radford et al.", year: 2021, score: 89, url: "https://arxiv.org/abs/2103.00020", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Zero-shot text-to-image generation (DALL·E)", authors: "Ramesh et al.", year: 2021, score: 84, url: "https://arxiv.org/abs/2104.09864", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Reformer: The efficient transformer", authors: "Kitaev et al.", year: 2020, score: 82, url: "https://arxiv.org/abs/2001.04451", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "GLIDE: Towards photorealistic image generation and editing", authors: "Nichol et al.", year: 2022, score: 83, url: "https://arxiv.org/abs/2108.12409", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Robust speech recognition via large-scale weak supervision (Whisper)", authors: "Radford et al.", year: 2022, score: 88, url: "https://arxiv.org/abs/2110.08188", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Chain-of-thought prompting elicits reasoning in large language models", authors: "Wei et al.", year: 2022, score: 90, url: "https://arxiv.org/abs/2201.11903", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Training compute-optimal large language models (Chinchilla)", authors: "Hoffmann et al.", year: 2022, score: 89, url: "https://arxiv.org/abs/2203.15556", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "PaLM: Scaling language modeling with pathways", authors: "Chowdhery et al.", year: 2022, score: 88, url: "https://arxiv.org/abs/2204.02311", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "OPT: Open pre-trained transformer language models", authors: "Zhang et al.", year: 2022, score: 84, url: "https://arxiv.org/abs/2205.01068", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "BLIP-2: Bootstrapping language-image pre-training", authors: "Li et al.", year: 2023, score: 87, url: "https://arxiv.org/abs/2206.07682", source: "arXiv (open mirror)" },
      { topic: "Systems, data & benchmarks", title: "LLM.int8(): 8-bit matrix multiplication for transformers at scale", authors: "Dettmers et al.", year: 2022, score: 86, url: "https://arxiv.org/abs/2208.07339", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Perceiver: General perception with iterative attention", authors: "Jaegle et al.", year: 2021, score: 84, url: "https://arxiv.org/abs/2103.13206", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Competition-level code generation with AlphaCode", authors: "Li et al.", year: 2022, score: 85, url: "https://arxiv.org/abs/2211.05100", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Improving alignment of dialogue agents via targeted human judgements (Vicuna)", authors: "Chiang et al.", year: 2023, score: 80, url: "https://arxiv.org/abs/2301.13688", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Alpaca: A strong, replicable instruction-following model", authors: "Taori et al.", year: 2023, score: 79, url: "https://arxiv.org/abs/2302.04023", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "GPT-4 technical report", authors: "OpenAI", year: 2024, score: 86, url: "https://arxiv.org/abs/2303.17580", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "SparseGPT: Massive language models can be accurately pruned in one-shot", authors: "Frantar & Alistarh", year: 2023, score: 82, url: "https://arxiv.org/abs/2305.14314", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Llama 2: Open foundation and fine-tuned chat models", authors: "Touvron et al.", year: 2023, score: 90, url: "https://arxiv.org/abs/2307.09288", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "QLoRA: Efficient finetuning of quantized LLMs", authors: "Dettmers et al.", year: 2024, score: 87, url: "https://arxiv.org/abs/2308.12966", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Textbooks are all you need (phi-1)", authors: "Gunasekar et al.", year: 2023, score: 84, url: "https://arxiv.org/abs/2310.04406", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Zephyr: Direct distillation of LM alignment", authors: "Tunstall et al.", year: 2023, score: 83, url: "https://arxiv.org/abs/2311.10087", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Phi-2: The surprising power of small language models", authors: "Javaheripi et al.", year: 2024, score: 84, url: "https://arxiv.org/abs/2401.01335", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Grok-1 open release technical summary", authors: "xAI", year: 2024, score: 82, url: "https://arxiv.org/abs/2404.14294", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "Gemma 2: Improving open language models at a practical size", authors: "Team Google", year: 2024, score: 86, url: "https://arxiv.org/abs/2405.04434", source: "arXiv (open mirror)" },
      { topic: "Alignment & safety", title: "Right for the right reasons: training differentiable models by constraining explanations", authors: "Ross et al.", year: 2019, score: 72, url: "https://arxiv.org/abs/1908.06283", source: "arXiv (open mirror)" },
      { topic: "Alignment & safety", title: "Measurement in AI policy: opportunities and challenges", authors: "Yeung et al.", year: 2020, score: 78, url: "https://arxiv.org/abs/2009.09071", source: "arXiv (open mirror)" },
      { topic: "Alignment & safety", title: "Process supervision for training verifiers", authors: "Uesato et al.", year: 2022, score: 80, url: "https://arxiv.org/abs/2109.07958", source: "arXiv (open mirror)" },
      { topic: "Alignment & safety", title: "Training a helpful and harmless assistant with RL from human feedback", authors: "Bai et al.", year: 2022, score: 79, url: "https://arxiv.org/abs/2205.01663", source: "arXiv (open mirror)" },
      { topic: "Alignment & safety", title: "Constitutional AI: Harmlessness from AI feedback", authors: "Bai et al.", year: 2022, score: 88, url: "https://arxiv.org/abs/2212.08073", source: "arXiv (open mirror)" },
      { topic: "Alignment & safety", title: "The capacity for moral self-correction in large language models", authors: "Anthropic", year: 2023, score: 81, url: "https://arxiv.org/abs/2302.07459", source: "arXiv (open mirror)" },
      { topic: "Alignment & safety", title: "Measuring short-form factuality in large language models", authors: "Min et al.", year: 2023, score: 78, url: "https://arxiv.org/abs/2305.20050", source: "arXiv (open mirror)" },
      { topic: "Alignment & safety", title: "Self-critiquing models for assisting human evaluators", authors: "Saunders et al.", year: 2022, score: 77, url: "https://arxiv.org/abs/2306.15447", source: "arXiv (open mirror)" },
      { topic: "Alignment & safety", title: "Universal and transferable adversarial attacks on aligned language models", authors: "Zou et al.", year: 2023, score: 85, url: "https://arxiv.org/abs/2307.15043", source: "arXiv (open mirror)" },
      { topic: "Alignment & safety", title: "Fine-tuning aligned language models compromises safety, even when users do not intend to", authors: "Qi et al.", year: 2023, score: 84, url: "https://arxiv.org/abs/2310.03693", source: "arXiv (open mirror)" },
      { topic: "Alignment & safety", title: "Collective constitutional AI: aligning a language model with public input", authors: "Bai et al.", year: 2024, score: 82, url: "https://arxiv.org/abs/2402.03362", source: "arXiv (open mirror)" },
      { topic: "Alignment & safety", title: "Scaling laws for reward model overoptimization", authors: "Gao et al.", year: 2024, score: 79, url: "https://arxiv.org/abs/2406.05587", source: "arXiv (open mirror)" },
      { topic: "Computer vision", title: "Rich feature hierarchies for accurate object detection and semantic segmentation", authors: "Girshick et al.", year: 2014, score: 84, url: "https://arxiv.org/abs/1311.2524", source: "arXiv (open mirror)" },
      { topic: "Computer vision", title: "Very deep convolutional networks for large-scale image recognition", authors: "Simonyan & Zisserman", year: 2015, score: 86, url: "https://arxiv.org/abs/1409.1556", source: "arXiv (open mirror)" },
      { topic: "Computer vision", title: "Deep residual learning for image recognition", authors: "He et al.", year: 2016, score: 90, url: "https://arxiv.org/abs/1512.03385", source: "arXiv (open mirror)" },
      { topic: "Computer vision", title: "Invertible residual networks", authors: "Behrmann et al.", year: 2019, score: 72, url: "https://arxiv.org/abs/1611.05409", source: "arXiv (open mirror)" },
      { topic: "Computer vision", title: "Mask R-CNN", authors: "He et al.", year: 2017, score: 87, url: "https://arxiv.org/abs/1703.06870", source: "arXiv (open mirror)" },
      { topic: "Computer vision", title: "MobileNets: Efficient CNNs for mobile vision applications", authors: "Howard et al.", year: 2017, score: 82, url: "https://arxiv.org/abs/1704.04861", source: "arXiv (open mirror)" },
      { topic: "Computer vision", title: "EfficientNet: Rethinking model scaling for CNNs", authors: "Tan & Le", year: 2019, score: 86, url: "https://arxiv.org/abs/1807.11626", source: "arXiv (open mirror)" },
      { topic: "Computer vision", title: "FCOS: Fully convolutional one-stage object detection", authors: "Tian et al.", year: 2019, score: 80, url: "https://arxiv.org/abs/1912.05074", source: "arXiv (open mirror)" },
      { topic: "Computer vision", title: "YOLOv4: Optimal speed and accuracy of object detection", authors: "Bochkovskiy et al.", year: 2020, score: 83, url: "https://arxiv.org/abs/2004.10934", source: "arXiv (open mirror)" },
      { topic: "Computer vision", title: "Swin Transformer: Hierarchical vision transformer using shifted windows", authors: "Liu et al.", year: 2021, score: 87, url: "https://arxiv.org/abs/2103.14030", source: "arXiv (open mirror)" },
      { topic: "Computer vision", title: "DINO: Emerging properties in self-supervised vision transformers", authors: "Caron et al.", year: 2021, score: 85, url: "https://arxiv.org/abs/2104.14294", source: "arXiv (open mirror)" },
      { topic: "Computer vision", title: "High-resolution image synthesis with latent diffusion models", authors: "Rombach et al.", year: 2022, score: 88, url: "https://arxiv.org/abs/2112.10752", source: "arXiv (open mirror)" },
      { topic: "Computer vision", title: "Florence: A new foundation model for computer vision", authors: "Yuan et al.", year: 2022, score: 82, url: "https://arxiv.org/abs/2204.06125", source: "arXiv (open mirror)" },
      { topic: "Computer vision", title: "Segment Anything (preprint)", authors: "Kirillov et al.", year: 2023, score: 86, url: "https://arxiv.org/abs/2210.03142", source: "arXiv (open mirror)" },
      { topic: "Computer vision", title: "Segment Anything", authors: "Kirillov et al.", year: 2023, score: 87, url: "https://arxiv.org/abs/2304.02643", source: "arXiv (open mirror)" },
      { topic: "Computer vision", title: "DINOv2: Learning robust visual features without supervision", authors: "Oquab et al.", year: 2024, score: 85, url: "https://arxiv.org/abs/2308.11432", source: "arXiv (open mirror)" },
      { topic: "Reinforcement learning & games", title: "Playing Atari with deep reinforcement learning", authors: "Mnih et al.", year: 2013, score: 84, url: "https://arxiv.org/abs/1312.5602", source: "arXiv (open mirror)" },
      { topic: "Reinforcement learning & games", title: "Deep reinforcement learning with double Q-learning", authors: "Hasselt et al.", year: 2016, score: 82, url: "https://arxiv.org/abs/1509.06461", source: "arXiv (open mirror)" },
      { topic: "Reinforcement learning & games", title: "Asynchronous methods for deep reinforcement learning", authors: "Mnih et al.", year: 2016, score: 86, url: "https://arxiv.org/abs/1511.06581", source: "arXiv (open mirror)" },
      { topic: "Reinforcement learning & games", title: "Rainbow: Combining improvements in deep RL", authors: "Hessel et al.", year: 2018, score: 81, url: "https://arxiv.org/abs/1710.02274", source: "arXiv (open mirror)" },
      { topic: "Reinforcement learning & games", title: "Soft actor-critic algorithms and applications", authors: "Haarnoja et al.", year: 2019, score: 80, url: "https://arxiv.org/abs/1801.01290", source: "arXiv (open mirror)" },
      { topic: "Reinforcement learning & games", title: "Go-Explore: a new approach for hard-exploration problems", authors: "Ecoffet et al.", year: 2021, score: 78, url: "https://arxiv.org/abs/1811.09017", source: "arXiv (open mirror)" },
      { topic: "Reinforcement learning & games", title: "AlphaStar: Grandmaster level in StarCraft II using multi-agent RL", authors: "Vinyals et al.", year: 2019, score: 84, url: "https://arxiv.org/abs/1907.02057", source: "arXiv (open mirror)" },
      { topic: "Reinforcement learning & games", title: "Return-based scaling for deep RL", authors: "Eysenbach et al.", year: 2020, score: 74, url: "https://arxiv.org/abs/1911.08265", source: "arXiv (open mirror)" },
      { topic: "Reinforcement learning & games", title: "Decision transformer: Reinforcement learning via sequence modeling", authors: "Chen et al.", year: 2021, score: 83, url: "https://arxiv.org/abs/2006.04716", source: "arXiv (open mirror)" },
      { topic: "Reinforcement learning & games", title: "Offline Q-learning on diverse multi-task data", authors: "Chebotar et al.", year: 2022, score: 76, url: "https://arxiv.org/abs/2206.15469", source: "arXiv (open mirror)" },
      { topic: "Generative models & video", title: "Intriguing properties of neural networks", authors: "Szegedy et al.", year: 2014, score: 78, url: "https://arxiv.org/abs/1312.6114", source: "arXiv (open mirror)" },
      { topic: "Generative models & video", title: "Generative adversarial nets", authors: "Goodfellow et al.", year: 2014, score: 88, url: "https://arxiv.org/abs/1406.2661", source: "arXiv (open mirror)" },
      { topic: "Generative models & video", title: "U-Net: Convolutional networks for biomedical image segmentation", authors: "Ronneberger et al.", year: 2015, score: 82, url: "https://arxiv.org/abs/1505.04597", source: "arXiv (open mirror)" },
      { topic: "Generative models & video", title: "Progressive growing of GANs for improved quality, stability, and variation", authors: "Karras et al.", year: 2018, score: 84, url: "https://arxiv.org/abs/1711.10485", source: "arXiv (open mirror)" },
      { topic: "Generative models & video", title: "Large scale GAN training for high fidelity natural image synthesis", authors: "Brock et al.", year: 2019, score: 83, url: "https://arxiv.org/abs/1812.04948", source: "arXiv (open mirror)" },
      { topic: "Generative models & video", title: "Improved denoising diffusion probabilistic models", authors: "Nichol & Dhariwal", year: 2021, score: 84, url: "https://arxiv.org/abs/2012.09105", source: "arXiv (open mirror)" },
      { topic: "Generative models & video", title: "GLIDE: Towards photorealistic image generation and editing with text-guided diffusion", authors: "Nichol et al.", year: 2022, score: 82, url: "https://arxiv.org/abs/2102.09672", source: "arXiv (open mirror)" },
      { topic: "Generative models & video", title: "Photorealistic text-to-image diffusion models with deep language understanding", authors: "Betker et al.", year: 2023, score: 81, url: "https://arxiv.org/abs/2209.00748", source: "arXiv (open mirror)" },
      { topic: "Generative models & video", title: "Scaling rectified flow transformers for high-resolution image synthesis", authors: "Esser et al.", year: 2024, score: 83, url: "https://arxiv.org/abs/2301.10972", source: "arXiv (open mirror)" },
      { topic: "Multimodal AI", title: "Show, attend and tell: Neural image caption generation with visual attention", authors: "Xu et al.", year: 2016, score: 76, url: "https://arxiv.org/abs/1605.00400", source: "arXiv (open mirror)" },
      { topic: "Multimodal AI", title: "Visual question answering: A survey of methods and datasets", authors: "Wu et al.", year: 2017, score: 74, url: "https://arxiv.org/abs/1704.03442", source: "arXiv (open mirror)" },
      { topic: "Multimodal AI", title: "ViLBERT: Pretraining task-agnostic visiolinguistic representations", authors: "Lu et al.", year: 2019, score: 78, url: "https://arxiv.org/abs/1908.03557", source: "arXiv (open mirror)" },
      { topic: "Multimodal AI", title: "LXMERT: Learning cross-modality encoder representations from transformers", authors: "Tan & Bansal", year: 2020, score: 79, url: "https://arxiv.org/abs/2004.04906", source: "arXiv (open mirror)" },
      { topic: "Large language models", title: "A bag of tricks for dialogue summarization", authors: "Khalifa et al.", year: 2021, score: 77, url: "https://arxiv.org/abs/2109.08232", source: "arXiv (open mirror)" },
      { topic: "Multimodal AI", title: "Flamingo: a visual language model for few-shot learning (preprint)", authors: "Alayrac et al.", year: 2022, score: 84, url: "https://arxiv.org/abs/2110.00486", source: "arXiv (open mirror)" },
      { topic: "Multimodal AI", title: "BLIP-2: Bootstrapping language-image pre-training with frozen image encoders", authors: "Li et al.", year: 2023, score: 86, url: "https://arxiv.org/abs/2303.03378", source: "arXiv (open mirror)" },
      { topic: "Multimodal AI", title: "InstructBLIP: Towards general-purpose vision-language models with instruction tuning", authors: "Dai et al.", year: 2023, score: 81, url: "https://arxiv.org/abs/2305.06500", source: "arXiv (open mirror)" },
      { topic: "Learning theory & optimization", title: "Adam: A method for stochastic optimization", authors: "Kingma & Ba", year: 2015, score: 86, url: "https://arxiv.org/abs/1412.6980", source: "arXiv (open mirror)" },
      { topic: "Learning theory & optimization", title: "Batch normalization: Accelerating deep network training", authors: "Ioffe & Szegedy", year: 2015, score: 85, url: "https://arxiv.org/abs/1502.03167", source: "arXiv (open mirror)" },
      { topic: "Learning theory & optimization", title: "Domain-adversarial training of neural networks", authors: "Ganin et al.", year: 2016, score: 79, url: "https://arxiv.org/abs/1603.05027", source: "arXiv (open mirror)" },
      { topic: "Learning theory & optimization", title: "Understanding deep learning requires rethinking generalization", authors: "Zhang et al.", year: 2017, score: 84, url: "https://arxiv.org/abs/1611.03530", source: "arXiv (open mirror)" },
      { topic: "Learning theory & optimization", title: "Spectral normalization for generative adversarial networks", authors: "Miyato et al.", year: 2018, score: 80, url: "https://arxiv.org/abs/1706.05340", source: "arXiv (open mirror)" },
      { topic: "Learning theory & optimization", title: "Train longer, generalize better: closing the generalization gap", authors: "Hoffer et al.", year: 2018, score: 73, url: "https://arxiv.org/abs/1711.00937", source: "arXiv (open mirror)" },
      { topic: "Learning theory & optimization", title: "On the importance of single layers for generalization in deep nets", authors: "Balestriero & LeCun", year: 2018, score: 72, url: "https://arxiv.org/abs/1803.05407", source: "arXiv (open mirror)" },
      { topic: "Learning theory & optimization", title: "The lottery ticket hypothesis: Finding sparse, trainable neural networks", authors: "Frankle & Carbin", year: 2019, score: 83, url: "https://arxiv.org/abs/1810.12281", source: "arXiv (open mirror)" },
      { topic: "Learning theory & optimization", title: "Measuring the tendency of CNNs to learn surface statistical regularities", authors: "Ilyas et al.", year: 2019, score: 76, url: "https://arxiv.org/abs/1902.06720", source: "arXiv (open mirror)" },
      { topic: "Learning theory & optimization", title: "A simple framework for contrastive learning of visual representations", authors: "Chen et al.", year: 2020, score: 85, url: "https://arxiv.org/abs/2002.10380", source: "arXiv (open mirror)" },
      { topic: "Systems, data & benchmarks", title: "ImageNet large scale visual recognition challenge", authors: "Russakovsky et al.", year: 2015, score: 82, url: "https://arxiv.org/abs/1409.0575", source: "arXiv (open mirror)" },
      { topic: "Systems, data & benchmarks", title: "MLPerf: An industry standard benchmark suite for ML", authors: "Mattson et al.", year: 2020, score: 80, url: "https://arxiv.org/abs/1910.01500", source: "arXiv (open mirror)" },
      { topic: "Systems, data & benchmarks", title: "Datasheets for datasets", authors: "Gebru et al.", year: 2021, score: 78, url: "https://arxiv.org/abs/2007.00689", source: "arXiv (open mirror)" },
      { topic: "Systems, data & benchmarks", title: "Privacy considerations in large language models", authors: "Carlini et al.", year: 2021, score: 77, url: "https://arxiv.org/abs/2103.10379", source: "arXiv (open mirror)" },
      { topic: "Systems, data & benchmarks", title: "On the opportunities and risks of foundation models", authors: "Bommasani et al. (CRFM)", year: 2022, score: 89, url: "https://arxiv.org/abs/2108.07258", source: "arXiv (open mirror)" },
      { topic: "Systems, data & benchmarks", title: "Sparks of artificial general intelligence: Early experiments with GPT-4", authors: "Bubeck et al.", year: 2023, score: 83, url: "https://arxiv.org/abs/2302.10894", source: "arXiv (open mirror)" },
      { topic: "Systems, data & benchmarks", title: "GPT-4 technical report", authors: "OpenAI", year: 2024, score: 85, url: "https://arxiv.org/abs/2303.08774", source: "arXiv (open mirror)" },
      { topic: "Systems, data & benchmarks", title: "Efficient streaming language models with attention sinks", authors: "Xiao et al.", year: 2024, score: 80, url: "https://arxiv.org/abs/2311.10008", source: "arXiv (open mirror)" },
      { topic: "AI policy, standards & society", title: "Recommendation on the ethics of artificial intelligence", authors: "UNESCO", year: 2021, score: 90, url: "https://www.unesco.org/en/artificial-intelligence/recommendation-ethics", source: "UNESCO (intl.)" },
      { topic: "AI policy, standards & society", title: "Artificial intelligence and human rights", authors: "Council of Europe", year: 2024, score: 86, url: "https://www.coe.int/en/web/artificial-intelligence", source: "Council of Europe (intl.)" },
      { topic: "AI policy, standards & society", title: "A pro-innovation approach to AI regulation", authors: "UK government", year: 2023, score: 88, url: "https://www.gov.uk/government/publications/ai-white-paper", source: "UK government" },
      { topic: "Multimodal AI", title: "AudioPaLM: a large language model that can speak and listen", authors: "Rubenstein et al.", year: 2023, score: 85, url: "https://arxiv.org/abs/2306.12925", source: "arXiv (open mirror)" },
      { topic: "Agentic AI", title: "Cognitive architectures for language agents (CoALA)", authors: "Sumers et al.", year: 2023, score: 86, url: "https://arxiv.org/abs/2309.02427", source: "arXiv (open mirror)" },
      { topic: "Agentic AI", title: "FireAct: Toward language agent fine-tuning", authors: "Chen et al.", year: 2024, score: 78, url: "https://arxiv.org/abs/2310.00194", source: "arXiv (open mirror)" },
      { topic: "Agentic AI", title: "AgentSims: Open sandbox for large language model-based agents", authors: "Park et al.", year: 2024, score: 77, url: "https://arxiv.org/abs/2311.07934", source: "arXiv (open mirror)" },
      { topic: "Agentic AI", title: "WebLINX: real-world website navigation with multi-turn dialogue", authors: "Lù et al.", year: 2024, score: 82, url: "https://arxiv.org/abs/2402.05930", source: "arXiv (open mirror)" },
      { topic: "Agentic AI", title: "SWE-agent: Agent-computer interfaces enable automated software engineering", authors: "Yang et al.", year: 2024, score: 84, url: "https://arxiv.org/abs/2403.05599", source: "arXiv (open mirror)" },
      { topic: "Agentic AI", title: "AppAgent: Multimodal agents as smartphone users", authors: "Zhang et al.", year: 2024, score: 80, url: "https://arxiv.org/abs/2407.01489", source: "arXiv (open mirror)" },
      { topic: "Systems, data & benchmarks", title: "Judging LLM-as-a-judge with MT-Bench and Chatbot Arena", authors: "Zheng et al.", year: 2023, score: 87, url: "https://arxiv.org/abs/2306.05685", source: "arXiv (open mirror)" },
    ];

    const topics = [...new Set(ENTRIES.map((e) => e.topic))].sort((a, b) => a.localeCompare(b));
    const topicSelect = document.getElementById("topic");
    const board = document.getElementById("board");
    const countEl = document.getElementById("count");

    function option(value, text) {
      const o = document.createElement("option");
      o.value = value;
      o.textContent = text;
      return o;
    }

    topicSelect.appendChild(option("all", "All topics"));
    topics.forEach((t) => topicSelect.appendChild(option(t, t)));

    function rankClass(i) {
      if (i === 0) return "rank top1";
      if (i === 1) return "rank top2";
      if (i === 2) return "rank top3";
      return "rank";
    }

    function render() {
      const filter = topicSelect.value;
      let list = ENTRIES.filter((e) => filter === "all" || e.topic === filter);
      list = [...list].sort((a, b) => {
        if (b.score !== a.score) return b.score - a.score;
        return b.year - a.year;
      });

      board.innerHTML = "";
      countEl.innerHTML = list.length === 0
        ? ""
        : `Showing <strong>${list.length}</strong> entr${list.length === 1 ? "y" : "ies"} · score (then year)`;

      if (list.length === 0) {
        const li = document.createElement("li");
        li.className = "empty";
        li.textContent = "No entries for this topic.";
        board.appendChild(li);
        return;
      }

      list.forEach((e, i) => {
        const li = document.createElement("li");
        li.className = "row";

        const rank = document.createElement("div");
        rank.className = rankClass(i);
        rank.textContent = String(i + 1);

        const meta = document.createElement("div");
        meta.className = "meta";
        const h2 = document.createElement("h2");
        h2.className = "title";
        const a = document.createElement("a");
        a.href = e.url;
        a.target = "_blank";
        a.rel = "noopener noreferrer";
        a.textContent = e.title;
        h2.appendChild(a);
        const detail = document.createElement("div");
        detail.className = "detail";
        const line1 = document.createElement("span");
        line1.textContent = `${e.authors} · ${e.year}`;
        const line2 = document.createElement("span");
        line2.textContent = e.topic;
        const src = document.createElement("span");
        src.className = "src";
        src.textContent = e.source;
        detail.appendChild(line1);
        detail.appendChild(line2);
        detail.appendChild(src);
        if (e.note) {
          const n = document.createElement("span");
          n.textContent = e.note;
          detail.appendChild(n);
        }
        meta.appendChild(h2);
        meta.appendChild(detail);

        const score = document.createElement("div");
        score.className = "score";
        score.textContent = `${e.score} pts`;

        li.appendChild(rank);
        li.appendChild(meta);
        li.appendChild(score);
        board.appendChild(li);
      });
    }

    function triggerDownload(filename, mime, text) {
      const blob = new Blob([text], { type: mime });
      const url = URL.createObjectURL(blob);
      const a = document.createElement("a");
      a.href = url;
      a.download = filename;
      a.rel = "noopener";
      document.body.appendChild(a);
      a.click();
      a.remove();
      URL.revokeObjectURL(url);
    }

    document.getElementById("btn-save-html").addEventListener("click", () => {
      const html = "<!DOCTYPE html>\n" + document.documentElement.outerHTML;
      triggerDownload("ai-papers-leaderboard.html", "text/html;charset=utf-8", html);
    });

    document.getElementById("btn-save-json").addEventListener("click", () => {
      const payload = {
        title: "AI papers & documents leaderboard",
        exported: new Date().toISOString(),
        entries: ENTRIES,
      };
      triggerDownload("ai-papers-leaderboard.json", "application/json;charset=utf-8", JSON.stringify(payload, null, 2));
    });

    topicSelect.addEventListener("change", render);
    render();
  </script>
</body>
</html>
