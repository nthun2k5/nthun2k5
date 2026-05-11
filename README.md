<style>
@import url('https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;500;600&family=Space+Grotesk:wght@300;400;500;600;700&display=swap');

* { box-sizing: border-box; margin: 0; padding: 0; }

.gh-wrap {
  font-family: 'Space Grotesk', sans-serif;
  background: #0d1117;
  color: #e6edf3;
  padding: 2rem;
  border-radius: 12px;
  min-height: 600px;
  position: relative;
  overflow: hidden;
}

.grid-bg {
  position: absolute; inset: 0;
  background-image: linear-gradient(rgba(88,166,255,0.04) 1px, transparent 1px),
    linear-gradient(90deg, rgba(88,166,255,0.04) 1px, transparent 1px);
  background-size: 32px 32px;
  pointer-events: none;
}

.glow-blob {
  position: absolute; width: 400px; height: 400px; border-radius: 50%;
  background: radial-gradient(circle, rgba(88,166,255,0.08) 0%, transparent 70%);
  top: -100px; right: -80px; pointer-events: none;
}

.header-row {
  display: flex; align-items: flex-start; gap: 1.5rem; margin-bottom: 1.5rem;
  position: relative; z-index: 1;
}

.avatar-wrap {
  position: relative; flex-shrink: 0;
}

.avatar {
  width: 80px; height: 80px; border-radius: 50%;
  background: linear-gradient(135deg, #58a6ff 0%, #bc8cff 50%, #ff7b72 100%);
  display: flex; align-items: center; justify-content: center;
  font-size: 2rem; font-weight: 700; color: #fff;
  font-family: 'Fira Code', monospace;
  box-shadow: 0 0 0 3px #21262d, 0 0 0 5px #58a6ff44;
}

.status-dot {
  position: absolute; bottom: 4px; right: 4px;
  width: 14px; height: 14px; border-radius: 50%;
  background: #3fb950; border: 2px solid #0d1117;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% { box-shadow: 0 0 0 0 rgba(63,185,80,0.4); }
  50% { box-shadow: 0 0 0 6px rgba(63,185,80,0); }
}

.name-block h1 {
  font-size: 1.6rem; font-weight: 700; color: #e6edf3;
  letter-spacing: -0.5px; line-height: 1.2; margin-bottom: 4px;
}

.username {
  font-family: 'Fira Code', monospace;
  color: #58a6ff; font-size: 0.95rem; margin-bottom: 8px;
}

.bio {
  font-size: 0.88rem; color: #8b949e; line-height: 1.6; max-width: 420px;
}

.badges {
  display: flex; flex-wrap: wrap; gap: 6px; margin-top: 10px;
}

.badge {
  font-family: 'Fira Code', monospace;
  font-size: 11px; padding: 3px 10px; border-radius: 20px;
  font-weight: 500; letter-spacing: 0.3px;
}

.badge-blue { background: #1f3a6e; color: #58a6ff; border: 1px solid #1f6feb55; }
.badge-purple { background: #2d1f6e; color: #bc8cff; border: 1px solid #8957e555; }
.badge-green { background: #1a3b24; color: #3fb950; border: 1px solid #2ea04355; }
.badge-orange { background: #3b2a1a; color: #f0883e; border: 1px solid #d2943355; }

.divider {
  height: 1px; background: linear-gradient(90deg, transparent, #30363d 30%, #30363d 70%, transparent);
  margin: 1.25rem 0; position: relative; z-index: 1;
}

.section-title {
  font-family: 'Fira Code', monospace;
  font-size: 11px; color: #58a6ff;
  text-transform: uppercase; letter-spacing: 1.5px;
  margin-bottom: 0.75rem; display: flex; align-items: center; gap: 8px;
}

.section-title::after {
  content: ''; flex: 1; height: 1px; background: #21262d;
}

.stats-grid {
  display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px;
  margin-bottom: 1.25rem; position: relative; z-index: 1;
}

.stat-card {
  background: #161b22; border: 1px solid #21262d;
  border-radius: 8px; padding: 12px 14px; text-align: center;
  transition: border-color 0.2s, transform 0.2s;
  cursor: default;
}

.stat-card:hover {
  border-color: #58a6ff44; transform: translateY(-2px);
}

.stat-num {
  font-family: 'Fira Code', monospace;
  font-size: 1.4rem; font-weight: 600;
  background: linear-gradient(135deg, #58a6ff, #bc8cff);
  -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  background-clip: text; display: block; line-height: 1;
}

.stat-lbl {
  font-size: 11px; color: #8b949e; margin-top: 4px; letter-spacing: 0.3px;
}

.skills-section { position: relative; z-index: 1; margin-bottom: 1.25rem; }

.skill-row {
  display: flex; flex-wrap: wrap; gap: 6px;
}

.skill-tag {
  display: flex; align-items: center; gap: 5px;
  background: #161b22; border: 1px solid #21262d;
  border-radius: 6px; padding: 5px 10px; font-size: 12px;
  color: #c9d1d9; font-family: 'Fira Code', monospace;
  transition: border-color 0.2s; cursor: default;
}

.skill-tag:hover { border-color: #58a6ff44; color: #e6edf3; }

.dot { width: 7px; height: 7px; border-radius: 50%; flex-shrink: 0; }
.dot-blue { background: #58a6ff; }
.dot-yellow { background: #e3b341; }
.dot-green { background: #3fb950; }
.dot-red { background: #ff7b72; }
.dot-purple { background: #bc8cff; }
.dot-cyan { background: #39d3f6; }
.dot-orange { background: #f0883e; }

.contrib-section { position: relative; z-index: 1; margin-bottom: 1.25rem; }

.contrib-graph {
  background: #161b22; border: 1px solid #21262d;
  border-radius: 8px; padding: 14px; overflow: hidden;
}

.contrib-grid {
  display: flex; gap: 3px; align-items: flex-end;
}

.contrib-col {
  display: flex; flex-direction: column; gap: 3px;
}

.contrib-cell {
  width: 11px; height: 11px; border-radius: 2px;
  background: #161b22; border: 1px solid #21262d22;
}

.c0 { background: #161b22; }
.c1 { background: #0e4429; }
.c2 { background: #006d32; }
.c3 { background: #26a641; }
.c4 { background: #39d353; }

.contrib-footer {
  display: flex; justify-content: space-between; align-items: center;
  margin-top: 8px; font-size: 11px; color: #8b949e;
  font-family: 'Fira Code', monospace;
}

.contrib-legend { display: flex; align-items: center; gap: 4px; }

.pinned-section { position: relative; z-index: 1; }

.pinned-grid {
  display: grid; grid-template-columns: 1fr 1fr; gap: 10px;
}

.repo-card {
  background: #161b22; border: 1px solid #21262d;
  border-radius: 8px; padding: 12px 14px;
  transition: border-color 0.2s; cursor: pointer;
}

.repo-card:hover { border-color: #58a6ff44; }

.repo-name {
  font-family: 'Fira Code', monospace;
  color: #58a6ff; font-size: 13px; font-weight: 600;
  margin-bottom: 4px; display: flex; align-items: center; gap: 5px;
}

.repo-desc {
  font-size: 11px; color: #8b949e; line-height: 1.5; margin-bottom: 10px;
}

.repo-meta {
  display: flex; align-items: center; gap: 12px;
  font-size: 11px; color: #8b949e; font-family: 'Fira Code', monospace;
}

.repo-lang { display: flex; align-items: center; gap: 4px; }

.streak-bar {
  display: flex; align-items: center; gap: 8px;
  background: #161b22; border: 1px solid #21262d;
  border-radius: 8px; padding: 12px 14px; margin-bottom: 1.25rem;
  position: relative; z-index: 1;
}

.streak-item { flex: 1; text-align: center; }

.streak-val {
  font-family: 'Fira Code', monospace;
  font-size: 1.5rem; font-weight: 700;
  color: #e3b341; display: block;
}

.streak-lbl {
  font-size: 10px; color: #8b949e; letter-spacing: 0.3px; margin-top: 2px;
}

.streak-sep { width: 1px; height: 40px; background: #21262d; }

.typing-cursor {
  display: inline-block; width: 2px; height: 1.1em;
  background: #58a6ff; margin-left: 2px; vertical-align: middle;
  animation: blink 1s steps(1) infinite;
}

@keyframes blink { 50% { opacity: 0; } }

.snake-wrap {
  text-align: center; margin-bottom: 1.25rem;
  position: relative; z-index: 1;
  background: #161b22; border: 1px solid #21262d;
  border-radius: 8px; padding: 10px;
}

.wave { display: inline-block; animation: wave 2.5s infinite; transform-origin: 70% 70%; }
@keyframes wave {
  0%,60%,100%{transform:rotate(0deg)}
  10%,30%{transform:rotate(14deg)}
  20%{transform:rotate(-8deg)}
  40%{transform:rotate(-4deg)}
  50%{transform:rotate(10deg)}
}

.social-row {
  display: flex; gap: 8px; flex-wrap: wrap;
  position: relative; z-index: 1;
}

.social-btn {
  display: flex; align-items: center; gap: 6px;
  background: #21262d; border: 1px solid #30363d;
  border-radius: 6px; padding: 6px 12px;
  font-size: 12px; font-family: 'Fira Code', monospace;
  color: #8b949e; text-decoration: none;
  transition: border-color 0.2s, color 0.2s;
}

.social-btn:hover { border-color: #58a6ff; color: #58a6ff; }
</style>

<div class="gh-wrap">
  <div class="grid-bg"></div>
  <div class="glow-blob"></div>

  <div class="header-row">
    <div class="avatar-wrap">
      <div class="avatar">YN</div>
      <div class="status-dot"></div>
    </div>
    <div class="name-block">
      <h1>Your Name <span class="wave">👋</span></h1>
      <div class="username">@yourusername</div>
      <div class="bio">Full-stack developer & open-source enthusiast. Building cool stuff with code.<br>Currently learning <span style="color:#58a6ff;font-family:'Fira Code',monospace">Rust</span> & <span style="color:#bc8cff;font-family:'Fira Code',monospace">WebAssembly</span>.</div>
      <div class="badges">
        <span class="badge badge-blue">💻 Full Stack</span>
        <span class="badge badge-purple">🚀 Open Source</span>
        <span class="badge badge-green">🌱 Always Learning</span>
        <span class="badge badge-orange">☕ Coffee Driven</span>
      </div>
    </div>
  </div>

  <div class="divider"></div>

  <div class="section-title">GitHub Stats</div>
  <div class="stats-grid">
    <div class="stat-card">
      <span class="stat-num">1.2k</span>
      <div class="stat-lbl">⭐ Stars Earned</div>
    </div>
    <div class="stat-card">
      <span class="stat-num">847</span>
      <div class="stat-lbl">📦 Commits (2024)</div>
    </div>
    <div class="stat-card">
      <span class="stat-num">142</span>
      <div class="stat-lbl">🔀 Pull Requests</div>
    </div>
  </div>

  <div class="streak-bar">
    <div class="streak-item">
      <span class="streak-val">312</span>
      <div class="streak-lbl">Total Contributions</div>
    </div>
    <div class="streak-sep"></div>
    <div class="streak-item">
      <span class="streak-val">🔥 24</span>
      <div class="streak-lbl">Current Streak</div>
    </div>
    <div class="streak-sep"></div>
    <div class="streak-item">
      <span class="streak-val">67</span>
      <div class="streak-lbl">Longest Streak</div>
    </div>
  </div>

  <div class="divider"></div>

  <div class="skills-section">
    <div class="section-title">Tech Stack</div>
    <div class="skill-row">
      <div class="skill-tag"><span class="dot dot-yellow"></span>JavaScript</div>
      <div class="skill-tag"><span class="dot dot-blue"></span>TypeScript</div>
      <div class="skill-tag"><span class="dot dot-cyan"></span>React</div>
      <div class="skill-tag"><span class="dot dot-green"></span>Node.js</div>
      <div class="skill-tag"><span class="dot dot-blue"></span>Python</div>
      <div class="skill-tag"><span class="dot dot-orange"></span>Rust</div>
      <div class="skill-tag"><span class="dot dot-blue"></span>Docker</div>
      <div class="skill-tag"><span class="dot dot-orange"></span>PostgreSQL</div>
      <div class="skill-tag"><span class="dot dot-purple"></span>GraphQL</div>
      <div class="skill-tag"><span class="dot dot-red"></span>Redis</div>
      <div class="skill-tag"><span class="dot dot-cyan"></span>Next.js</div>
      <div class="skill-tag"><span class="dot dot-green"></span>MongoDB</div>
    </div>
  </div>

  <div class="divider"></div>

  <div class="contrib-section">
    <div class="section-title">Contribution Graph</div>
    <div class="contrib-graph">
      <div class="contrib-grid" id="cgrid"></div>
      <div class="contrib-footer">
        <span>Less</span>
        <div class="contrib-legend">
          <div class="contrib-cell c0"></div>
          <div class="contrib-cell c1"></div>
          <div class="contrib-cell c2"></div>
          <div class="contrib-cell c3"></div>
          <div class="contrib-cell c4"></div>
        </div>
        <span>More</span>
      </div>
    </div>
  </div>

  <div class="divider"></div>

  <div class="pinned-section">
    <div class="section-title">Pinned Repositories</div>
    <div class="pinned-grid">
      <div class="repo-card">
        <div class="repo-name">📁 awesome-cli-tool</div>
        <div class="repo-desc">A blazing-fast command-line tool for developers who live in the terminal.</div>
        <div class="repo-meta">
          <div class="repo-lang"><span class="dot dot-orange" style="width:9px;height:9px"></span>Rust</div>
          <span>⭐ 312</span>
          <span>🍴 48</span>
        </div>
      </div>
      <div class="repo-card">
        <div class="repo-name">📁 react-hooks-lib</div>
        <div class="repo-desc">Collection of custom React hooks for production-ready apps.</div>
        <div class="repo-meta">
          <div class="repo-lang"><span class="dot dot-yellow" style="width:9px;height:9px"></span>TypeScript</div>
          <span>⭐ 521</span>
          <span>🍴 87</span>
        </div>
      </div>
      <div class="repo-card">
        <div class="repo-name">📁 my-portfolio</div>
        <div class="repo-desc">Personal website built with Next.js, Tailwind, and too much caffeine.</div>
        <div class="repo-meta">
          <div class="repo-lang"><span class="dot dot-cyan" style="width:9px;height:9px"></span>Next.js</div>
          <span>⭐ 89</span>
          <span>🍴 23</span>
        </div>
      </div>
      <div class="repo-card">
        <div class="repo-name">📁 api-boilerplate</div>
        <div class="repo-desc">Production-ready Node.js REST API with auth, testing, and CI/CD.</div>
        <div class="repo-meta">
          <div class="repo-lang"><span class="dot dot-green" style="width:9px;height:9px"></span>Node.js</div>
          <span>⭐ 278</span>
          <span>🍴 65</span>
        </div>
      </div>
    </div>
  </div>

  <div class="divider"></div>

  <div class="social-row">
    <a class="social-btn" href="#">🌐 Portfolio</a>
    <a class="social-btn" href="#">🐦 Twitter</a>
    <a class="social-btn" href="#">💼 LinkedIn</a>
    <a class="social-btn" href="#">📧 Email</a>
    <a class="social-btn" href="#">📝 Blog</a>
  </div>

  <div style="text-align:center; margin-top: 1.25rem; font-family: 'Fira Code', monospace; font-size:11px; color:#8b949e; position:relative; z-index:1;">
    <span style="color:#58a6ff">console</span>.<span style="color:#d2a8ff">log</span>(<span style="color:#a5d6ff">"Thanks for visiting!"</span>)<span class="typing-cursor"></span>
  </div>
</div>

<script>
const grid = document.getElementById('cgrid');
const levels = [0,0,0,1,0,0,1,2,1,0,0,1,1,2,3,2,1,1,0,1,2,2,3,4,3,2,1,2,3,3,4,4,3,2,3,3,4,4,3,3,2,3,3,4,3,2,1,1,2,3,4,4,3,2,3,3];
for(let w=0;w<53;w++){
  const col = document.createElement('div');
  col.className='contrib-col';
  for(let d=0;d<7;d++){
    const cell = document.createElement('div');
    cell.className='contrib-cell c'+Math.min(levels[(w*7+d)%levels.length], 4);
    col.appendChild(cell);
  }
  grid.appendChild(col);
}
</script>
