<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Vivek Kumar — GitHub Profile Preview</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;500;700&family=Syne:wght@400;700;800&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #080b10;
    --bg2: #0d1117;
    --bg3: #161b22;
    --bg4: #1c2333;
    --border: #21262d;
    --border2: #30363d;
    --text: #e6edf3;
    --muted: #7d8590;
    --accent: #00d9ff;
    --accent2: #7c3aed;
    --accent3: #10b981;
    --accent4: #f59e0b;
    --red: #f85149;
    --mono: 'JetBrains Mono', monospace;
    --display: 'Syne', sans-serif;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  html { background: var(--bg); color: var(--text); font-family: var(--mono); scroll-behavior: smooth; }
  body { min-height: 100vh; overflow-x: hidden; }

  /* Scanline overlay */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,217,255,0.012) 2px, rgba(0,217,255,0.012) 4px);
    pointer-events: none; z-index: 9999;
  }

  /* Grid bg */
  .grid-bg {
    position: fixed; inset: 0; z-index: 0;
    background-image:
      linear-gradient(rgba(0,217,255,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,217,255,0.04) 1px, transparent 1px);
    background-size: 40px 40px;
    mask-image: radial-gradient(ellipse 80% 60% at 50% 20%, black 30%, transparent 100%);
  }

  .container { max-width: 860px; margin: 0 auto; padding: 0 24px; position: relative; z-index: 1; }

  /* ── HEADER ── */
  .header { padding: 80px 0 60px; text-align: center; position: relative; }

  .header-orb {
    position: absolute; top: -60px; left: 50%; transform: translateX(-50%);
    width: 500px; height: 500px; border-radius: 50%;
    background: radial-gradient(circle, rgba(0,217,255,0.08) 0%, rgba(124,58,237,0.06) 40%, transparent 70%);
    pointer-events: none;
    animation: pulse 4s ease-in-out infinite;
  }
  @keyframes pulse { 0%,100%{transform:translateX(-50%) scale(1);opacity:.7} 50%{transform:translateX(-50%) scale(1.05);opacity:1} }

  .status-bar {
    display: inline-flex; align-items: center; gap: 8px;
    padding: 6px 14px; border: 1px solid var(--border2);
    border-radius: 100px; background: var(--bg3); font-size: 11px;
    color: var(--accent3); letter-spacing: .08em; text-transform: uppercase;
    margin-bottom: 28px; animation: fadeDown .6s ease both;
  }
  .status-dot { width: 7px; height: 7px; border-radius: 50%; background: var(--accent3); animation: blink 2s ease infinite; }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:.3} }
  @keyframes fadeDown { from{opacity:0;transform:translateY(-12px)} to{opacity:1;transform:translateY(0)} }
  @keyframes fadeUp   { from{opacity:0;transform:translateY(16px)} to{opacity:1;transform:translateY(0)} }
  @keyframes fadeIn   { from{opacity:0} to{opacity:1} }

  .name {
    font-family: var(--display); font-size: clamp(48px,9vw,82px); font-weight: 800;
    line-height: 1; letter-spacing: -2px; margin-bottom: 6px;
    animation: fadeDown .7s .1s ease both;
  }
  .name .accent-word { color: var(--accent); text-shadow: 0 0 40px rgba(0,217,255,.35); }

  .tagline {
    font-size: 13px; color: var(--muted); letter-spacing: .06em;
    text-transform: uppercase; margin-bottom: 24px;
    animation: fadeDown .7s .2s ease both;
  }
  .tagline span { color: var(--accent); }

  .location-chip {
    display: inline-flex; align-items: center; gap: 6px;
    font-size: 12px; color: var(--muted); margin-bottom: 36px;
    animation: fadeDown .7s .3s ease both;
  }
  .location-chip::before { content: '◉'; color: var(--red); font-size: 9px; }

  /* Typing cursor */
  .cursor-line {
    font-size: 14px; color: var(--accent3);
    animation: fadeUp .7s .4s ease both;
    min-height: 22px;
  }
  .cursor-line .cursor { display: inline-block; width: 2px; height: 14px; background: var(--accent3); margin-left: 2px; vertical-align: middle; animation: blink 1s step-end infinite; }

  /* ── TERMINAL BLOCK ── */
  .terminal {
    background: var(--bg2); border: 1px solid var(--border2);
    border-radius: 10px; overflow: hidden; margin: 48px 0;
    animation: fadeUp .7s .5s ease both;
    box-shadow: 0 0 40px rgba(0,217,255,.04), 0 20px 60px rgba(0,0,0,.5);
  }
  .terminal-bar {
    padding: 10px 16px; background: var(--bg3); border-bottom: 1px solid var(--border);
    display: flex; align-items: center; gap: 8px;
  }
  .dot { width: 12px; height: 12px; border-radius: 50%; }
  .dot.r{background:#f85149} .dot.y{background:#d29922} .dot.g{background:#3fb950}
  .terminal-title { font-size: 12px; color: var(--muted); margin-left: auto; margin-right: auto; letter-spacing: .05em; }
  .terminal-body { padding: 20px 24px; font-size: 13px; line-height: 1.9; }
  .t-prompt { color: var(--accent2); }
  .t-cmd { color: var(--text); }
  .t-comment { color: var(--muted); }
  .t-key { color: var(--accent); }
  .t-val { color: var(--accent3); }
  .t-str { color: var(--accent4); }
  .t-bracket { color: var(--muted); }
  .t-class { color: #79c0ff; }
  .t-def { color: var(--accent2); }
  .t-line { display: block; }

  /* ── SECTION ── */
  .section { margin: 64px 0; }
  .section-header {
    display: flex; align-items: center; gap: 12px; margin-bottom: 28px;
  }
  .section-label {
    font-family: var(--mono); font-size: 11px; font-weight: 500;
    color: var(--accent); text-transform: uppercase; letter-spacing: .1em;
  }
  .section-line { flex: 1; height: 1px; background: linear-gradient(90deg, var(--border2), transparent); }
  .section-num { font-size: 11px; color: var(--muted); }

  /* ── PROJECTS ── */
  .projects-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px,1fr)); gap: 16px; }
  .project-card {
    background: var(--bg2); border: 1px solid var(--border);
    border-radius: 8px; padding: 20px 22px; cursor: pointer;
    transition: border-color .2s, transform .2s, box-shadow .2s;
    position: relative; overflow: hidden;
  }
  .project-card::before {
    content: ''; position: absolute; inset: 0;
    background: linear-gradient(135deg, rgba(0,217,255,.04) 0%, transparent 60%);
    opacity: 0; transition: opacity .2s;
  }
  .project-card:hover { border-color: var(--accent); transform: translateY(-3px); box-shadow: 0 8px 30px rgba(0,217,255,.08); }
  .project-card:hover::before { opacity: 1; }
  .card-top { display: flex; align-items: flex-start; justify-content: space-between; margin-bottom: 10px; }
  .card-icon { font-size: 20px; }
  .card-status { font-size: 10px; padding: 2px 8px; border-radius: 100px; letter-spacing: .06em; }
  .status-active { background: rgba(16,185,129,.12); color: var(--accent3); border: 1px solid rgba(16,185,129,.25); }
  .status-deployed { background: rgba(0,217,255,.1); color: var(--accent); border: 1px solid rgba(0,217,255,.2); }
  .status-research { background: rgba(245,158,11,.1); color: var(--accent4); border: 1px solid rgba(245,158,11,.2); }
  .card-name { font-family: var(--display); font-size: 15px; font-weight: 700; margin-bottom: 6px; color: var(--text); }
  .card-desc { font-size: 12px; color: var(--muted); line-height: 1.6; margin-bottom: 14px; }
  .card-tags { display: flex; flex-wrap: wrap; gap: 6px; }
  .tag { font-size: 10px; padding: 3px 8px; border-radius: 4px; background: var(--bg4); color: var(--muted); border: 1px solid var(--border); letter-spacing: .03em; }

  /* ── TECH STACK ── */
  .stack-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px,1fr)); gap: 12px; }
  .stack-cat { background: var(--bg2); border: 1px solid var(--border); border-radius: 8px; padding: 16px 18px; }
  .cat-label { font-size: 10px; color: var(--accent); text-transform: uppercase; letter-spacing: .1em; margin-bottom: 12px; display: flex; align-items: center; gap: 6px; }
  .cat-label::before { content: '//'; color: var(--border2); }
  .tech-list { display: flex; flex-wrap: wrap; gap: 6px; }
  .tech-pill {
    font-size: 11px; padding: 4px 10px; border-radius: 5px;
    border: 1px solid var(--border2); background: var(--bg3);
    color: var(--muted); transition: all .15s;
    cursor: default;
  }
  .tech-pill:hover { border-color: var(--accent); color: var(--accent); background: rgba(0,217,255,.05); }

  /* ── STATS ROW ── */
  .stats-row { display: grid; grid-template-columns: repeat(auto-fit, minmax(140px,1fr)); gap: 12px; }
  .stat-card {
    background: var(--bg2); border: 1px solid var(--border); border-radius: 8px;
    padding: 18px 20px; text-align: center; position: relative; overflow: hidden;
  }
  .stat-card::after {
    content: ''; position: absolute; bottom: 0; left: 0; right: 0; height: 2px;
    background: linear-gradient(90deg, var(--accent2), var(--accent));
    transform: scaleX(0); transform-origin: left; transition: transform .4s;
  }
  .stat-card:hover::after { transform: scaleX(1); }
  .stat-num { font-family: var(--display); font-size: 32px; font-weight: 800; color: var(--text); line-height: 1; }
  .stat-num .unit { font-size: 18px; color: var(--accent); }
  .stat-label { font-size: 10px; color: var(--muted); text-transform: uppercase; letter-spacing: .08em; margin-top: 6px; }

  /* ── MISSION BLOCK ── */
  .mission-block {
    background: var(--bg2); border: 1px solid var(--border2); border-radius: 8px;
    padding: 28px 32px; position: relative; overflow: hidden;
  }
  .mission-block::before {
    content: ''; position: absolute; left: 0; top: 0; bottom: 0; width: 3px;
    background: linear-gradient(180deg, var(--accent), var(--accent2));
    border-radius: 0 2px 2px 0;
  }
  .mission-item { display: flex; align-items: flex-start; gap: 10px; margin-bottom: 12px; font-size: 13px; color: var(--muted); }
  .mission-item:last-child { margin-bottom: 0; }
  .mission-item .plus { color: var(--accent3); font-weight: 700; flex-shrink: 0; }
  .mission-item .text { line-height: 1.6; }
  .mission-item .highlight { color: var(--text); }

  /* ── CONNECT ── */
  .connect-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(160px,1fr)); gap: 10px; }
  .connect-card {
    background: var(--bg2); border: 1px solid var(--border); border-radius: 8px;
    padding: 14px 18px; display: flex; align-items: center; gap: 10px;
    cursor: pointer; transition: all .2s; text-decoration: none; color: var(--muted);
  }
  .connect-card:hover { border-color: var(--border2); background: var(--bg3); color: var(--text); }
  .connect-icon { font-size: 18px; flex-shrink: 0; }
  .connect-info { min-width: 0; }
  .connect-platform { font-size: 11px; color: var(--muted); text-transform: uppercase; letter-spacing: .07em; }
  .connect-handle { font-size: 13px; color: var(--text); font-weight: 500; }

  /* ── FOOTER ── */
  .footer {
    border-top: 1px solid var(--border); padding: 40px 0; text-align: center;
    font-size: 12px; color: var(--muted); margin-top: 80px;
  }
  .footer .quote { font-size: 14px; color: var(--text); margin-bottom: 8px; font-style: italic; }
  .footer .quote span { color: var(--accent); font-style: normal; }

  /* ── CONTRIBUTION GRAPH ── */
  .contrib-graph { background: var(--bg2); border: 1px solid var(--border); border-radius: 8px; padding: 20px 24px; overflow-x: auto; }
  .contrib-weeks { display: flex; gap: 3px; }
  .contrib-col { display: flex; flex-direction: column; gap: 3px; }
  .contrib-cell {
    width: 11px; height: 11px; border-radius: 2px;
    background: var(--bg4); transition: transform .1s;
  }
  .contrib-cell:hover { transform: scale(1.3); }
  .contrib-cell.l1 { background: rgba(0,217,255,.18); }
  .contrib-cell.l2 { background: rgba(0,217,255,.38); }
  .contrib-cell.l3 { background: rgba(0,217,255,.62); }
  .contrib-cell.l4 { background: rgba(0,217,255,.9); }
  .contrib-legend { display: flex; align-items: center; gap: 6px; font-size: 10px; color: var(--muted); margin-top: 10px; justify-content: flex-end; }
  .legend-cell { width: 10px; height: 10px; border-radius: 2px; }

  /* ── SKILL BARS ── */
  .skill-rows { display: flex; flex-direction: column; gap: 14px; }
  .skill-row { display: grid; grid-template-columns: 130px 1fr 36px; align-items: center; gap: 12px; }
  .skill-name { font-size: 12px; color: var(--muted); }
  .skill-track { height: 4px; background: var(--bg4); border-radius: 100px; overflow: hidden; }
  .skill-fill { height: 100%; border-radius: 100px; transition: width 1.5s cubic-bezier(0.16,1,0.3,1); }
  .skill-pct { font-size: 11px; color: var(--muted); text-align: right; }

  /* Glitch text */
  @keyframes glitch {
    0%,100%{clip-path:inset(0 0 100% 0);transform:translate(0)}
    20%{clip-path:inset(10% 0 80% 0);transform:translate(-3px,1px)}
    40%{clip-path:inset(40% 0 50% 0);transform:translate(3px,-1px)}
    60%{clip-path:inset(70% 0 20% 0);transform:translate(-2px,2px)}
    80%{clip-path:inset(85% 0 5% 0);transform:translate(2px,-2px)}
  }
</style>
</head>
<body>
<div class="grid-bg"></div>

<div class="container">

  <!-- HEADER -->
  <header class="header">
    <div class="header-orb"></div>

    <div class="status-bar">
      <span class="status-dot"></span>
      Available for collaboration
    </div>

    <h1 class="name">
      <span class="accent-word">Vivek</span> Kumar
    </h1>

    <p class="tagline">AI Engineer · <span>Delhi, India</span></p>
    <p class="location-chip">Gurugram, Haryana, India</p>

    <div class="cursor-line" id="typing-line">
      <span id="typed-text"></span><span class="cursor"></span>
    </div>
  </header>

  <!-- TERMINAL -->
  <div class="terminal">
    <div class="terminal-bar">
      <div class="dot r"></div><div class="dot y"></div><div class="dot g"></div>
      <span class="terminal-title">~/vivek-kumar/whoami.py</span>
    </div>
    <div class="terminal-body">
      <span class="t-line"><span class="t-def">class</span> <span class="t-class">VivekKumar</span><span class="t-bracket">:</span></span>
      <span class="t-line">&nbsp;</span>
      <span class="t-line">&nbsp;&nbsp;<span class="t-key">role</span> <span class="t-bracket">=</span> <span class="t-str">"AI Engineer"</span></span>
      <span class="t-line">&nbsp;&nbsp;<span class="t-key">specialization</span> <span class="t-bracket">=</span> <span class="t-str">"Artificial Intelligence & Data Science"</span></span>
      <span class="t-line">&nbsp;</span>
      <span class="t-line">&nbsp;&nbsp;<span class="t-key">currently_building</span> <span class="t-bracket">= [</span></span>
      <span class="t-line">&nbsp;&nbsp;&nbsp;&nbsp;<span class="t-str">"Agentic AI Systems"</span><span class="t-bracket">,</span> &nbsp;<span class="t-comment"># 🤖</span></span>
      <span class="t-line">&nbsp;&nbsp;&nbsp;&nbsp;<span class="t-str">"Autonomous Workflows"</span><span class="t-bracket">,</span></span>
      <span class="t-line">&nbsp;&nbsp;&nbsp;&nbsp;<span class="t-str">"LLM Applications"</span><span class="t-bracket">,</span></span>
      <span class="t-line">&nbsp;&nbsp;&nbsp;&nbsp;<span class="t-str">"Multi-Agent Systems"</span></span>
      <span class="t-line">&nbsp;&nbsp;<span class="t-bracket">]</span></span>
      <span class="t-line">&nbsp;</span>
      <span class="t-line">&nbsp;&nbsp;<span class="t-key">mission</span> <span class="t-bracket">=</span></span>
      <span class="t-line">&nbsp;&nbsp;&nbsp;&nbsp;<span class="t-str">"Build AI systems that think, reason and create impact"</span></span>
    </div>
  </div>

  <!-- STATS -->
  <div class="section">
    <div class="section-header">
      <span class="section-label">// metrics</span>
      <div class="section-line"></div>
      <span class="section-num">01</span>
    </div>
    <div class="stats-row">
      <div class="stat-card">
        <div class="stat-num">4<span class="unit">+</span></div>
        <div class="stat-label">Years Coding</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">10<span class="unit">+</span></div>
        <div class="stat-label">AI Projects</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">15<span class="unit">+</span></div>
        <div class="stat-label">Technologies</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">∞</div>
        <div class="stat-label">Curiosity</div>
      </div>
    </div>
  </div>

  <!-- PROJECTS -->
  <div class="section">
    <div class="section-header">
      <span class="section-label">// featured projects</span>
      <div class="section-line"></div>
      <span class="section-num">02</span>
    </div>
    <div class="projects-grid">

      <div class="project-card">
        <div class="card-top">
          <span class="card-icon">🤖</span>
          <span class="card-status status-active">ACTIVE</span>
        </div>
        <div class="card-name">Agentic AI Assistant</div>
        <div class="card-desc">Autonomous system for data cleaning, analysis, visualization & NL interaction.</div>
        <div class="card-tags">
          <span class="tag">Python</span><span class="tag">LangChain</span><span class="tag">OpenAI</span>
        </div>
      </div>

      <div class="project-card">
        <div class="card-top">
          <span class="card-icon">🎬</span>
          <span class="card-status status-deployed">DEPLOYED</span>
        </div>
        <div class="card-name">Movie Recommender</div>
        <div class="card-desc">AI-powered recommendation engine using collaborative and content-based filtering.</div>
        <div class="card-tags">
          <span class="tag">Scikit-Learn</span><span class="tag">Pandas</span><span class="tag">ML</span>
        </div>
      </div>

      <div class="project-card">
        <div class="card-top">
          <span class="card-icon">😊</span>
          <span class="card-status status-active">ACTIVE</span>
        </div>
        <div class="card-name">Emotion Detection</div>
        <div class="card-desc">Real-time facial emotion recognition using deep learning and computer vision.</div>
        <div class="card-tags">
          <span class="tag">TensorFlow</span><span class="tag">OpenCV</span><span class="tag">CNN</span>
        </div>
      </div>

      <div class="project-card">
        <div class="card-top">
          <span class="card-icon">🗳</span>
          <span class="card-status status-research">RESEARCH</span>
        </div>
        <div class="card-name">Blockchain Voting</div>
        <div class="card-desc">Transparent, tamper-proof voting platform built on distributed ledger technology.</div>
        <div class="card-tags">
          <span class="tag">Solidity</span><span class="tag">Web3</span><span class="tag">Ethereum</span>
        </div>
      </div>

    </div>
  </div>

  <!-- TECH STACK -->
  <div class="section">
    <div class="section-header">
      <span class="section-label">// tech arsenal</span>
      <div class="section-line"></div>
      <span class="section-num">03</span>
    </div>
    <div class="stack-grid">
      <div class="stack-cat">
        <div class="cat-label">Machine Learning</div>
        <div class="tech-list">
          <span class="tech-pill">PyTorch</span>
          <span class="tech-pill">TensorFlow</span>
          <span class="tech-pill">Scikit-Learn</span>
        </div>
      </div>
      <div class="stack-cat">
        <div class="cat-label">Generative AI</div>
        <div class="tech-list">
          <span class="tech-pill">LangChain</span>
          <span class="tech-pill">OpenAI API</span>
          <span class="tech-pill">HuggingFace</span>
          <span class="tech-pill">CrewAI</span>
          <span class="tech-pill">AutoGen</span>
        </div>
      </div>
      <div class="stack-cat">
        <div class="cat-label">Data Science</div>
        <div class="tech-list">
          <span class="tech-pill">Pandas</span>
          <span class="tech-pill">NumPy</span>
          <span class="tech-pill">Matplotlib</span>
          <span class="tech-pill">Power BI</span>
        </div>
      </div>
      <div class="stack-cat">
        <div class="cat-label">Infrastructure</div>
        <div class="tech-list">
          <span class="tech-pill">Python</span>
          <span class="tech-pill">FastAPI</span>
          <span class="tech-pill">Docker</span>
          <span class="tech-pill">Git</span>
        </div>
      </div>
    </div>
  </div>

  <!-- SKILL BARS -->
  <div class="section">
    <div class="section-header">
      <span class="section-label">// proficiency</span>
      <div class="section-line"></div>
      <span class="section-num">04</span>
    </div>
    <div class="skill-rows" id="skill-rows">
      <div class="skill-row"><span class="skill-name">Python</span><div class="skill-track"><div class="skill-fill" data-pct="95" style="background:linear-gradient(90deg,#00d9ff,#7c3aed);width:0"></div></div><span class="skill-pct">95%</span></div>
      <div class="skill-row"><span class="skill-name">Machine Learning</span><div class="skill-track"><div class="skill-fill" data-pct="85" style="background:linear-gradient(90deg,#10b981,#00d9ff);width:0"></div></div><span class="skill-pct">85%</span></div>
      <div class="skill-row"><span class="skill-name">LLM / GenAI</span><div class="skill-track"><div class="skill-fill" data-pct="88" style="background:linear-gradient(90deg,#7c3aed,#f59e0b);width:0"></div></div><span class="skill-pct">88%</span></div>
      <div class="skill-row"><span class="skill-name">Data Science</span><div class="skill-track"><div class="skill-fill" data-pct="90" style="background:linear-gradient(90deg,#f59e0b,#10b981);width:0"></div></div><span class="skill-pct">90%</span></div>
      <div class="skill-row"><span class="skill-name">Deep Learning</span><div class="skill-track"><div class="skill-fill" data-pct="80" style="background:linear-gradient(90deg,#00d9ff,#10b981);width:0"></div></div><span class="skill-pct">80%</span></div>
    </div>
  </div>

  <!-- CONTRIBUTION GRAPH -->
  <div class="section">
    <div class="section-header">
      <span class="section-label">// contribution activity</span>
      <div class="section-line"></div>
      <span class="section-num">05</span>
    </div>
    <div class="contrib-graph">
      <div class="contrib-weeks" id="contrib-graph"></div>
      <div class="contrib-legend">
        <span>Less</span>
        <div class="legend-cell" style="background:var(--bg4)"></div>
        <div class="legend-cell" style="background:rgba(0,217,255,.18)"></div>
        <div class="legend-cell" style="background:rgba(0,217,255,.38)"></div>
        <div class="legend-cell" style="background:rgba(0,217,255,.62)"></div>
        <div class="legend-cell" style="background:rgba(0,217,255,.9)"></div>
        <span>More</span>
      </div>
    </div>
  </div>

  <!-- CURRENT MISSION -->
  <div class="section">
    <div class="section-header">
      <span class="section-label">// current mission</span>
      <div class="section-line"></div>
      <span class="section-num">06</span>
    </div>
    <div class="mission-block">
      <div class="mission-item"><span class="plus">+</span><span class="text">Building <span class="highlight">Production-Ready AI Agents</span> with real-world tool use</span></div>
      <div class="mission-item"><span class="plus">+</span><span class="text">Deep-diving <span class="highlight">Multi-Agent Architectures</span> & orchestration patterns</span></div>
      <div class="mission-item"><span class="plus">+</span><span class="text">Exploring <span class="highlight">Advanced RAG Pipelines</span> with hybrid retrieval</span></div>
      <div class="mission-item"><span class="plus">+</span><span class="text">Contributing to <span class="highlight">Open Source AI</span> projects & publishing research</span></div>
      <div class="mission-item"><span class="plus">+</span><span class="text">Innovating at the intersection of <span class="highlight">LLMs × Agentic Systems</span></span></div>
    </div>
  </div>

  <!-- CONNECT -->
  <div class="section">
    <div class="section-header">
      <span class="section-label">// connect</span>
      <div class="section-line"></div>
      <span class="section-num">07</span>
    </div>
    <div class="connect-grid">
      <a class="connect-card" href="#">
        <span class="connect-icon">⚡</span>
        <div class="connect-info">
          <div class="connect-platform">GitHub</div>
          <div class="connect-handle">@vivek-kumar</div>
        </div>
      </a>
      <a class="connect-card" href="#">
        <span class="connect-icon">💼</span>
        <div class="connect-info">
          <div class="connect-platform">LinkedIn</div>
          <div class="connect-handle">Vivek Kumar</div>
        </div>
      </a>
      <a class="connect-card" href="#">
        <span class="connect-icon">🐦</span>
        <div class="connect-info">
          <div class="connect-platform">Twitter / X</div>
          <div class="connect-handle">@vivek_ai</div>
        </div>
      </a>
      <a class="connect-card" href="#">
        <span class="connect-icon">📧</span>
        <div class="connect-info">
          <div class="connect-platform">Email</div>
          <div class="connect-handle">vivek@email.com</div>
        </div>
      </a>
    </div>
  </div>

  <!-- FOOTER -->
  <footer class="footer">
    <p class="quote">"Artificial Intelligence is the <span>new electricity.</span>"</p>
    <p>Building the future, one intelligent system at a time.</p>
    <p style="margin-top:12px;font-size:10px;color:#3a4050">made with 🤖 + ☕ · Vivek Kumar · Delhi, India</p>
  </footer>

</div>

<script>
// Typing animation
const phrases = [
  'Building agentic AI systems...',
  'Training neural networks...',
  'Orchestrating LLM agents...',
  'Exploring multi-agent architectures...',
  'Pushing the limits of AI...'
];
let phraseIdx = 0, charIdx = 0, deleting = false;
const el = document.getElementById('typed-text');

function type() {
  const current = phrases[phraseIdx];
  if (!deleting) {
    el.textContent = current.slice(0, ++charIdx);
    if (charIdx === current.length) { deleting = true; setTimeout(type, 2000); return; }
  } else {
    el.textContent = current.slice(0, --charIdx);
    if (charIdx === 0) { deleting = false; phraseIdx = (phraseIdx + 1) % phrases.length; }
  }
  setTimeout(type, deleting ? 35 : 65);
}
setTimeout(type, 1000);

// Skill bars animate on scroll
const observer = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.querySelectorAll('.skill-fill').forEach(bar => {
        bar.style.width = bar.dataset.pct + '%';
      });
      observer.unobserve(e.target);
    }
  });
}, { threshold: 0.3 });
observer.observe(document.getElementById('skill-rows'));

// Contribution graph
const graph = document.getElementById('contrib-graph');
const levels = [0,0,1,1,2,2,3,3,4,4,3,2,1,0];
for (let w = 0; w < 52; w++) {
  const col = document.createElement('div');
  col.className = 'contrib-col';
  for (let d = 0; d < 7; d++) {
    const cell = document.createElement('div');
    const rand = Math.random();
    let level = 0;
    if (rand > 0.7) level = 1;
    if (rand > 0.82) level = 2;
    if (rand > 0.91) level = 3;
    if (rand > 0.96) level = 4;
    // more activity toward recent weeks
    if (w > 38 && rand > 0.55) level = Math.min(level + 1, 4);
    cell.className = 'contrib-cell' + (level ? ' l' + level : '');
    col.appendChild(cell);
  }
  graph.appendChild(col);
}
</script>
</body>
</html>
