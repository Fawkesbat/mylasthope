<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>My Last Hope — Em Desenvolvimento</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;600;900&family=Inter:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --black:   #0D0F0B;
    --deep:    #131510;
    --moss:    #2D4A2D;
    --moss2:   #3D6B3D;
    --amber:   #C8891A;
    --amber2:  #E8A830;
    --paper:   #E8E4D9;
    --muted:   #9A9688;
    --border:  rgba(232,228,217,0.1);
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--black);
    color: var(--paper);
    font-family: 'Inter', sans-serif;
    font-weight: 300;
    line-height: 1.7;
    overflow-x: hidden;
  }

  /* NAV */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px 48px;
    background: linear-gradient(to bottom, rgba(13,15,11,0.95), transparent);
    backdrop-filter: blur(2px);
  }
  .nav-logo {
    font-family: 'Cinzel', serif;
    font-weight: 900;
    font-size: 15px;
    letter-spacing: 0.2em;
    color: var(--amber);
    text-transform: uppercase;
    text-decoration: none;
  }
  .nav-links { display: flex; gap: 36px; list-style: none; }
  .nav-links a {
    font-size: 12px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--muted);
    text-decoration: none;
    transition: color 0.3s;
  }
  .nav-links a:hover { color: var(--paper); }

  /* HERO */
  #hero {
    position: relative;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: 120px 24px 80px;
    overflow: hidden;
  }

  #hero-canvas {
    position: absolute;
    inset: 0;
    pointer-events: none;
  }

  .hero-eyebrow {
    font-size: 11px;
    letter-spacing: 0.35em;
    text-transform: uppercase;
    color: var(--amber);
    margin-bottom: 28px;
    opacity: 0;
    animation: fadeUp 1s ease 0.3s forwards;
  }

  .hero-title {
    font-family: 'Cinzel', serif;
    font-weight: 900;
    font-size: clamp(52px, 10vw, 120px);
    line-height: 0.92;
    letter-spacing: -0.01em;
    color: var(--paper);
    opacity: 0;
    animation: fadeUp 1s ease 0.6s forwards;
  }

  .hero-title span {
    display: block;
    color: var(--moss2);
    font-weight: 400;
    font-size: 0.45em;
    letter-spacing: 0.08em;
    margin-top: 16px;
  }

  .hero-desc {
    max-width: 540px;
    margin: 40px auto 0;
    font-size: 16px;
    color: var(--muted);
    line-height: 1.8;
    opacity: 0;
    animation: fadeUp 1s ease 0.9s forwards;
  }

  .hero-ctas {
    display: flex;
    gap: 16px;
    margin-top: 48px;
    flex-wrap: wrap;
    justify-content: center;
    opacity: 0;
    animation: fadeUp 1s ease 1.1s forwards;
  }

  .btn-primary {
    background: var(--amber);
    color: var(--black);
    padding: 14px 36px;
    font-family: 'Cinzel', serif;
    font-size: 12px;
    font-weight: 600;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    text-decoration: none;
    border: none;
    cursor: pointer;
    transition: background 0.3s, transform 0.2s;
  }
  .btn-primary:hover { background: var(--amber2); transform: translateY(-2px); }

  .btn-outline {
    background: transparent;
    color: var(--paper);
    padding: 14px 36px;
    font-family: 'Cinzel', serif;
    font-size: 12px;
    font-weight: 600;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    text-decoration: none;
    border: 1px solid var(--border);
    cursor: pointer;
    transition: border-color 0.3s, transform 0.2s;
  }
  .btn-outline:hover { border-color: var(--paper); transform: translateY(-2px); }

  .scroll-hint {
    position: absolute;
    bottom: 36px;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
    color: var(--muted);
    font-size: 10px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    opacity: 0;
    animation: fadeUp 1s ease 1.6s forwards;
  }
  .scroll-line {
    width: 1px;
    height: 40px;
    background: linear-gradient(to bottom, var(--muted), transparent);
    animation: scrollPulse 2s ease-in-out infinite;
  }

  /* SOBRE */
  #sobre {
    padding: 120px 48px;
    max-width: 1100px;
    margin: 0 auto;
  }

  .section-label {
    font-size: 10px;
    letter-spacing: 0.4em;
    text-transform: uppercase;
    color: var(--amber);
    margin-bottom: 24px;
  }

  .sobre-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 80px;
    align-items: center;
  }

  .sobre-title {
    font-family: 'Cinzel', serif;
    font-size: clamp(28px, 4vw, 48px);
    font-weight: 600;
    line-height: 1.2;
    margin-bottom: 28px;
  }

  .sobre-title em {
    font-style: italic;
    color: var(--moss2);
  }

  .sobre-text { color: var(--muted); font-size: 15px; line-height: 1.9; }
  .sobre-text + .sobre-text { margin-top: 20px; }

  .sobre-visual {
    position: relative;
    aspect-ratio: 4/5;
    background: var(--deep);
    border: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }

  .sobre-visual-inner {
    text-align: center;
    padding: 40px;
  }

  .falco-ascii {
    font-family: monospace;
    font-size: 13px;
    line-height: 1.4;
    color: var(--moss2);
    white-space: pre;
    margin-bottom: 24px;
  }

  .sobre-visual-label {
    font-size: 10px;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    color: var(--muted);
  }

  .sobre-visual::before {
    content: '';
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 120px;
    background: linear-gradient(to top, var(--moss) 0%, transparent 100%);
    opacity: 0.15;
  }

  /* FEATURES */
  #features {
    padding: 100px 48px;
    background: var(--deep);
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
  }

  .features-inner { max-width: 1100px; margin: 0 auto; }

  .features-header {
    text-align: center;
    margin-bottom: 72px;
  }

  .features-title {
    font-family: 'Cinzel', serif;
    font-size: clamp(24px, 3vw, 40px);
    font-weight: 600;
  }

  .features-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2px;
  }

  .feature-card {
    background: var(--black);
    padding: 48px 36px;
    border: 1px solid var(--border);
    transition: border-color 0.3s;
  }
  .feature-card:hover { border-color: rgba(200,137,26,0.3); }

  .feature-icon {
    font-size: 32px;
    margin-bottom: 20px;
    display: block;
  }

  .feature-name {
    font-family: 'Cinzel', serif;
    font-size: 16px;
    font-weight: 600;
    margin-bottom: 12px;
    color: var(--paper);
  }

  .feature-desc { font-size: 14px; color: var(--muted); line-height: 1.8; }

  /* FALCO */
  #falco {
    padding: 120px 48px;
    max-width: 1100px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 1fr 1.2fr;
    gap: 80px;
    align-items: center;
  }

  .falco-quote {
    font-family: 'Cinzel', serif;
    font-size: clamp(20px, 2.5vw, 32px);
    font-weight: 400;
    font-style: italic;
    line-height: 1.5;
    color: var(--paper);
    border-left: 2px solid var(--amber);
    padding-left: 28px;
    margin-bottom: 32px;
  }

  .falco-text { color: var(--muted); font-size: 15px; line-height: 1.9; }
  .falco-text + .falco-text { margin-top: 16px; }

  .status-badge {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: rgba(45,74,45,0.3);
    border: 1px solid rgba(61,107,61,0.4);
    padding: 8px 16px;
    font-size: 11px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--moss2);
    margin-top: 28px;
  }

  .status-dot {
    width: 6px; height: 6px;
    background: var(--moss2);
    border-radius: 50%;
    animation: pulse 2s ease-in-out infinite;
  }

  /* APOIO */
  #apoio {
    padding: 120px 48px;
    background: var(--deep);
    border-top: 1px solid var(--border);
  }

  .apoio-inner {
    max-width: 800px;
    margin: 0 auto;
    text-align: center;
  }

  .apoio-title {
    font-family: 'Cinzel', serif;
    font-size: clamp(28px, 4vw, 52px);
    font-weight: 900;
    line-height: 1.15;
    margin-bottom: 20px;
  }

  .apoio-title span { color: var(--amber); }

  .apoio-sub { color: var(--muted); font-size: 16px; max-width: 520px; margin: 0 auto 60px; }

  .tiers {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2px;
    margin-bottom: 60px;
    text-align: left;
  }

  .tier {
    background: var(--black);
    border: 1px solid var(--border);
    padding: 40px 32px;
    position: relative;
    transition: border-color 0.3s, transform 0.3s;
    cursor: default;
  }
  .tier:hover { border-color: rgba(200,137,26,0.4); transform: translateY(-4px); }

  .tier.featured {
    border-color: rgba(200,137,26,0.5);
    background: rgba(200,137,26,0.04);
  }

  .tier-badge {
    position: absolute;
    top: -1px; right: 24px;
    background: var(--amber);
    color: var(--black);
    font-size: 9px;
    font-weight: 500;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    padding: 4px 12px;
  }

  .tier-icon { font-size: 28px; margin-bottom: 16px; display: block; }

  .tier-name {
    font-family: 'Cinzel', serif;
    font-size: 14px;
    font-weight: 600;
    letter-spacing: 0.1em;
    color: var(--paper);
    margin-bottom: 8px;
  }

  .tier-price {
    font-family: 'Cinzel', serif;
    font-size: 36px;
    font-weight: 900;
    color: var(--amber);
    margin-bottom: 20px;
    line-height: 1;
  }

  .tier-price sup { font-size: 16px; vertical-align: super; }

  .tier-perks { list-style: none; }
  .tier-perks li {
    font-size: 13px;
    color: var(--muted);
    padding: 6px 0;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    gap: 8px;
  }
  .tier-perks li:last-child { border-bottom: none; }
  .tier-perks li::before { content: '—'; color: var(--amber); font-size: 10px; }

  .apoio-note {
    font-size: 13px;
    color: var(--muted);
    line-height: 1.8;
    border: 1px solid var(--border);
    padding: 24px 32px;
    margin-bottom: 40px;
    text-align: left;
  }

  .apoio-note strong { color: var(--paper); font-weight: 500; }

  .pix-section {
    background: var(--black);
    border: 1px solid rgba(200,137,26,0.3);
    padding: 40px;
    text-align: center;
    margin-bottom: 32px;
  }

  .pix-label {
    font-size: 11px;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    color: var(--amber);
    margin-bottom: 12px;
  }

  .pix-key {
    font-family: monospace;
    font-size: 18px;
    color: var(--paper);
    background: var(--deep);
    padding: 12px 24px;
    display: inline-block;
    margin: 12px 0;
    cursor: pointer;
    border: 1px solid var(--border);
    transition: border-color 0.3s;
    user-select: all;
  }
  .pix-key:hover { border-color: var(--amber); }

  .pix-hint { font-size: 12px; color: var(--muted); }

  .copy-toast {
    display: inline-block;
    background: var(--moss);
    color: var(--paper);
    font-size: 11px;
    letter-spacing: 0.1em;
    padding: 4px 12px;
    margin-top: 8px;
    opacity: 0;
    transition: opacity 0.3s;
  }
  .copy-toast.show { opacity: 1; }

  /* NEWSLETTER */
  #newsletter {
    padding: 100px 48px;
    max-width: 600px;
    margin: 0 auto;
    text-align: center;
  }

  .nl-title {
    font-family: 'Cinzel', serif;
    font-size: clamp(22px, 3vw, 36px);
    font-weight: 600;
    margin-bottom: 16px;
  }

  .nl-sub { color: var(--muted); font-size: 15px; margin-bottom: 36px; }

  .nl-form {
    display: flex;
    gap: 0;
    max-width: 460px;
    margin: 0 auto;
  }

  .nl-input {
    flex: 1;
    background: var(--deep);
    border: 1px solid var(--border);
    border-right: none;
    padding: 14px 20px;
    color: var(--paper);
    font-family: 'Inter', sans-serif;
    font-size: 14px;
    outline: none;
    transition: border-color 0.3s;
  }
  .nl-input::placeholder { color: var(--muted); }
  .nl-input:focus { border-color: rgba(200,137,26,0.5); }

  .nl-btn {
    background: var(--amber);
    color: var(--black);
    border: none;
    padding: 14px 24px;
    font-family: 'Cinzel', serif;
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    cursor: pointer;
    transition: background 0.3s;
    white-space: nowrap;
  }
  .nl-btn:hover { background: var(--amber2); }

  /* FOOTER */
  footer {
    padding: 40px 48px;
    border-top: 1px solid var(--border);
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 16px;
  }

  .footer-logo {
    font-family: 'Cinzel', serif;
    font-size: 13px;
    font-weight: 900;
    letter-spacing: 0.2em;
    color: var(--amber);
  }

  .footer-copy { font-size: 12px; color: var(--muted); }

  .footer-links { display: flex; gap: 24px; }
  .footer-links a {
    font-size: 12px;
    color: var(--muted);
    text-decoration: none;
    letter-spacing: 0.1em;
    transition: color 0.3s;
  }
  .footer-links a:hover { color: var(--paper); }

  /* ANIMATIONS */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to   { opacity: 1; transform: translateY(0); }
  }
  @keyframes scrollPulse {
    0%, 100% { opacity: 0.3; }
    50%       { opacity: 1; }
  }
  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50%       { opacity: 0.4; transform: scale(0.8); }
  }

  .reveal {
    opacity: 0;
    transform: translateY(32px);
    transition: opacity 0.8s ease, transform 0.8s ease;
  }
  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  @media (prefers-reduced-motion: reduce) {
    *, *::before, *::after { animation-duration: 0.01ms !important; transition-duration: 0.01ms !important; }
  }

  @media (max-width: 768px) {
    nav { padding: 16px 24px; }
    .nav-links { display: none; }
    #sobre, #falco { padding: 80px 24px; }
    .sobre-grid, #falco { grid-template-columns: 1fr; gap: 48px; }
    #features, #apoio, #newsletter { padding: 80px 24px; }
    .features-grid, .tiers { grid-template-columns: 1fr; }
    footer { padding: 32px 24px; flex-direction: column; align-items: flex-start; }
    .nl-form { flex-direction: column; }
    .nl-input { border-right: 1px solid var(--border); border-bottom: none; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <a href="#" class="nav-logo">My Last Hope</a>
  <ul class="nav-links">
    <li><a href="#sobre">O Jogo</a></li>
    <li><a href="#features">Mecânicas</a></li>
    <li><a href="#falco">Falco</a></li>
    <li><a href="#apoio">Apoiar</a></li>
  </ul>
</nav>

<!-- HERO -->
<section id="hero">
  <canvas id="hero-canvas"></canvas>
  <p class="hero-eyebrow">Em desenvolvimento · 2025</p>
  <h1 class="hero-title">
    My Last Hope
    <span>Um recomeço. Um propósito. Uma fazenda.</span>
  </h1>
  <p class="hero-desc">
    Um jogo indie de fazenda e vida onde encontrar seu lugar no mundo
    pode ser tão simples quanto plantar uma semente.
  </p>
  <div class="hero-ctas">
    <a href="#apoio" class="btn-primary">Apoiar o desenvolvimento</a>
    <a href="#sobre" class="btn-outline">Saber mais</a>
  </div>
  <div class="scroll-hint">
    <span>Rolar</span>
    <div class="scroll-line"></div>
  </div>
</section>

<!-- SOBRE -->
<section id="sobre">
  <div class="sobre-grid">
    <div class="reveal">
      <p class="section-label">Sobre o jogo</p>
      <h2 class="sobre-title">Quando tudo vai mal,<br>a terra <em>não mente.</em></h2>
      <p class="sobre-text">
        My Last Hope é um RPG de fazenda 2D topdown onde você acompanha Falco —
        um homem que perdeu o sentido no ritmo acelerado da cidade corporativa
        e decide recomeçar do zero numa pequena vila rural.
      </p>
      <p class="sobre-text">
        Plante, cuide de animais, pesque, construa laços com os moradores
        da vila e, aos poucos, redescubra o que realmente importa:
        criar o jogo que sempre sonhou.
      </p>
      <p class="sobre-text">
        Uma história sobre propósito, desaceleração e a coragem
        de começar de novo — contada pixel a pixel.
      </p>
    </div>
    <div class="sobre-visual reveal">
      <div class="sobre-visual-inner">
        <div class="falco-ascii">
    ░░░░░░░░░░░
    ░░ ◉   ◉ ░░
    ░░   ‿   ░░
    ░░░░░░░░░░░
    ░▓▓░░░░▓▓░
    ░░░▓▓▓▓░░░
    ░░░ ▌ ▌ ░░
        </div>
        <p class="sobre-visual-label">Falco · Protagonista</p>
      </div>
    </div>
  </div>
</section>

<!-- FEATURES -->
<section id="features">
  <div class="features-inner">
    <div class="features-header reveal">
      <p class="section-label">Mecânicas</p>
      <h2 class="features-title">O que você fará em My Last Hope</h2>
    </div>
    <div class="features-grid">
      <div class="feature-card reveal">
        <span class="feature-icon">🌱</span>
        <h3 class="feature-name">Fazenda</h3>
        <p class="feature-desc">Plante, regue e colha dezenas de culturas. O solo responde às estações e ao seu cuidado — negligência tem consequências.</p>
      </div>
      <div class="feature-card reveal">
        <span class="feature-icon">🐓</span>
        <h3 class="feature-name">Animais</h3>
        <p class="feature-desc">Crie galinhas, vacas e outros animais. Cada um tem personalidade própria e reage ao modo como Falco os trata.</p>
      </div>
      <div class="feature-card reveal">
        <span class="feature-icon">🎣</span>
        <h3 class="feature-name">Pesca</h3>
        <p class="feature-desc">Mini-game de pesca com dezenas de espécies diferentes. Peixes raros aparecem em certas estações e condições climáticas.</p>
      </div>
      <div class="feature-card reveal">
        <span class="feature-icon">🏘️</span>
        <h3 class="feature-name">Vila viva</h3>
        <p class="feature-desc">Moradores com rotinas reais, histórias próprias e relações que mudam conforme suas escolhas ao longo do tempo.</p>
      </div>
      <div class="feature-card reveal">
        <span class="feature-icon">⭐</span>
        <h3 class="feature-name">Habilidades</h3>
        <p class="feature-desc">Sistema de progressão orgânico — quanto mais você faz, mais Falco melhora. Sem grinding forçado, só evolução natural.</p>
      </div>
      <div class="feature-card reveal">
        <span class="feature-icon">🎮</span>
        <h3 class="feature-name">O jogo no jogo</h3>
        <p class="feature-desc">O grande sonho de Falco: criar seu primeiro jogo. Desbloqueie inspiração vivendo e transforme experiências em mecânicas.</p>
      </div>
    </div>
  </div>
</section>

<!-- FALCO -->
<section id="falco">
  <div class="reveal">
    <p class="section-label">O protagonista</p>
    <blockquote class="falco-quote">
      "Eu não cabia naquele mundo. Talvez eu caiba nesse."
    </blockquote>
    <p class="falco-text">
      Falco não é um herói. É alguém que chegou num ponto em que continuar
      do jeito que estava simplesmente não era mais uma opção.
    </p>
    <p class="falco-text">
      Ele carrega o peso de quem tentou se encaixar numa vida que nunca
      foi a dele — o escritório, as metas, o barulho constante.
      A mudança para a vila não é fuga. É a única saída honesta.
    </p>
    <p class="falco-text">
      My Last Hope é, em muitos aspectos, uma história real.
      A história de quem decidiu criar esse jogo.
    </p>
    <div class="status-badge">
      <span class="status-dot"></span>
      Em desenvolvimento ativo
    </div>
  </div>
  <div class="reveal" style="background: var(--deep); border: 1px solid var(--border); padding: 48px; display: flex; flex-direction: column; gap: 24px;">
    <div>
      <p style="font-size: 10px; letter-spacing: 0.3em; text-transform: uppercase; color: var(--amber); margin-bottom: 8px;">Engine</p>
      <p style="font-family: 'Cinzel', serif; font-size: 15px; color: var(--paper);">Unity 6 · 2D Topdown</p>
    </div>
    <div style="height: 1px; background: var(--border);"></div>
    <div>
      <p style="font-size: 10px; letter-spacing: 0.3em; text-transform: uppercase; color: var(--amber); margin-bottom: 8px;">Estágio atual</p>
      <p style="font-size: 14px; color: var(--muted);">Prototipagem — movimento, câmera e mapa base</p>
      <div style="margin-top: 12px; height: 3px; background: var(--border); border-radius: 2px; overflow: hidden;">
        <div style="width: 8%; height: 100%; background: var(--moss2); border-radius: 2px; transition: width 1s ease;"></div>
      </div>
      <p style="font-size: 11px; color: var(--muted); margin-top: 6px;">8% concluído</p>
    </div>
    <div style="height: 1px; background: var(--border);"></div>
    <div>
      <p style="font-size: 10px; letter-spacing: 0.3em; text-transform: uppercase; color: var(--amber); margin-bottom: 8px;">Plataformas planejadas</p>
      <p style="font-size: 14px; color: var(--muted);">PC (Windows / Mac) · Steam</p>
    </div>
    <div style="height: 1px; background: var(--border);"></div>
    <div>
      <p style="font-size: 10px; letter-spacing: 0.3em; text-transform: uppercase; color: var(--amber); margin-bottom: 8px;">Desenvolvedor</p>
      <p style="font-size: 14px; color: var(--muted);">Projeto indie solo</p>
    </div>
  </div>
</section>

<!-- APOIO -->
<section id="apoio">
  <div class="apoio-inner">
    <div class="reveal">
      <p class="section-label">Apoio financeiro</p>
      <h2 class="apoio-title">Faça parte<br>desta <span>história.</span></h2>
      <p class="apoio-sub">
        My Last Hope é desenvolvido por uma única pessoa, com dedicação e propósito.
        Seu apoio transforma esse sonho em realidade.
      </p>
    </div>

    <div class="tiers reveal">
      <div class="tier">
        <span class="tier-icon">🌿</span>
        <p class="tier-name">Semente</p>
        <p class="tier-price"><sup>R$</sup>15</p>
        <ul class="tier-perks">
          <li>Nome nos créditos do jogo</li>
          <li>Acesso ao diário de dev</li>
          <li>Gratidão eterna do Falco</li>
        </ul>
      </div>
      <div class="tier featured">
        <span class="tier-badge">Mais popular</span>
        <span class="tier-icon">🌾</span>
        <p class="tier-name">Colheita</p>
        <p class="tier-price"><sup>R$</sup>45</p>
        <ul class="tier-perks">
          <li>Tudo do nível Semente</li>
          <li>Acesso antecipado à demo</li>
          <li>Wallpapers exclusivos</li>
          <li>Voto em features futuras</li>
        </ul>
      </div>
      <div class="tier">
        <span class="tier-icon">🏡</span>
        <p class="tier-name">Fazendeiro</p>
        <p class="tier-price"><sup>R$</sup>120</p>
        <ul class="tier-perks">
          <li>Tudo do nível Colheita</li>
          <li>Personagem NPC com seu nome</li>
          <li>Acesso à versão beta completa</li>
          <li>Canal direto com o dev</li>
        </ul>
      </div>
    </div>

    <div class="apoio-note reveal">
      <strong>Como funciona o apoio:</strong> Este projeto está em fase inicial de desenvolvimento.
      Todo valor recebido é reinvestido diretamente em assets, ferramentas e dedicação de tempo.
      Apoiadores recebem atualizações regulares sobre o progresso e têm voz ativa nas decisões do jogo.
    </div>

    <div class="pix-section reveal">
      <p class="pix-label">Apoiar via Pix</p>
      <p style="font-size: 13px; color: var(--muted); margin-bottom: 8px;">Chave Pix (coloque sua chave aqui)</p>
      <div class="pix-key" onclick="copyPix(this)" title="Clique para copiar">
        seupix@email.com
      </div>
      <div class="copy-toast" id="copy-toast">Copiado!</div>
      <p class="pix-hint" style="margin-top: 12px;">Após o Pix, envie seu comprovante para receber os benefícios do nível escolhido.</p>
    </div>

    <div class="reveal" style="display: flex; gap: 16px; justify-content: center; flex-wrap: wrap;">
      <a href="https://apoia.se" target="_blank" class="btn-primary" style="text-align:center;">Apoiar no Apoia.se</a>
      <a href="https://ko-fi.com" target="_blank" class="btn-outline" style="text-align:center;">Ko-fi</a>
    </div>
  </div>
</section>

<!-- NEWSLETTER -->
<section id="newsletter">
  <div class="reveal">
    <p class="section-label">Fique por dentro</p>
    <h2 class="nl-title">Acompanhe o desenvolvimento</h2>
    <p class="nl-sub">Receba atualizações sobre o progresso do jogo, bastidores e lançamentos direto no seu email.</p>
    <form class="nl-form" onsubmit="handleNewsletter(event)">
      <input type="email" class="nl-input" placeholder="seu@email.com" required>
      <button type="submit" class="nl-btn">Entrar</button>
    </form>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <span class="footer-logo">My Last Hope</span>
  <span class="footer-copy">© 2025 · Projeto indie em desenvolvimento</span>
  <div class="footer-links">
    <a href="#">Twitter</a>
    <a href="#">Instagram</a>
    <a href="#">itch.io</a>
  </div>
</footer>

<script>
/* PARTICLE CANVAS — folhas caindo */
const canvas = document.getElementById('hero-canvas');
const ctx = canvas.getContext('2d');
let W, H, particles = [];

function resize() {
  W = canvas.width  = canvas.offsetWidth;
  H = canvas.height = canvas.offsetHeight;
}
resize();
window.addEventListener('resize', resize);

function randomLeaf() {
  return {
    x: Math.random() * W,
    y: -20,
    size: 3 + Math.random() * 5,
    speedY: 0.4 + Math.random() * 0.8,
    speedX: (Math.random() - 0.5) * 0.5,
    rotation: Math.random() * Math.PI * 2,
    rotSpeed: (Math.random() - 0.5) * 0.03,
    opacity: 0.1 + Math.random() * 0.25,
    color: Math.random() > 0.5 ? '#2D4A2D' : '#C8891A'
  };
}

for (let i = 0; i < 40; i++) {
  const p = randomLeaf();
  p.y = Math.random() * H;
  particles.push(p);
}

function drawLeaf(p) {
  ctx.save();
  ctx.translate(p.x, p.y);
  ctx.rotate(p.rotation);
  ctx.globalAlpha = p.opacity;
  ctx.fillStyle = p.color;
  ctx.beginPath();
  ctx.ellipse(0, 0, p.size, p.size * 0.5, 0, 0, Math.PI * 2);
  ctx.fill();
  ctx.restore();
}

function animate() {
  ctx.clearRect(0, 0, W, H);
  for (let p of particles) {
    p.y += p.speedY;
    p.x += p.speedX;
    p.rotation += p.rotSpeed;
    if (p.y > H + 20) { Object.assign(p, randomLeaf()); }
    drawLeaf(p);
  }
  requestAnimationFrame(animate);
}
animate();

/* SCROLL REVEAL */
const reveals = document.querySelectorAll('.reveal');
const observer = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting) { e.target.classList.add('visible'); }
  });
}, { threshold: 0.12 });
reveals.forEach(el => observer.observe(el));

/* COPY PIX */
function copyPix(el) {
  navigator.clipboard.writeText(el.textContent.trim()).then(() => {
    const toast = document.getElementById('copy-toast');
    toast.classList.add('show');
    setTimeout(() => toast.classList.remove('show'), 2000);
  });
}

/* NEWSLETTER */
function handleNewsletter(e) {
  e.preventDefault();
  const btn = e.target.querySelector('button');
  btn.textContent = 'Obrigado!';
  btn.style.background = '#2D4A2D';
  btn.style.color = '#E8E4D9';
  setTimeout(() => {
    btn.textContent = 'Entrar';
    btn.style.background = '';
    btn.style.color = '';
    e.target.reset();
  }, 3000);
}
</script>
</body>
</html>
