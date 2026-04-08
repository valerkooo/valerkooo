<!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Valerii Starko — Network Specialist</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;600;700&family=Syne:wght@400;600;800&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #080c10;
    --bg2: #0d1318;
    --panel: #111820;
    --border: #1e2d3d;
    --accent: #00d4ff;
    --accent2: #00ff88;
    --accent3: #ff6b35;
    --text: #c9d8e8;
    --muted: #4a6070;
    --mono: 'JetBrains Mono', monospace;
    --sans: 'Syne', sans-serif;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--mono);
    overflow-x: hidden;
  }

  /* ── CANVAS ── */
  #net-canvas {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0;
    opacity: 0.18;
  }

  /* ── NAV ── */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 18px 48px;
    background: rgba(8,12,16,0.85);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid var(--border);
  }

  .nav-logo {
    font-family: var(--sans);
    font-weight: 800;
    font-size: 1.1rem;
    color: var(--accent);
    letter-spacing: -0.02em;
  }

  .nav-logo span { color: var(--accent2); }

  .nav-links { display: flex; gap: 32px; }

  .nav-links a {
    text-decoration: none;
    color: var(--muted);
    font-size: 0.75rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    transition: color 0.2s;
  }

  .nav-links a:hover { color: var(--accent); }

  /* ── STATUS BAR ── */
  .status-bar {
    position: fixed;
    bottom: 0; left: 0; right: 0;
    z-index: 100;
    background: rgba(8,12,16,0.9);
    border-top: 1px solid var(--border);
    padding: 6px 48px;
    display: flex;
    gap: 32px;
    font-size: 0.65rem;
    color: var(--muted);
  }

  .status-item { display: flex; align-items: center; gap: 6px; }
  .status-dot {
    width: 6px; height: 6px;
    border-radius: 50%;
    background: var(--accent2);
    animation: pulse 2s infinite;
  }
  .status-dot.orange { background: var(--accent3); }

  @keyframes pulse {
    0%,100% { opacity: 1; }
    50% { opacity: 0.3; }
  }

  /* ── SECTIONS ── */
  section {
    position: relative;
    z-index: 1;
    min-height: 100vh;
    display: flex;
    align-items: center;
  }

  .container {
    max-width: 1100px;
    margin: 0 auto;
    padding: 0 48px;
    width: 100%;
  }

  /* ── HERO ── */
  #hero {
    padding-top: 80px;
  }

  .hero-tag {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: rgba(0,212,255,0.08);
    border: 1px solid rgba(0,212,255,0.2);
    border-radius: 3px;
    padding: 5px 12px;
    font-size: 0.7rem;
    color: var(--accent);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-bottom: 32px;
    animation: fadeUp 0.6s ease both;
  }

  .hero-title {
    font-family: var(--sans);
    font-weight: 800;
    font-size: clamp(2.8rem, 6vw, 5.5rem);
    line-height: 0.95;
    letter-spacing: -0.03em;
    animation: fadeUp 0.6s 0.1s ease both;
    margin-bottom: 8px;
  }

  .hero-title .name { color: #fff; }
  .hero-title .role { color: var(--accent); display: block; }

  .hero-sub {
    font-size: 0.85rem;
    color: var(--muted);
    max-width: 500px;
    line-height: 1.7;
    margin: 24px 0 40px;
    animation: fadeUp 0.6s 0.2s ease both;
  }

  .hero-ctas {
    display: flex;
    gap: 16px;
    animation: fadeUp 0.6s 0.3s ease both;
    flex-wrap: wrap;
  }

  .btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 12px 24px;
    font-family: var(--mono);
    font-size: 0.78rem;
    font-weight: 600;
    letter-spacing: 0.05em;
    text-decoration: none;
    border-radius: 3px;
    transition: all 0.2s;
    cursor: pointer;
    border: none;
  }

  .btn-primary {
    background: var(--accent);
    color: var(--bg);
  }

  .btn-primary:hover {
    background: #fff;
    transform: translateY(-2px);
    box-shadow: 0 8px 24px rgba(0,212,255,0.3);
  }

  .btn-outline {
    background: transparent;
    color: var(--text);
    border: 1px solid var(--border);
  }

  .btn-outline:hover {
    border-color: var(--accent);
    color: var(--accent);
    transform: translateY(-2px);
  }

  /* ── TERMINAL BLOCK ── */
  .terminal {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 6px;
    overflow: hidden;
    margin: 60px 0 0;
    animation: fadeUp 0.6s 0.4s ease both;
  }

  .terminal-bar {
    background: #151d26;
    padding: 10px 16px;
    display: flex;
    align-items: center;
    gap: 8px;
    border-bottom: 1px solid var(--border);
  }

  .t-dot {
    width: 10px; height: 10px;
    border-radius: 50%;
  }

  .t-red { background: #ff5f56; }
  .t-yellow { background: #ffbd2e; }
  .t-green { background: #27c93f; }

  .terminal-title {
    font-size: 0.68rem;
    color: var(--muted);
    margin-left: 8px;
    letter-spacing: 0.1em;
  }

  .terminal-body {
    padding: 20px 24px;
    font-size: 0.78rem;
    line-height: 2;
  }

  .t-prompt { color: var(--accent2); }
  .t-cmd { color: #fff; }
  .t-out { color: var(--muted); }
  .t-val { color: var(--accent); }
  .t-cursor {
    display: inline-block;
    width: 8px; height: 14px;
    background: var(--accent);
    animation: blink 1.1s step-end infinite;
    vertical-align: middle;
    margin-left: 2px;
  }

  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

  /* ── SECTION HEADER ── */
  .section-header {
    margin-bottom: 48px;
  }

  .section-label {
    font-size: 0.65rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
    max-width: 60px;
  }

  .section-title {
    font-family: var(--sans);
    font-weight: 800;
    font-size: clamp(1.8rem, 4vw, 2.8rem);
    letter-spacing: -0.03em;
    color: #fff;
  }

  /* ── SKILLS ── */
  #skills { background: var(--bg2); }

  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 16px;
  }

  .skill-card {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 24px;
    transition: all 0.25s;
    position: relative;
    overflow: hidden;
  }

  .skill-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 3px; height: 100%;
    background: var(--accent);
    opacity: 0;
    transition: opacity 0.25s;
  }

  .skill-card:hover {
    border-color: var(--accent);
    transform: translateY(-3px);
    box-shadow: 0 12px 32px rgba(0,0,0,0.4);
  }

  .skill-card:hover::before { opacity: 1; }

  .skill-icon {
    font-size: 1.5rem;
    margin-bottom: 12px;
  }

  .skill-name {
    font-family: var(--sans);
    font-weight: 600;
    font-size: 0.95rem;
    color: #fff;
    margin-bottom: 8px;
  }

  .skill-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    margin-top: 12px;
  }

  .tag {
    font-size: 0.62rem;
    padding: 3px 8px;
    border-radius: 3px;
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }

  .tag-blue {
    background: rgba(0,212,255,0.1);
    color: var(--accent);
    border: 1px solid rgba(0,212,255,0.2);
  }

  .tag-green {
    background: rgba(0,255,136,0.1);
    color: var(--accent2);
    border: 1px solid rgba(0,255,136,0.2);
  }

  .tag-orange {
    background: rgba(255,107,53,0.1);
    color: var(--accent3);
    border: 1px solid rgba(255,107,53,0.2);
  }

  /* ── PROJECTS ── */
  .projects-list {
    display: grid;
    gap: 20px;
  }

  .project-card {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 28px 32px;
    display: grid;
    grid-template-columns: 1fr auto;
    gap: 24px;
    align-items: start;
    transition: all 0.25s;
  }

  .project-card:hover {
    border-color: rgba(0,212,255,0.3);
    box-shadow: 0 0 0 1px rgba(0,212,255,0.08), 0 16px 40px rgba(0,0,0,0.4);
  }

  .project-num {
    font-size: 0.65rem;
    color: var(--muted);
    letter-spacing: 0.1em;
    margin-bottom: 8px;
  }

  .project-name {
    font-family: var(--sans);
    font-weight: 700;
    font-size: 1.15rem;
    color: #fff;
    margin-bottom: 10px;
  }

  .project-desc {
    font-size: 0.78rem;
    color: var(--muted);
    line-height: 1.8;
    margin-bottom: 16px;
  }

  .project-meta {
    display: flex;
    align-items: center;
    gap: 16px;
    font-size: 0.68rem;
    color: var(--muted);
  }

  .project-status {
    display: flex;
    align-items: center;
    gap: 6px;
    color: var(--accent2);
  }

  .project-link {
    display: flex;
    align-items: center;
    gap: 6px;
    text-decoration: none;
    color: var(--accent);
    font-size: 0.72rem;
    font-weight: 600;
    white-space: nowrap;
    padding: 10px 18px;
    border: 1px solid rgba(0,212,255,0.25);
    border-radius: 4px;
    transition: all 0.2s;
    align-self: center;
  }

  .project-link:hover {
    background: rgba(0,212,255,0.1);
    transform: translateX(3px);
  }

  /* ── CERTS ── */
  #certifications { background: var(--bg2); }

  .certs-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
    gap: 16px;
  }

  .cert-card {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 24px 20px;
    text-align: center;
    transition: all 0.25s;
  }

  .cert-card:hover {
    border-color: var(--accent2);
    transform: translateY(-3px);
  }

  .cert-badge {
    width: 56px; height: 56px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.4rem;
    margin: 0 auto 14px;
    border: 2px solid var(--border);
  }

  .cert-name {
    font-family: var(--sans);
    font-weight: 700;
    font-size: 0.95rem;
    color: #fff;
    margin-bottom: 4px;
  }

  .cert-issuer {
    font-size: 0.68rem;
    color: var(--muted);
    margin-bottom: 10px;
  }

  .cert-year {
    font-size: 0.65rem;
    color: var(--accent);
    letter-spacing: 0.1em;
  }

  /* ── CONTACT ── */
  .contact-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 48px;
    align-items: center;
  }

  .contact-intro {
    font-size: 0.85rem;
    color: var(--muted);
    line-height: 1.9;
    margin-bottom: 32px;
  }

  .contact-links {
    display: flex;
    flex-direction: column;
    gap: 12px;
  }

  .contact-item {
    display: flex;
    align-items: center;
    gap: 14px;
    text-decoration: none;
    color: var(--text);
    font-size: 0.8rem;
    padding: 14px 18px;
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 5px;
    transition: all 0.2s;
  }

  .contact-item:hover {
    border-color: var(--accent);
    color: var(--accent);
    transform: translateX(4px);
  }

  .contact-icon {
    font-size: 1rem;
    width: 20px;
    text-align: center;
  }

  /* ── NETWORK STATS PANEL ── */
  .stats-panel {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 6px;
    overflow: hidden;
  }

  .stats-header {
    background: #151d26;
    padding: 12px 20px;
    font-size: 0.68rem;
    color: var(--muted);
    letter-spacing: 0.1em;
    border-bottom: 1px solid var(--border);
    display: flex;
    justify-content: space-between;
  }

  .stat-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px 20px;
    border-bottom: 1px solid rgba(30,45,61,0.5);
    font-size: 0.75rem;
  }

  .stat-label { color: var(--muted); }
  .stat-value { color: var(--accent); font-weight: 600; }
  .stat-value.green { color: var(--accent2); }

  .bar-wrap {
    height: 3px;
    background: var(--border);
    border-radius: 2px;
    margin: 8px 20px;
  }

  .bar-fill {
    height: 100%;
    border-radius: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    transition: width 1.5s ease;
  }

  /* ── ANIMATIONS ── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .reveal {
    opacity: 0;
    transform: translateY(24px);
    transition: opacity 0.6s ease, transform 0.6s ease;
  }

  .reveal.visible {
    opacity: 1;
    transform: none;
  }

  /* ── FOOTER ── */
  footer {
    position: relative;
    z-index: 1;
    text-align: center;
    padding: 40px 0 70px;
    font-size: 0.68rem;
    color: var(--muted);
    border-top: 1px solid var(--border);
  }

  /* ── RESPONSIVE ── */
  @media (max-width: 768px) {
    nav { padding: 14px 24px; }
    .nav-links { gap: 16px; }
    .container { padding: 0 24px; }
    .contact-grid { grid-template-columns: 1fr; }
    .project-card { grid-template-columns: 1fr; }
    .hero-title { font-size: 2.4rem; }
  }
</style>
</head>
<body>

<canvas id="net-canvas"></canvas>

<!-- NAV -->
<nav>
  <div class="nav-logo">MR<span>.</span>dev</div>
  <div class="nav-links">
    <a href="#skills">Skills</a>
    <a href="#projects">Progetti</a>
    <a href="#certifications">Certificazioni</a>
    <a href="#contact">Contatti</a>
  </div>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="container">
    <div class="hero-tag">
      <span style="width:7px;height:7px;background:var(--accent2);border-radius:50%;display:inline-block;animation:pulse 2s infinite"></span>
      Online
    </div>
    <h1 class="hero-title">
      <span class="name">Valerii Starko</span>
      <span class="role">Network Specialist</span>
    </h1>
    <p class="hero-sub">
      Progetto, configuro e proteggo infrastrutture di rete enterprise. Specializzato in routing avanzato, sicurezza perimetrale e automazione di rete con Ansible e Python.
    </p>
    <div class="hero-ctas">
      <a href="#projects" class="btn btn-primary">▶ Vedi i progetti</a>
      <a href="#contact" class="btn btn-outline">✉ Contattami</a>
    </div>

    <div class="terminal">
      <div class="terminal-bar">
        <div class="t-dot t-red"></div>
        <div class="t-dot t-yellow"></div>
        <div class="t-dot t-green"></div>
        <span class="terminal-title">valerii@network:~$</span>
      </div>
      <div class="terminal-body">
        <div><span class="t-prompt">valerii@network:~$</span> <span class="t-cmd">whoami --verbose</span></div>
        <div class="t-out">→ Nome:       <span class="t-val">Valerii Starko</span></div>
        <div class="t-out">→ Ruolo:      <span class="t-val">Network Specialist / NOC Engineer</span></div>
        <div class="t-out">→ Esperienza: <span class="t-val">2+ anni in infrastrutture enterprise</span></div>
        <div class="t-out">→ Location:   <span class="t-val">Milano, Italia 🇮🇹</span></div>
        <div style="margin-top:6px"><span class="t-prompt">Valerii@network:~$</span> <span class="t-cursor"></span></div>
      </div>
    </div>
  </div>
</section>

<!-- SKILLS -->
<section id="skills">
  <div class="container">
    <div class="section-header reveal">
      <div class="section-label">// 01 — competenze</div>
      <h2 class="section-title">Stack tecnico</h2>
    </div>
    <div class="skills-grid">

      <div class="skill-card reveal">
        <div class="skill-icon">🔀</div>
        <div class="skill-name">Routing & Switching</div>
        <p class="t-out" style="font-size:0.75rem;line-height:1.7">Progettazione e configurazione di reti scalabili con protocolli enterprise-grade.</p>
        <div class="skill-tags">
          <span class="tag tag-blue">OSPF</span>
          <span class="tag tag-blue">BGP</span>
          <span class="tag tag-blue">EIGRP</span>
          <span class="tag tag-blue">VLAN / VTP</span>
          <span class="tag tag-blue">STP / RSTP</span>
        </div>
      </div>

      <div class="skill-card reveal">
        <div class="skill-icon">🛡️</div>
        <div class="skill-name">Network Security</div>
        <p class="t-out" style="font-size:0.75rem;line-height:1.7">Configurazione di firewall, IDS/IPS e policy di sicurezza perimetrale e interna.</p>
        <div class="skill-tags">
          <span class="tag tag-orange">Cisco ASA</span>
          <span class="tag tag-orange">pfSense</span>
          <span class="tag tag-orange">FortiGate</span>
          <span class="tag tag-orange">ACL</span>
          <span class="tag tag-orange">VPN IPSec</span>
        </div>
      </div>

      <div class="skill-card reveal">
        <div class="skill-icon">⚙️</div>
        <div class="skill-name">Automazione di Rete</div>
        <p class="t-out" style="font-size:0.75rem;line-height:1.7">Provisioning automatizzato e gestione configurazioni su larga scala.</p>
        <div class="skill-tags">
          <span class="tag tag-green">Ansible</span>
          <span class="tag tag-green">Python / Netmiko</span>
          <span class="tag tag-green">NAPALM</span>
          <span class="tag tag-green">Terraform</span>
        </div>
      </div>

      <div class="skill-card reveal">
        <div class="skill-icon">📡</div>
        <div class="skill-name">Monitoring & NOC</div>
        <p class="t-out" style="font-size:0.75rem;line-height:1.7">Monitoraggio proattivo dell'infrastruttura con alerting e dashboard in tempo reale.</p>
        <div class="skill-tags">
          <span class="tag tag-blue">Zabbix</span>
          <span class="tag tag-blue">Grafana</span>
          <span class="tag tag-blue">PRTG</span>
          <span class="tag tag-blue">Nagios</span>
          <span class="tag tag-blue">Wireshark</span>
        </div>
      </div>

      <div class="skill-card reveal">
        <div class="skill-icon">☁️</div>
        <div class="skill-name">Cloud & Virtualizzazione</div>
        <p class="t-out" style="font-size:0.75rem;line-height:1.7">Gestione di reti ibride e deploy di ambienti virtualizzati per lab e produzione.</p>
        <div class="skill-tags">
          <span class="tag tag-green">AWS VPC</span>
          <span class="tag tag-green">Azure vNet</span>
          <span class="tag tag-green">GNS3</span>
          <span class="tag tag-green">EVE-NG</span>
        </div>
      </div>

      <div class="skill-card reveal">
        <div class="skill-icon">📶</div>
        <div class="skill-name">Wireless & SD-WAN</div>
        <p class="t-out" style="font-size:0.75rem;line-height:1.7">Progettazione di reti Wi-Fi enterprise e infrastrutture WAN software-defined.</p>
        <div class="skill-tags">
          <span class="tag tag-orange">Cisco Meraki</span>
          <span class="tag tag-orange">Aruba</span>
          <span class="tag tag-orange">SD-WAN</span>
          <span class="tag tag-orange">802.1X</span>
        </div>
      </div>

    </div>
  </div>
</section>

<!-- PROJECTS -->
<section id="projects">
  <div class="container">
    <div class="section-header reveal">
      <div class="section-label">// 02 — progetti</div>
      <h2 class="section-title">Casi studio</h2>
    </div>
    <div class="projects-list">

      <div class="project-card reveal">
        <div>
          <div class="project-num">PROGETTO 001</div>
          <div class="project-name">Redesign infrastruttura WAN aziendale</div>
          <div class="project-desc">
            Migrazione completa da WAN MPLS legacy a SD-WAN per un'azienda con 12 sedi distribuite sul territorio nazionale.
            Riduzione dei costi del 40% e latenza migliorata del 60% con failover automatico tra link ISP multipli.
          </div>
          <div class="project-meta">
            <div class="project-status">● COMPLETATO</div>
            <span>12 sedi</span>
            <span>•</span>
            <span>Cisco Viptela + BGP</span>
          </div>
          <div class="skill-tags" style="margin-top:14px">
            <span class="tag tag-blue">SD-WAN</span>
            <span class="tag tag-blue">BGP</span>
            <span class="tag tag-blue">QoS</span>
            <span class="tag tag-green">Ansible</span>
          </div>
        </div>
        <a href="#" class="project-link">GitHub →</a>
      </div>

      <div class="project-card reveal">
        <div>
          <div class="project-num">PROGETTO 002</div>
          <div class="project-name">Automazione provisioning con Ansible</div>
          <div class="project-desc">
            Sviluppo di playbook Ansible per il provisioning automatico di switch Cisco e Juniper.
            Riduzione del tempo di configurazione da 4 ore a 8 minuti per dispositivo, con zero errori manuali.
          </div>
          <div class="project-meta">
            <div class="project-status">● OPEN SOURCE</div>
            <span>200+ dispositivi</span>
            <span>•</span>
            <span>Python / Ansible</span>
          </div>
          <div class="skill-tags" style="margin-top:14px">
            <span class="tag tag-green">Ansible</span>
            <span class="tag tag-green">Python</span>
            <span class="tag tag-green">Netmiko</span>
            <span class="tag tag-blue">IOS-XE</span>
          </div>
        </div>
        <a href="#" class="project-link">GitHub →</a>
      </div>

      <div class="project-card reveal">
        <div>
          <div class="project-num">PROGETTO 003</div>
          <div class="project-name">Lab Enterprise: OSPF + BGP Multi-Area</div>
          <div class="project-desc">
            Lab virtualizzato su EVE-NG che replica un'infrastruttura enterprise completa con OSPF multi-area,
            BGP eBGP/iBGP, VRF-Lite per separazione traffico e policy di sicurezza avanzate.
          </div>
          <div class="project-meta">
            <div class="project-status" style="color:var(--accent)">● LAB</div>
            <span>EVE-NG</span>
            <span>•</span>
            <span>20+ router virtuali</span>
          </div>
          <div class="skill-tags" style="margin-top:14px">
            <span class="tag tag-blue">OSPF</span>
            <span class="tag tag-blue">BGP</span>
            <span class="tag tag-orange">VRF</span>
            <span class="tag tag-orange">ACL</span>
          </div>
        </div>
        <a href="#" class="project-link">GitHub →</a>
      </div>

    </div>
  </div>
</section>

<!-- CERTIFICATIONS -->
<section id="certifications">
  <div class="container">
    <div class="section-header reveal">
      <div class="section-label">// 03 — certificazioni</div>
      <h2 class="section-title">Qualifiche</h2>
    </div>
    <div class="certs-grid">

      <div class="cert-card reveal">
        <div class="cert-badge" style="background:rgba(0,212,255,0.08);border-color:rgba(0,212,255,0.2)">🏆</div>
        <div class="cert-name">CCNP Enterprise</div>
        <div class="cert-issuer">Cisco Systems</div>
        <div class="cert-year">2023</div>
      </div>

      <div class="cert-card reveal">
        <div class="cert-badge" style="background:rgba(0,255,136,0.08);border-color:rgba(0,255,136,0.2)">🎓</div>
        <div class="cert-name">CCNA</div>
        <div class="cert-issuer">Cisco Systems</div>
        <div class="cert-year">2021</div>
      </div>

      <div class="cert-card reveal">
        <div class="cert-badge" style="background:rgba(255,107,53,0.08);border-color:rgba(255,107,53,0.2)">🔐</div>
        <div class="cert-name">NSE 4 FortiGate</div>
        <div class="cert-issuer">Fortinet</div>
        <div class="cert-year">2022</div>
      </div>

      <div class="cert-card reveal">
        <div class="cert-badge" style="background:rgba(0,212,255,0.08);border-color:rgba(0,212,255,0.2)">☁️</div>
        <div class="cert-name">AWS SAA-C03</div>
        <div class="cert-issuer">Amazon Web Services</div>
        <div class="cert-year">2023</div>
      </div>

      <div class="cert-card reveal">
        <div class="cert-badge" style="background:rgba(0,255,136,0.08);border-color:rgba(0,255,136,0.2)">🛡️</div>
        <div class="cert-name">CompTIA Security+</div>
        <div class="cert-issuer">CompTIA</div>
        <div class="cert-year">2022</div>
      </div>

      <div class="cert-card reveal">
        <div class="cert-badge" style="background:rgba(255,107,53,0.08);border-color:rgba(255,107,53,0.2)">📶</div>
        <div class="cert-name">Aruba ACMA</div>
        <div class="cert-issuer">Aruba Networks</div>
        <div class="cert-year">2024</div>
      </div>

    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="container">
    <div class="contact-grid">
      <div>
        <div class="section-header reveal">
          <div class="section-label">// 04 — contatti</div>
          <h2 class="section-title">Parliamoci</h2>
        </div>
        <p class="contact-intro reveal">
          Sono disponibile per opportunità full-time, collaborazioni freelance o semplicemente per scambiare idee su infrastrutture di rete. Rispondoa in meno di 24 ore.
        </p>
        <div class="contact-links reveal">
          <a href="mailto:valerii.starko@email.com" class="contact-item">
            <span class="contact-icon">✉</span>
            valerii.starko@email.com
          </a>
          <a href="https://www.linkedin.com/in/valerii-starko-a12948152/" class="contact-item" target="_blank">
            <span class="contact-icon">in</span>
            linkedin.com/in/
          </a>
        </div>
      </div>

      <div class="stats-panel reveal">
        <div class="stats-header">
          <span>NETWORK_STATS.log</span>
          <span style="color:var(--accent2)">● LIVE</span>
        </div>
        <div class="stat-row">
          <span class="stat-label">Anni di esperienza</span>
          <span class="stat-value">2+</span>
        </div>
        <div class="bar-wrap"><div class="bar-fill" style="width:83%"></div></div>
        <div class="stat-row">
          <span class="stat-label">Progetti completati</span>
          <span class="stat-value green">28</span>
        </div>
        <div class="bar-wrap"><div class="bar-fill" style="width:70%"></div></div>
        <div class="stat-row">
          <span class="stat-label">Dispositivi gestiti</span>
          <span class="stat-value">500+</span>
        </div>
        <div class="bar-wrap"><div class="bar-fill" style="width:90%"></div></div>
        <div class="stat-row">
          <span class="stat-label">Uptime garantito</span>
          <span class="stat-value green">99.97%</span>
        </div>
        <div class="bar-wrap"><div class="bar-fill" style="width:99%"></div></div>
        <div class="stat-row">
          <span class="stat-label">Certificazioni attive</span>
          <span class="stat-value">6</span>
        </div>
        <div class="bar-wrap"><div class="bar-fill" style="width:60%"></div></div>
      </div>
    </div>
  </div>
</section>

<footer>
  <div>Valerii Starko — Network Specialist &nbsp;·&nbsp; Milano, Italia &nbsp;·&nbsp;</div>
  <div style="margin-top:6px;font-size:0.6rem">Built with HTML · CSS · JS · ☕</div>
</footer>

<div class="status-bar">
  <div class="status-item"><div class="status-dot"></div> sys.online</div>
  <div class="status-item"><div class="status-dot orange"></div> latency: 2ms</div>
  <div class="status-item">uptime: 99.97%</div>
  <div class="status-item">IPv4 · IPv6 ready</div>
</div>

<script>
  // ── NETWORK CANVAS ANIMATION ──
  const canvas = document.getElementById('net-canvas');
  const ctx = canvas.getContext('2d');
  let nodes = [], W, H;

  function resize() {
    W = canvas.width = window.innerWidth;
    H = canvas.height = window.innerHeight;
  }

  function initNodes() {
    nodes = [];
    const count = Math.floor((W * H) / 18000);
    for (let i = 0; i < count; i++) {
      nodes.push({
        x: Math.random() * W,
        y: Math.random() * H,
        vx: (Math.random() - 0.5) * 0.4,
        vy: (Math.random() - 0.5) * 0.4,
        r: Math.random() * 2 + 1
      });
    }
  }

  function draw() {
    ctx.clearRect(0, 0, W, H);
    const maxDist = 160;

    nodes.forEach(n => {
      n.x += n.vx; n.y += n.vy;
      if (n.x < 0 || n.x > W) n.vx *= -1;
      if (n.y < 0 || n.y > H) n.vy *= -1;

      ctx.beginPath();
      ctx.arc(n.x, n.y, n.r, 0, Math.PI * 2);
      ctx.fillStyle = '#00d4ff';
      ctx.fill();
    });

    for (let i = 0; i < nodes.length; i++) {
      for (let j = i + 1; j < nodes.length; j++) {
        const dx = nodes[i].x - nodes[j].x;
        const dy = nodes[i].y - nodes[j].y;
        const dist = Math.sqrt(dx*dx + dy*dy);
        if (dist < maxDist) {
          ctx.beginPath();
          ctx.moveTo(nodes[i].x, nodes[i].y);
          ctx.lineTo(nodes[j].x, nodes[j].y);
          ctx.strokeStyle = `rgba(0,212,255,${1 - dist/maxDist})`;
          ctx.lineWidth = 0.5;
          ctx.stroke();
        }
      }
    }

    requestAnimationFrame(draw);
  }

  window.addEventListener('resize', () => { resize(); initNodes(); });
  resize(); initNodes(); draw();

  // ── SCROLL REVEAL ──
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver(entries => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) {
        setTimeout(() => e.target.classList.add('visible'), i * 60);
        observer.unobserve(e.target);
      }
    });
  }, { threshold: 0.1 });

  reveals.forEach(el => observer.observe(el));

  // ── TERMINAL TYPEWRITER ──
  const lines = [
    { prompt: true, text: 'ping 8.8.8.8 -c 3' },
    { prompt: false, text: '64 bytes from 8.8.8.8: icmp_seq=1 time=1.8ms' },
    { prompt: false, text: '64 bytes from 8.8.8.8: icmp_seq=2 time=1.6ms' },
    { prompt: false, text: '64 bytes from 8.8.8.8: icmp_seq=3 time=1.9ms' },
  ];
</script>
</body>
</html>
