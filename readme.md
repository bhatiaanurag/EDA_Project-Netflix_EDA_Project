<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Netflix Data Analysis – EDA Project</title>
<style>
  @keyframes fadeUp { from { opacity: 0; transform: translateY(24px); } to { opacity: 1; transform: translateY(0); } }
  @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
  @keyframes pulse { 0%,100% { opacity:1; } 50% { opacity: 0.5; } }
  @keyframes countUp { from { opacity:0; transform: scale(0.8); } to { opacity:1; transform: scale(1); } }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    background: #0a0a0a;
    color: #e5e5e5;
    min-height: 100vh;
  }

  .wrap { max-width: 860px; margin: 0 auto; padding: 0 1rem 4rem; }

  /* Hero */
  .hero { padding: 3.5rem 2rem 2.5rem; text-align: center; border-bottom: 0.5px solid #2a2a2a; animation: fadeIn 0.7s ease; }
  .nfx-badge { display: inline-flex; align-items: center; gap: 8px; background: #e50914; color: #fff; font-size: 12px; font-weight: 500; padding: 4px 14px; border-radius: 20px; margin-bottom: 1.2rem; letter-spacing: 0.08em; text-transform: uppercase; }
  .nfx-dot { width: 6px; height: 6px; background: #fff; border-radius: 50%; animation: pulse 1.6s ease infinite; }
  .hero h1 { font-size: 30px; font-weight: 500; margin-bottom: 0.6rem; color: #fff; }
  .hero p { font-size: 14px; color: #888; max-width: 500px; margin: 0 auto; line-height: 1.7; }

  /* Tabs */
  .tabs { display: flex; gap: 4px; padding: 1rem 1.5rem 0; border-bottom: 0.5px solid #2a2a2a; overflow-x: auto; }
  .tab { font-size: 13px; padding: 8px 16px; border-radius: 6px 6px 0 0; border: 0.5px solid transparent; cursor: pointer; white-space: nowrap; color: #888; background: transparent; transition: all 0.2s; }
  .tab:hover { color: #ccc; background: #161616; }
  .tab.active { color: #e50914; border-color: #2a2a2a; border-bottom-color: #0a0a0a; background: #0a0a0a; font-weight: 500; }

  /* Sections */
  .section { display: none; padding: 2rem 1.5rem; animation: fadeUp 0.4s ease; }
  .section.visible { display: block; }

  .sec-title { font-size: 18px; font-weight: 500; margin-bottom: 0.4rem; color: #fff; }
  .sec-sub { font-size: 13px; color: #666; margin-bottom: 1.5rem; line-height: 1.6; }

  /* Cards */
  .card-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(160px, 1fr)); gap: 12px; margin-bottom: 1.5rem; }
  .card { background: #111; border: 0.5px solid #2a2a2a; border-radius: 12px; padding: 1rem 1.25rem; }
  .card-label { font-size: 11px; color: #555; margin-bottom: 6px; text-transform: uppercase; letter-spacing: 0.06em; }
  .card-value { font-size: 22px; font-weight: 500; animation: countUp 0.5s ease; }
  .card-note { font-size: 12px; color: #555; margin-top: 4px; }

  .accent-red { color: #e50914; }
  .accent-teal { color: #1D9E75; }
  .accent-blue { color: #378ADD; }
  .accent-amber { color: #d4960f; }

  /* Bar chart */
  .bar-section { margin-bottom: 1.5rem; }
  .bar-row { display: flex; align-items: center; gap: 10px; margin-bottom: 10px; }
  .bar-label { font-size: 13px; color: #888; min-width: 120px; text-align: right; }
  .bar-track { flex: 1; height: 10px; background: #1a1a1a; border-radius: 5px; overflow: hidden; }
  .bar-fill { height: 100%; border-radius: 5px; width: 0; transition: width 1.2s cubic-bezier(.4,0,.2,1); }
  .bar-num { font-size: 12px; color: #555; min-width: 36px; }

  /* Donut */
  .donut-wrap { display: flex; align-items: center; gap: 2.5rem; margin-bottom: 1.5rem; flex-wrap: wrap; }
  .donut-legend { display: flex; flex-direction: column; gap: 10px; }
  .legend-item { display: flex; align-items: center; gap: 8px; font-size: 13px; color: #aaa; }
  .legend-dot { width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; }

  /* Timeline */
  .timeline { display: flex; flex-direction: column; gap: 0; }
  .tl-item { display: flex; gap: 1rem; }
  .tl-spine { display: flex; flex-direction: column; align-items: center; }
  .tl-dot { width: 12px; height: 12px; border-radius: 50%; border: 2px solid #e50914; background: #0a0a0a; flex-shrink: 0; margin-top: 3px; transition: background 0.2s; }
  .tl-item:hover .tl-dot { background: #e50914; }
  .tl-line { width: 1px; flex: 1; background: #2a2a2a; margin: 3px 0; }
  .tl-content { padding-bottom: 1.2rem; }
  .tl-year { font-size: 12px; color: #555; margin-bottom: 3px; }
  .tl-text { font-size: 14px; color: #aaa; line-height: 1.6; }

  /* Tags */
  .tag-cloud { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 1.5rem; }
  .tag { padding: 5px 14px; border-radius: 20px; font-size: 13px; border: 0.5px solid #2a2a2a; cursor: default; transition: all 0.2s; color: #aaa; }
  .tag:hover { border-color: #e50914; color: #e50914; }
  .tag.lg { font-size: 15px; padding: 7px 18px; }
  .tag.sm { font-size: 11px; padding: 4px 10px; }

  /* Two-col */
  .two-col { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 1.5rem; }

  /* List */
  .clean-list { list-style: none; display: flex; flex-direction: column; gap: 10px; }
  .clean-list li { font-size: 14px; line-height: 1.5; display: flex; align-items: flex-start; gap: 10px; color: #aaa; }
  .li-dot { width: 5px; height: 5px; border-radius: 50%; background: #e50914; flex-shrink: 0; margin-top: 7px; }

  /* Insight */
  .insight-box { border-left: 3px solid #e50914; padding: 0.75rem 1rem; background: #111; border-radius: 0 8px 8px 0; margin-bottom: 1rem; font-size: 14px; line-height: 1.6; color: #aaa; }

  /* Tool chips */
  .tool-chip { display: flex; align-items: center; gap: 8px; background: #111; border: 0.5px solid #2a2a2a; border-radius: 8px; padding: 10px 14px; font-size: 13px; color: #ccc; }
  .tool-icon { width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0; }

  .divider { border: none; border-top: 0.5px solid #2a2a2a; margin: 1.5rem 0; }

  .mono-box { background: #111; border: 0.5px solid #2a2a2a; border-radius: 10px; padding: 1rem 1.25rem; font-size: 13px; line-height: 1.8; font-family: 'Courier New', monospace; color: #888; }

  .footer { text-align: center; padding: 1.5rem; font-size: 12px; color: #444; border-top: 0.5px solid #2a2a2a; }
  .sub-head { font-size: 13px; font-weight: 500; color: #ccc; margin-bottom: 10px; }
</style>
</head>
<body>
<div class="wrap">

  <div class="hero">
    <div class="nfx-badge"><span class="nfx-dot"></span> EDA Project</div>
    <h1>Netflix Data Analysis</h1>
    <p>Exploratory analysis of Netflix's content library — uncovering trends, genre patterns, and strategic insights from streaming data.</p>
  </div>

  <div class="tabs" id="tabs">
    <div class="tab active" data-tab="overview">Overview</div>
    <div class="tab" data-tab="dataset">Dataset</div>
    <div class="tab" data-tab="eda">EDA</div>
    <div class="tab" data-tab="insights">Insights</div>
    <div class="tab" data-tab="tools">Tools</div>
    <div class="tab" data-tab="future">Future work</div>
  </div>

  <!-- OVERVIEW -->
  <div class="section visible" id="overview">
    <div class="sec-title">Project overview</div>
    <div class="sec-sub">Understanding how Netflix's content library has evolved — and what that means for content strategy and decision-making.</div>
    <div class="card-grid">
      <div class="card"><div class="card-label">Content type</div><div class="card-value accent-red">Movies</div><div class="card-note">Dominate the platform</div></div>
      <div class="card"><div class="card-label">Growth spike</div><div class="card-value accent-teal">2015+</div><div class="card-note">Rapid content expansion</div></div>
      <div class="card"><div class="card-label">Top genre</div><div class="card-value accent-blue">Drama</div><div class="card-note">Drama &amp; Comedy lead</div></div>
      <div class="card"><div class="card-label">Focus</div><div class="card-value accent-amber">Global</div><div class="card-note">Country-wise patterns</div></div>
    </div>
    <hr class="divider">
    <div class="sub-head">Problem statement</div>
    <ul class="clean-list">
      <li><span class="li-dot"></span>With rapid growth of streaming platforms, understanding content trends is essential.</li>
      <li><span class="li-dot"></span>Analyzes patterns in content type, genre, and release trends over time.</li>
      <li><span class="li-dot"></span>Generates insights to support content acquisition and regional strategy.</li>
    </ul>
    <hr class="divider">
    <div class="sub-head">Key questions</div>
    <ul class="clean-list">
      <li><span class="li-dot"></span>What type of content is more prevalent: Movies or TV Shows?</li>
      <li><span class="li-dot"></span>How has Netflix content grown over the years?</li>
      <li><span class="li-dot"></span>Which countries produce the most content?</li>
      <li><span class="li-dot"></span>What are the most popular genres on Netflix?</li>
    </ul>
  </div>

  <!-- DATASET -->
  <div class="section" id="dataset">
    <div class="sec-title">Dataset description</div>
    <div class="sec-sub">A structured dataset combining categorical and numerical variables, with some missing values requiring preprocessing.</div>
    <div class="two-col">
      <div>
        <div class="sub-head">Fields</div>
        <ul class="clean-list">
          <li><span class="li-dot"></span>Title</li>
          <li><span class="li-dot"></span>Type (Movie / TV Show)</li>
          <li><span class="li-dot"></span>Director &amp; Cast</li>
          <li><span class="li-dot"></span>Country</li>
          <li><span class="li-dot"></span>Release year</li>
          <li><span class="li-dot"></span>Rating &amp; Duration</li>
          <li><span class="li-dot"></span>Genre (Listed In)</li>
        </ul>
      </div>
      <div>
        <div class="sub-head">Preprocessing steps</div>
        <ul class="clean-list">
          <li><span class="li-dot"></span>Handle missing values in Director, Cast, Country</li>
          <li><span class="li-dot"></span>Convert and normalize data types</li>
          <li><span class="li-dot"></span>Clean categorical columns</li>
          <li><span class="li-dot"></span>Remove duplicates</li>
        </ul>
      </div>
    </div>
  </div>

  <!-- EDA -->
  <div class="section" id="eda">
    <div class="sec-title">Exploratory Data Analysis</div>
    <div class="sec-sub">Multi-level analysis from individual variable distributions to combined country, genre, and release year trends.</div>

    <div class="sub-head">Content type split</div>
    <div class="donut-wrap">
      <svg width="110" height="110" viewBox="0 0 110 110">
        <circle cx="55" cy="55" r="38" fill="none" stroke="#1a1a1a" stroke-width="18"/>
        <circle cx="55" cy="55" r="38" fill="none" stroke="#e50914" stroke-width="18"
          stroke-dasharray="168 71" stroke-dashoffset="-10"
          style="transform: rotate(-90deg); transform-origin: 55px 55px;"/>
        <circle cx="55" cy="55" r="38" fill="none" stroke="#378ADD" stroke-width="18"
          stroke-dasharray="71 168" stroke-dashoffset="-178"
          style="transform: rotate(-90deg); transform-origin: 55px 55px;"/>
        <text x="55" y="52" text-anchor="middle" font-size="13" font-weight="500" fill="#e5e5e5">70%</text>
        <text x="55" y="64" text-anchor="middle" font-size="10" fill="#666">movies</text>
      </svg>
      <div class="donut-legend">
        <div class="legend-item"><div class="legend-dot" style="background:#e50914;"></div><span>Movies — 70%</span></div>
        <div class="legend-item"><div class="legend-dot" style="background:#378ADD;"></div><span>TV Shows — 30%</span></div>
      </div>
    </div>

    <div class="sub-head">Top producing countries</div>
    <div class="bar-section" id="bars">
      <div class="bar-row"><span class="bar-label">United States</span><div class="bar-track"><div class="bar-fill" data-w="82%" style="background:#e50914;"></div></div><span class="bar-num">82%</span></div>
      <div class="bar-row"><span class="bar-label">India</span><div class="bar-track"><div class="bar-fill" data-w="48%" style="background:#378ADD;"></div></div><span class="bar-num">48%</span></div>
      <div class="bar-row"><span class="bar-label">United Kingdom</span><div class="bar-track"><div class="bar-fill" data-w="30%" style="background:#1D9E75;"></div></div><span class="bar-num">30%</span></div>
      <div class="bar-row"><span class="bar-label">Japan</span><div class="bar-track"><div class="bar-fill" data-w="22%" style="background:#d4960f;"></div></div><span class="bar-num">22%</span></div>
      <div class="bar-row"><span class="bar-label">South Korea</span><div class="bar-track"><div class="bar-fill" data-w="16%" style="background:#7F77DD;"></div></div><span class="bar-num">16%</span></div>
    </div>

    <div class="sub-head">Popular genres</div>
    <div class="tag-cloud">
      <span class="tag lg" style="border-color:#e50914; color:#e50914;">Drama</span>
      <span class="tag lg" style="border-color:#378ADD; color:#378ADD;">Comedy</span>
      <span class="tag">Documentaries</span>
      <span class="tag">Action &amp; Adventure</span>
      <span class="tag">Thrillers</span>
      <span class="tag sm">Children &amp; Family</span>
      <span class="tag sm">Romantic</span>
      <span class="tag sm">Horror</span>
      <span class="tag sm">Sci-Fi</span>
      <span class="tag sm">International</span>
    </div>
  </div>

  <!-- INSIGHTS -->
  <div class="section" id="insights">
    <div class="sec-title">Key insights</div>
    <div class="sec-sub">Findings from the analysis that can directly inform Netflix's content strategy.</div>

    <div class="insight-box">Movies dominate the platform, comprising approximately 70% of all titles compared to TV Shows.</div>
    <div class="insight-box">Rapid content growth was observed after 2015 — Netflix significantly accelerated its original production pipeline.</div>
    <div class="insight-box">A small number of countries — led by the US and India — contribute the vast majority of content on the platform.</div>
    <div class="insight-box">Drama and Comedy consistently rank as the most common genres, signaling strong viewer preference for these categories.</div>

    <hr class="divider">
    <div class="sub-head">Business impact</div>
    <ul class="clean-list">
      <li><span class="li-dot"></span>Helps understand viewer preferences and content demand patterns.</li>
      <li><span class="li-dot"></span>Supports content acquisition strategy with data-backed recommendations.</li>
      <li><span class="li-dot"></span>Enables better regional content planning for underrepresented markets.</li>
    </ul>

    <hr class="divider">
    <div class="sub-head">Content growth timeline</div>
    <div class="timeline">
      <div class="tl-item"><div class="tl-spine"><div class="tl-dot"></div><div class="tl-line"></div></div><div class="tl-content"><div class="tl-year">Pre-2015</div><div class="tl-text">Moderate library — mostly licensed content from major studios.</div></div></div>
      <div class="tl-item"><div class="tl-spine"><div class="tl-dot"></div><div class="tl-line"></div></div><div class="tl-content"><div class="tl-year">2015–2017</div><div class="tl-text">Originals push begins. International expansion drives content diversity.</div></div></div>
      <div class="tl-item"><div class="tl-spine"><div class="tl-dot"></div><div class="tl-line"></div></div><div class="tl-content"><div class="tl-year">2018–2020</div><div class="tl-text">Rapid acceleration. Regional content (India, Korea, Europe) enters the spotlight.</div></div></div>
      <div class="tl-item"><div class="tl-spine"><div class="tl-dot"></div></div><div class="tl-content"><div class="tl-year">2021+</div><div class="tl-text">Catalog matures. Focus shifts toward quality and genre diversity.</div></div></div>
    </div>
  </div>

  <!-- TOOLS -->
  <div class="section" id="tools">
    <div class="sec-title">Tools and technologies</div>
    <div class="sec-sub">Built entirely in Python using industry-standard data science libraries within Jupyter Notebook.</div>
    <div class="card-grid">
      <div class="tool-chip"><div class="tool-icon" style="background:#378ADD;"></div>Python</div>
      <div class="tool-chip"><div class="tool-icon" style="background:#e50914;"></div>Jupyter Notebook</div>
      <div class="tool-chip"><div class="tool-icon" style="background:#1D9E75;"></div>Pandas</div>
      <div class="tool-chip"><div class="tool-icon" style="background:#d4960f;"></div>NumPy</div>
      <div class="tool-chip"><div class="tool-icon" style="background:#7F77DD;"></div>Matplotlib</div>
      <div class="tool-chip"><div class="tool-icon" style="background:#D4537E;"></div>Seaborn</div>
    </div>
    <hr class="divider">
    <div class="sub-head">Project structure</div>
    <div class="mono-box">
      <div style="color:#555;">📁 Netflix EDA</div>
      <div style="padding-left:16px;">📓 03 Netflix.ipynb</div>
      <div style="padding-left:32px; color:#444;">├─ Data cleaning</div>
      <div style="padding-left:32px; color:#444;">├─ EDA</div>
      <div style="padding-left:32px; color:#444;">├─ Visualizations</div>
      <div style="padding-left:32px; color:#444;">└─ Insights</div>
    </div>
  </div>

  <!-- FUTURE WORK -->
  <div class="section" id="future">
    <div class="sec-title">Future work</div>
    <div class="sec-sub">Extending this analysis into machine learning and interactive applications.</div>
    <div class="card-grid">
      <div class="card"><div class="card-label">Phase 1</div><div class="card-value" style="font-size:16px; margin-top:6px; color:#fff;">Recommendation system</div><div class="card-note">Personalized content suggestions using collaborative filtering</div></div>
      <div class="card"><div class="card-label">Phase 2</div><div class="card-value" style="font-size:16px; margin-top:6px; color:#fff;">ML models</div><div class="card-note">Predict content success and genre popularity trends</div></div>
      <div class="card"><div class="card-label">Phase 3</div><div class="card-value" style="font-size:16px; margin-top:6px; color:#fff;">Interactive dashboards</div><div class="card-note">Live filters for exploring Netflix data visually</div></div>
    </div>
    <hr class="divider">
    <div class="insight-box">The analysis highlights key trends in Netflix content distribution. Insights can directly improve content strategy and drive stronger user engagement.</div>
  </div>

</div>

<div class="footer">Guided by Yash Jain — Future Vision Computer</div>

<script>
  const tabs = document.querySelectorAll('.tab');
  const sections = document.querySelectorAll('.section');

  function animateBars() {
    document.querySelectorAll('.bar-fill').forEach(bar => {
      bar.style.width = bar.dataset.w || '0%';
    });
  }

  tabs.forEach(tab => {
    tab.addEventListener('click', () => {
      tabs.forEach(t => t.classList.remove('active'));
      sections.forEach(s => s.classList.remove('visible'));
      tab.classList.add('active');
      const target = document.getElementById(tab.dataset.tab);
      if (target) {
        target.classList.add('visible');
        target.style.animation = 'none';
        void target.offsetWidth;
        target.style.animation = 'fadeUp 0.4s ease';
        if (tab.dataset.tab === 'eda') {
          setTimeout(animateBars, 100);
        }
      }
    });
  });
</script>
</body>
</html>
