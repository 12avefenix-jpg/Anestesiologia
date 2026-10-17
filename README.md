<!DOCTYPE html>
<html lang="es" data-theme="dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Simulador Clínico: 4 Etapas del Dolor, Analgesia Multimodal e Intervencionismo</title>
  <style>
    :root {
      --bg-primary: #0f172a;
      --bg-secondary: #1e293b;
      --bg-tertiary: #334155;
      --text-primary: #f8fafc;
      --text-secondary: #cbd5e1;
      --text-muted: #94a3b8;
      --border-color: #334155;
      --accent-blue: #38bdf8;
      --accent-indigo: #818cf8;
      --status-red: #ef4444;
      --status-red-bg: rgba(239, 68, 68, 0.15);
      --status-yellow: #f59e0b;
      --status-yellow-bg: rgba(245, 158, 11, 0.15);
      --status-green: #10b981;
      --status-green-bg: rgba(16, 185, 129, 0.15);
      --card-radius: 14px;
      --shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.35);
    }

    [data-theme="light"] {
      --bg-primary: #f1f5f9;
      --bg-secondary: #ffffff;
      --bg-tertiary: #e2e8f0;
      --text-primary: #0f172a;
      --text-secondary: #334155;
      --text-muted: #64748b;
      --border-color: #cbd5e1;
      --accent-blue: #0284c7;
      --accent-indigo: #4f46e5;
      --status-red: #dc2626;
      --status-red-bg: rgba(220, 38, 38, 0.12);
      --status-yellow: #d97706;
      --status-yellow-bg: rgba(217, 119, 6, 0.12);
      --status-green: #059669;
      --status-green-bg: rgba(5, 150, 105, 0.12);
      --shadow: 0 8px 20px -4px rgba(15, 23, 42, 0.08);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
      background-color: var(--bg-primary);
      color: var(--text-primary);
      line-height: 1.5;
      padding: 20px;
      transition: background-color 0.25s ease, color 0.25s ease;
    }

    .container {
      max-width: 1380px;
      margin: 0 auto;
      display: flex;
      flex-direction: column;
      gap: 20px;
    }

    /* HEADER */
    .header {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
      gap: 16px;
      background: var(--bg-secondary);
      padding: 18px 24px;
      border-radius: var(--card-radius);
      border: 1px solid var(--border-color);
      box-shadow: var(--shadow);
    }

    .header-title h1 {
      font-size: 1.35rem;
      font-weight: 700;
      letter-spacing: -0.02em;
      display: flex;
      align-items: center;
      flex-wrap: wrap;
      gap: 10px;
    }

    .badge-specialty {
      font-size: 0.75rem;
      text-transform: uppercase;
      letter-spacing: 0.06em;
      padding: 4px 10px;
      border-radius: 999px;
      background: rgba(56, 189, 248, 0.15);
      color: var(--accent-blue);
      font-weight: 700;
    }

    .header-title p {
      color: var(--text-muted);
      font-size: 0.88rem;
      margin-top: 4px;
    }

    .header-actions {
      display: flex;
      gap: 8px;
      align-items: center;
      flex-wrap: wrap;
    }

    .btn {
      padding: 8px 13px;
      border-radius: 8px;
      border: 1px solid var(--border-color);
      background: var(--bg-tertiary);
      color: var(--text-primary);
      font-size: 0.82rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.2s ease;
    }

    .btn:hover {
      border-color: var(--accent-blue);
      transform: translateY(-1px);
    }

    .btn-primary {
      background: var(--accent-blue);
      color: #0f172a;
      border-color: transparent;
    }

    [data-theme="light"] .btn-primary {
      color: #ffffff;
    }

    /* KPI METRICS ROW */
    .kpi-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 16px;
    }

    .kpi-card {
      background: var(--bg-secondary);
      border: 1px solid var(--border-color);
      border-radius: var(--card-radius);
      padding: 16px 20px;
      box-shadow: var(--shadow);
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      gap: 8px;
    }

    .kpi-top {
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 0.78rem;
      color: var(--text-muted);
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.04em;
    }

    .kpi-value {
      font-size: 1.75rem;
      font-weight: 800;
      letter-spacing: -0.02em;
    }

    .kpi-badge {
      display: inline-block;
      padding: 3px 10px;
      border-radius: 999px;
      font-size: 0.72rem;
      font-weight: 700;
    }

    .status-critical {
      color: var(--status-red);
      background: var(--status-red-bg);
    }

    .status-moderate {
      color: var(--status-yellow);
      background: var(--status-yellow-bg);
    }

    .status-controlled {
      color: var(--status-green);
      background: var(--status-green-bg);
    }

    .kpi-subtext {
      font-size: 0.8rem;
      color: var(--text-secondary);
    }

    /* SVG DIAGRAM CONTAINER */
    .diagram-card {
      background: var(--bg-secondary);
      border: 1px solid var(--border-color);
      border-radius: var(--card-radius);
      padding: 20px;
      box-shadow: var(--shadow);
    }

    .section-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 14px;
      flex-wrap: wrap;
      gap: 10px;
    }

    .section-header h2 {
      font-size: 1.05rem;
      font-weight: 700;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .legend {
      display: flex;
      gap: 14px;
      font-size: 0.78rem;
      color: var(--text-muted);
      flex-wrap: wrap;
    }

    .legend-item {
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .legend-dot {
      width: 10px;
      height: 10px;
      border-radius: 50%;
    }

    .svg-wrapper {
      width: 100%;
      overflow-x: auto;
    }

    svg#pain-pathway-svg {
      width: 100%;
      height: auto;
      min-width: 860px;
      max-height: 310px;
      display: block;
      user-select: none;
    }

    .svg-node {
      cursor: pointer;
      transition: transform 0.2s ease;
    }

    .svg-node rect.node-box {
      fill: var(--bg-primary);
      stroke: var(--border-color);
      stroke-width: 2.5;
      rx: 12;
      transition: all 0.25s ease;
    }

    .svg-node.active rect.node-box {
      stroke: var(--accent-blue);
      stroke-width: 4;
      filter: drop-shadow(0 0 12px rgba(56, 189, 248, 0.35));
    }

    .svg-node:hover rect.node-box {
      stroke: var(--accent-blue);
    }

    .pulse-line {
      stroke-dasharray: 10 8;
      animation: flowPulse 1s linear infinite;
      transition: stroke 0.3s ease, stroke-width 0.3s ease, opacity 0.3s ease;
    }

    .descending-line {
      stroke-dasharray: 8 6;
      animation: flowDescending 1.4s linear infinite;
      transition: opacity 0.3s ease, stroke-width 0.3s ease;
    }

    @keyframes flowPulse {
      from { stroke-dashoffset: 36; }
      to { stroke-dashoffset: 0; }
    }

    @keyframes flowDescending {
      from { stroke-dashoffset: 0; }
      to { stroke-dashoffset: 28; }
    }

    /* MAIN SIMULATION GRID: CONTROLS + STAGE DETAIL */
    .main-grid {
      display: grid;
      grid-template-columns: 1.2fr 1fr;
      gap: 20px;
    }

    @media (max-width: 1080px) {
      .main-grid {
        grid-template-columns: 1fr;
      }
    }

    .panel-card {
      background: var(--bg-secondary);
      border: 1px solid var(--border-color);
      border-radius: var(--card-radius);
      padding: 20px;
      box-shadow: var(--shadow);
      display: flex;
      flex-direction: column;
      gap: 16px;
    }

    /* DRUG CONTROLS GRID */
    .drugs-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
      gap: 12px;
    }

    .drug-card {
      background: var(--bg-primary);
      border: 1px solid var(--border-color);
      border-radius: 10px;
      padding: 12px 14px;
      cursor: pointer;
      transition: all 0.2s ease;
      display: flex;
      flex-direction: column;
      gap: 8px;
      position: relative;
    }

    .drug-card:hover {
      border-color: var(--accent-blue);
    }

    .drug-card.active {
      border-color: var(--status-green);
      background: var(--status-green-bg);
    }

    .drug-header {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      gap: 8px;
    }

    .drug-name {
      font-weight: 700;
      font-size: 0.9rem;
      color: var(--text-primary);
    }

    .drug-dose {
      font-size: 0.74rem;
      color: var(--accent-blue);
      font-weight: 600;
    }

    .toggle-pill {
      width: 38px;
      height: 20px;
      border-radius: 999px;
      background: var(--bg-tertiary);
      position: relative;
      flex-shrink: 0;
      transition: background 0.2s ease;
    }

    .toggle-pill::after {
      content: "";
      width: 14px;
      height: 14px;
      border-radius: 50%;
      background: var(--text-primary);
      position: absolute;
      top: 3px;
      left: 3px;
      transition: transform 0.2s ease;
    }

    .drug-card.active .toggle-pill {
      background: var(--status-green);
    }

    .drug-card.active .toggle-pill::after {
      transform: translateX(18px);
      background: #ffffff;
    }

    .drug-stages {
      display: flex;
      flex-wrap: wrap;
      gap: 5px;
    }

    .stage-pill {
      font-size: 0.68rem;
      font-weight: 700;
      padding: 2px 7px;
      border-radius: 6px;
      background: var(--bg-tertiary);
      color: var(--text-secondary);
    }

    .stage-pill.s1 { border-left: 3px solid #f97316; }
    .stage-pill.s2 { border-left: 3px solid #eab308; }
    .stage-pill.s3 { border-left: 3px solid #8b5cf6; }
    .stage-pill.s4 { border-left: 3px solid #ec4899; }

    .drug-mech {
      font-size: 0.76rem;
      color: var(--text-secondary);
      line-height: 1.35;
    }

    /* STAGE DETAIL PANEL */
    .stage-nav {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 10px;
      padding-bottom: 12px;
      border-bottom: 1px solid var(--border-color);
    }

    .stage-title-wrap h3 {
      font-size: 1.15rem;
      font-weight: 800;
      color: var(--accent-blue);
    }

    .stage-title-wrap span {
      font-size: 0.78rem;
      color: var(--text-muted);
      font-weight: 700;
    }

    .detail-block {
      background: var(--bg-primary);
      border: 1px solid var(--border-color);
      border-radius: 10px;
      padding: 13px 15px;
    }

    .detail-block h4 {
      font-size: 0.76rem;
      text-transform: uppercase;
      letter-spacing: 0.05em;
      color: var(--accent-blue);
      margin-bottom: 6px;
    }

    .detail-block p {
      font-size: 0.86rem;
      color: var(--text-primary);
      line-height: 1.45;
    }

    .mediators-list {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
      margin-top: 6px;
    }

    .mediator-tag {
      font-size: 0.75rem;
      padding: 3px 9px;
      border-radius: 6px;
      background: var(--bg-secondary);
      border: 1px solid var(--border-color);
      font-weight: 600;
    }

    .stage-drugs-list {
      display: flex;
      flex-direction: column;
      gap: 8px;
      margin-top: 8px;
    }

    .stage-drug-item {
      display: flex;
      flex-direction: column;
      gap: 4px;
      padding: 9px 12px;
      border-radius: 8px;
      background: var(--bg-secondary);
      border: 1px solid var(--border-color);
      font-size: 0.81rem;
    }

    .stage-drug-item.is-active {
      border-color: var(--status-green);
      background: var(--status-green-bg);
    }

    .stage-drug-top {
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-weight: 700;
    }

    .feedback-banner {
      padding: 13px 16px;
      border-radius: 10px;
      border-left: 4px solid var(--accent-blue);
      background: var(--bg-primary);
      font-size: 0.84rem;
      line-height: 1.45;
    }

    /* FIBER COMPARISON TABLE */
    .fiber-table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 8px;
      font-size: 0.78rem;
    }

    .fiber-table th, .fiber-table td {
      border: 1px solid var(--border-color);
      padding: 6px 8px;
      text-align: left;
    }

    .fiber-table th {
      background: var(--bg-secondary);
      color: var(--accent-blue);
      font-weight: 700;
    }

    .bib-footer {
      background: var(--bg-secondary);
      border: 1px solid var(--border-color);
      border-radius: var(--card-radius);
      padding: 14px 20px;
      font-size: 0.78rem;
      color: var(--text-muted);
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      gap: 10px;
    }
  </style>
</head>
<body>
  <div class="container">
    <!-- HEADER -->
    <header class="header">
      <div class="header-title">
        <h1>
          <span>🧠 Simulador de la Vía Nociceptiva, Analgesia Multimodal e Intervencionismo</span>
          <span class="badge-specialty">Dr. Alan Michel Laureano Hernández • Algología</span>
        </h1>
        <p>Basado en el Cuaderno de Algología para Karime (<em>Principles &amp; Practice of Pain Medicine</em> / <em>Longnecker's Anesthesiology</em>).</p>
      </div>
      <div class="header-actions">
        <button class="btn" id="btn-reset">🔄 Sin Analgesia</button>
        <button class="btn" id="btn-basic">💊 AINE + Paracetamol</button>
        <button class="btn" id="btn-interventional">🎯 Bloqueo US + Epidural</button>
        <button class="btn btn-primary" id="btn-multimodal">✨ Multimodal Total</button>
        <button class="btn" id="btn-theme">☀️ / 🌙 Tema</button>
      </div>
    </header>

    <!-- KPI ROW -->
    <section class="kpi-grid">
      <div class="kpi-card">
        <div class="kpi-top">
          <span>Impulso Cortical (Percepción)</span>
          <span id="kpi-pain-badge" class="kpi-badge status-critical">DOLOR SEVERO</span>
        </div>
        <div class="kpi-value" id="kpi-pain-value">100% (EVA 10/10)</div>
        <div class="kpi-subtext" id="kpi-pain-sub">Vías espinotalámica (S1/S2) y espinorreticular (límbica) íntegras.</div>
      </div>

      <div class="kpi-card">
        <div class="kpi-top">
          <span>Sensibilización Central (Wind-up)</span>
          <span id="kpi-windup-badge" class="kpi-badge status-critical">ALTO RIESGO</span>
        </div>
        <div class="kpi-value" id="kpi-windup-value">95%</div>
        <div class="kpi-subtext" id="kpi-windup-sub">Co-activación NK-1 (Sustancia P) + NMDA y alodinia por fibras Aβ.</div>
      </div>

      <div class="kpi-card">
        <div class="kpi-top">
          <span>Respuesta Reticular / Hipotalámica</span>
          <span id="kpi-hemo-badge" class="kpi-badge status-critical">TAQUICARDIA / HTA</span>
        </div>
        <div class="kpi-value" id="kpi-hemo-value">118 lpm | 164/98</div>
        <div class="kpi-subtext" id="kpi-hemo-sub">Activación neuroendocrina y autonómica vía formación reticular.</div>
      </div>

      <div class="kpi-card">
        <div class="kpi-top">
          <span>Sinergia Multimodal</span>
          <span id="kpi-multi-badge" class="kpi-badge status-critical">0 / 4 ETAPAS</span>
        </div>
        <div class="kpi-value" id="kpi-multi-value">Sin cobertura</div>
        <div class="kpi-subtext" id="kpi-multi-sub">Combina fármacos, bloqueos guiados por imagen y psicoterapia.</div>
      </div>
    </section>

    <!-- INTERACTIVE SVG DIAGRAM -->
    <section class="diagram-card">
      <div class="section-header">
        <h2>⚡ Mapa Interactivo de las 4 Etapas de la Nocicepción (Haz clic en cualquier etapa para inspeccionar)</h2>
        <div class="legend">
          <div class="legend-item">
            <span class="legend-dot" style="background: #ef4444;"></span> Impulso Nociceptivo Alto
          </div>
          <div class="legend-item">
            <span class="legend-dot" style="background: #f59e0b;"></span> Impulso Atenuado
          </div>
          <div class="legend-item">
            <span class="legend-dot" style="background: #10b981;"></span> Etapa Controlada / Bloqueada
          </div>
          <div class="legend-item">
            <span class="legend-dot" style="background: #38bdf8;"></span> Vía Inhibitoria Descendente (SGPA / RVM: NA, 5-HT, Encefalinas)
          </div>
        </div>
      </div>

      <div class="svg-wrapper">
        <svg id="pain-pathway-svg" viewBox="0 0 1120 290" xmlns="http://www.w3.org/2000/svg">
          <defs>
            <marker id="arrow-cyan" viewBox="0 0 10 10" refX="7" refY="5" markerWidth="6" markerHeight="6" orient="auto-start-reverse">
              <path d="M 0 1 L 10 5 L 0 9 z" fill="#38bdf8" />
            </marker>
          </defs>

          <!-- VÍA INHIBITORIA DESCENDENTE (Curva superior de Etapa 4 a Etapa 3) -->
          <path id="svg-descending-path"
                d="M 940 60 C 860 10, 720 10, 650 60"
                fill="none"
                stroke="#38bdf8"
                stroke-width="3"
                opacity="0.25"
                class="descending-line"
                marker-end="url(#arrow-cyan)" />
          <text id="svg-descending-label" x="795" y="24" text-anchor="middle" fill="#38bdf8" font-size="11" font-weight="700" opacity="0.55">
            Vía Inhibitoria Descendente (SGPA + Médula Ventromedial Rostral: NA, 5-HT, Opioides Endógenos)
          </text>

          <!-- CONECTORES ASCENDENTES ENTRE NODOS -->
          <line id="conn-1-2" x1="235" y1="145" x2="305" y2="145" stroke="#ef4444" stroke-width="6" class="pulse-line" />
          <text id="conn-label-1" x="270" y="130" text-anchor="middle" fill="#94a3b8" font-size="11" font-weight="700">100%</text>

          <line id="conn-2-3" x1="515" y1="145" x2="585" y2="145" stroke="#ef4444" stroke-width="6" class="pulse-line" />
          <text id="conn-label-2" x="550" y="130" text-anchor="middle" fill="#94a3b8" font-size="11" font-weight="700">100%</text>

          <line id="conn-3-4" x1="795" y1="145" x2="865" y2="145" stroke="#ef4444" stroke-width="6" class="pulse-line" />
          <text id="conn-label-3" x="830" y="130" text-anchor="middle" fill="#94a3b8" font-size="11" font-weight="700">100%</text>

          <!-- NODO 1: TRANSDUCCIÓN -->
          <g class="svg-node active" id="node-1" onclick="selectStage(1)">
            <rect class="node-box" x="25" y="65" width="210" height="175" />
            <rect x="25" y="65" width="210" height="8" rx="4" fill="#f97316" />
            <text x="40" y="95" fill="#f97316" font-size="11.5" font-weight="800">ETAPA 1 • NOCICEPTORES</text>
            <text x="40" y="116" fill="currentColor" font-size="15.5" font-weight="800">1. Transducción</text>
            <text x="40" y="135" fill="#94a3b8" font-size="10.8">Terminales libres Aδ y C polimorfas</text>
            <rect id="badge-bg-1" x="40" y="148" width="180" height="24" rx="6" fill="rgba(239,68,68,0.15)" />
            <text id="badge-txt-1" x="130" y="164" text-anchor="middle" fill="#ef4444" font-size="10.5" font-weight="700">SEÑAL GENERADA: 100%</text>
            <text id="drugs-txt-1" x="40" y="194" fill="#38bdf8" font-size="10" font-weight="600">Intervención activa: Ninguna</text>
            <text id="drugs-txt-1b" x="40" y="210" fill="#38bdf8" font-size="10" font-weight="600"></text>
          </g>

          <!-- NODO 2: TRANSMISIÓN -->
          <g class="svg-node" id="node-2" onclick="selectStage(2)">
            <rect class="node-box" x="305" y="65" width="210" height="175" />
            <rect x="305" y="65" width="210" height="8" rx="4" fill="#eab308" />
            <text x="320" y="95" fill="#eab308" font-size="11.5" font-weight="800">ETAPA 2 • AXONAL Y TRACTOS</text>
            <text x="320" y="116" fill="currentColor" font-size="15.5" font-weight="800">2. Transmisión</text>
            <text x="320" y="135" fill="#94a3b8" font-size="10.8">Aδ (5-15 m/s) y C (&lt;2 m/s) → GRD</text>
            <rect id="badge-bg-2" x="320" y="148" width="180" height="24" rx="6" fill="rgba(239,68,68,0.15)" />
            <text id="badge-txt-2" x="410" y="164" text-anchor="middle" fill="#ef4444" font-size="10.5" font-weight="700">CONDUCCIÓN: 100%</text>
            <text id="drugs-txt-2" x="320" y="194" fill="#38bdf8" font-size="10" font-weight="600">Intervención activa: Ninguna</text>
            <text id="drugs-txt-2b" x="320" y="210" fill="#38bdf8" font-size="10" font-weight="600"></text>
          </g>

          <!-- NODO 3: MODULACIÓN -->
          <g class="svg-node" id="node-3" onclick="selectStage(3)">
            <rect class="node-box" x="585" y="65" width="210" height="175" />
            <rect x="585" y="65" width="210" height="8" rx="4" fill="#8b5cf6" />
            <text x="600" y="95" fill="#8b5cf6" font-size="11.5" font-weight="800">ETAPA 3 • ASTA DORSAL</text>
            <text x="600" y="116" fill="currentColor" font-size="15.5" font-weight="800">3. Modulación</text>
            <text x="600" y="135" fill="#94a3b8" font-size="10.8">Láminas I, IIo, V, X (NK-1, NMDA)</text>
            <rect id="badge-bg-3" x="600" y="148" width="180" height="24" rx="6" fill="rgba(239,68,68,0.15)" />
            <text id="badge-txt-3" x="690" y="164" text-anchor="middle" fill="#ef4444" font-size="10.5" font-weight="700">SALIDA ESPINAL: 100%</text>
            <text id="drugs-txt-3" x="600" y="194" fill="#38bdf8" font-size="10" font-weight="600">Intervención activa: Ninguna</text>
            <text id="drugs-txt-3b" x="600" y="210" fill="#38bdf8" font-size="10" font-weight="600"></text>
          </g>

          <!-- NODO 4: PERCEPCIÓN Y EXPRESIÓN -->
          <g class="svg-node" id="node-4" onclick="selectStage(4)">
            <rect class="node-box" x="865" y="65" width="230" height="175" />
            <rect x="865" y="65" width="230" height="8" rx="4" fill="#ec4899" />
            <text x="880" y="95" fill="#ec4899" font-size="11.5" font-weight="800">ETAPA 4 • SUPRAESPINAL</text>
            <text x="880" y="116" fill="currentColor" font-size="15.5" font-weight="800">4. Percepción</text>
            <text x="880" y="135" fill="#94a3b8" font-size="10.8">Tálamo, S1/S2, Cíngulo Anterior, Reticular</text>
            <rect id="badge-bg-4" x="880" y="148" width="200" height="24" rx="6" fill="rgba(239,68,68,0.15)" />
            <text id="badge-txt-4" x="980" y="164" text-anchor="middle" fill="#ef4444" font-size="10.5" font-weight="700">PERCEPCIÓN FINAL: 100%</text>
            <text id="drugs-txt-4" x="880" y="194" fill="#38bdf8" font-size="10" font-weight="600">Intervención activa: Ninguna</text>
            <text id="drugs-txt-4b" x="880" y="210" fill="#38bdf8" font-size="10" font-weight="600"></text>
          </g>
        </svg>
      </div>
    </section>

    <!-- MAIN GRID: PHARMACOLOGY PANEL + STAGE INSPECTOR -->
    <section class="main-grid">
      <!-- LEFT: MEDICATION & INTERVENTION SWITCHES -->
      <div class="panel-card">
        <div class="section-header" style="margin-bottom: 4px;">
          <h2>💉 Arsenal Multimodal: Farmacología, Intervencionismo y Psicología</h2>
          <span style="font-size: 0.78rem; color: var(--text-muted);">Haz clic para activar/desactivar modalidades</span>
        </div>

        <div class="drugs-grid" id="drugs-container"></div>

        <div class="feedback-banner" id="clinical-pearl-box"></div>
      </div>

      <!-- RIGHT: DETAILED STAGE CARD -->
      <div class="panel-card">
        <div class="stage-nav">
          <button class="btn" onclick="prevStage()">◀ Etapa Anterior</button>
          <div class="stage-title-wrap" style="text-align: center;">
            <span id="detail-stage-badge">ETAPA 1 DE 4</span>
            <h3 id="detail-stage-title">1. Transducción</h3>
          </div>
          <button class="btn" onclick="nextStage()">Siguiente Etapa ▶</button>
        </div>

        <div class="detail-block">
          <h4>📍 Neuroanatomía y Clasificación (Cuaderno de Algología)</h4>
          <p id="detail-anatomy"></p>
          <div id="detail-extra-table"></div>
        </div>

        <div class="detail-block">
          <h4>🧬 Mediadores Bioquímicos, Receptores y Vías</h4>
          <div class="mediators-list" id="detail-mediators"></div>
        </div>

        <div class="detail-block">
          <h4>⚙️ Fisiopatología y Procesamiento Nociceptivo</h4>
          <p id="detail-physiology"></p>
        </div>

        <div class="detail-block">
          <h4>🎯 Efecto de las Intervenciones Seleccionadas en esta Etapa</h4>
          <div class="stage-drugs-list" id="detail-stage-drugs"></div>
        </div>
      </div>
    </section>

    <footer class="bib-footer">
      <div><strong>Fuentes Bibliográficas (Cuaderno de Algología para Karime):</strong> Bajwa ZH, Wootton RJ, Warfield CA. <em>Principles and Practice of Pain Medicine</em>, 3e (McGraw-Hill) • Longnecker DE, Mackey SC, et al. <em>Anesthesiology</em>, 3e (Cap. 8, 86, 92, 133).</div>
      <div>Educación Médica Basada en Simulación • Anestesiología y Algología</div>
    </footer>
  </div>

  <script>
    // =========================================================================
    // 1. BASE DE DATOS DE MODALIDADES TERAPÉUTICAS (FARMACOLOGÍA, BLOQUEOS Y PSICOLOGÍA)
    // =========================================================================
    const DRUGS = [
      {
        id: "diclofenaco",
        name: "Diclofenaco / AINE COX",
        dose: "75 mg IV",
        category: "Inhibidor COX-1 y COX-2",
        active: false,
        stages: [1, 3],
        effects: { 1: 35, 2: 0, 3: 12, 4: 0 },
        descendingBoost: 0,
        shortMech: "Inhibe síntesis de prostaglandinas periféricas y espinales, frenando la sensibilización de nociceptores Aδ y C polimorfos.",
        stageDetails: {
          1: "Reduce la síntesis de PGE₂ en el tejido lesionado, elevando nuevamente el umbral de activación de los nociceptores mecánicos y térmicos Aδ y C para prevenir la sensibilización periférica.",
          3: "Disminuye la producción de prostanoides inducida por inflamación glial en el asta dorsal medular."
        }
      },
      {
        id: "dexametasona",
        name: "Dexametasona / Esteroide",
        dose: "4 – 8 mg IV / Perineural",
        category: "Glucocorticoide / Antiinflamatorio",
        active: false,
        stages: [1, 2, 3],
        effects: { 1: 30, 2: 20, 3: 10, 4: 0 },
        descendingBoost: 0,
        shortMech: "Inhibe fosfolipasa A₂, TNF-α e inflamación radicular/perineural; suprime descargas ectópicas en fibras C sensibilizadas.",
        stageDetails: {
          1: "Bloquea la cascada inflamatoria (TNF-α, especies reactivas de oxígeno y prostanoides) evitando que estímulos inocuos activen fibras Aα/Aβ (alodinia).",
          2: "Reduce la inflamación intensa de las raíces nerviosas (p. ej. por extrusión del núcleo pulposo hacia el nervio sinuvertebral y raíz posterolateral) y frena focos ectópicos de transmisión efáptica.",
          3: "Atenúa la activación de células gliales e inmunes circundantes en el sistema nervioso central."
        }
      },
      {
        id: "metamizol",
        name: "Metamizol (Dipirona)",
        dose: "1 – 2 g IV",
        category: "Pirazolona no opioide",
        active: false,
        stages: [1, 3, 4],
        effects: { 1: 24, 2: 0, 3: 18, 4: 10 },
        descendingBoost: 15,
        shortMech: "Abre canales de K⁺ vía NO-GMPc periféricos, inhibe COX central y estimula liberación de opioides endógenos en SGPA.",
        stageDetails: {
          1: "Hiperpolariza las terminaciones nerviosas libres de las fibras Aδ y C mediante la vía L-arginina-NO-GMPc.",
          3: "Reduce la transmisión excitatoria en la sustancia gelatinosa del asta dorsal.",
          4: "Coopera en la activación de la Sustancia Gris Periacueductal (SGPA) reforzando la inhibición descendente."
        }
      },
      {
        id: "bloqueo_pnb",
        name: "Bloqueo Nervioso Guiado por US",
        dose: "Anestésico Local Perineural",
        category: "Intervencionismo Ecoguiado",
        active: false,
        stages: [1, 2],
        effects: { 1: 25, 2: 75, 3: 0, 4: 0 },
        descendingBoost: 0,
        shortMech: "Visualización directa por ultrasonido de tejidos blandos, vasos y nervios: bloquea la conducción axonal de fibras Aδ y C.",
        stageDetails: {
          1: "Suprime la transducción de mecanorreceptores de alto umbral y nociceptores libres en el territorio inervado.",
          2: "Interrumpe directamente la propagación del potencial de acción en axones Aδ (5–15 m/s) y C (<2 m/s) hacia el ganglio de la raíz dorsal (GRD), disminuyendo requerimiento de opioides, NVPO y estancia hospitalaria."
        }
      },
      {
        id: "epidural_tf",
        name: "Inyección Epidural / Transforaminal",
        dose: "Fluoroscopia + Contraste",
        category: "Intervencionismo Espinal",
        active: false,
        stages: [2, 3],
        effects: { 1: 0, 2: 55, 3: 45, 4: 0 },
        descendingBoost: 10,
        shortMech: "Abordaje interlaminar, transforaminal o caudal guiado por imagen sobre el GRD y raíces dorsales/ventrales.",
        stageDetails: {
          2: "Deposita esteroide y anestésico local con precisión anatómica en el foramen intervertebral (junto al GRD) o espacio epidural, frenando el dolor radicular secundario a hernia discal o estenosis espinal.",
          3: "Modula directamente la entrada de aferentes primarias por el tracto de Lissauer hacia las láminas I, IIo y V del asta dorsal."
        }
      },
      {
        id: "paracetamol",
        name: "Paracetamol",
        dose: "1 g IV",
        category: "Analgésico Central No Opioide",
        active: false,
        stages: [3, 4],
        effects: { 1: 5, 2: 0, 3: 24, 4: 20 },
        descendingBoost: 25,
        shortMech: "Actúa a nivel central potenciando las vías inhibitorias descendentes serotoninérgicas (5-HT) y endocannabinoides.",
        stageDetails: {
          3: "Refuerza la modulación inhibitoria descendente desde la médula ventromedial rostral hacia el asta dorsal espinal.",
          4: "Modula el procesamiento central en tálamo e hipotálamo sin efecto antiinflamatorio periférico significativo."
        }
      },
      {
        id: "tramadol",
        name: "Tramadol",
        dose: "50 – 100 mg IV",
        category: "Opioide Atípico Dual (μ + NA/5-HT)",
        active: false,
        stages: [3, 4],
        effects: { 1: 0, 2: 5, 3: 42, 4: 28 },
        descendingBoost: 45,
        shortMech: "Agonista μ-opioide + inhibidor de la recaptación de Noradrenalina (NA) y Serotonina (5-HT) en la vía descendente.",
        stageDetails: {
          3: "Doble freno en el asta dorsal: activa receptores opioides e incrementa la concentración sináptica de noradrenalina y serotonina provenientes de la vía inhibitoria descendente (SGPA y médula ventromedial rostral).",
          4: "Atenúa la transmisión hacia la formación reticular y corteza somatosensorial/límbica."
        }
      },
      {
        id: "morfina",
        name: "Morfina / Opioide μ",
        dose: "Titulación IV o Neuroaxial",
        category: "Agonista Opioide Puro",
        active: false,
        stages: [2, 3, 4],
        effects: { 1: 0, 2: 15, 3: 60, 4: 55 },
        descendingBoost: 55,
        shortMech: "Inhibe de forma dosis-dependiente las fibras C polimorfas y mecanorreceptores en sustancia gelatinosa y modula la formación reticular.",
        stageDetails: {
          2: "Atenúa la conducción de aferentes primarias nociceptivas en su ingreso espinal.",
          3: "Inhibe de manera dosis-dependiente las fibras C polimorfas termosensibles y mecanorreceptores en el asta dorsal, frenando la liberación de Sustancia P y Neurocinina A en la sustancia gelatinosa.",
          4: "Actúa en la SGPA, médula ventromedial rostral, tálamo medial y formación reticular; como propuso Casey, alivia el componente afectivo de sufrimiento sin abolir la capacidad de reconocer el estímulo."
        }
      },
      {
        id: "ketamina",
        name: "Ketamina / Antagonista NK-1-NMDA",
        dose: "0.15 – 0.3 mg/kg IV",
        category: "Antagonista Receptor NMDA / Anti-Wind-up",
        active: false,
        stages: [3, 4],
        effects: { 1: 0, 2: 0, 3: 55, 4: 30 },
        descendingBoost: 15,
        shortMech: "Frena el fenómeno de 'Wind-up' (sensibilización central) mediado por receptores NMDA, NK-1 y mGlu en el asta dorsal.",
        stageDetails: {
          3: "Bloquea la cascada de sensibilización central ('wind-up') donde la liberación de Sustancia P (receptor NK-1) y Neurocinina A (NK-2) potencia a los receptores NMDA y mGlu acoplados a fosfolipasa C, evitando el aumento en amplitud y duración de las señales hacia el SNC.",
          4: "Disminuye la hiperactividad talamocortical y la amplificación afectivo-motivacional en la corteza cingulada anterior e ínsula."
        }
      },
      {
        id: "psicoterapia",
        name: "CBT / ACT / Mindfulness (MBSR)",
        dose: "Intervención Conductual",
        category: "Psicología del Dolor y Biofeedback",
        active: false,
        stages: [3, 4],
        effects: { 1: 0, 2: 0, 3: 15, 4: 42 },
        descendingBoost: 30,
        shortMech: "Reduce la catastrofización (escala PCS: rumiación, magnificación, indefensión), ansiedad y respuesta autonómica simpática.",
        stageDetails: {
          3: "El control cognitivo y la relajación diafragmática refuerzan las vías inhibitorias descendentes supraespinales hacia el asta dorsal.",
          4: "Desacopla los aspectos físicos y psicológicos del dolor (MBSR de Kabat-Zinn, CBT y ACT), reduciendo la hipervigilancia, la conducta de evitación por miedo y modulando la frecuencia cardiaca, respiratoria y tensión muscular."
        }
      }
    ];

    // =========================================================================
    // 2. INFORMACIÓN DETALLADA DE LAS 4 ETAPAS (CUADERNO DE ALGOLOGÍA)
    // =========================================================================
    const STAGES_INFO = {
      1: {
        badge: "ETAPA 1 DE 4 • PERIFERIA",
        title: "1. Transducción (Nociceptores Periféricos)",
        anatomy: "Terminaciones nerviosas libres de aferentes primarias Aδ (mielinizadas delgadas) y fibras C (amielínicas) localizadas en piel, músculo, fascia, tendones, articulaciones facetarias y anillo fibroso (nervio sinuvertebral). Según la clasificación de Erlanger-Gasser, mientras los mecanorreceptores terminan en estructuras especializadas, los nociceptores poseen terminaciones libres.",
        mediators: [
          "Fibras Aδ (Mecanotérmicas)",
          "Fibras C Polimorfas",
          "Fibras Aα y Aβ (Alodinia)",
          "TNF-α y Especies Reactivas de O₂",
          "Prostaglandinas y Bradicinina",
          "Isquemia / Contracción Muscular"
        ],
        physiology: "Los nociceptores detectan estímulos térmicos, mecánicos y químicos intensos y los transforman en señales eléctricas. Las fibras Aδ median el 'primer dolor' (rápido, agudo, bien localizado o epicrítico), mientras que las fibras C polimorfas median el 'segundo dolor' (lento, urente, sordo y difuso o protopático). Cuando ocurre sensibilización periférica por inflamación o lesión tisular, los mecanorreceptores Aδ de alto umbral disminuyen su umbral y la información dolorosa también es transportada por fibras Aα y Aβ, manifestándose clínicamente como alodinia."
      },
      2: {
        badge: "ETAPA 2 DE 4 • CONDUCCIÓN AXONAL Y TRACTOS",
        title: "2. Transmisión (Nervio Periférico, GRD y Vías Ascendentes)",
        anatomy: "Los axones de las fibras Aδ (diámetro 2–5 µm, velocidad 5–15 m/s) y fibras C (<2 µm, velocidad <2 m/s) tienen sus somas en el Ganglio de la Raíz Dorsal (GRD) e ingresan a la médula espinal. De ahí ascienden por el cuadrante ventrolateral contralateral a través de dos vías principales: el Tracto Espinotalámico (STT) y el Tracto Espinorreticular (SRT), además de proyecciones a la región parabraquial.",
        mediators: [
          "Ganglio de la Raíz Dorsal (GRD)",
          "Tracto de Lissauer",
          "Tracto Espinotalámico (Localización)",
          "Tracto Espinorreticular (Afectivo)",
          "Focos Ectópicos / Transmisión Efáptica",
          "Nervio Sinuvertebral (Disco)"
        ],
        physiology: "La neurona aferente primaria conduce el impulso hasta el asta dorsal. Las neuronas de segundo orden decusan a pocos segmentos de su entrada y ascienden por el Tracto Espinotalámico hacia el tálamo ventrobasal/lateral (preservando la somatotopía para el componente sensorial-discriminativo) y por el Tracto Espinorreticular hacia la formación reticular del tallo, tálamo medial e hipotálamo (componente afectivo-motivacional). En lesiones nerviosas periféricas o radiculopatías por hernia discal, pueden formarse neuromas y focos de sensibilidad anormal con transmisión efáptica."
      },
      3: {
        badge: "ETAPA 3 DE 4 • MÉDULA ESPINAL",
        title: "3. Modulación y Fenómeno de 'Wind-up' (Asta Dorsal)",
        anatomy: "Asta dorsal de la médula espinal: las fibras Aδ terminan en las láminas I y IIo (con colaterales a las láminas V y X), mientras que las fibras C ingresan por el aspecto lateral del tracto de Lissauer hacia la sustancia gelatinosa (lámina II). Recibe proyecciones descendentes desde la Sustancia Gris Periacueductal (SGPA) en el mesencéfalo y la Médula Ventromedial Rostral (RVM).",
        mediators: [
          "Sustancia P → Receptor NK-1",
          "Neurocinina A (NKA) → Receptor NK-2",
          "Receptor NMDA (Glutamato)",
          "Receptores mGlu → Fosfolipasa C (↑Ca²⁺)",
          "Somatostatina (Estímulo Térmico)",
          "Noradrenalina, Serotonina (5-HT) y Encefalinas",
          "Células Gliales e Inmunes"
        ],
        physiology: "La modulación cambia o inhibe la transmisión de impulsos en la médula espinal mediante vías excitatorias o inhibitorias. La estimulación de fibras C libera Sustancia P y Neurocinina A en la sustancia gelatinosa, activando receptores NK-1 y NK-2. Los receptores NK-1 fortalecen la acción sensibilizadora de los receptores NMDA, mientras que los receptores mGlu acoplados a fosfolipasa C elevan el Ca²⁺ intracelular. Esto incrementa la amplitud y duración de las señales que ingresan al SNC, fenómeno conocido como 'Wind-up' o sensibilización central."
      },
      4: {
        badge: "ETAPA 4 DE 4 • PROCESAMIENTO SUPRAESPINAL",
        title: "4. Percepción, Expresión Autonómica y Psicología del Dolor",
        anatomy: "Tálamo (núcleos ventrobasal/lateral con organización somatotópica y núcleos mediales/intralaminares sin somatotopía), Corteza Somatosensorial (S1/S2), Formación Reticular, Hipotálamo y Sistema Límbico (corteza cingulada anterior, ínsula, amígdala, hipocampo, núcleo accumbens, área tegmental ventral y núcleos del rafe).",
        mediators: [
          "Componente Sensorial-Discriminativo (Tálamo Lateral → S1/S2)",
          "Componente Afectivo-Motivacional (Tálamo Medial → Cíngulo/Ínsula)",
          "Hipotálamo (Respuesta Autonómica y Neuroendocrina)",
          "Formación Reticular (Respuesta Motora y Aversiva)",
          "Catastrofización (Escala PCS: Rumiación, Magnificación, Indefensión)"
        ],
        physiology: "La percepción es el resultado final donde el dolor se convierte en una experiencia consciente multidimensional (sensorial y emocional). La corteza somatosensorial identifica intensidad, tipo y localización; el sistema límbico genera la respuesta emocional y conductual; y el sistema reticular e hipotalámico median la activación autonómica (taquicardia, hipertensión) y neuroendocrina. Factores psicológicos como la catastrofización del dolor (evaluada con la escala PCS de 13 ítems) y la ansiedad impiden desengancharse de las señales dolorosas, amplificando la percepción y el riesgo de discapacidad."
      }
    };

    let currentStage = 1;

    // =========================================================================
    // 3. RENDERIZADO DE CONTROLES FARMACOLÓGICOS E INTERVENCIONISTAS
    // =========================================================================
    function renderDrugs() {
      const container = document.getElementById("drugs-container");
      container.innerHTML = "";

      DRUGS.forEach(drug => {
        const card = document.createElement("div");
        card.className = `drug-card ${drug.active ? "active" : ""}`;
        card.onclick = () => toggleDrug(drug.id);

        const stagePills = drug.stages.map(s => {
          const names = { 1: "E1: Transducción", 2: "E2: Transmisión", 3: "E3: Modulación", 4: "E4: Percepción" };
          return `<span class="stage-pill s${s}">${names[s]}</span>`;
        }).join("");

        card.innerHTML = `
          <div class="drug-header">
            <div>
              <div class="drug-name">${drug.name}</div>
              <div class="drug-dose">${drug.dose} • ${drug.category}</div>
            </div>
            <div class="toggle-pill"></div>
          </div>
          <div class="drug-stages">${stagePills}</div>
          <div class="drug-mech">${drug.shortMech}</div>
        `;
        container.appendChild(card);
      });
    }

    function toggleDrug(drugId) {
      const drug = DRUGS.find(d => d.id === drugId);
      if (drug) {
        drug.active = !drug.active;
        updateSimulation();
      }
    }

    // =========================================================================
    // 4. MOTOR MATEMÁTICO DE SIMULACIÓN NOCICEPTIVA EN CASCADA
    // =========================================================================
    function calculatePathwayState() {
      const activeDrugs = DRUGS.filter(d => d.active);

      // Cálculo de inhibición local en cada etapa (con rendimientos decrecientes realistas)
      const stageBlock = { 1: 0, 2: 0, 3: 0, 4: 0 };
      let descendingTotal = 20; // Tono inhibitorio basal endógeno (SGPA / RVM)

      activeDrugs.forEach(d => {
        for (let s = 1; s <= 4; s++) {
          const eff = d.effects[s] || 0;
          stageBlock[s] = 100 - ((100 - stageBlock[s]) * (100 - eff) / 100);
        }
        descendingTotal = Math.min(100, descendingTotal + (d.descendingBoost || 0));
      });

      // El refuerzo descendente potencia adicionalmente la inhibición en Etapa 3 (Asta Dorsal)
      const extraDescendingModulation = (descendingTotal - 20) * 0.35;
      stageBlock[3] = Math.min(96, stageBlock[3] + extraDescendingModulation);

      // Propagación en cascada de la señal nociceptiva de Etapa 1 a Etapa 4
      const s1Out = Math.max(4, Math.round(100 * (1 - stageBlock[1] / 100)));
      const s2Out = Math.max(2, Math.round(s1Out * (1 - stageBlock[2] / 100)));
      const s3Out = Math.max(1, Math.round(s2Out * (1 - stageBlock[3] / 100)));
      const s4Out = Math.max(0, Math.round(s3Out * (1 - stageBlock[4] / 100)));

      // Riesgo de Wind-up (depende de la aferencia que llega a E3 y del bloqueo NK-1/NMDA en E3)
      const windupRisk = Math.min(98, Math.max(2, Math.round(s3Out * 0.95)));

      // Cobertura de etapas (cuántas etapas tienen al menos un fármaco/intervención activa)
      const coveredStages = [1, 2, 3, 4].filter(s =>
        activeDrugs.some(d => d.stages.includes(s))
      ).length;

      return {
        activeDrugs,
        stageBlock,
        descendingTotal,
        outputs: { 1: s1Out, 2: s2Out, 3: s3Out, 4: s4Out },
        windupRisk,
        coveredStages
      };
    }

    function getStatusColor(signalValue) {
      if (signalValue >= 60) return { hex: "#ef4444", bg: "rgba(239,68,68,0.15)", cls: "status-critical" };
      if (signalValue >= 28) return { hex: "#f59e0b", bg: "rgba(245,158,11,0.15)", cls: "status-moderate" };
      return { hex: "#10b981", bg: "rgba(16,185,129,0.15)", cls: "status-controlled" };
    }

    // =========================================================================
    // 5. ACTUALIZACIÓN VISUAL DE KPIS, DIAGRAMA SVG E INSPECTOR
    // =========================================================================
    function updateSimulation() {
      renderDrugs();
      const state = calculatePathwayState();
      const out = state.outputs;

      // 1. KPI: Percepción Cortical (EVA)
      const eva = Math.round(out[4] / 10);
      const painStatus = getStatusColor(out[4]);
      const painBadge = document.getElementById("kpi-pain-badge");
      painBadge.className = `kpi-badge ${painStatus.cls}`;
      painBadge.textContent = eva >= 7 ? "DOLOR SEVERO" : (eva >= 4 ? "DOLOR MODERADO" : (eva >= 1 ? "DOLOR LEVE" : "ANALGESIA ÓPTIMA"));
      document.getElementById("kpi-pain-value").textContent = `${out[4]}% (EVA ${eva}/10)`;
      document.getElementById("kpi-pain-sub").textContent =
        eva >= 7
          ? "Intensa activación talamocortical (S1/S2) y afectivo-motivacional (corteza cingulada)."
          : eva >= 4
          ? "Atenuación parcial de las vías espinotalámica y espinorreticular."
          : "Control efectivo de los componentes sensorial-discriminativo y afectivo del dolor.";

      // 2. KPI: Wind-up (NMDA / NK-1)
      const wuStatus = getStatusColor(state.windupRisk);
      const wuBadge = document.getElementById("kpi-windup-badge");
      wuBadge.className = `kpi-badge ${wuStatus.cls}`;
      wuBadge.textContent = state.windupRisk >= 60 ? "ALTO RIESGO" : (state.windupRisk >= 28 ? "RIESGO MODERADO" : "PROTEGIDO");
      document.getElementById("kpi-windup-value").textContent = `${state.windupRisk}%`;
      document.getElementById("kpi-windup-sub").textContent =
        state.windupRisk >= 60
          ? "Co-activación Sustancia P (NK-1) + NMDA y mGlu (↑Ca²⁺) en lámina II."
          : "Freno de la sensibilización central en el asta dorsal medular.";

      // 3. KPI: Respuesta Autonómica (Hipotálamo y Formación Reticular)
      const hr = Math.round(66 + (out[4] * 0.52));
      const sys = Math.round(112 + (out[4] * 0.52));
      const dia = Math.round(68 + (out[4] * 0.30));
      const hemoBadge = document.getElementById("kpi-hemo-badge");
      hemoBadge.className = `kpi-badge ${painStatus.cls}`;
      hemoBadge.textContent = out[4] >= 60 ? "TAQUICARDIA / HTA" : (out[4] >= 28 ? "RESPUESTA SIMPÁTICA LEVE" : "ESTABILIDAD AUTONÓMICA");
      document.getElementById("kpi-hemo-value").textContent = `${hr} lpm | ${sys}/${dia}`;
      document.getElementById("kpi-hemo-sub").textContent =
        out[4] >= 60
          ? "Hiperactividad hipotalámica y reticular con descarga simpática y neuroendocrina."
          : "Modulación de la respuesta autonómica, motora y neuroendocrina al estrés.";

      // 4. KPI: Cobertura Multimodal
      const multiBadge = document.getElementById("kpi-multi-badge");
      const cov = state.coveredStages;
      multiBadge.className = `kpi-badge ${cov === 4 ? "status-controlled" : (cov >= 2 ? "status-moderate" : "status-critical")}`;
      multiBadge.textContent = `${cov} / 4 ETAPAS`;
      document.getElementById("kpi-multi-value").textContent =
        cov === 4 ? "Multimodal Completa" : (cov >= 2 ? `${state.activeDrugs.length} intervenciones` : (cov === 1 ? "Monoterapia" : "Sin cobertura"));

      // 5. Actualizar Conectores y Nodos del SVG
      for (let s = 1; s <= 4; s++) {
        const sig = out[s];
        const col = getStatusColor(sig);
        const badgeBg = document.getElementById(`badge-bg-${s}`);
        const badgeTxt = document.getElementById(`badge-txt-${s}`);

        badgeBg.setAttribute("fill", col.bg);
        badgeTxt.setAttribute("fill", col.hex);

        const labels = {
          1: `TRANSDUCCIÓN: ${sig}%`,
          2: `CONDUCCIÓN: ${sig}%`,
          3: `SALIDA ESPINAL: ${sig}%`,
          4: `PERCEPCIÓN FINAL: ${sig}%`
        };
        badgeTxt.textContent = labels[s];

        // Listar fármacos activos en el nodo SVG
        const stageDrugs = state.activeDrugs.filter(d => d.stages.includes(s)).map(d => d.name.split(" ")[0]);
        const txt1 = document.getElementById(`drugs-txt-${s}`);
        const txt2 = document.getElementById(`drugs-txt-${s}b`);
        if (stageDrugs.length === 0) {
          txt1.textContent = "Intervención activa: Ninguna";
          txt2.textContent = "";
        } else {
          txt1.textContent = "Activos: " + stageDrugs.slice(0, 2).join(", ");
          txt2.textContent = stageDrugs.length > 2 ? "+ " + stageDrugs.slice(2).join(", ") : "";
        }
      }

      // Actualizar líneas conectoras entre nodos
      const connectors = [
        { line: "conn-1-2", label: "conn-label-1", val: out[1] },
        { line: "conn-2-3", label: "conn-label-2", val: out[2] },
        { line: "conn-3-4", label: "conn-label-3", val: out[3] }
      ];

      connectors.forEach(c => {
        const col = getStatusColor(c.val);
        const lineEl = document.getElementById(c.line);
        const labelEl = document.getElementById(c.label);
        lineEl.setAttribute("stroke", col.hex);
        lineEl.setAttribute("stroke-width", Math.max(2.5, (c.val / 100) * 6.5));
        labelEl.textContent = `${c.val}%`;
        labelEl.setAttribute("fill", col.hex);
      });

      // Actualizar Vía Inhibitoria Descendente
      const descPath = document.getElementById("svg-descending-path");
      const descLabel = document.getElementById("svg-descending-label");
      const descOpacity = 0.2 + (state.descendingTotal / 100) * 0.8;
      descPath.setAttribute("opacity", descOpacity.toFixed(2));
      descPath.setAttribute("stroke-width", (2.5 + (state.descendingTotal / 100) * 3.5).toFixed(1));
      descLabel.setAttribute("opacity", Math.min(1, descOpacity + 0.15).toFixed(2));
      descLabel.textContent = `Vía Inhibitoria Descendente (SGPA / RVM: NA, 5-HT, Encefalinas) • Actividad: ${state.descendingTotal}%`;

      // Actualizar Perla Clínica Pedagógica
      updateClinicalPearl(state);

      // Actualizar Inspector de Etapa
      renderStageDetail(currentStage, state);
    }

    function updateClinicalPearl(state) {
      const box = document.getElementById("clinical-pearl-box");
      if (state.activeDrugs.length === 0) {
        box.innerHTML = `<strong>👨‍⚕️ Razonamiento Algológico (Paciente sin analgesia):</strong> Los nociceptores de fibras <strong>Aδ</strong> (dolor rápido/epicrítico, 5–15 m/s) y <strong>C polimorfas</strong> (dolor lento/protopático, &lt;2 m/s) descargan sin freno hacia las láminas I, IIo y V. En la sustancia gelatinosa, la liberación de <strong>Sustancia P (NK-1) y Neurocinina A (NK-2)</strong> potencia al receptor <strong>NMDA</strong> generando <em>wind-up</em>, alodinia mediada por fibras Aβ y una intensa respuesta hipotalámica, reticular y afectivo-motivacional.`;
      } else if (state.coveredStages === 4) {
        box.innerHTML = `<strong>✨ Sinergia Multimodal e Interdisciplinaria Óptima:</strong> Como enfatiza el <em>Cuaderno de Algología</em>, el especialista en dolor debe equilibrar el manejo farmacológico, intervencionista guiado por imagen (US/fluoroscopia) y psicológico (CBT/ACT/MBSR). Al bloquear simultáneamente la transducción periférica, la conducción axonal en fibras Aδ/C, el fenómeno de <em>wind-up</em> espinal (NK-1/NMDA) y la catastrofización cortical, se logra analgesia superior con menor dosis de opioides y menor morbimortalidad.`;
      } else {
        const missing = [1, 2, 3, 4].filter(s => !state.activeDrugs.some(d => d.stages.includes(s)));
        box.innerHTML = `<strong>🔍 Evaluación Educativa de tu Esquema:</strong> Tienes activas <strong>${state.activeDrugs.length} modalidad(es)</strong> cubriendo <strong>${state.coveredStages} de las 4 etapas</strong>. Aún quedan sin cobertura específica la(s) etapa(s): <strong>${missing.join(", ")}</strong>. Explora cómo la adición de bloqueos regionales ecoguiados (Etapa 2), antagonistas NMDA (Etapa 3) o intervenciones cognitivo-conductuales (Etapa 4) cierra la brecha nociceptiva.`;
      }
    }

    // =========================================================================
    // 6. INSPECTOR DETALLADO DE CADA ETAPA DEL DOLOR
    // =========================================================================
    function selectStage(stageNum) {
      currentStage = stageNum;
      for (let s = 1; s <= 4; s++) {
        const node = document.getElementById(`node-${s}`);
        if (s === stageNum) node.classList.add("active");
        else node.classList.remove("active");
      }
      const state = calculatePathwayState();
      renderStageDetail(stageNum, state);
    }

    function prevStage() {
      selectStage(currentStage > 1 ? currentStage - 1 : 4);
    }

    function nextStage() {
      selectStage(currentStage < 4 ? currentStage + 1 : 1);
    }

    function renderStageDetail(stageNum, state) {
      const info = STAGES_INFO[stageNum];
      document.getElementById("detail-stage-badge").textContent = info.badge;
      document.getElementById("detail-stage-title").textContent = info.title;
      document.getElementById("detail-anatomy").textContent = info.anatomy;
      document.getElementById("detail-physiology").textContent = info.physiology;

      // Tabla comparativa de fibras en Etapa 1 y 2 (Tabla 133-1 del Cuaderno)
      const extraTable = document.getElementById("detail-extra-table");
      if (stageNum === 1 || stageNum === 2) {
        extraTable.innerHTML = `
          <table class="fiber-table">
            <thead>
              <tr>
                <th>Característica (Tabla 133-1)</th>
                <th>Fibras Aδ (Primer Dolor)</th>
                <th>Fibras C (Segundo Dolor)</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><strong>Diámetro y Mielina</strong></td>
                <td>2 – 5 µm (Mielinización delgada)</td>
                <td>&lt; 2 µm (Amielínicas)</td>
              </tr>
              <tr>
                <td><strong>Velocidad de conducción</strong></td>
                <td>5 – 15 m/s</td>
                <td>&lt; 2 m/s (1 – 2 m/s)</td>
              </tr>
              <tr>
                <td><strong>Umbral y Sensación</strong></td>
                <td>Alto y bajo • Rápido, agudo, localizado (epicrítico)</td>
                <td>Alto (Polimodal) • Lento, sordo, difuso, urente (protopático)</td>
              </tr>
            </tbody>
          </table>
        `;
      } else {
        extraTable.innerHTML = "";
      }

      // Mediadores
      const medContainer = document.getElementById("detail-mediators");
      medContainer.innerHTML = info.mediators.map(m => `<span class="mediator-tag">${m}</span>`).join("");

      // Fármacos que actúan en esta etapa
      const stageDrugsContainer = document.getElementById("detail-stage-drugs");
      const relevantDrugs = DRUGS.filter(d => d.stages.includes(stageNum));

      stageDrugsContainer.innerHTML = relevantDrugs.map(d => `
        <div class="stage-drug-item ${d.active ? "is-active" : ""}" onclick="toggleDrug('${d.id}')" style="cursor:pointer;">
          <div class="stage-drug-top">
            <span>${d.active ? "✅" : "⚪"} ${d.name} (${d.dose})</span>
            <span style="font-size:0.74rem; color: var(--accent-blue);">-${d.effects[stageNum]}% en Etapa ${stageNum}</span>
          </div>
          <div style="color: var(--text-secondary);">${d.stageDetails[stageNum]}</div>
        </div>
      `).join("");
    }

    // =========================================================================
    // 7. BOTONES DE ESCENARIOS CLÍNICOS PRECONFIGURADOS Y TEMA
    // =========================================================================
    document.getElementById("btn-reset").addEventListener("click", () => {
      DRUGS.forEach(d => d.active = false);
      updateSimulation();
    });

    document.getElementById("btn-basic").addEventListener("click", () => {
      DRUGS.forEach(d => {
        d.active = ["diclofenaco", "paracetamol"].includes(d.id);
      });
      updateSimulation();
    });

    document.getElementById("btn-interventional").addEventListener("click", () => {
      DRUGS.forEach(d => {
        d.active = ["bloqueo_pnb", "epidural_tf", "dexametasona"].includes(d.id);
      });
      updateSimulation();
    });

    document.getElementById("btn-multimodal").addEventListener("click", () => {
      DRUGS.forEach(d => {
        d.active = ["diclofenaco", "dexametasona", "bloqueo_pnb", "paracetamol", "ketamina", "psicoterapia"].includes(d.id);
      });
      updateSimulation();
    });

    document.getElementById("btn-theme").addEventListener("click", () => {
      const html = document.documentElement;
      const current = html.getAttribute("data-theme");
      html.setAttribute("data-theme", current === "dark" ? "light" : "dark");
    });

    // Inicializar simulador al cargar
    updateSimulation();
  </script>
</body>
</html>
