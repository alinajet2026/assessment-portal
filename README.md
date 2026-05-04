[index.html](https://github.com/user-attachments/files/27376791/index.html)
# assessment-portal
Portal de Assessment JET Brasil
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Portal de Assessment — JET Brasil</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #f0f5ff;
    --sidebar-bg: #ffffff;
    --sidebar-text: #1e293b;
    --sidebar-muted: #64748b;
    --sidebar-active: #2563eb;
    --sidebar-border: #e2e8f0;
    --surface: #ffffff;
    --surface2: #f5f8ff;
    --border: #dce6f8;
    --accent: #2563eb;
    --accent2: #6d28d9;
    --accent3: #0ea5e9;
    --text: #111827;
    --text-muted: #6b7280;
    --success: #059669;
    --warning: #d97706;
    --danger: #dc2626;
    --blue-light: #eff6ff;
  }
  * { margin:0; padding:0; box-sizing:border-box; }
  body { background:var(--bg); color:var(--text); font-family:'DM Sans',sans-serif; min-height:100vh; }
  .sidebar { position:fixed; left:0; top:0; bottom:0; width:260px; background:#ffffff; border-right:1.5px solid #e2e8f0; z-index:10; display:flex; flex-direction:column; box-shadow:2px 0 16px rgba(37,99,235,0.07); }
  .sidebar-logo { padding:18px 16px 14px; border-bottom:1px solid #e2e8f0; background:linear-gradient(135deg,#eff6ff 0%,#f8faff 100%); }
  .logo-badge { display:flex; align-items:center; gap:10px; }
  .logo-icon { width:38px; height:38px; background:linear-gradient(135deg,#2563eb,#6d28d9); border-radius:10px; display:flex; align-items:center; justify-content:center; font-size:18px; flex-shrink:0; box-shadow:0 2px 8px rgba(37,99,235,0.3); }
  .logo-text { font-family:'Syne',sans-serif; font-weight:800; font-size:15px; color:#111827; }
  .logo-sub { font-size:10px; color:#64748b; letter-spacing:1px; text-transform:uppercase; margin-top:2px; }
  .sidebar-search { padding:12px 12px; border-bottom:1px solid #e2e8f0; }
  .search-input { width:100%; background:#f0f5ff; border:1.5px solid #dce6f8; border-radius:8px; padding:7px 11px; color:#111827; font-family:'DM Sans',sans-serif; font-size:12.5px; outline:none; transition:all .2s; }
  .search-input::placeholder { color:#94a3b8; }
  .search-input:focus { border-color:#2563eb; background:#fff; box-shadow:0 0 0 3px rgba(37,99,235,0.08); }
  .sidebar-nav { flex:1; overflow-y:auto; padding:8px 8px; }
  .sidebar-nav::-webkit-scrollbar { width:3px; }
  .sidebar-nav::-webkit-scrollbar-thumb { background:#dce6f8; border-radius:4px; }
  .dept-group { margin-bottom:2px; }
  .dept-header { display:flex; align-items:center; gap:8px; padding:8px 10px; cursor:pointer; font-size:11px; font-weight:700; letter-spacing:.6px; text-transform:uppercase; color:#64748b; transition:all .15s; user-select:none; border-radius:8px; }
  .dept-header:hover { background:#eff6ff; color:#2563eb; }
  .dept-group.open .dept-header { color:#2563eb; background:#eff6ff; }
  .dept-chevron { margin-left:auto; transition:transform .2s; font-size:9px; opacity:.5; }
  .dept-group.open .dept-chevron { transform:rotate(90deg); opacity:1; }
  .dept-positions { display:none; padding:2px 0 6px 0; }
  .dept-group.open .dept-positions { display:block; }
  .position-item { display:flex; align-items:center; gap:7px; padding:6px 10px 6px 22px; cursor:pointer; font-size:12px; color:#64748b; transition:all .15s; border-radius:7px; margin:1px 0; }
  .position-item:hover { color:#1e293b; background:#f0f5ff; }
  .position-item.active { color:#2563eb; background:#dbeafe; font-weight:600; }
  .pos-dot { width:5px; height:5px; border-radius:50%; background:currentColor; opacity:.4; flex-shrink:0; }
  .position-item.active .pos-dot { opacity:1; background:#2563eb; }
  .main { margin-left:260px; min-height:100vh; }
  .topbar { position:sticky; top:0; background:rgba(240,245,255,0.92); backdrop-filter:blur(12px); border-bottom:1px solid var(--border); padding:14px 32px; display:flex; align-items:center; justify-content:space-between; z-index:5; }
  .topbar-title { font-family:'Syne',sans-serif; font-size:18px; font-weight:800; color:var(--text); }
  .topbar-subtitle { font-size:12px; color:var(--text-muted); margin-top:1px; }
  .badge { display:inline-flex; align-items:center; padding:4px 10px; border-radius:20px; font-size:11px; font-weight:600; }
  .badge-blue { background:#dbeafe; color:#1d4ed8; border:1px solid #bfdbfe; }
  .badge-green { background:#d1fae5; color:#065f46; border:1px solid #a7f3d0; }
  .badge-orange { background:#fef3c7; color:#92400e; border:1px solid #fde68a; }
  .content { padding:28px 32px; }
  @keyframes fadeUp { from{opacity:0;transform:translateY(10px)} to{opacity:1;transform:translateY(0)} }
  .stats-row { display:grid; grid-template-columns:repeat(4,1fr); gap:14px; margin-bottom:28px; animation:fadeUp .4s ease; }
  .stat-card { background:var(--surface); border:1px solid var(--border); border-radius:14px; padding:20px; position:relative; overflow:hidden; box-shadow:0 1px 6px rgba(37,99,235,.06); transition:box-shadow .2s,transform .2s; }
  .stat-card:hover { box-shadow:0 4px 16px rgba(37,99,235,.12); transform:translateY(-2px); }
  .stat-card::after { content:''; position:absolute; top:0; left:0; right:0; height:3px; background:linear-gradient(90deg,var(--accent),var(--accent3)); }
  .stat-label { font-size:11px; color:var(--text-muted); text-transform:uppercase; letter-spacing:.8px; margin-bottom:8px; font-weight:600; }
  .stat-value { font-family:'Syne',sans-serif; font-size:30px; font-weight:800; color:var(--text); }
  .stat-icon { position:absolute; right:18px; top:18px; font-size:24px; opacity:.2; }
  .dept-cards { display:grid; grid-template-columns:repeat(auto-fill,minmax(270px,1fr)); gap:14px; animation:fadeUp .4s ease; }
  .dept-card { background:var(--surface); border:1.5px solid var(--border); border-radius:16px; padding:22px; cursor:pointer; transition:all .2s; box-shadow:0 1px 4px rgba(37,99,235,.05); }
  .dept-card:hover { border-color:var(--accent); box-shadow:0 6px 24px rgba(37,99,235,.12); transform:translateY(-3px); }
  .dept-card-icon { font-size:30px; margin-bottom:12px; }
  .dept-card-name { font-family:'Syne',sans-serif; font-size:15px; font-weight:700; color:var(--text); margin-bottom:6px; }
  .dept-card-count { font-size:12px; color:var(--text-muted); margin-bottom:14px; }
  .dept-card-bar { height:4px; background:var(--border); border-radius:4px; overflow:hidden; }
  .dept-card-bar-fill { height:100%; border-radius:4px; background:linear-gradient(90deg,var(--accent),var(--accent3)); }
  .position-view { display:none; }
  .position-view.visible { display:block; animation:fadeUp .35s ease; }
  .position-header { background:var(--surface); border:1.5px solid var(--border); border-radius:16px; padding:26px; margin-bottom:22px; display:flex; align-items:flex-start; justify-content:space-between; gap:20px; box-shadow:0 2px 8px rgba(37,99,235,.06); }
  .back-link { font-size:12px; color:var(--accent); cursor:pointer; margin-bottom:8px; display:inline-block; font-weight:500; }
  .back-link:hover { text-decoration:underline; }
  .position-info h1 { font-family:'Syne',sans-serif; font-size:22px; font-weight:800; color:var(--text); margin-bottom:8px; }
  .position-meta { display:flex; gap:8px; flex-wrap:wrap; }
  .progress-ring { position:relative; width:80px; height:80px; flex-shrink:0; }
  .progress-ring svg { transform:rotate(-90deg); }
  .progress-ring circle { fill:none; stroke-width:6; stroke-linecap:round; }
  .ring-bg { stroke:#e2e8f0; }
  .ring-fill { stroke:var(--accent); stroke-dasharray:214; stroke-dashoffset:160; transition:stroke-dashoffset .8s ease; }
  .ring-text { position:absolute; inset:0; display:flex; flex-direction:column; align-items:center; justify-content:center; font-family:'Syne',sans-serif; font-weight:800; font-size:15px; color:var(--text); }
  .ring-label { font-size:9px; color:var(--text-muted); font-family:'DM Sans',sans-serif; font-weight:400; }
  .tabs { display:flex; gap:2px; border-bottom:2px solid var(--border); margin-bottom:22px; }
  .tab { padding:9px 18px; font-size:13px; cursor:pointer; color:var(--text-muted); border-bottom:2px solid transparent; margin-bottom:-2px; transition:all .15s; font-weight:500; }
  .tab:hover { color:var(--text); }
  .tab.active { color:var(--accent); border-bottom-color:var(--accent); }
  .section-title { font-family:'Syne',sans-serif; font-size:12px; font-weight:700; letter-spacing:1px; text-transform:uppercase; color:var(--text-muted); margin-bottom:14px; display:flex; align-items:center; gap:10px; }
  .section-title::after { content:''; flex:1; height:1px; background:var(--border); }
  .docs-grid { display:grid; grid-template-columns:repeat(auto-fill,minmax(260px,1fr)); gap:12px; margin-bottom:28px; }
  .doc-card { background:var(--surface); border:1.5px solid var(--border); border-radius:12px; padding:16px 18px; cursor:pointer; transition:all .2s; text-decoration:none; display:block; box-shadow:0 1px 4px rgba(37,99,235,.04); }
  .doc-card:hover { border-color:var(--accent); box-shadow:0 6px 20px rgba(37,99,235,.1); transform:translateY(-2px); }
  .doc-card-top { display:flex; align-items:flex-start; justify-content:space-between; margin-bottom:10px; }
  .doc-icon { font-size:22px; }
  .doc-name { font-weight:500; font-size:13px; color:var(--text); margin-bottom:6px; line-height:1.4; }
  .doc-meta { font-size:11px; color:var(--text-muted); }
  .doc-status-bar { height:3px; border-radius:2px; margin-top:12px; background:var(--border); overflow:hidden; }
  .doc-status-fill { height:100%; border-radius:2px; background:linear-gradient(90deg,var(--accent),var(--accent3)); }
  .timeline { position:relative; padding-left:8px; }
  .timeline::before { content:''; position:absolute; left:20px; top:0; bottom:0; width:1px; background:var(--border); }
  .timeline-item { display:flex; gap:14px; margin-bottom:16px; }
  .timeline-dot { width:40px; height:40px; border-radius:50%; background:var(--blue-light); border:1.5px solid var(--border); display:flex; align-items:center; justify-content:center; font-size:16px; flex-shrink:0; z-index:1; }
  .timeline-content { background:var(--surface); border:1.5px solid var(--border); border-radius:10px; padding:12px 16px; flex:1; }
  .timeline-title { font-weight:500; font-size:13px; color:var(--text); margin-bottom:3px; }
  .timeline-date { font-size:11px; color:var(--text-muted); }
  .comp-chip { background:var(--blue-light); border:1px solid #bfdbfe; border-radius:8px; padding:10px 14px; font-size:13px; color:#1e40af; font-weight:500; display:flex; align-items:center; gap:8px; }
  .comp-num { width:24px; height:24px; background:var(--accent); color:#fff; border-radius:6px; display:flex; align-items:center; justify-content:center; font-size:11px; font-weight:700; flex-shrink:0; }
</style>
</head>
<body>
<aside class="sidebar">
  <div class="sidebar-logo">
    <div class="logo-badge">
      <div class="logo-icon">🎯</div>
      <div><div class="logo-text">JET Brasil</div><div class="logo-sub">Portal de Assessment</div></div>
    </div>
  </div>
  <div class="sidebar-search">
    <input class="search-input" type="text" placeholder="🔍  Buscar cargo..." oninput="filterPositions(this.value)">
  </div>
  <nav class="sidebar-nav">
    <div class="dept-group open"><div class="dept-header" onclick="toggleDept(this)"><span>🚚</span> Logística <span class="dept-chevron">▶</span></div><div class="dept-positions">
      <div class="position-item active" onclick="showPosition('log_gerente2',this)"><div class="pos-dot"></div> Gerente de Logística II / Territorial</div>
      <div class="position-item" onclick="showPosition('log_gerente1',this)"><div class="pos-dot"></div> Gerente de Logística I</div>
      <div class="position-item" onclick="showPosition('log_lider',this)"><div class="pos-dot"></div> Líder de Equipe</div>
      <div class="position-item" onclick="showPosition('log_motorista',this)"><div class="pos-dot"></div> Motorista</div>
      <div class="position-item" onclick="showPosition('log_auxiliar',this)"><div class="pos-dot"></div> Auxiliar de Logística / Charger</div>
      <div class="position-item" onclick="showPosition('log_auxiliar_pj',this)"><div class="pos-dot"></div> Auxiliar (PJ)</div>
      <div class="position-item" onclick="showPosition('log_agente',this)"><div class="pos-dot"></div> Agente de Logística / Charger PJ</div>
      <div class="position-item" onclick="showPosition('log_motoboy',this)"><div class="pos-dot"></div> Motoboy</div>
    </div></div>
    <div class="dept-group"><div class="dept-header" onclick="toggleDept(this)"><span>🔧</span> SC (Oficina) <span class="dept-chevron">▶</span></div><div class="dept-positions">
      <div class="position-item" onclick="showPosition('sc_gerente',this)"><div class="pos-dot"></div> Gerente de SC</div>
      <div class="position-item" onclick="showPosition('sc_subgerente',this)"><div class="pos-dot"></div> Subgerente de SC</div>
      <div class="position-item" onclick="showPosition('sc_lider_mec',this)"><div class="pos-dot"></div> Líder Mecânico / Líder Técnico</div>
      <div class="position-item" onclick="showPosition('sc_sublider',this)"><div class="pos-dot"></div> Sublíder Mecânico / Técnico</div>
      <div class="position-item" onclick="showPosition('sc_mecanico',this)"><div class="pos-dot"></div> Mecânico I/II / Técnico Esp.</div>
      <div class="position-item" onclick="showPosition('sc_lavador',this)"><div class="pos-dot"></div> Lavador / Pintor</div>
    </div></div>
    <div class="dept-group"><div class="dept-header" onclick="toggleDept(this)"><span>👥</span> RH <span class="dept-chevron">▶</span></div><div class="dept-positions">
      <div class="position-item" onclick="showPosition('rh_gerente',this)"><div class="pos-dot"></div> Gerente de RH</div>
      <div class="position-item" onclick="showPosition('rh_gerente_td',this)"><div class="pos-dot"></div> Gerente T&D</div>
      <div class="position-item" onclick="showPosition('rh_coord',this)"><div class="pos-dot"></div> Coordenador</div>
      <div class="position-item" onclick="showPosition('rh_engenheiro',this)"><div class="pos-dot"></div> Eng./Técnico Seg. Trabalho</div>
      <div class="position-item" onclick="showPosition('rh_analista_sr',this)"><div class="pos-dot"></div> Analista RH / Folha Sênior</div>
      <div class="position-item" onclick="showPosition('rh_analista_pl',this)"><div class="pos-dot"></div> Analista RH / Folha Pleno</div>
      <div class="position-item" onclick="showPosition('rh_analista_jr',this)"><div class="pos-dot"></div> Analista RH / Folha Júnior</div>
      <div class="position-item" onclick="showPosition('rh_assistente',this)"><div class="pos-dot"></div> Assistente de RH / Folha</div>
      <div class="position-item" onclick="showPosition('rh_assistente_seg',this)"><div class="pos-dot"></div> Assistente de Segurança</div>
    </div></div>
    <div class="dept-group"><div class="dept-header" onclick="toggleDept(this)"><span>🎯</span> Recrutamento <span class="dept-chevron">▶</span></div><div class="dept-positions">
      <div class="position-item" onclick="showPosition('rec_gerente',this)"><div class="pos-dot"></div> Gerente de R&S</div>
      <div class="position-item" onclick="showPosition('rec_coord',this)"><div class="pos-dot"></div> Coordenadora de Recrutamento</div>
      <div class="position-item" onclick="showPosition('rec_recrutador',this)"><div class="pos-dot"></div> Recrutador(a)</div>
    </div></div>
    <div class="dept-group"><div class="dept-header" onclick="toggleDept(this)"><span>💻</span> Suporte / TI <span class="dept-chevron">▶</span></div><div class="dept-positions">
      <div class="position-item" onclick="showPosition('ti_gerente',this)"><div class="pos-dot"></div> Gerente de Suporte</div>
      <div class="position-item" onclick="showPosition('ti_analista',this)"><div class="pos-dot"></div> Analista de Suporte (QA)</div>
      <div class="position-item" onclick="showPosition('ti_gerente_l2',this)"><div class="pos-dot"></div> Gerente de Suporte L2</div>
    </div></div>
    <div class="dept-group"><div class="dept-header" onclick="toggleDept(this)"><span>💰</span> Admin. / Financeiro <span class="dept-chevron">▶</span></div><div class="dept-positions">
      <div class="position-item" onclick="showPosition('fin_analista_cont_sr',this)"><div class="pos-dot"></div> Analista Contábil Sênior</div>
      <div class="position-item" onclick="showPosition('fin_analista_fin_sr',this)"><div class="pos-dot"></div> Analista Financeiro Sênior</div>
      <div class="position-item" onclick="showPosition('fin_analista_pl',this)"><div class="pos-dot"></div> Analistas Pleno</div>
      <div class="position-item" onclick="showPosition('fin_agente',this)"><div class="pos-dot"></div> Agente Administrativo</div>
      <div class="position-item" onclick="showPosition('fin_assistente',this)"><div class="pos-dot"></div> Assistentes / Analistas Júnior</div>
    </div></div>
    <div class="dept-group"><div class="dept-header" onclick="toggleDept(this)"><span>⚖️</span> Rel. Gov. / Legal <span class="dept-chevron">▶</span></div><div class="dept-positions">
      <div class="position-item" onclick="showPosition('jur_ger_gov',this)"><div class="pos-dot"></div> Ger. Relações Governamentais</div>
      <div class="position-item" onclick="showPosition('jur_ger_pub',this)"><div class="pos-dot"></div> Ger. Relações Públicas</div>
      <div class="position-item" onclick="showPosition('jur_ger_jur',this)"><div class="pos-dot"></div> Gerente Jurídico</div>
      <div class="position-item" onclick="showPosition('jur_sub',this)"><div class="pos-dot"></div> Subger. / Analistas</div>
      <div class="position-item" onclick="showPosition('jur_assist',this)"><div class="pos-dot"></div> Assistentes</div>
    </div></div>
    <div class="dept-group"><div class="dept-header" onclick="toggleDept(this)"><span>📣</span> Promo Marketing <span class="dept-chevron">▶</span></div><div class="dept-positions">
      <div class="position-item" onclick="showPosition('mkt_ger_prom',this)"><div class="pos-dot"></div> Gerente de Promotores</div>
      <div class="position-item" onclick="showPosition('mkt_ger_mkt',this)"><div class="pos-dot"></div> Gerente de Marketing</div>
      <div class="position-item" onclick="showPosition('mkt_supervisor',this)"><div class="pos-dot"></div> Supervisor / Líder de Promotores</div>
      <div class="position-item" onclick="showPosition('mkt_analista',this)"><div class="pos-dot"></div> Subger. / Analista de Marketing</div>
      <div class="position-item" onclick="showPosition('mkt_promotor',this)"><div class="pos-dot"></div> Promotor / Instrutor</div>
      <div class="position-item" onclick="showPosition('mkt_assistente',this)"><div class="pos-dot"></div> Assistente de Marketing</div>
    </div></div>
    <div class="dept-group"><div class="dept-header" onclick="toggleDept(this)"><span>🔋</span> Power Banks / Comercial <span class="dept-chevron">▶</span></div><div class="dept-positions">
      <div class="position-item" onclick="showPosition('com_consultor',this)"><div class="pos-dot"></div> Consultor Comercial</div>
      <div class="position-item" onclick="showPosition('com_lider',this)"><div class="pos-dot"></div> Líder Vendedores de Powerbanks</div>
    </div></div>
  </nav>
</aside>

<main class="main">
  <div class="topbar">
    <div>
      <div class="topbar-title" id="topbarTitle">Visão Geral</div>
      <div class="topbar-subtitle" id="topbarSubtitle">Portal de Assessment — JET Brasil</div>
    </div>
    <span class="badge badge-green">● Q1 2026 Ativo</span>
  </div>
  <div class="content">
    <div id="overviewScreen">
      <div class="stats-row">
        <div class="stat-card"><div class="stat-label">Departamentos</div><div class="stat-value">9</div><div class="stat-icon">🏢</div></div>
        <div class="stat-card"><div class="stat-label">Cargos Totais</div><div class="stat-value">45</div><div class="stat-icon">👤</div></div>
        <div class="stat-card"><div class="stat-label">Docs por Cargo</div><div class="stat-value">4–6</div><div class="stat-icon">📄</div></div>
        <div class="stat-card"><div class="stat-label">Campanha Ativa</div><div class="stat-value">23%</div><div class="stat-icon">🎯</div></div>
      </div>
      <div class="section-title">Departamentos</div>
      <div class="dept-cards">
        <div class="dept-card" onclick="openDept('logistica')"><div class="dept-card-icon">🚚</div><div class="dept-card-name">Logística</div><div class="dept-card-count">8 cargos · 6 docs por cargo</div><div class="dept-card-bar"><div class="dept-card-bar-fill" style="width:70%"></div></div></div>
        <div class="dept-card" onclick="openDept('sc')"><div class="dept-card-icon">🔧</div><div class="dept-card-name">SC (Oficina)</div><div class="dept-card-count">6 cargos · 5 docs por cargo</div><div class="dept-card-bar"><div class="dept-card-bar-fill" style="width:55%"></div></div></div>
        <div class="dept-card" onclick="openDept('rh')"><div class="dept-card-icon">👥</div><div class="dept-card-name">RH</div><div class="dept-card-count">9 cargos · 4 docs por cargo</div><div class="dept-card-bar"><div class="dept-card-bar-fill" style="width:40%"></div></div></div>
        <div class="dept-card" onclick="openDept('rec')"><div class="dept-card-icon">🎯</div><div class="dept-card-name">Recrutamento</div><div class="dept-card-count">3 cargos · 4 docs por cargo</div><div class="dept-card-bar"><div class="dept-card-bar-fill" style="width:60%"></div></div></div>
        <div class="dept-card" onclick="openDept('ti')"><div class="dept-card-icon">💻</div><div class="dept-card-name">Suporte / TI</div><div class="dept-card-count">3 cargos · 4 docs por cargo</div><div class="dept-card-bar"><div class="dept-card-bar-fill" style="width:30%"></div></div></div>
        <div class="dept-card" onclick="openDept('fin')"><div class="dept-card-icon">💰</div><div class="dept-card-name">Admin. / Financeiro</div><div class="dept-card-count">5 cargos · 4 docs por cargo</div><div class="dept-card-bar"><div class="dept-card-bar-fill" style="width:45%"></div></div></div>
        <div class="dept-card" onclick="openDept('jur')"><div class="dept-card-icon">⚖️</div><div class="dept-card-name">Rel. Gov. / Legal</div><div class="dept-card-count">5 cargos · 5 docs por cargo</div><div class="dept-card-bar"><div class="dept-card-bar-fill" style="width:35%"></div></div></div>
        <div class="dept-card" onclick="openDept('mkt')"><div class="dept-card-icon">📣</div><div class="dept-card-name">Promo Marketing</div><div class="dept-card-count">6 cargos · 4 docs por cargo</div><div class="dept-card-bar"><div class="dept-card-bar-fill" style="width:25%"></div></div></div>
        <div class="dept-card" onclick="openDept('com')"><div class="dept-card-icon">🔋</div><div class="dept-card-name">Power Banks / Comercial</div><div class="dept-card-count">2 cargos · 4 docs por cargo</div><div class="dept-card-bar"><div class="dept-card-bar-fill" style="width:20%"></div></div></div>
      </div>
    </div>
    <div id="positionView" class="position-view">
      <div class="position-header">
        <div class="position-info">
          <div class="back-link" onclick="showOverview()">← Voltar para visão geral</div>
          <h1 id="positionTitle"></h1>
          <div class="position-meta">
            <span class="badge badge-blue" id="positionDept"></span>
            <span class="badge badge-green">Ativo</span>
            <span class="badge badge-orange" id="positionDocsCount"></span>
          </div>
        </div>
        <div class="progress-ring">
          <svg width="80" height="80" viewBox="0 0 80 80">
            <circle class="ring-bg" cx="40" cy="40" r="34"/>
            <circle class="ring-fill" id="ringFill" cx="40" cy="40" r="34"/>
          </svg>
          <div class="ring-text"><span id="ringPercent">—</span><span class="ring-label">progresso</span></div>
        </div>
      </div>
      <div class="tabs">
        <div class="tab active" onclick="switchTab('docs',this)">📄 Documentos</div>
        <div class="tab" onclick="switchTab('timeline',this)">📅 Histórico</div>
        <div class="tab" onclick="switchTab('competencias',this)">🎯 Competências</div>
      </div>
      <div id="tab-docs"><div class="section-title">Documentos de Ассесмент</div><div class="docs-grid" id="docsGrid"></div></div>
      <div id="tab-timeline" style="display:none"><div class="section-title">Histórico de Avaliações</div><div class="timeline" id="timelineContainer"></div></div>
      <div id="tab-competencias" style="display:none"><div class="section-title">Competências Avaliadas</div><div id="competenciasContainer"></div></div>
    </div>
  </div>
</main>

<script>
const P={
  log_gerente2:{title:'Gerente de Logística II / Gerente Territorial',dept:'🚚 Logística',progress:65,docs:[{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:100,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'},{icon:'📊',name:'Entrevista por Competências — Especialidade (Logística / SC)',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1FOC0qfC9bUuS5yudld6WHfhuVfNtnT6NX8bgbm_NiUM'},{icon:'📊',name:'Entrevista por Competências — Outras (RH, Recrutamento, Seg. do Trabalho)',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},],timeline:[{icon:'📊',title:'Avaliação 360° iniciada',date:'Abril 2026'},{icon:'✅',title:'Checklist aplicado',date:'Abril 2026'},{icon:'📝',title:'Resultados coletados',date:'Abril 2026'}],competencias:['Avaliação 360°','Entrevista por Competências — Especialidade (Logística/SC)','Entrevista por Competências — Outras (RH, Recrutamento, Seg. Trabalho)']},
  log_gerente1:{title:'Gerente de Logística I',dept:'🚚 Logística',progress:50,docs:[{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:100,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'},{icon:'📊',name:'Entrevista por Competências — Especialidade (Logística / SC)',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1FOC0qfC9bUuS5yudld6WHfhuVfNtnT6NX8bgbm_NiUM'},{icon:'📊',name:'Entrevista por Competências — Outras (RH, Recrutamento, Seg. do Trabalho)',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},],timeline:[{icon:'🔄',title:'Avaliação 360° em andamento',date:'Abril 2026'}],competencias:['Avaliação 360°','Entrevista por Competências — Especialidade (Logística/SC)','Entrevista por Competências — Outras (RH, Recrutamento, Seg. Trabalho)']},
  log_lider:{title:'Líder de Equipe',dept:'🚚 Logística',progress:78,docs:[{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:100,url:'https://docs.google.com/forms/d/1KGo8pDKKxUPkp_54yS4W9T87zbMpsv6PqpYlLjRvVqM'},{icon:'📊',name:'Entrevista por Competências Reduzida — Especialidade (Logística / SC)',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1HhY_hJ1qOCAkpdwEJh-vPfwb07lpW10bxL3_Qg9OSfM'},{icon:'📊',name:'Entrevista por Competências Reduzida — Outras (RH, Recrutamento, Seg. do Trabalho)',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},],timeline:[{icon:'📊',title:'Checklist aplicado',date:'Abril 2026'},{icon:'📋',title:'360° concluído — Julio Jesus',date:'Abril 2026'},{icon:'📋',title:'360° concluído — Matheus Santos',date:'Abril 2026'}],competencias:['Avaliação 360°','Entrevista por Competências Reduzida — Especialidade (Logística/SC)','Entrevista por Competências Reduzida — Outras (RH, Recrutamento, Seg. Trabalho)']},
  log_motorista:{title:'Motorista',dept:'🚚 Logística',progress:30,docs:[{icon:'📊',name:'Checklist Competências',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1FOC0qfC9bUuS5yudld6WHfhuVfNtnT6NX8bgbm_NiUM'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:60,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'},{icon:'📄',name:'Perguntas + Competências',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'}],timeline:[{icon:'🔄',title:'Em andamento',date:'Abril 2026'}],competencias:['Responsabilidade pelas decisões','Conclusão de tarefas','Busca por desenvolvimento']},
  log_auxiliar:{title:'Auxiliar de Logística / Charger',dept:'🚚 Logística',progress:40,docs:[{icon:'📊',name:'Checklist Competências',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1FOC0qfC9bUuS5yudld6WHfhuVfNtnT6NX8bgbm_NiUM'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:80,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'},{icon:'📄',name:'Perguntas + Competências',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'}],timeline:[{icon:'🔄',title:'Em andamento',date:'Abril 2026'}],competencias:['Responsabilidade pelas decisões','Conclusão de tarefas','Respeito pela opinião dos colegas']},
  log_auxiliar_pj:{title:'Auxiliar (PJ)',dept:'🚚 Logística',progress:20,docs:[{icon:'📊',name:'Checklist Competências (PJ)',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1FOC0qfC9bUuS5yudld6WHfhuVfNtnT6NX8bgbm_NiUM'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:40,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'⏳',title:'Aguardando início',date:'Maio 2026'}],competencias:['Responsabilidade pelas decisões','Conclusão de tarefas']},
  log_agente:{title:'Agente de Logística / Charger PJ',dept:'🚚 Logística',progress:20,docs:[{icon:'📊',name:'Checklist Competências',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1FOC0qfC9bUuS5yudld6WHfhuVfNtnT6NX8bgbm_NiUM'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:40,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'⏳',title:'Aguardando início',date:'Maio 2026'}],competencias:['Responsabilidade pelas decisões','Conclusão de tarefas']},
  log_motoboy:{title:'Motoboy',dept:'🚚 Logística',progress:15,docs:[{icon:'📊',name:'Checklist Competências',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1FOC0qfC9bUuS5yudld6WHfhuVfNtnT6NX8bgbm_NiUM'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:30,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'⏳',title:'Aguardando início',date:'Maio 2026'}],competencias:['Responsabilidade pelas decisões','Conclusão de tarefas']},
  sc_gerente:{title:'Gerente de SC',dept:'🔧 SC (Oficina)',progress:55,docs:[{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:100,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'},{icon:'📊',name:'Entrevista por Competências — Especialidade (Logística / SC)',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1FOC0qfC9bUuS5yudld6WHfhuVfNtnT6NX8bgbm_NiUM'},{icon:'📊',name:'Entrevista por Competências — Outras (RH, Recrutamento, Seg. do Trabalho)',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},],timeline:[{icon:'📊',title:'Checklist aplicado',date:'Abril 2026'},{icon:'🔄',title:'360° em andamento',date:'Abril 2026'}],competencias:['Avaliação 360°','Entrevista por Competências — Especialidade (Logística/SC)','Entrevista por Competências — Outras (RH, Recrutamento, Seg. Trabalho)']},
  sc_subgerente:{title:'Subgerente de SC',dept:'🔧 SC (Oficina)',progress:45,docs:[{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:100,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'},{icon:'📊',name:'Entrevista por Competências — Especialidade (Logística / SC)',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1FOC0qfC9bUuS5yudld6WHfhuVfNtnT6NX8bgbm_NiUM'},{icon:'📊',name:'Entrevista por Competências — Outras (RH, Recrutamento, Seg. do Trabalho)',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},],timeline:[{icon:'🔄',title:'Em andamento',date:'Abril 2026'}],competencias:['Avaliação 360°','Entrevista por Competências — Especialidade (Logística/SC)','Entrevista por Competências — Outras (RH, Recrutamento, Seg. Trabalho)']},
  sc_lider_mec:{title:'Líder Mecânico / Líder Técnico de Manutenção',dept:'🔧 SC (Oficina)',progress:80,docs:[{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:100,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'},{icon:'📊',name:'Entrevista por Competências — Especialidade (Logística / SC)',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1FOC0qfC9bUuS5yudld6WHfhuVfNtnT6NX8bgbm_NiUM'},{icon:'📊',name:'Entrevista por Competências — Outras (RH, Recrutamento, Seg. do Trabalho)',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},],timeline:[{icon:'✅',title:'Checklist concluído',date:'Abril 2026'},{icon:'✅',title:'360° concluído',date:'Abril 2026'},{icon:'🏆',title:'Relatório de promoção gerado — Daniel Gumercindo',date:'Abril 2026'}],competencias:['Avaliação 360°','Entrevista por Competências — Especialidade (Logística/SC)','Entrevista por Competências — Outras (RH, Recrutamento, Seg. Trabalho)']},
  sc_sublider:{title:'Sublíder Mecânico / Técnico',dept:'🔧 SC (Oficina)',progress:50,docs:[{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:100,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'},{icon:'📊',name:'Entrevista por Competências — Especialidade (Logística / SC)',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1FOC0qfC9bUuS5yudld6WHfhuVfNtnT6NX8bgbm_NiUM'},{icon:'📊',name:'Entrevista por Competências — Outras (RH, Recrutamento, Seg. do Trabalho)',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},],timeline:[{icon:'🔄',title:'Em andamento',date:'Abril 2026'}],competencias:['Avaliação 360°','Entrevista por Competências — Especialidade (Logística/SC)','Entrevista por Competências — Outras (RH, Recrutamento, Seg. Trabalho)']},
  sc_mecanico:{title:'Mecânico I/II / Técnico Especializado',dept:'🔧 SC (Oficina)',progress:40,docs:[{icon:'📊',name:'Checklist Competências Técnicas',type:'Google Sheets',status:100,url:'https://drive.google.com/drive/folders/1L0CGI880DymKf6zyvEyJ_KMrYKXpJxr0'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:60,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'🔄',title:'Em andamento',date:'Abril 2026'}],competencias:['Conhecimento técnico','Qualidade do trabalho','Responsabilidade']},
  sc_lavador:{title:'Lavador / Pintor',dept:'🔧 SC (Oficina)',progress:20,docs:[{icon:'📊',name:'Checklist Competências',type:'Google Sheets',status:100,url:'https://drive.google.com/drive/folders/1L0CGI880DymKf6zyvEyJ_KMrYKXpJxr0'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:30,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'⏳',title:'Aguardando início',date:'Maio 2026'}],competencias:['Qualidade do trabalho','Responsabilidade']},
  rh_gerente:{title:'Gerente de RH',dept:'👥 RH',progress:45,docs:[{icon:'📊',name:'Checklist Gerente RH',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:80,url:'https://docs.google.com/forms/d/1uqB1RbH9Ip-IMlTow0d6L7RwJ6Epmn1B3kxRSPTxptI'},{icon:'📈',name:'Resultado 360°',type:'Google Sheets',status:90,url:'https://docs.google.com/spreadsheets/d/18fhLgNG1SlHzIsfOGHRB9O5D38zSSaMnN72X7ItZB7Q'},{icon:'📄',name:'Perguntas + Competências',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'}],timeline:[{icon:'📊',title:'Checklist aplicado',date:'Abril 2026'},{icon:'🔄',title:'360° em andamento',date:'Abril 2026'}],competencias:['Habilidades de entrevista','Avaliação de candidatos','Liderança RH','Conformidade legal','Gestão de equipe']},
  rh_gerente_td:{title:'Gerente de T&D',dept:'👥 RH',progress:35,docs:[{icon:'📊',name:'Checklist T&D',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:60,url:'https://docs.google.com/forms/d/1uqB1RbH9Ip-IMlTow0d6L7RwJ6Epmn1B3kxRSPTxptI'},{icon:'📄',name:'Perguntas + Competências',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'}],timeline:[{icon:'🔄',title:'Em andamento',date:'Abril 2026'}],competencias:['Desenvolvimento de programas T&D','Liderança','Compartilhamento de conhecimento']},
  rh_coord:{title:'Coordenador RH',dept:'👥 RH',progress:40,docs:[{icon:'📊',name:'Checklist Coordenador',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:70,url:'https://docs.google.com/forms/d/1uqB1RbH9Ip-IMlTow0d6L7RwJ6Epmn1B3kxRSPTxptI'},{icon:'📄',name:'Perguntas + Competências',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'}],timeline:[{icon:'🔄',title:'Em andamento',date:'Abril 2026'}],competencias:['Gestão de processos','Feedback','Liderança operacional']},
  rh_engenheiro:{title:'Eng./Técnico de Segurança do Trabalho',dept:'👥 RH',progress:55,docs:[{icon:'📊',name:'Checklist Engenheiro de Segurança',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:80,url:'https://docs.google.com/forms/d/1uqB1RbH9Ip-IMlTow0d6L7RwJ6Epmn1B3kxRSPTxptI'},{icon:'📈',name:'Resultado 360°',type:'Google Sheets',status:80,url:'https://docs.google.com/spreadsheets/d/18fhLgNG1SlHzIsfOGHRB9O5D38zSSaMnN72X7ItZB7Q'},{icon:'📄',name:'Perguntas + Competências',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'}],timeline:[{icon:'📊',title:"Checklist NR's aplicado",date:'Abril 2026'},{icon:'🔄',title:'360° em andamento',date:'Abril 2026'}],competencias:["Conhecimento NR's",'Segurança do trabalho','EPI','Normas sanitárias','Prevenção de riscos']},
  rh_analista_sr:{title:'Analista RH / Folha Sênior',dept:'👥 RH',progress:30,docs:[{icon:'📊',name:'Checklist Analista Sr.',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:50,url:'https://docs.google.com/forms/d/1uqB1RbH9Ip-IMlTow0d6L7RwJ6Epmn1B3kxRSPTxptI'}],timeline:[{icon:'⏳',title:'Em andamento',date:'Abril 2026'}],competencias:['Gestão de folha','Legislação trabalhista','Análise de dados RH']},
  rh_analista_pl:{title:'Analista RH / Folha Pleno',dept:'👥 RH',progress:25,docs:[{icon:'📊',name:'Checklist Analista Pleno',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:40,url:'https://docs.google.com/forms/d/1uqB1RbH9Ip-IMlTow0d6L7RwJ6Epmn1B3kxRSPTxptI'}],timeline:[{icon:'⏳',title:'Aguardando',date:'Maio 2026'}],competencias:['Folha de pagamento','Benefícios','Legislação trabalhista']},
  rh_analista_jr:{title:'Analista RH / Folha Júnior',dept:'👥 RH',progress:20,docs:[{icon:'📊',name:'Checklist Analista Jr.',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:30,url:'https://docs.google.com/forms/d/1uqB1RbH9Ip-IMlTow0d6L7RwJ6Epmn1B3kxRSPTxptI'}],timeline:[{icon:'⏳',title:'Aguardando',date:'Maio 2026'}],competencias:['Folha básica','Organização','Busca por desenvolvimento']},
  rh_assistente:{title:'Assistente de RH / Folha',dept:'👥 RH',progress:15,docs:[{icon:'📊',name:'Checklist Assistente RH',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:20,url:'https://docs.google.com/forms/d/1uqB1RbH9Ip-IMlTow0d6L7RwJ6Epmn1B3kxRSPTxptI'}],timeline:[{icon:'⏳',title:'Aguardando',date:'Maio 2026'}],competencias:['Organização','Responsabilidade','Trabalho em equipe']},
  rh_assistente_seg:{title:'Assistente de Segurança do Trabalho',dept:'👥 RH',progress:15,docs:[{icon:'📊',name:'Checklist Segurança Trabalho',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:20,url:'https://docs.google.com/forms/d/1uqB1RbH9Ip-IMlTow0d6L7RwJ6Epmn1B3kxRSPTxptI'}],timeline:[{icon:'⏳',title:'Aguardando',date:'Maio 2026'}],competencias:['NR básico','EPIs','Prevenção de riscos']},
  rec_gerente:{title:'Gerente de R&S',dept:'🎯 Recrutamento',progress:60,docs:[{icon:'📊',name:'Checklist Gerente R&S',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:100,url:'https://docs.google.com/forms/d/1KOPvhti0BDCTA6DAS0uTrCMirGg8myfF4VxRFkksHhE'},{icon:'📈',name:'Resultado 360°',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1HAjNb4ntQ7CscH4Di02KFVV5x0o39f1QjPsjwN_RA40'},{icon:'📄',name:'Perguntas + Competências',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'}],timeline:[{icon:'✅',title:'360° concluído',date:'Abril 2026'}],competencias:['Seleção de candidatos','Entrevista','Avaliação de competências','Construção de funil']},
  rec_coord:{title:'Coordenadora de Recrutamento',dept:'🎯 Recrutamento',progress:45,docs:[{icon:'📊',name:'Checklist Coordenadora',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:70,url:'https://docs.google.com/forms/d/1KOPvhti0BDCTA6DAS0uTrCMirGg8myfF4VxRFkksHhE'}],timeline:[{icon:'🔄',title:'Em andamento',date:'Abril 2026'}],competencias:['Seleção','Entrevista','Feedback a candidatos']},
  rec_recrutador:{title:'Recrutador(a)',dept:'🎯 Recrutamento',progress:40,docs:[{icon:'📊',name:'Checklist Recrutador',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/11XZolXlijbeO_A4zw7xcGF6Yt4ofQYkZ4cjtl8ceQ1I'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:60,url:'https://docs.google.com/forms/d/1KOPvhti0BDCTA6DAS0uTrCMirGg8myfF4VxRFkksHhE'}],timeline:[{icon:'🔄',title:'Em andamento',date:'Abril 2026'}],competencias:['Triagem de currículos','Entrevista comportamental','Comunicação']},
  ti_gerente:{title:'Gerente de Suporte',dept:'💻 Suporte / TI',progress:35,docs:[{icon:'📊',name:'Checklist Ger. Suporte',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:50,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'🔄',title:'Em andamento',date:'Abril 2026'}],competencias:['Gestão de equipe TI','Resolução de problemas','SLA']},
  ti_analista:{title:'Analista de Suporte (QA)',dept:'💻 Suporte / TI',progress:25,docs:[{icon:'📊',name:'Checklist Analista QA',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:40,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'⏳',title:'Aguardando',date:'Maio 2026'}],competencias:['QA','Testes','Documentação técnica']},
  ti_gerente_l2:{title:'Gerente de Suporte L2',dept:'💻 Suporte / TI',progress:30,docs:[{icon:'📊',name:'Checklist Suporte L2',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:45,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'⏳',title:'Aguardando',date:'Maio 2026'}],competencias:['Suporte avançado','Escalation','Gestão de incidentes']},
  fin_analista_cont_sr:{title:'Analista Contábil Sênior',dept:'💰 Admin. / Financeiro',progress:40,docs:[{icon:'📊',name:'Checklist Contábil Sr.',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:60,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'🔄',title:'Em andamento',date:'Abril 2026'}],competencias:['Contabilidade avançada','Compliance','Relatórios financeiros']},
  fin_analista_fin_sr:{title:'Analista Financeiro Sênior',dept:'💰 Admin. / Financeiro',progress:40,docs:[{icon:'📊',name:'Checklist Financeiro Sr.',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:60,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'🔄',title:'Em andamento',date:'Abril 2026'}],competencias:['Análise financeira','Fluxo de caixa','Relatórios']},
  fin_analista_pl:{title:'Analistas Pleno',dept:'💰 Admin. / Financeiro',progress:30,docs:[{icon:'📊',name:'Checklist Analista Pleno',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:45,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'⏳',title:'Aguardando',date:'Maio 2026'}],competencias:['Contabilidade/Financeiro','Organização','Análise']},
  fin_agente:{title:'Agente Administrativo',dept:'💰 Admin. / Financeiro',progress:20,docs:[{icon:'📊',name:'Checklist Agente Admin.',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:30,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'⏳',title:'Aguardando',date:'Maio 2026'}],competencias:['Organização','Comunicação','Processos administrativos']},
  fin_assistente:{title:'Assistentes / Analistas Júnior',dept:'💰 Admin. / Financeiro',progress:15,docs:[{icon:'📊',name:'Checklist Jr.',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:20,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'⏳',title:'Aguardando',date:'Maio 2026'}],competencias:['Contabilidade básica','Organização','Responsabilidade']},
  jur_ger_gov:{title:'Ger. Relações Governamentais',dept:'⚖️ Rel. Gov. / Legal',progress:40,docs:[{icon:'📊',name:'Checklist Rel. Governamentais',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:60,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'🔄',title:'Em andamento',date:'Abril 2026'}],competencias:['Relações institucionais','Legislação','Negociação']},
  jur_ger_pub:{title:'Ger. Relações Públicas',dept:'⚖️ Rel. Gov. / Legal',progress:35,docs:[{icon:'📊',name:'Checklist RP',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:50,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'🔄',title:'Em andamento',date:'Abril 2026'}],competencias:['Comunicação externa','Imagem institucional','Gestão de crises']},
  jur_ger_jur:{title:'Gerente Jurídico',dept:'⚖️ Rel. Gov. / Legal',progress:45,docs:[{icon:'📊',name:'Checklist Jurídico',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:70,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'🔄',title:'Em andamento',date:'Abril 2026'}],competencias:['Direito empresarial','Contratos','Compliance','Gestão jurídica']},
  jur_sub:{title:'Subger. / Analistas',dept:'⚖️ Rel. Gov. / Legal',progress:25,docs:[{icon:'📊',name:'Checklist Analistas',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:40,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'⏳',title:'Aguardando',date:'Maio 2026'}],competencias:['Área específica','Análise','Comunicação']},
  jur_assist:{title:'Assistentes',dept:'⚖️ Rel. Gov. / Legal',progress:15,docs:[{icon:'📊',name:'Checklist Assistentes',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:20,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'⏳',title:'Aguardando',date:'Maio 2026'}],competencias:['Organização','Apoio administrativo']},
  mkt_ger_prom:{title:'Gerente de Promotores',dept:'📣 Promo Marketing',progress:30,docs:[{icon:'📊',name:'Checklist Ger. Promotores',type:'Google Sheets',status:100,url:'https://drive.google.com/drive/folders/1o10hMw5oV0hsuz4jUu5nrWdeK73CtLtv'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:50,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'🔄',title:'Em andamento',date:'Abril 2026'}],competencias:['Gestão de promotores','Planejamento','Liderança de campo']},
  mkt_ger_mkt:{title:'Gerente de Marketing',dept:'📣 Promo Marketing',progress:35,docs:[{icon:'📊',name:'Checklist Ger. Marketing',type:'Google Sheets',status:100,url:'https://drive.google.com/drive/folders/1o10hMw5oV0hsuz4jUu5nrWdeK73CtLtv'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:55,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'🔄',title:'Em andamento',date:'Abril 2026'}],competencias:['Estratégia de marketing','Análise de campanhas','Liderança criativa']},
  mkt_supervisor:{title:'Supervisor / Líder de Promotores',dept:'📣 Promo Marketing',progress:25,docs:[{icon:'📊',name:'Checklist Supervisor',type:'Google Sheets',status:100,url:'https://drive.google.com/drive/folders/1o10hMw5oV0hsuz4jUu5nrWdeK73CtLtv'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:35,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'⏳',title:'Aguardando',date:'Maio 2026'}],competencias:['Liderança de equipe','Metas','Feedback']},
  mkt_analista:{title:'Subger. / Analista de Marketing',dept:'📣 Promo Marketing',progress:20,docs:[{icon:'📊',name:'Checklist Analista Mkt.',type:'Google Sheets',status:100,url:'https://drive.google.com/drive/folders/1o10hMw5oV0hsuz4jUu5nrWdeK73CtLtv'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:30,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'⏳',title:'Aguardando',date:'Maio 2026'}],competencias:['Análise de dados','Campanhas','Relatórios']},
  mkt_promotor:{title:'Promotor / Instrutor',dept:'📣 Promo Marketing',progress:15,docs:[{icon:'📊',name:'Checklist Promotor',type:'Google Sheets',status:100,url:'https://drive.google.com/drive/folders/1o10hMw5oV0hsuz4jUu5nrWdeK73CtLtv'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:20,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'⏳',title:'Aguardando',date:'Maio 2026'}],competencias:['Técnicas de venda','Comunicação','Produto']},
  mkt_assistente:{title:'Assistente de Marketing',dept:'📣 Promo Marketing',progress:10,docs:[{icon:'📊',name:'Checklist Assistente Mkt.',type:'Google Sheets',status:100,url:'https://drive.google.com/drive/folders/1o10hMw5oV0hsuz4jUu5nrWdeK73CtLtv'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:15,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'⏳',title:'Aguardando',date:'Maio 2026'}],competencias:['Organização','Comunicação','Apoio criativo']},
  com_consultor:{title:'Consultor Comercial',dept:'🔋 Power Banks / Comercial',progress:25,docs:[{icon:'📊',name:'Checklist Consultor Comercial',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:40,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'⏳',title:'Aguardando',date:'Maio 2026'}],competencias:['Técnicas de venda','Negociação','Metas comerciais']},
  com_lider:{title:'Líder Vendedores de Powerbanks',dept:'🔋 Power Banks / Comercial',progress:20,docs:[{icon:'📊',name:'Checklist Líder Vendas',type:'Google Sheets',status:100,url:'https://docs.google.com/spreadsheets/d/1PCj0yMSRFbbu2XUNILYaPIatw8e0xVhsQn1kLDlzw2E'},{icon:'📋',name:'Avaliação 360°',type:'Google Forms',status:30,url:'https://docs.google.com/forms/d/1as1pVNXzrnMTb71F3hyqjhWE70KXF009U4V3hp_5HEM'}],timeline:[{icon:'⏳',title:'Aguardando',date:'Maio 2026'}],competencias:['Liderança de vendas','Metas','Produto Powerbank']},
};

const TC={'Google Sheets':{bg:'#d1fae5',color:'#065f46',border:'#a7f3d0'},'Google Forms':{bg:'#fef3c7',color:'#92400e',border:'#fde68a'},'Google Drive':{bg:'#dbeafe',color:'#1d4ed8',border:'#bfdbfe'},'PowerPoint':{bg:'#fee2e2',color:'#991b1b',border:'#fecaca'}};
const DEPTS={logistica:'log_',sc:'sc_',rh:'rh_',rec:'rec_',ti:'ti_',fin:'fin_',jur:'jur_',mkt:'mkt_',com:'com_'};

function toggleDept(el){el.closest('.dept-group').classList.toggle('open');}
function openDept(k){const g=document.querySelector(`[data-dept="${k}"]`);if(!g)return;g.classList.add('open');g.scrollIntoView({behavior:'smooth',block:'center'});const f=g.querySelector('.position-item');if(f)f.click();}
function showPosition(id,el){
  document.querySelectorAll('.position-item').forEach(i=>i.classList.remove('active'));
  if(el)el.classList.add('active');
  const pos=P[id];if(!pos)return;
  document.getElementById('overviewScreen').style.display='none';
  const pv=document.getElementById('positionView');pv.classList.add('visible');
  document.getElementById('topbarTitle').textContent=pos.title;
  document.getElementById('topbarSubtitle').textContent=pos.dept;
  document.getElementById('positionTitle').textContent=pos.title;
  document.getElementById('positionDept').textContent=pos.dept;
  document.getElementById('positionDocsCount').textContent=pos.docs.length+' documentos';
  const C=2*Math.PI*34,off=C-(pos.progress/100)*C;
  const r=document.getElementById('ringFill');r.style.strokeDasharray=C;r.style.strokeDashoffset=off;
  document.getElementById('ringPercent').textContent=pos.progress+'%';
  switchTab('docs',document.querySelectorAll('.tab')[0]);
  renderDocs(pos.docs);renderTimeline(pos.timeline);renderCompetencias(pos.competencias);
}
function renderDocs(docs){
  document.getElementById('docsGrid').innerHTML=docs.map(d=>{
    const c=TC[d.type]||{bg:'#eff6ff',color:'#1d4ed8',border:'#bfdbfe'};
    return`<a href="${d.url}" target="_blank" class="doc-card"><div class="doc-card-top"><span class="doc-icon">${d.icon}</span><span style="font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:.5px;padding:3px 8px;border-radius:6px;background:${c.bg};color:${c.color};border:1px solid ${c.border}">${d.type}</span></div><div class="doc-name">${d.name}</div><div class="doc-meta">${d.status}% completo</div><div class="doc-status-bar"><div class="doc-status-fill" style="width:${d.status}%"></div></div></a>`;
  }).join('');
}
function renderTimeline(items){
  document.getElementById('timelineContainer').innerHTML=items.map(i=>`<div class="timeline-item"><div class="timeline-dot">${i.icon}</div><div class="timeline-content"><div class="timeline-title">${i.title}</div><div class="timeline-date">${i.date}</div></div></div>`).join('');
}
function renderCompetencias(comps){
  document.getElementById('competenciasContainer').innerHTML=`<div style="display:flex;flex-wrap:wrap;gap:10px">${comps.map((c,i)=>`<div class="comp-chip"><div class="comp-num">${i+1}</div>${c}</div>`).join('')}</div>`;
}
function switchTab(id,el){
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
  if(el)el.classList.add('active');
  ['docs','timeline','competencias'].forEach(t=>{document.getElementById('tab-'+t).style.display=t===id?'block':'none';});
}
function showOverview(){
  document.getElementById('overviewScreen').style.display='block';
  document.getElementById('positionView').classList.remove('visible');
  document.querySelectorAll('.position-item').forEach(i=>i.classList.remove('active'));
  document.getElementById('topbarTitle').textContent='Visão Geral';
  document.getElementById('topbarSubtitle').textContent='Portal de Assessment — JET Brasil';
}
function filterPositions(q){
  q=q.toLowerCase();
  document.querySelectorAll('.position-item').forEach(el=>{el.style.display=!q||el.textContent.toLowerCase().includes(q)?'':'none';});
  if(q)document.querySelectorAll('.dept-group').forEach(g=>g.classList.add('open'));
}
document.addEventListener('DOMContentLoaded',()=>{const f=document.querySelector('.position-item.active');if(f)f.click();});
</script>
</body>
</html>
