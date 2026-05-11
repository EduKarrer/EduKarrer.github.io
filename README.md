# EduKarrer.github.io
teste de site para maratona de programação Unisinos



<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Maratona de Programação · UNISINOS 2026</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;700;800&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #0a0a0f;
    --surface: #111118;
    --border: #1e1e2e;
    --accent: #00e5a0;
    --accent2: #7c3aed;
    --accent3: #f59e0b;
    --text: #e8e8f0;
    --muted: #6b6b7e;
    --mono: 'Space Mono', monospace;
    --sans: 'Syne', sans-serif;
  }

  html, body {
    min-height: 100vh;
    background: var(--bg);
    color: var(--text);
    font-family: var(--sans);
    overflow-x: hidden;
  }

  body {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    padding: 2rem 1rem;
    position: relative;
  }

  /* Grid background */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(0,229,160,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,229,160,0.04) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none;
    z-index: 0;
  }

  /* Glow orbs */
  .orb {
    position: fixed;
    border-radius: 50%;
    filter: blur(120px);
    pointer-events: none;
    z-index: 0;
  }
  .orb-1 {
    width: 500px; height: 500px;
    background: rgba(124, 58, 237, 0.18);
    top: -150px; left: -150px;
  }
  .orb-2 {
    width: 400px; height: 400px;
    background: rgba(0, 229, 160, 0.12);
    bottom: -100px; right: -100px;
  }
  .orb-3 {
    width: 300px; height: 300px;
    background: rgba(245, 158, 11, 0.08);
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
  }

  .container {
    position: relative;
    z-index: 1;
    width: 100%;
    max-width: 900px;
    text-align: center;
  }

  /* Badge */
  .badge {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: rgba(0,229,160,0.08);
    border: 1px solid rgba(0,229,160,0.25);
    border-radius: 100px;
    padding: 6px 18px;
    font-family: var(--mono);
    font-size: 11px;
    color: var(--accent);
    letter-spacing: 0.12em;
    text-transform: uppercase;
    margin-bottom: 2rem;
  }
  .badge-dot {
    width: 6px; height: 6px;
    border-radius: 50%;
    background: var(--accent);
    animation: pulse 2s infinite;
  }
  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.4; transform: scale(0.8); }
  }

  /* Event name */
  .event-label {
    font-family: var(--mono);
    font-size: 12px;
    color: var(--muted);
    letter-spacing: 0.2em;
    text-transform: uppercase;
    margin-bottom: 0.75rem;
  }

  h1 {
    font-family: var(--sans);
    font-size: clamp(2.8rem, 8vw, 5.5rem);
    font-weight: 800;
    line-height: 1;
    margin-bottom: 0.4rem;
    letter-spacing: -0.02em;
    background: linear-gradient(135deg, #fff 0%, #a78bfa 50%, #00e5a0 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .subtitle {
    font-size: clamp(1.2rem, 3vw, 1.8rem);
    font-weight: 700;
    color: var(--accent);
    margin-bottom: 0.5rem;
    letter-spacing: -0.01em;
  }

  .date-info {
    font-family: var(--mono);
    font-size: 13px;
    color: var(--muted);
    margin-bottom: 3.5rem;
    letter-spacing: 0.08em;
  }
  .date-info span {
    color: var(--accent3);
  }

  /* Countdown */
  .countdown {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 16px;
    margin-bottom: 3.5rem;
    max-width: 700px;
    margin-left: auto;
    margin-right: auto;
  }

  .unit {
    position: relative;
  }

  .unit-box {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 1.5rem 0.5rem 1.2rem;
    position: relative;
    overflow: hidden;
    transition: border-color 0.3s;
  }
  .unit-box::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, var(--accent), transparent);
    opacity: 0;
    transition: opacity 0.3s;
  }
  .unit-box.tick::before { opacity: 1; }

  .unit-number {
    font-family: var(--mono);
    font-size: clamp(2.5rem, 8vw, 4.5rem);
    font-weight: 700;
    color: #fff;
    line-height: 1;
    display: block;
    letter-spacing: -0.02em;
    transition: transform 0.15s ease, color 0.15s ease;
  }
  .unit-box.tick .unit-number {
    color: var(--accent);
  }

  .unit-label {
    font-family: var(--mono);
    font-size: 10px;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 0.15em;
    margin-top: 0.5rem;
    display: block;
  }

  /* Separator dots */
  .sep {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 6px;
    padding-bottom: 1.8rem;
    position: absolute;
    right: -12px;
    top: 50%;
    transform: translateY(-60%);
    z-index: 2;
  }
  .sep span {
    display: block;
    width: 4px; height: 4px;
    border-radius: 50%;
    background: var(--muted);
  }

  /* Event details */
  .details {
    display: flex;
    justify-content: center;
    gap: 2rem;
    flex-wrap: wrap;
    margin-bottom: 3rem;
  }

  .detail-item {
    display: flex;
    align-items: center;
    gap: 10px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 100px;
    padding: 10px 20px;
    font-size: 13px;
    color: var(--muted);
  }
  .detail-item svg {
    flex-shrink: 0;
    color: var(--accent);
  }
  .detail-item strong {
    color: var(--text);
    font-weight: 700;
  }

  /* Finished state */
  .finished-msg {
    display: none;
    font-family: var(--mono);
    font-size: clamp(1.5rem, 5vw, 3rem);
    color: var(--accent);
    font-weight: 700;
    letter-spacing: 0.05em;
    margin: 2rem 0;
    animation: glitch 0.5s infinite alternate;
  }
  @keyframes glitch {
    0% { text-shadow: 2px 0 var(--accent2), -2px 0 var(--accent3); }
    100% { text-shadow: -2px 0 var(--accent2), 2px 0 var(--accent3); }
  }

  /* Progress bar */
  .progress-section {
    max-width: 700px;
    margin: 0 auto 3rem;
  }
  .progress-meta {
    display: flex;
    justify-content: space-between;
    font-family: var(--mono);
    font-size: 11px;
    color: var(--muted);
    margin-bottom: 8px;
    letter-spacing: 0.08em;
  }
  .progress-track {
    height: 4px;
    background: var(--border);
    border-radius: 100px;
    overflow: hidden;
  }
  .progress-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--accent2), var(--accent));
    border-radius: 100px;
    transition: width 1s linear;
  }

  /* Footer */
  footer {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.1em;
    opacity: 0.6;
    position: relative;
    z-index: 1;
  }

  @media (max-width: 480px) {
    .countdown { gap: 8px; }
    .unit-box { padding: 1rem 0.25rem 0.8rem; border-radius: 12px; }
    .details { gap: 0.75rem; }
    .detail-item { padding: 8px 14px; font-size: 12px; }
    .sep { right: -8px; }
    .sep span { width: 3px; height: 3px; }
  }
</style>
</head>
<body>

<div class="orb orb-1"></div>
<div class="orb orb-2"></div>
<div class="orb orb-3"></div>

<div class="container">

  <div class="badge">
    <span class="badge-dot"></span>
    Contagem regressiva oficial
  </div>

  <p class="event-label">UNISINOS · São Leopoldo / RS</p>
  <h1>Maratona de<br>Programação</h1>
  <p class="subtitle">2026</p>
  <p class="date-info">30 de maio de 2026 &nbsp;·&nbsp; <span>08:00h</span></p>

  <div id="finished-msg" class="finished-msg">// EVENTO EM ANDAMENTO 🚀</div>

  <div class="countdown" id="countdown">
    <div class="unit" id="wrap-dias">
      <div class="unit-box" id="box-dias">
        <span class="unit-number" id="dias">--</span>
        <span class="unit-label">dias</span>
      </div>
      <div class="sep"><span></span><span></span></div>
    </div>
    <div class="unit" id="wrap-horas">
      <div class="unit-box" id="box-horas">
        <span class="unit-number" id="horas">--</span>
        <span class="unit-label">horas</span>
      </div>
      <div class="sep"><span></span><span></span></div>
    </div>
    <div class="unit" id="wrap-min">
      <div class="unit-box" id="box-min">
        <span class="unit-number" id="min">--</span>
        <span class="unit-label">minutos</span>
      </div>
      <div class="sep"><span></span><span></span></div>
    </div>
    <div class="unit">
      <div class="unit-box" id="box-seg">
        <span class="unit-number" id="seg">--</span>
        <span class="unit-label">segundos</span>
      </div>
    </div>
  </div>

  <div class="progress-section">
    <div class="progress-meta">
      <span id="prog-start">início da contagem</span>
      <span id="prog-pct">0%</span>
    </div>
    <div class="progress-track">
      <div class="progress-fill" id="progress-fill" style="width:0%"></div>
    </div>
  </div>

  <div class="details">
    <div class="detail-item">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <rect x="3" y="4" width="18" height="18" rx="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/>
      </svg>
      <span>30/05/2026</span>
      &nbsp;·&nbsp; <strong>Sexta-feira</strong>
    </div>
    <div class="detail-item">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/>
      </svg>
      <span>Início:</span>
      <strong>08:00h</strong>
    </div>
    <div class="detail-item">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"/><circle cx="12" cy="10" r="3"/>
      </svg>
      <strong>UNISINOS</strong>
    </div>
  </div>

</div>

<footer>MARATONA DE PROGRAMAÇÃO UNISINOS © 2026</footer>

<script>
  const target = new Date('2026-05-30T08:00:00');

  const pad = n => String(n).padStart(2, '0');

  const $d = document.getElementById('dias');
  const $h = document.getElementById('horas');
  const $m = document.getElementById('min');
  const $s = document.getElementById('seg');
  const $fill = document.getElementById('progress-fill');
  const $pct = document.getElementById('prog-pct');
  const $finished = document.getElementById('finished-msg');
  const $countdown = document.getElementById('countdown');

  const startRef = new Date();
  const totalDuration = target - startRef;

  let prevSec = -1;
  let prevMin = -1;
  let prevHour = -1;
  let prevDay = -1;

  function flash(id) {
    const box = document.getElementById('box-' + id);
    box.classList.add('tick');
    setTimeout(() => box.classList.remove('tick'), 400);
  }

  function tick() {
    const now = new Date();
    const diff = target - now;

    if (diff <= 0) {
      $countdown.style.opacity = '0.3';
      $finished.style.display = 'block';
      $d.textContent = '00';
      $h.textContent = '00';
      $m.textContent = '00';
      $s.textContent = '00';
      $fill.style.width = '100%';
      $pct.textContent = '100%';
      return;
    }

    const totalSec = Math.floor(diff / 1000);
    const d = Math.floor(totalSec / 86400);
    const h = Math.floor((totalSec % 86400) / 3600);
    const mn = Math.floor((totalSec % 3600) / 60);
    const sc = totalSec % 60;

    if (sc !== prevSec) { $s.textContent = pad(sc); flash('seg'); prevSec = sc; }
    if (mn !== prevMin) { $m.textContent = pad(mn); flash('min'); prevMin = mn; }
    if (h !== prevHour) { $h.textContent = pad(h); flash('horas'); prevHour = h; }
    if (d !== prevDay) { $d.textContent = pad(d); flash('dias'); prevDay = d; }

    const elapsed = totalDuration - diff;
    const pct = Math.min(100, Math.max(0, (elapsed / totalDuration) * 100));
    $fill.style.width = pct.toFixed(2) + '%';
    $pct.textContent = pct.toFixed(1) + '%';
  }

  tick();
  setInterval(tick, 1000);
</script>
</body>
</html>
