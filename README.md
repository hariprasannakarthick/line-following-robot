<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Arduino Line Following Robot — README</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600&family=Outfit:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0d1117;
    --surface: #161b22;
    --border: #30363d;
    --text: #e6edf3;
    --muted: #8b949e;
    --accent: #58a6ff;
    --green: #3fb950;
    --orange: #d29922;
    --red: #f85149;
    --purple: #bc8cff;
    --code-bg: #161b22;
    --code-border: #30363d;
    --table-alt: #161b22;
    --heading-border: #21262d;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Outfit', sans-serif;
    font-size: 16px;
    line-height: 1.7;
    padding: 40px 20px;
  }

  .readme {
    max-width: 860px;
    margin: 0 auto;
    background: var(--bg);
  }

  /* ── Header ── */
  .readme-header {
    border-bottom: 1px solid var(--border);
    padding-bottom: 28px;
    margin-bottom: 32px;
  }

  h1 {
    font-size: 2rem;
    font-weight: 700;
    color: var(--text);
    letter-spacing: -0.5px;
    margin-bottom: 12px;
  }

  .badges {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 16px;
  }

  .badge {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    padding: 3px 10px;
    border-radius: 20px;
    font-weight: 600;
    letter-spacing: 0.3px;
  }
  .badge-blue   { background: #1f3a5c; color: #58a6ff; border: 1px solid #2d5986; }
  .badge-green  { background: #1a3a28; color: #3fb950; border: 1px solid #2a5c3d; }
  .badge-orange { background: #3a2e14; color: #d29922; border: 1px solid #5c4a1e; }
  .badge-purple { background: #2d1f4a; color: #bc8cff; border: 1px solid #4a2d80; }

  .tagline {
    color: var(--muted);
    font-size: 15px;
    max-width: 680px;
  }

  /* ── Typography ── */
  h2 {
    font-size: 1.35rem;
    font-weight: 700;
    color: var(--text);
    margin: 36px 0 14px;
    padding-bottom: 8px;
    border-bottom: 1px solid var(--heading-border);
  }

  h3 {
    font-size: 1.05rem;
    font-weight: 600;
    color: var(--accent);
    margin: 22px 0 10px;
  }

  p { margin: 10px 0; color: var(--text); }

  a { color: var(--accent); text-decoration: none; }
  a:hover { text-decoration: underline; }

  ul, ol {
    padding-left: 22px;
    margin: 8px 0 12px;
  }
  li { margin: 5px 0; color: var(--text); }

  strong { color: var(--text); font-weight: 600; }

  /* ── Code ── */
  code {
    font-family: 'JetBrains Mono', monospace;
    font-size: 13px;
    background: #21262d;
    color: #e6edf3;
    padding: 2px 6px;
    border-radius: 4px;
    border: 1px solid var(--code-border);
  }

  pre {
    background: #010409;
    border: 1px solid var(--code-border);
    border-radius: 8px;
    padding: 20px;
    overflow-x: auto;
    margin: 14px 0;
    position: relative;
  }

  pre code {
    background: none;
    border: none;
    padding: 0;
    font-size: 13.5px;
    line-height: 1.7;
    color: #e6edf3;
  }

  /* Syntax highlight classes */
  .kw  { color: #ff7b72; }   /* keywords */
  .fn  { color: #d2a8ff; }   /* functions */
  .num { color: #79c0ff; }   /* numbers */
  .str { color: #a5d6ff; }   /* strings */
  .cmt { color: #8b949e; font-style: italic; }  /* comments */
  .pp  { color: #ff7b72; }   /* preprocessor */
  .typ { color: #ffa657; }   /* types */
  .var { color: #e6edf3; }   /* vars */

  .code-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: #161b22;
    border: 1px solid var(--code-border);
    border-bottom: none;
    border-radius: 8px 8px 0 0;
    padding: 8px 16px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    color: var(--muted);
    margin-top: 14px;
  }
  .code-header + pre {
    border-radius: 0 0 8px 8px;
    margin-top: 0;
  }

  /* ── Tables ── */
  table {
    width: 100%;
    border-collapse: collapse;
    margin: 14px 0;
    font-size: 15px;
  }

  th {
    background: #161b22;
    color: var(--muted);
    font-weight: 600;
    text-align: left;
    padding: 10px 14px;
    border: 1px solid var(--border);
    font-family: 'JetBrains Mono', monospace;
    font-size: 13px;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }

  td {
    padding: 9px 14px;
    border: 1px solid var(--border);
    color: var(--text);
  }

  tr:nth-child(even) td { background: var(--table-alt); }

  td:first-child, th:first-child { border-radius: 0; }

  /* ── Info boxes ── */
  .callout {
    border-left: 3px solid;
    padding: 14px 18px;
    border-radius: 0 8px 8px 0;
    margin: 16px 0;
    font-size: 15px;
  }
  .callout-blue   { border-color: var(--accent); background: #0d1f33; }
  .callout-green  { border-color: var(--green);  background: #0d2218; }
  .callout-orange { border-color: var(--orange); background: #251d0a; }
  .callout-red    { border-color: var(--red);    background: #260d0d; }

  .callout-label {
    font-weight: 700;
    font-size: 12px;
    letter-spacing: 1px;
    text-transform: uppercase;
    margin-bottom: 5px;
  }
  .callout-blue   .callout-label { color: var(--accent); }
  .callout-green  .callout-label { color: var(--green); }
  .callout-orange .callout-label { color: var(--orange); }
  .callout-red    .callout-label { color: var(--red); }

  /* ── Architecture flow ── */
  .flow {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    gap: 6px;
    margin: 16px 0;
    padding: 18px;
    background: #010409;
    border: 1px solid var(--border);
    border-radius: 8px;
  }

  .flow-step {
    display: flex;
    align-items: center;
    gap: 8px;
    background: #161b22;
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 8px 14px;
    font-size: 14px;
    font-weight: 500;
  }

  .flow-step .num-badge {
    width: 22px;
    height: 22px;
    background: var(--accent);
    color: #0d1117;
    border-radius: 50%;
    font-size: 11px;
    font-weight: 700;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'JetBrains Mono', monospace;
  }

  .flow-arrow {
    color: var(--muted);
    font-size: 18px;
    font-weight: 300;
  }

  /* ── Sensor layout viz ── */
  .sensor-layout {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    padding: 24px;
    background: #010409;
    border: 1px solid var(--border);
    border-radius: 8px;
    margin: 14px 0;
    flex-wrap: wrap;
  }

  .sensor-box {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 6px;
  }

  .sensor-circle {
    width: 48px;
    height: 48px;
    border-radius: 50%;
    border: 2px solid;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'JetBrains Mono', monospace;
    font-size: 13px;
    font-weight: 700;
  }
  .sensor-left  { border-color: #f85149; color: #f85149; background: #1a0606; }
  .sensor-mid   { border-color: #3fb950; color: #3fb950; background: #061a0d; }
  .sensor-right { border-color: #58a6ff; color: #58a6ff; background: #060f1a; }

  .sensor-label {
    font-size: 11px;
    font-family: 'JetBrains Mono', monospace;
    color: var(--muted);
    text-align: center;
  }

  .sensor-weight {
    font-size: 13px;
    font-weight: 700;
    font-family: 'JetBrains Mono', monospace;
  }
  .sensor-left  .sensor-weight { color: #f85149; }
  .sensor-mid   .sensor-weight { color: #3fb950; }
  .sensor-right .sensor-weight { color: #58a6ff; }

  /* ── Formula box ── */
  .formula {
    background: #010409;
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 18px 24px;
    margin: 14px 0;
    text-align: center;
    font-family: 'JetBrains Mono', monospace;
    font-size: 15px;
    color: #d2a8ff;
    letter-spacing: 0.5px;
  }

  /* ── Performance grid ── */
  .perf-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
    gap: 10px;
    margin: 14px 0;
  }

  .perf-card {
    background: #161b22;
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 14px 16px;
  }

  .perf-card .label {
    font-size: 12px;
    color: var(--muted);
    font-family: 'JetBrains Mono', monospace;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    margin-bottom: 4px;
  }

  .perf-card .value {
    font-size: 15px;
    font-weight: 600;
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    flex-shrink: 0;
  }
  .dot-green  { background: #3fb950; }
  .dot-orange { background: #d29922; }
  .dot-red    { background: #f85149; }

  /* ── Footer ── */
  .readme-footer {
    margin-top: 48px;
    padding-top: 24px;
    border-top: 1px solid var(--border);
    display: flex;
    align-items: center;
    gap: 14px;
  }

  .avatar {
    width: 48px;
    height: 48px;
    border-radius: 50%;
    background: linear-gradient(135deg, #58a6ff, #bc8cff);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 20px;
    font-weight: 700;
    color: #fff;
    flex-shrink: 0;
  }

  .author-info .name {
    font-weight: 700;
    font-size: 16px;
  }

  .author-info .role {
    color: var(--muted);
    font-size: 14px;
  }

  hr {
    border: none;
    border-top: 1px solid var(--border);
    margin: 32px 0;
  }

  .toc {
    background: #0d1117;
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 18px 22px;
    margin: 24px 0;
  }

  .toc-title {
    font-size: 13px;
    font-weight: 700;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 1px;
    margin-bottom: 10px;
    font-family: 'JetBrains Mono', monospace;
  }

  .toc ul {
    list-style: none;
    padding: 0;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 4px 20px;
  }

  .toc li { margin: 0; }
  .toc a { color: var(--muted); font-size: 14px; }
  .toc a:hover { color: var(--accent); }

  @media (max-width: 600px) {
    h1 { font-size: 1.5rem; }
    .toc ul { grid-template-columns: 1fr; }
    .flow { flex-direction: column; }
    .flow-arrow { transform: rotate(90deg); }
  }
</style>
</head>
<body>
<article class="readme">

  <!-- ── Header ── -->
  <div class="readme-header">
    <h1>🚗 Arduino Line Following Robot</h1>
    <div class="badges">
      <span class="badge badge-blue">🔵 Arduino</span>
      <span class="badge badge-green">✅ 5-IR Sensor Array</span>
      <span class="badge badge-orange">⚡ Weighted Estimation</span>
      <span class="badge badge-purple">🔧 C++ / Embedded</span>
    </div>
    <p class="tagline">
      An autonomous line-following robot that estimates line position using a
      <strong>weighted sensor approach</strong> and adjusts motor speeds dynamically —
      smoother and more stable than traditional rule-based systems.
    </p>
  </div>

  <!-- ── TOC ── -->
  <div class="toc">
    <div class="toc-title">📋 Table of Contents</div>
    <ul>
      <li><a href="#overview">Overview</a></li>
      <li><a href="#components">Components Used</a></li>
      <li><a href="#architecture">System Architecture</a></li>
      <li><a href="#position">Position Estimation</a></li>
      <li><a href="#control">Control Strategy</a></li>
      <li><a href="#circuit">Circuit Connections</a></li>
      <li><a href="#code">Full Code</a></li>
      <li><a href="#performance">Performance</a></li>
      <li><a href="#limitations">Limitations</a></li>
      <li><a href="#future">Future Improvements</a></li>
    </ul>
  </div>

  <!-- ── Overview ── -->
  <h2 id="overview">📌 Overview</h2>
  <p>
    The robot detects a contrasting line on the ground and continuously estimates its position
    relative to the center of the robot. Based on this deviation (error), motor speeds are
    adjusted in real time to maintain alignment with the path.
  </p>
  <div class="callout callout-blue">
    <div class="callout-label">💡 Key Advantage</div>
    This approach improves stability, reduces jerky motion, and performs significantly better than
    traditional if-else logic systems by treating line position as a <strong>continuous value</strong>,
    not a discrete state.
  </div>

  <!-- ── Components ── -->
  <h2 id="components">🧩 Components Used</h2>
  <table>
    <thead>
      <tr><th>Component</th><th>Specification</th></tr>
    </thead>
    <tbody>
      <tr><td>Microcontroller</td><td>Arduino Nano / Uno</td></tr>
      <tr><td>Sensor Array</td><td>5-Channel IR Sensor Array</td></tr>
      <tr><td>Motor Driver</td><td>L298N Dual H-Bridge</td></tr>
      <tr><td>Actuators</td><td>DC Motors (×2)</td></tr>
      <tr><td>Chassis</td><td>Robot Chassis with Wheels</td></tr>
      <tr><td>Power</td><td>Battery Pack</td></tr>
    </tbody>
  </table>

  <!-- ── Architecture ── -->
  <h2 id="architecture">🧠 System Architecture</h2>
  <div class="flow">
    <div class="flow-step"><span class="num-badge">1</span> IR Sensors detect line</div>
    <span class="flow-arrow">→</span>
    <div class="flow-step"><span class="num-badge">2</span> Compute positional error</div>
    <span class="flow-arrow">→</span>
    <div class="flow-step"><span class="num-badge">3</span> Calculate correction</div>
    <span class="flow-arrow">→</span>
    <div class="flow-step"><span class="num-badge">4</span> Adjust motor speeds</div>
    <span class="flow-arrow">→</span>
    <div class="flow-step"><span class="num-badge">5</span> Robot aligns to path</div>
  </div>

  <!-- ── Position Estimation ── -->
  <h2 id="position">📐 Position Estimation (Weighted Sensor Method)</h2>
  <p>Each sensor is assigned a positional weight reflecting its distance from center:</p>

  <div class="sensor-layout">
    <div class="sensor-box">
      <div class="sensor-circle sensor-left">S1</div>
      <div class="sensor-label">Far Left</div>
      <div class="sensor-weight sensor-left">−2</div>
    </div>
    <div class="sensor-box">
      <div class="sensor-circle sensor-left">S2</div>
      <div class="sensor-label">Left</div>
      <div class="sensor-weight sensor-left">−1</div>
    </div>
    <div class="sensor-box">
      <div class="sensor-circle sensor-mid">S3</div>
      <div class="sensor-label">Center</div>
      <div class="sensor-weight sensor-mid">0</div>
    </div>
    <div class="sensor-box">
      <div class="sensor-circle sensor-right">S4</div>
      <div class="sensor-label">Right</div>
      <div class="sensor-weight sensor-right">+1</div>
    </div>
    <div class="sensor-box">
      <div class="sensor-circle sensor-right">S5</div>
      <div class="sensor-label">Far Right</div>
      <div class="sensor-weight sensor-right">+2</div>
    </div>
  </div>

  <p>Line position is calculated using the weighted centroid formula:</p>
  <div class="formula">
    Position = Σ( sensor[i] × weight[i] ) / Σ( sensor[i] )
  </div>

  <h3>Implementation</h3>
  <div class="code-header">
    <span>⚙️ calculatePosition.cpp</span>
    <span>Arduino C++</span>
  </div>
<pre><code><span class="typ">int</span> <span class="var">weights</span>[<span class="num">5</span>] = {<span class="num">-2</span>, <span class="num">-1</span>, <span class="num">0</span>, <span class="num">1</span>, <span class="num">2</span>};

<span class="typ">int</span> <span class="fn">calculatePosition</span>(<span class="typ">int</span> <span class="var">sensors</span>[]) {
  <span class="typ">int</span> <span class="var">numerator</span>   = <span class="num">0</span>;
  <span class="typ">int</span> <span class="var">denominator</span> = <span class="num">0</span>;

  <span class="kw">for</span> (<span class="typ">int</span> <span class="var">i</span> = <span class="num">0</span>; <span class="var">i</span> &lt; <span class="num">5</span>; <span class="var">i</span>++) {
    <span class="var">numerator</span>   += <span class="var">sensors</span>[<span class="var">i</span>] * <span class="var">weights</span>[<span class="var">i</span>];
    <span class="var">denominator</span> += <span class="var">sensors</span>[<span class="var">i</span>];
  }

  <span class="kw">if</span> (<span class="var">denominator</span> == <span class="num">0</span>) <span class="kw">return</span> <span class="num">0</span>; <span class="cmt">// Line lost</span>
  <span class="kw">return</span> <span class="var">numerator</span> / <span class="var">denominator</span>;
}</code></pre>

  <!-- ── Control Strategy ── -->
  <h2 id="control">⚙️ Control Strategy</h2>
  <p>The robot uses <strong>error-based differential control</strong> to smoothly steer toward the line:</p>

  <div class="code-header">
    <span>🎛️ motorControl.cpp</span>
    <span>Arduino C++</span>
  </div>
<pre><code><span class="typ">int</span>   <span class="var">baseSpeed</span> = <span class="num">150</span>;
<span class="typ">float</span> <span class="var">K</span>         = <span class="num">50.0</span>; <span class="cmt">// Tuning gain constant</span>

<span class="typ">int</span> <span class="var">leftSpeed</span>  = <span class="var">baseSpeed</span> - <span class="var">K</span> * <span class="var">error</span>;
<span class="typ">int</span> <span class="var">rightSpeed</span> = <span class="var">baseSpeed</span> + <span class="var">K</span> * <span class="var">error</span>;</code></pre>

  <table>
    <thead>
      <tr><th>Condition</th><th>Behavior</th></tr>
    </thead>
    <tbody>
      <tr><td><code>error = 0</code></td><td>Both motors equal → move straight</td></tr>
      <tr><td><code>error &lt; 0</code></td><td>Right motor faster → turn left</td></tr>
      <tr><td><code>error &gt; 0</code></td><td>Left motor faster → turn right</td></tr>
    </tbody>
  </table>

  <!-- ── Circuit Connections ── -->
  <h2 id="circuit">🔌 Circuit Connections</h2>

  <h3>Sensor Pins</h3>
  <table>
    <thead><tr><th>Sensor</th><th>Arduino Pin</th></tr></thead>
    <tbody>
      <tr><td>S1 (Far Left)</td><td><code>D2</code></td></tr>
      <tr><td>S2 (Left)</td><td><code>D3</code></td></tr>
      <tr><td>S3 (Center)</td><td><code>D4</code></td></tr>
      <tr><td>S4 (Right)</td><td><code>D5</code></td></tr>
      <tr><td>S5 (Far Right)</td><td><code>D6</code></td></tr>
    </tbody>
  </table>

  <h3>Motor Driver (L298N)</h3>
  <table>
    <thead><tr><th>Function</th><th>Pin</th></tr></thead>
    <tbody>
      <tr><td>ENA (Left Enable)</td><td><code>D9</code></td></tr>
      <tr><td>IN1</td><td><code>D8</code></td></tr>
      <tr><td>IN2</td><td><code>D7</code></td></tr>
      <tr><td>ENB (Right Enable)</td><td><code>D10</code></td></tr>
      <tr><td>IN3</td><td><code>D12</code></td></tr>
      <tr><td>IN4</td><td><code>D11</code></td></tr>
    </tbody>
  </table>

  <!-- ── Full Code ── -->
  <h2 id="code">💻 Full Code</h2>
  <div class="code-header">
    <span>📄 line_follower.ino</span>
    <span>Arduino C++</span>
  </div>
<pre><code><span class="cmt">// ────────────────────────────────────────────
//  Arduino Line Following Robot
//  Weighted Sensor Position Estimation
// ────────────────────────────────────────────</span>

<span class="cmt">// Sensor Pins</span>
<span class="pp">#define</span> <span class="var">S1</span> <span class="num">2</span>
<span class="pp">#define</span> <span class="var">S2</span> <span class="num">3</span>
<span class="pp">#define</span> <span class="var">S3</span> <span class="num">4</span>
<span class="pp">#define</span> <span class="var">S4</span> <span class="num">5</span>
<span class="pp">#define</span> <span class="var">S5</span> <span class="num">6</span>

<span class="cmt">// Motor Driver Pins</span>
<span class="pp">#define</span> <span class="var">ENA</span> <span class="num">9</span>
<span class="pp">#define</span> <span class="var">IN1</span> <span class="num">8</span>
<span class="pp">#define</span> <span class="var">IN2</span> <span class="num">7</span>
<span class="pp">#define</span> <span class="var">ENB</span> <span class="num">10</span>
<span class="pp">#define</span> <span class="var">IN3</span> <span class="num">12</span>
<span class="pp">#define</span> <span class="var">IN4</span> <span class="num">11</span>

<span class="typ">int</span>   <span class="var">baseSpeed</span> = <span class="num">150</span>;
<span class="typ">float</span> <span class="var">K</span>         = <span class="num">50.0</span>;
<span class="typ">int</span>   <span class="var">weights</span>[<span class="num">5</span>] = {<span class="num">-2</span>, <span class="num">-1</span>, <span class="num">0</span>, <span class="num">1</span>, <span class="num">2</span>};

<span class="kw">void</span> <span class="fn">setup</span>() {
  <span class="fn">pinMode</span>(<span class="var">S1</span>, <span class="var">INPUT</span>); <span class="fn">pinMode</span>(<span class="var">S2</span>, <span class="var">INPUT</span>);
  <span class="fn">pinMode</span>(<span class="var">S3</span>, <span class="var">INPUT</span>); <span class="fn">pinMode</span>(<span class="var">S4</span>, <span class="var">INPUT</span>);
  <span class="fn">pinMode</span>(<span class="var">S5</span>, <span class="var">INPUT</span>);

  <span class="fn">pinMode</span>(<span class="var">ENA</span>, <span class="var">OUTPUT</span>); <span class="fn">pinMode</span>(<span class="var">IN1</span>, <span class="var">OUTPUT</span>);
  <span class="fn">pinMode</span>(<span class="var">IN2</span>, <span class="var">OUTPUT</span>); <span class="fn">pinMode</span>(<span class="var">ENB</span>, <span class="var">OUTPUT</span>);
  <span class="fn">pinMode</span>(<span class="var">IN3</span>, <span class="var">OUTPUT</span>); <span class="fn">pinMode</span>(<span class="var">IN4</span>, <span class="var">OUTPUT</span>);

  <span class="var">Serial</span>.<span class="fn">begin</span>(<span class="num">9600</span>);
}

<span class="cmt">// Read all 5 sensors into array</span>
<span class="kw">void</span> <span class="fn">readSensors</span>(<span class="typ">int</span> <span class="var">sensors</span>[]) {
  <span class="var">sensors</span>[<span class="num">0</span>] = <span class="fn">digitalRead</span>(<span class="var">S1</span>);
  <span class="var">sensors</span>[<span class="num">1</span>] = <span class="fn">digitalRead</span>(<span class="var">S2</span>);
  <span class="var">sensors</span>[<span class="num">2</span>] = <span class="fn">digitalRead</span>(<span class="var">S3</span>);
  <span class="var">sensors</span>[<span class="num">3</span>] = <span class="fn">digitalRead</span>(<span class="var">S4</span>);
  <span class="var">sensors</span>[<span class="num">4</span>] = <span class="fn">digitalRead</span>(<span class="var">S5</span>);
}

<span class="cmt">// Weighted centroid line position estimation</span>
<span class="typ">int</span> <span class="fn">calculatePosition</span>(<span class="typ">int</span> <span class="var">sensors</span>[]) {
  <span class="typ">int</span> <span class="var">numerator</span> = <span class="num">0</span>, <span class="var">denominator</span> = <span class="num">0</span>;

  <span class="kw">for</span> (<span class="typ">int</span> <span class="var">i</span> = <span class="num">0</span>; <span class="var">i</span> &lt; <span class="num">5</span>; <span class="var">i</span>++) {
    <span class="var">numerator</span>   += <span class="var">sensors</span>[<span class="var">i</span>] * <span class="var">weights</span>[<span class="var">i</span>];
    <span class="var">denominator</span> += <span class="var">sensors</span>[<span class="var">i</span>];
  }

  <span class="kw">if</span> (<span class="var">denominator</span> == <span class="num">0</span>) <span class="kw">return</span> <span class="num">0</span>; <span class="cmt">// Line lost</span>
  <span class="kw">return</span> <span class="var">numerator</span> / <span class="var">denominator</span>;
}

<span class="cmt">// Differential motor speed control</span>
<span class="kw">void</span> <span class="fn">setMotorSpeed</span>(<span class="typ">int</span> <span class="var">leftSpeed</span>, <span class="typ">int</span> <span class="var">rightSpeed</span>) {
  <span class="var">leftSpeed</span>  = <span class="fn">constrain</span>(<span class="var">leftSpeed</span>,  <span class="num">0</span>, <span class="num">255</span>);
  <span class="var">rightSpeed</span> = <span class="fn">constrain</span>(<span class="var">rightSpeed</span>, <span class="num">0</span>, <span class="num">255</span>);

  <span class="fn">analogWrite</span>(<span class="var">ENA</span>, <span class="var">leftSpeed</span>);
  <span class="fn">analogWrite</span>(<span class="var">ENB</span>, <span class="var">rightSpeed</span>);

  <span class="fn">digitalWrite</span>(<span class="var">IN1</span>, <span class="var">HIGH</span>); <span class="fn">digitalWrite</span>(<span class="var">IN2</span>, <span class="var">LOW</span>);
  <span class="fn">digitalWrite</span>(<span class="var">IN3</span>, <span class="var">HIGH</span>); <span class="fn">digitalWrite</span>(<span class="var">IN4</span>, <span class="var">LOW</span>);
}

<span class="kw">void</span> <span class="fn">stopBot</span>() {
  <span class="fn">analogWrite</span>(<span class="var">ENA</span>, <span class="num">0</span>);
  <span class="fn">analogWrite</span>(<span class="var">ENB</span>, <span class="num">0</span>);
}

<span class="kw">void</span> <span class="fn">loop</span>() {
  <span class="typ">int</span> <span class="var">sensors</span>[<span class="num">5</span>];
  <span class="fn">readSensors</span>(<span class="var">sensors</span>);

  <span class="cmt">// Stop if line is completely lost</span>
  <span class="kw">if</span> (<span class="var">sensors</span>[<span class="num">0</span>]==<span class="num">0</span> &amp;&amp; <span class="var">sensors</span>[<span class="num">1</span>]==<span class="num">0</span> &amp;&amp; <span class="var">sensors</span>[<span class="num">2</span>]==<span class="num">0</span> &amp;&amp;
      <span class="var">sensors</span>[<span class="num">3</span>]==<span class="num">0</span> &amp;&amp; <span class="var">sensors</span>[<span class="num">4</span>]==<span class="num">0</span>) {
    <span class="fn">stopBot</span>();
    <span class="kw">return</span>;
  }

  <span class="typ">int</span> <span class="var">error</span>      = <span class="fn">calculatePosition</span>(<span class="var">sensors</span>);
  <span class="typ">int</span> <span class="var">leftSpeed</span>  = <span class="var">baseSpeed</span> - <span class="var">K</span> * <span class="var">error</span>;
  <span class="typ">int</span> <span class="var">rightSpeed</span> = <span class="var">baseSpeed</span> + <span class="var">K</span> * <span class="var">error</span>;

  <span class="var">Serial</span>.<span class="fn">print</span>(<span class="str">"Error: "</span>); <span class="var">Serial</span>.<span class="fn">println</span>(<span class="var">error</span>);

  <span class="fn">setMotorSpeed</span>(<span class="var">leftSpeed</span>, <span class="var">rightSpeed</span>);
}</code></pre>

  <!-- ── Features ── -->
  <h2>🚀 Features</h2>
  <ul>
    <li>Weighted sensor-based line position estimation (continuous, not discrete)</li>
    <li>Smooth differential motor control via proportional gain</li>
    <li>Real-time error correction on every loop iteration</li>
    <li>Better stability than basic rule-based if-else systems</li>
    <li>Modular and scalable code — ready for PID upgrade</li>
  </ul>

  <!-- ── Performance ── -->
  <h2 id="performance">📊 Performance Evaluation</h2>
  <div class="perf-grid">
    <div class="perf-card">
      <div class="label">Straight Path</div>
      <div class="value"><span class="dot dot-green"></span>Stable</div>
    </div>
    <div class="perf-card">
      <div class="label">Sharp Turns</div>
      <div class="value"><span class="dot dot-orange"></span>Moderate deviation</div>
    </div>
    <div class="perf-card">
      <div class="label">Low Lighting</div>
      <div class="value"><span class="dot dot-orange"></span>Slight accuracy drop</div>
    </div>
    <div class="perf-card">
      <div class="label">Rough Surface</div>
      <div class="value"><span class="dot dot-orange"></span>Minor oscillations</div>
    </div>
  </div>

  <!-- ── Limitations ── -->
  <h2 id="limitations">⚠️ Limitations</h2>
  <div class="callout callout-orange">
    <div class="callout-label">Known Constraints</div>
    <ul style="margin-top:6px;">
      <li>No PID control — limits performance and stability at higher speeds</li>
      <li>Sensitive to extreme or uneven lighting conditions</li>
      <li>No advanced recovery algorithm if line is completely lost</li>
    </ul>
  </div>

  <!-- ── Future ── -->
  <h2 id="future">🔮 Future Improvements</h2>
  <ul>
    <li>Implement full <strong>PID control</strong> (proportional + integral + derivative)</li>
    <li>Add <strong>adaptive speed control</strong> based on path curvature</li>
    <li>Line recovery algorithm for lost-line scenarios</li>
    <li>Obstacle detection via ultrasonic sensors</li>
    <li>Camera-based visual line tracking</li>
  </ul>

  <!-- ── What Makes It Different ── -->
  <h2>🏁 What Makes This Project Different</h2>
  <div class="callout callout-green">
    <div class="callout-label">Design Philosophy</div>
    <p>
      Uses <strong>weighted multi-sensor estimation</strong> instead of discrete if-else branching,
      producing smoother and more stable movement. Structured with scalability in mind — the architecture
      directly accommodates PID or vision-based upgrades without a full rewrite.
    </p>
  </div>

  <hr>

  <!-- ── Author ── -->
  <div class="readme-footer">
    <div class="avatar">HP</div>
    <div class="author-info">
      <div class="name">Hari Prasanna</div>
      <div class="role">B.Tech Robotics Engineering</div>
    </div>
  </div>

</article>
</body>
</html>
