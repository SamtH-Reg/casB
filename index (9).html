<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>AutoEscuela Chile - Simulador CONASET Clase B</title>
<link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #f1f5f9; --card: #ffffff; --text: #0f172a; --sub: #64748b; --muted: #94a3b8;
  --border: #e2e8f0; --accent: #f59e0b; --accent2: #1e293b; --ok: #059669; --bad: #dc2626;
  --radius: 14px; --font: 'Outfit', sans-serif; --mono: 'JetBrains Mono', monospace;
}
* { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: var(--font); background: var(--bg); color: var(--text); min-height: 100vh; -webkit-font-smoothing: antialiased; }
button { cursor: pointer; font-family: var(--font); border: none; outline: none; }
button:disabled { opacity: .45; cursor: not-allowed; }
input { font-family: var(--font); outline: none; }
.app { max-width: 480px; margin: 0 auto; min-height: 100vh; position: relative; }

/* Animations */
@keyframes fadeIn { from { opacity:0; transform:translateY(8px) } to { opacity:1; transform:translateY(0) } }
@keyframes slideUp { from { opacity:0; transform:translateY(20px) } to { opacity:1; transform:translateY(0) } }
@keyframes pulse { 0%,100%{opacity:1} 50%{opacity:.5} }
@keyframes spin { to { transform:rotate(360deg) } }
.fade-in { animation: fadeIn .4s ease both; }
.slide-up { animation: slideUp .4s ease both; }

/* LOGIN */
.login-screen { display:flex; flex-direction:column; align-items:center; justify-content:center; min-height:100vh; padding:24px; }
.login-box { width:100%; max-width:360px; background:var(--card); border-radius:20px; padding:32px 24px; box-shadow:0 8px 40px rgba(0,0,0,.08); }
.login-logo { text-align:center; margin-bottom:20px; }
.login-logo svg { width:56px; height:56px; }
.login-title { font-size:1.3rem; font-weight:800; text-align:center; margin-bottom:4px; }
.login-sub { font-size:.78rem; color:var(--sub); text-align:center; margin-bottom:24px; }
.form-group { margin-bottom:16px; }
.form-label { display:block; font-size:.75rem; font-weight:600; color:var(--sub); margin-bottom:5px; text-transform:uppercase; letter-spacing:.04em; }
.form-input { width:100%; padding:12px 14px; border:2px solid var(--border); border-radius:10px; font-size:.9rem; transition:border-color .2s; background:var(--bg); }
.form-input:focus { border-color:var(--accent); }
.login-btn { width:100%; padding:14px; border-radius:12px; background:linear-gradient(135deg,var(--accent2),#334155); color:#fff; font-size:.9rem; font-weight:700; margin-top:8px; transition:transform .1s; }
.login-btn:active { transform:scale(.97); }
.login-error { font-size:.78rem; color:var(--bad); text-align:center; margin-top:10px; }

/* HEADER */
.top-bar { display:flex; align-items:center; gap:10px; padding:12px 16px; background:var(--card); border-bottom:1px solid var(--border); position:sticky; top:0; z-index:100; }
.back-btn { background:none; font-size:1.2rem; color:var(--sub); padding:4px 8px; border-radius:8px; }
.top-title { font-size:.95rem; font-weight:700; flex:1; }
.avatar-btn { width:32px; height:32px; border-radius:50%; background:var(--accent); color:var(--accent2); font-size:.75rem; font-weight:800; display:flex; align-items:center; justify-content:center; }

/* HOME HEADER */
.home-header { display:flex; align-items:center; gap:12px; padding:16px 16px 0; }
.brand-title { font-size:1.15rem; font-weight:800; letter-spacing:-.02em; }
.brand-sub { font-size:.68rem; color:var(--muted); font-weight:500; }

/* PROGRESS CARD */
.prog-card { margin:14px 16px 0; padding:18px; border-radius:18px; background:linear-gradient(135deg,#0f172a,#1e293b); color:#fff; }
.prog-top { display:flex; justify-content:space-between; align-items:center; }
.prog-label { font-size:.7rem; color:var(--muted); }
.prog-pct { font-size:2rem; font-weight:800; color:var(--accent); font-family:var(--mono); }
.prog-stats { display:flex; gap:16px; margin-top:14px; padding-top:14px; border-top:1px solid #334155; }
.prog-stat { display:flex; flex-direction:column; align-items:center; flex:1; }
.stat-num { font-size:1.05rem; font-weight:700; font-family:var(--mono); }
.stat-label { font-size:.62rem; color:var(--muted); margin-top:2px; }
.prog-bar-outer { height:6px; border-radius:3px; background:#334155; margin-top:14px; overflow:hidden; }
.prog-bar-inner { height:100%; border-radius:3px; background:linear-gradient(90deg,var(--accent),#eab308); transition:width .6s ease; }
.prog-msg { font-size:.68rem; color:var(--muted); text-align:center; margin-top:8px; }

/* WEAK ALERT */
.weak-box { margin:12px 16px 0; padding:12px; border-radius:12px; background:#fffbeb; border:1px solid #fde68a; }
.weak-title { font-size:.8rem; font-weight:700; margin-bottom:6px; }
.weak-chips { display:flex; flex-wrap:wrap; gap:5px; margin-bottom:8px; }
.weak-chip { font-size:.67rem; font-weight:600; padding:3px 8px; border-radius:6px; border:1.5px solid; background:#fff; }
.refuerzo-btn { width:100%; padding:9px; border-radius:8px; background:var(--accent); color:var(--accent2); font-size:.78rem; font-weight:700; }

/* ACTIONS */
.actions { display:flex; flex-direction:column; gap:10px; margin:16px 16px 0; }
.action-btn { display:flex; align-items:center; gap:12px; padding:14px 16px; border:1.5px solid var(--border); border-radius:var(--radius); background:var(--card); text-align:left; width:100%; transition:all .15s; }
.action-btn.dark { background:linear-gradient(135deg,#0f172a,#1e293b); color:#fff; border:none; box-shadow:0 4px 20px rgba(15,23,42,.2); }
.action-icon { font-size:1.4rem; }
.action-label { font-size:.88rem; font-weight:700; }
.action-desc { font-size:.7rem; color:var(--muted); margin-top:1px; }
.action-arrow { margin-left:auto; font-size:1.1rem; color:var(--muted); }

/* INFO BAR */
.info-bar { display:grid; grid-template-columns:repeat(4,1fr); gap:8px; margin:16px 16px 0; }
.info-item { text-align:center; padding:10px 4px; background:var(--card); border-radius:10px; border:1px solid var(--border); font-size:.62rem; color:var(--muted); }
.info-num { display:block; font-size:1.1rem; font-weight:700; color:var(--accent); font-family:var(--mono); }

/* TEMARIOS */
.tem-list { padding:8px 16px 30px; }
.tem-card { display:flex; align-items:center; gap:12px; width:100%; padding:14px; border:1.5px solid var(--border); border-radius:var(--radius); background:var(--card); text-align:left; margin-bottom:10px; }
.tem-icon { width:52px; height:52px; border-radius:12px; display:flex; align-items:center; justify-content:center; flex-shrink:0; overflow:hidden; }
.tem-title { font-size:.85rem; font-weight:700; }
.tem-desc { font-size:.7rem; color:var(--muted); margin-top:2px; line-height:1.4; }
.tem-studied { font-size:.67rem; background:#f0fdf4; color:var(--ok); border-radius:4px; padding:1px 6px; font-weight:700; margin-left:6px; }
.tem-errors { font-size:.63rem; color:var(--bad); font-weight:600; margin-top:3px; display:inline-block; }
.tem-arrow { font-size:1.3rem; color:#cbd5e1; flex-shrink:0; margin-left:auto; }

/* TEMARIO DETALLE */
.tem-hero { margin:0 16px; padding:22px; border-radius:16px; text-align:center; }
.tem-hero svg, .tem-hero img { max-width:80px; height:auto; }
.tem-section { background:var(--card); border:1px solid var(--border); border-radius:var(--radius); padding:16px; margin:0 16px 12px; }
.tem-sec-title { font-size:.88rem; font-weight:700; margin-bottom:8px; }
.tem-sec-text { font-size:.8rem; color:#475569; line-height:1.65; }
.tem-sec-illust { display:flex; justify-content:center; margin:8px 0; }
.tem-actions { padding:12px 16px 30px; display:flex; flex-direction:column; gap:8px; }
.tem-test-btn { padding:13px; border-radius:12px; color:#fff; font-size:.85rem; font-weight:700; }
.tem-mark-btn { padding:11px; border:2px solid var(--border); border-radius:12px; background:var(--card); font-size:.82rem; font-weight:600; color:#475569; }

/* EXAMEN */
.exam-top { display:flex; align-items:center; justify-content:space-between; padding:10px 16px; background:var(--card); border-bottom:1px solid var(--border); position:sticky; top:0; z-index:100; }
.exam-label { font-size:.8rem; font-weight:600; color:var(--sub); }
.timer-badge { padding:5px 12px; border-radius:20px; background:var(--bg); font-size:.8rem; font-weight:600; font-family:var(--mono); color:#334155; }
.timer-badge.low { background:#fef2f2; color:var(--bad); animation:pulse 1s ease infinite; }
.prog-wrap { height:4px; background:var(--border); margin:0 16px; }
.prog-fill { height:100%; border-radius:2px; background:linear-gradient(90deg,var(--accent),#eab308); transition:width .4s; }
.prog-text { font-size:.66rem; color:var(--muted); text-align:right; padding:3px 16px 0; }
.dots-toggle { display:block; width:100%; background:none; border-bottom:1px solid var(--border); color:var(--sub); font-size:.7rem; padding:5px 16px; text-align:center; }
.dots-grid { display:grid; grid-template-columns:repeat(7,1fr); gap:5px; padding:8px 16px; background:var(--card); border-bottom:1px solid var(--border); }
.dot { aspect-ratio:1; border-radius:7px; border:1.5px solid var(--border); font-size:.63rem; font-weight:600; display:flex; flex-direction:column; align-items:center; justify-content:center; position:relative; line-height:1; background:var(--card); color:var(--muted); }
.dot.current { border-color:var(--accent); background:#fffbeb; color:#b45309; box-shadow:0 0 0 2px rgba(245,158,11,.2); }
.dot.ok { background:#f0fdf4; border-color:var(--ok); color:var(--ok); }
.dot.bad { background:#fef2f2; border-color:var(--bad); color:var(--bad); }
.dot.answered { background:var(--bg); border-color:var(--muted); color:#475569; }
.dot-x2 { position:absolute; top:-3px; right:-3px; font-size:.43rem; background:var(--bad); color:#fff; border-radius:3px; padding:1px 2px; font-weight:700; }

/* QUESTION */
.q-box { padding:16px; }
.q-meta { display:flex; align-items:center; gap:6px; flex-wrap:wrap; margin-bottom:10px; }
.q-tema { font-size:.66rem; font-weight:600; padding:3px 8px; border-radius:5px; }
.q-doble { font-size:.66rem; font-weight:700; padding:3px 8px; border-radius:5px; background:linear-gradient(135deg,#dc2626,#ef4444); color:#fff; }
.q-illust { display:flex; justify-content:center; margin:8px 0 12px; }
.q-illust img { max-width:100%; max-height:150px; border-radius:10px; object-fit:cover; box-shadow:0 2px 12px rgba(0,0,0,.1); }
.q-num { font-size:.7rem; color:var(--muted); margin-bottom:4px; }
.q-text { font-size:.95rem; font-weight:600; line-height:1.5; margin-bottom:16px; }
.change-hint { font-size:.65rem; color:var(--accent); text-align:center; margin-top:8px; opacity:.8; }
.opts { display:flex; flex-direction:column; gap:8px; }
.opt { display:flex; align-items:flex-start; gap:10px; padding:12px 14px; border:2px solid var(--border); border-radius:11px; background:var(--card); text-align:left; width:100%; font-size:.83rem; line-height:1.4; color:#334155; transition:all .15s; }
.opt.sel { border-color:var(--accent); background:#fffbeb; }
.opt.ok { border-color:var(--ok); background:#f0fdf4; }
.opt.bad { border-color:var(--bad); background:#fef2f2; }
.opt-letter { min-width:26px; height:26px; border-radius:7px; display:flex; align-items:center; justify-content:center; font-size:.73rem; font-weight:700; background:var(--bg); color:var(--sub); flex-shrink:0; }
.opt.sel .opt-letter { background:var(--accent); color:#fff; }
.opt.ok .opt-letter { background:var(--ok); color:#fff; }
.opt.bad .opt-letter { background:var(--bad); color:#fff; }
.expl-box { margin-top:16px; padding:14px; border-radius:11px; border:1px solid; }
.expl-box.correct { background:#f0fdf4; border-color:#bbf7d0; }
.expl-box.wrong { background:#fef2f2; border-color:#fecaca; }
.expl-head { font-size:.83rem; font-weight:700; margin-bottom:6px; }
.expl-text { font-size:.78rem; color:#334155; line-height:1.6; }

/* NAV */
.nav-row { display:flex; gap:8px; padding:14px 16px; }
.nav-btn { flex:1; padding:11px; border:2px solid var(--border); border-radius:11px; background:var(--card); font-size:.8rem; font-weight:600; color:var(--sub); }
.nav-btn.next { background:var(--accent2); color:#fff; border:none; }
.nav-btn.finish { background:linear-gradient(135deg,var(--accent),#eab308); color:var(--accent2); border:none; font-weight:700; }

/* RESULTADO */
.res-banner { text-align:center; padding:30px 20px; border-radius:0 0 20px 20px; color:#fff; }
.res-banner.pass { background:linear-gradient(135deg,#059669,#10b981); }
.res-banner.fail { background:linear-gradient(135deg,#dc2626,#ef4444); }
.res-title { font-size:1.5rem; font-weight:800; letter-spacing:-.02em; }
.res-sub { font-size:.82rem; opacity:.9; margin-top:4px; }
.res-grid { display:grid; grid-template-columns:repeat(3,1fr); gap:8px; padding:14px 16px 0; }
.res-card { text-align:center; padding:12px 6px; background:var(--card); border-radius:12px; border:1px solid var(--border); }
.res-num { font-size:1.2rem; font-weight:800; font-family:var(--mono); }
.res-label { font-size:.68rem; font-weight:600; color:var(--sub); margin-top:2px; }
.res-temas { margin:14px 16px 0; background:var(--card); border-radius:var(--radius); border:1px solid var(--border); padding:16px; }
.res-tema-row { margin-bottom:12px; }
.res-tema-header { display:flex; justify-content:space-between; margin-bottom:3px; }
.res-tema-name { font-size:.76rem; font-weight:600; }
.res-tema-score { font-size:.76rem; font-weight:600; font-family:var(--mono); }
.res-tema-bar { height:5px; border-radius:3px; background:var(--bg); overflow:hidden; }
.res-tema-fill { height:100%; border-radius:3px; transition:width .6s; }
.res-actions { display:flex; gap:8px; padding:16px; }
.rev-btn { flex:1; padding:12px; border:2px solid var(--border); border-radius:11px; background:var(--card); font-size:.8rem; font-weight:600; color:#475569; }
.new-btn { flex:1; padding:12px; border-radius:11px; background:linear-gradient(135deg,#0f172a,#1e293b); color:#fff; font-size:.8rem; font-weight:600; }

/* REVISION */
.rev-card { background:var(--card); border-radius:13px; border:1px solid var(--border); padding:16px; margin:0 16px 12px; }
.rev-opt { display:flex; gap:8px; align-items:flex-start; padding:6px 8px; border-radius:7px; font-size:.78rem; line-height:1.4; background:var(--bg); margin-bottom:4px; }
.rev-opt.ok { background:#f0fdf4; color:#065f46; font-weight:500; }
.rev-opt.bad { background:#fef2f2; color:#991b1b; text-decoration:line-through; opacity:.8; }
.rev-letter { min-width:20px; height:20px; border-radius:5px; display:flex; align-items:center; justify-content:center; font-size:.66rem; font-weight:700; flex-shrink:0; }
.rev-expl { font-size:.76rem; color:#475569; line-height:1.6; padding:10px; background:var(--bg); border-radius:7px; border-left:3px solid var(--accent); margin-top:8px; }

/* SETTINGS */
.settings-section { margin:0 16px 16px; background:var(--card); border-radius:var(--radius); border:1px solid var(--border); padding:16px; }
.settings-title { font-size:.88rem; font-weight:700; margin-bottom:12px; }
.user-row { display:flex; align-items:center; justify-content:space-between; padding:8px 0; border-bottom:1px solid var(--border); }
.user-row:last-child { border-bottom:none; }
.user-name { font-size:.82rem; font-weight:600; }
.user-role { font-size:.65rem; color:var(--muted); }
.del-user-btn { font-size:.7rem; color:var(--bad); background:none; font-weight:600; padding:4px 8px; }
.add-user-form { display:flex; gap:6px; margin-top:10px; }
.add-user-form input { flex:1; padding:8px 10px; border:1.5px solid var(--border); border-radius:8px; font-size:.8rem; }
.add-user-btn { padding:8px 14px; border-radius:8px; background:var(--accent2); color:#fff; font-size:.78rem; font-weight:600; white-space:nowrap; }

.disclaimer { font-size:.65rem; color:#cbd5e1; text-align:center; margin:14px 16px 24px; line-height:1.5; }
.logout-btn { display:block; margin:8px auto 20px; background:none; color:var(--muted); font-size:.72rem; text-decoration:underline; }
</style>
</head>
<body>
<div class="app" id="app"></div>

<script>
// ═══════════════════════════════════════════════════════════════════════
// AUTOESCUELA CHILE - COMPLETE APP
// ═══════════════════════════════════════════════════════════════════════

// ── SVG ILLUSTRATIONS ────────────────────────────────────────────────
const SVG = {
  logo: `<svg viewBox="0 0 50 50" xmlns="http://www.w3.org/2000/svg"><circle cx="25" cy="25" r="23" fill="#0f172a" stroke="#f59e0b" stroke-width="2"/><path d="M15 32 L25 12 L35 32" fill="none" stroke="#f59e0b" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"/><line x1="19" y1="26" x2="31" y2="26" stroke="#f59e0b" stroke-width="2.5" stroke-linecap="round"/><circle cx="25" cy="37" r="2.5" fill="#f59e0b"/></svg>`,
  pare: `<svg viewBox="0 0 80 80"><polygon points="40,4 68,16 76,44 64,72 40,80 16,72 4,44 12,16" fill="#cc0000" stroke="#fff" stroke-width="2.5"/><text x="40" y="46" text-anchor="middle" fill="#fff" font-size="16" font-weight="bold" font-family="sans-serif">PARE</text></svg>`,
  cedaPaso: `<svg viewBox="0 0 80 80"><polygon points="40,72 4,8 76,8" fill="#fff" stroke="#cc0000" stroke-width="4"/><text x="40" y="32" text-anchor="middle" fill="#333" font-size="9" font-weight="bold">CEDA</text><text x="40" y="46" text-anchor="middle" fill="#333" font-size="9" font-weight="bold">EL PASO</text></svg>`,
  velocidad: `<svg viewBox="0 0 80 80"><circle cx="40" cy="40" r="35" fill="#fff" stroke="#cc0000" stroke-width="5"/><text x="40" y="47" text-anchor="middle" fill="#333" font-size="22" font-weight="bold">60</text></svg>`,
  curva: `<svg viewBox="0 0 80 80"><rect x="8" y="8" width="64" height="64" rx="3" fill="#f7c948" stroke="#333" stroke-width="1.5" transform="rotate(45 40 40)"/><path d="M28 56 Q28 28 52 28" fill="none" stroke="#333" stroke-width="5" stroke-linecap="round"/><polygon points="52,20 60,28 52,32" fill="#333"/></svg>`,
  peatones: `<svg viewBox="0 0 80 80"><rect x="8" y="8" width="64" height="64" rx="3" fill="#f7c948" stroke="#333" stroke-width="1.5" transform="rotate(45 40 40)"/><circle cx="40" cy="24" r="5.5" fill="#333"/><line x1="40" y1="30" x2="40" y2="47" stroke="#333" stroke-width="3"/><line x1="40" y1="34" x2="30" y2="42" stroke="#333" stroke-width="2.5"/><line x1="40" y1="34" x2="50" y2="42" stroke="#333" stroke-width="2.5"/><line x1="40" y1="47" x2="30" y2="60" stroke="#333" stroke-width="2.5"/><line x1="40" y1="47" x2="50" y2="60" stroke="#333" stroke-width="2.5"/></svg>`,
  info: `<svg viewBox="0 0 80 80"><rect x="6" y="16" width="68" height="48" rx="5" fill="#006b3f" stroke="#fff" stroke-width="2.5"/><text x="40" y="38" text-anchor="middle" fill="#fff" font-size="10" font-weight="bold">Santiago</text><text x="40" y="52" text-anchor="middle" fill="#fff" font-size="9">120 km →</text></svg>`,
  tablero: `<svg viewBox="0 0 120 60"><rect x="4" y="4" width="112" height="52" rx="7" fill="#1e293b"/><circle cx="30" cy="30" r="15" fill="none" stroke="#475569" stroke-width="1.5"/><text x="30" y="34" text-anchor="middle" fill="#22c55e" font-size="11" font-weight="bold">80</text><text x="30" y="50" text-anchor="middle" fill="#94a3b8" font-size="5.5">km/h</text><circle cx="65" cy="30" r="15" fill="none" stroke="#475569" stroke-width="1.5"/><line x1="65" y1="30" x2="65" y2="18" stroke="#ef4444" stroke-width="1.5"/><text x="65" y="50" text-anchor="middle" fill="#94a3b8" font-size="5.5">RPM</text><rect x="86" y="18" width="22" height="7" rx="2" fill="#1e293b" stroke="#475569" stroke-width="1"/><rect x="86" y="18" width="14" height="7" rx="2" fill="#22c55e"/><circle cx="92" cy="42" r="3.5" fill="#ef4444"/><circle cx="102" cy="42" r="3.5" fill="#fbbf24"/></svg>`,
  neumatico: `<svg viewBox="0 0 70 70"><circle cx="35" cy="35" r="30" fill="#1e293b"/><circle cx="35" cy="35" r="24" fill="#334155"/><circle cx="35" cy="35" r="10" fill="#94a3b8"/><circle cx="35" cy="35" r="5" fill="#64748b"/></svg>`,
  alcohol: `<svg viewBox="0 0 70 80"><circle cx="35" cy="40" r="30" fill="none" stroke="#dc2626" stroke-width="2.5"/><rect x="22" y="10" width="26" height="35" rx="3" fill="none" stroke="#dc2626" stroke-width="2.5"/><rect x="25" y="25" width="20" height="18" rx="1" fill="#fca5a5" opacity=".5"/><line x1="12" y1="12" x2="58" y2="68" stroke="#dc2626" stroke-width="4" stroke-linecap="round"/></svg>`,
  sri: `<svg viewBox="0 0 70 80"><path d="M18 75 L18 30 Q18 12 35 12 Q52 12 52 30 L52 75" fill="none" stroke="#f59e0b" stroke-width="3.5"/><rect x="20" y="30" width="30" height="42" rx="7" fill="#fef3c7" stroke="#f59e0b" stroke-width="2"/><circle cx="35" cy="24" r="7" fill="#fbbf24"/><line x1="28" y1="44" x2="42" y2="44" stroke="#f59e0b" stroke-width="2.5" stroke-linecap="round"/><line x1="35" y1="38" x2="35" y2="58" stroke="#f59e0b" stroke-width="2.5" stroke-linecap="round"/></svg>`,
  cinturon: `<svg viewBox="0 0 70 80"><circle cx="35" cy="20" r="9" fill="none" stroke="#0891b2" stroke-width="2.5"/><line x1="35" y1="29" x2="35" y2="52" stroke="#0891b2" stroke-width="2.5"/><path d="M22 38 L35 52 L48 38" fill="none" stroke="#ef4444" stroke-width="3.5" stroke-linecap="round" stroke-linejoin="round"/><rect x="30" y="50" width="10" height="5" rx="2" fill="#ef4444"/></svg>`,
  efectoTunel: `<svg viewBox="0 0 100 60"><rect x="0" y="0" width="100" height="60" fill="#1e293b" rx="4"/><ellipse cx="50" cy="30" rx="45" ry="25" fill="none" stroke="#475569" stroke-width="1.2" stroke-dasharray="3,2"/><ellipse cx="50" cy="30" rx="30" ry="18" fill="none" stroke="#64748b" stroke-width="1.2" stroke-dasharray="3,2"/><ellipse cx="50" cy="30" rx="16" ry="10" fill="#f59e0b" opacity=".25"/><ellipse cx="50" cy="30" rx="6" ry="4" fill="#f59e0b" opacity=".5"/><text x="50" y="55" text-anchor="middle" fill="#94a3b8" font-size="6">Campo visual reducido</text></svg>`,
  lluvia: `<svg viewBox="0 0 80 65"><path d="M20 32 Q20 16 40 16 Q52 8 62 20 Q72 20 68 32" fill="#94a3b8"/><line x1="24" y1="40" x2="20" y2="52" stroke="#3b82f6" stroke-width="1.5" stroke-linecap="round"/><line x1="36" y1="38" x2="32" y2="54" stroke="#3b82f6" stroke-width="1.5" stroke-linecap="round"/><line x1="48" y1="40" x2="44" y2="52" stroke="#3b82f6" stroke-width="1.5" stroke-linecap="round"/><line x1="60" y1="38" x2="56" y2="50" stroke="#3b82f6" stroke-width="1.5" stroke-linecap="round"/></svg>`,
  primerAux: `<svg viewBox="0 0 70 70"><rect x="8" y="8" width="54" height="54" rx="10" fill="#dc2626"/><rect x="28" y="16" width="14" height="38" rx="2.5" fill="#fff"/><rect x="16" y="28" width="38" height="14" rx="2.5" fill="#fff"/></svg>`,
};

function svgHTML(key, size=50) {
  return `<div style="width:${size}px;height:${size}px;flex-shrink:0;display:inline-flex">${SVG[key]||''}</div>`;
}

// ── STORAGE HELPERS ──────────────────────────────────────────────────
const LS = {
  get(k) { try { return JSON.parse(localStorage.getItem(k)); } catch(e) { return null; } },
  set(k,v) { localStorage.setItem(k, JSON.stringify(v)); },
  del(k) { localStorage.removeItem(k); }
};

// ── USER SYSTEM ──────────────────────────────────────────────────────
function getUsers() {
  let u = LS.get('ae_users');
  if (!u || !u.length) {
    u = [{ username:'admin', password:'123456', role:'admin', created: new Date().toISOString() }];
    LS.set('ae_users', u);
  }
  return u;
}
function saveUsers(u) { LS.set('ae_users', u); }
function getSession() { return LS.get('ae_session'); }
function setSession(u) { LS.set('ae_session', u); }
function clearSession() { LS.del('ae_session'); }
function getUserProgress(username) { return LS.get('ae_prog_'+username) || { temasEstudiados:{}, examenes:[], erroresPorTema:{}, preguntasRespondidas:{}, preguntasCorrectas:{} }; }
function saveUserProgress(username, p) { LS.set('ae_prog_'+username, p); }

// ── TEMARIOS ─────────────────────────────────────────────────────────
const TEMARIOS = [
  { id:"convivencia", titulo:"Convivencia Vial", icono:"🤝", color:"#059669", desc:"Educación vial, respeto y seguridad compartida", svg:"pare",
    contenido:[
      {t:"¿Qué es la Convivencia Vial?", txt:"Es la interacción armoniosa y segura entre conductores, peatones, ciclistas y todos los usuarios de las vías. Se basa en respeto, solidaridad, comprensión y tolerancia."},
      {t:"Educación Vial", txt:"Adquisición de valores para la conducción: hábitos positivos, conocimiento de la Ley de Tránsito y señales. La meta es eliminar los siniestros de tránsito."},
      {t:"Siniestros vs Accidentes", txt:"Se usa 'siniestro' porque la mayoría son prevenibles. El 90% ocurre por falla humana. Más de 3.000 personas mueren diariamente en el mundo por esta causa."},
      {t:"Responsabilidad Colectiva", txt:"Conducir ebrio o sin cinturón no es decisión personal: afecta a todos. Los costos médicos, legales y emocionales los paga toda la sociedad."},
    ]},
  { id:"individuo", titulo:"El Individuo en el Tránsito", icono:"🧠", color:"#7c3aed", desc:"Capacidades del conductor, percepción del riesgo, fatiga y alcohol", svg:"alcohol",
    contenido:[
      {t:"Capacidades del Conductor", txt:"Se necesita: buena visión, concentración, velocidad de reacción adecuada y estado emocional estable. Cualquier alteración aumenta el riesgo."},
      {t:"Efectos del Alcohol", txt:"Con 0,3 g/l = 'bajo la influencia'. Con 0,8 g/l = 'estado de ebriedad'. Deteriora juicio, coordinación, tiempo de reacción. Genera falsa confianza.", svg:"alcohol", img:"https://cdn.pixabay.com/photo/2017/06/09/14/09/drink-2387193_640.jpg"},
      {t:"Ley Emilia (20.770)", txt:"Cárcel efectiva para quien conduzca ebrio y cause lesiones graves o muerte. Si hay siniestro, se presume culpabilidad del conductor ebrio."},
      {t:"Fatiga y Somnolencia", txt:"Reduce atención, aumenta tiempos de reacción, puede provocar microsueños. Descansar cada 2 horas, no más de 4 horas seguidas."},
      {t:"Medicamentos", txt:"Ansiolíticos, antihistamínicos, antidepresivos pueden producir somnolencia y alterar reflejos. Consultar al médico antes de conducir."},
    ]},
  { id:"vulnerables", titulo:"Usuarios Vulnerables", icono:"🚶", color:"#ea580c", desc:"Peatones, ciclistas, niños, adultos mayores", svg:"peatones",
    contenido:[
      {t:"¿Quiénes son?", txt:"Peatones, ciclistas, motociclistas, niños, adultos mayores y personas con discapacidad. 15% de siniestros pero 40% de las muertes.", svg:"peatones", img:"https://cdn.pixabay.com/photo/2016/11/22/21/57/crosswalk-1850688_640.jpg"},
      {t:"Peatones", txt:"Preferencia en cruces demarcados. El conductor debe detenerse completamente en paso de cebra."},
      {t:"Ciclistas", txt:"Ley 21.088: mínimo 1,5 metros de distancia lateral al adelantar. Respetar ciclovías y zonas de espera adelantada."},
      {t:"Niños y Adultos Mayores", txt:"Niños: baja percepción del riesgo, pueden aparecer inesperadamente. Adultos mayores: movilidad o audición reducida."},
    ]},
  { id:"normas", titulo:"Normas de Circulación", icono:"📜", color:"#2563eb", desc:"Velocidades, adelantamientos, estacionamiento, virajes", svg:"velocidad",
    contenido:[
      {t:"Velocidades Máximas", txt:"Urbana: 60 km/h. Rural: 100 km/h (livianos). Autopistas: 120 km/h. Zonas escolares: 30 km/h. Prevalece la señalización local.", svg:"velocidad", img:"https://cdn.pixabay.com/photo/2018/01/28/10/59/speed-limit-3113592_640.jpg"},
      {t:"Adelantamiento", txt:"Solo donde la señalización lo permita (línea segmentada). Nunca en intersecciones, curvas, puentes, pasos peatonales o túneles. Por la izquierda."},
      {t:"Estacionamiento", txt:"Prohibido a menos de 10m de esquinas y señales PARE/CEDA. Línea amarilla continua = prohibido estacionar y detenerse."},
      {t:"Virajes", txt:"Señalizar con anticipación mínima de 30m en zona urbana. Usar intermitentes. Verificar espejos y punto ciego."},
      {t:"Autopistas", txt:"Si se pasa una salida, continuar hasta la siguiente autorizada. Nunca retroceder ni hacer virajes en U."},
      {t:"Luces", txt:"Obligatorio circular con luces bajas las 24 horas, en todas las vías, desde 2005 (Art. 68 Ley de Tránsito)."},
    ]},
  { id:"conduccion", titulo:"Conducción Segura", icono:"🛡️", color:"#0891b2", desc:"Conducción defensiva, distancias, efecto túnel", svg:"efectoTunel",
    contenido:[
      {t:"Conducción Defensiva", txt:"Anticiparse a riesgos, mantener distancia segura, estar atento al entorno. Prever lo que otros pueden hacer mal."},
      {t:"Efecto Túnel", txt:"A mayor velocidad, el campo visual lateral se reduce. A 65 km/h = 70°. A 130 km/h = solo 30°.", svg:"efectoTunel", img:"https://cdn.pixabay.com/photo/2016/01/19/17/53/car-1149997_640.jpg"},
      {t:"Distancia de Frenado", txt:"Al duplicar velocidad, distancia de frenado se CUADRUPLICA (E=½mv²). Regla de los 3 segundos para distancia segura."},
      {t:"Zona de Incertidumbre", txt:"Espacio alrededor de peatones/ciclistas donde podrían moverse impredeciblemente. Ampliar distancia al pasar."},
      {t:"Conducción bajo Lluvia", txt:"Reducir velocidad, aumentar distancia, encender luces bajas. Riesgo de aquaplaning con neumáticos desgastados.", svg:"lluvia", img:"https://cdn.pixabay.com/photo/2016/11/29/09/32/auto-1868726_640.jpg"},
      {t:"Celular", txt:"Prohibido manipular celular al conducir. Solo manos libres. Multa gravísima (Art. 107)."},
    ]},
  { id:"senales", titulo:"Señales de Tránsito", icono:"🚦", color:"#dc2626", desc:"Reglamentarias, preventivas, informativas, demarcación", svg:"pare",
    contenido:[
      {t:"Clasificación", txt:"Reglamentarias (circulares), Preventivas (romboidales/diamante), Informativas (rectangulares). PARE y CEDA son excepciones."},
      {t:"Reglamentarias", txt:"Cumplimiento obligatorio. Prioridad (PARE, CEDA), prohibición (No entrar), restricción (Velocidad máxima), obligación. Circular, borde rojo.", svg:"pare", img:"https://upload.wikimedia.org/wikipedia/commons/thumb/e/ef/Chile_road_sign_RPO-1.svg/240px-Chile_road_sign_RPO-1.svg.png"},
      {t:"Preventivas", txt:"Advierten peligros: curvas, cruces, peatones, animales, resaltos. Rombo, fondo amarillo, símbolo negro.", svg:"curva", img:"https://upload.wikimedia.org/wikipedia/commons/thumb/0/09/Chile_road_sign_PG-1a.svg/240px-Chile_road_sign_PG-1a.svg.png"},
      {t:"Informativas", txt:"Guían con rutas, distancias, servicios. Rectangular, fondo verde, texto blanco.", svg:"info"},
      {t:"Demarcación Horizontal", txt:"Continua: no cruzar. Segmentada: permitido. Amarilla en solera: prohibido estacionar. Paso cebra: preferencia peatonal."},
    ]},
  { id:"vehiculo", titulo:"Conoce tu Vehículo", icono:"🔧", color:"#4f46e5", desc:"Panel, frenos, neumáticos, aceite, mecánica básica", svg:"tablero",
    contenido:[
      {t:"Panel de Instrumentos", txt:"Indicadores de velocidad, RPM, temperatura, combustible. Testigos: aceite, batería, ABS, airbag.", svg:"tablero", img:"https://cdn.pixabay.com/photo/2019/07/07/14/03/fiat-4322521_640.jpg"},
      {t:"Sistema de Frenos", txt:"Convencionales y ABS (antibloqueo). ABS evita bloqueo de ruedas, mantiene control de dirección. Líquido de frenos transmite presión hidráulica."},
      {t:"Neumáticos", txt:"Profundidad mínima dibujo: 1,6mm (recomendable 3mm). Revisar presión cada 500km o mensualmente, en frío.", svg:"neumatico", img:"https://cdn.pixabay.com/photo/2013/07/12/18/39/tire-153720_640.png"},
      {t:"Aceite y Batería", txt:"Luz de aceite = presión insuficiente, detenerse. Batería en mal estado dificulta arranque en frío."},
    ]},
  { id:"seguridad", titulo:"Seguridad Pasiva y SRI", icono:"🧒", color:"#f59e0b", desc:"Cinturón, airbag, sistemas de retención infantil", svg:"sri",
    contenido:[
      {t:"Cinturón de Seguridad", txt:"Obligatorio SIEMPRE para todos. Individual. Reduce 50% riesgo de muerte en siniestros frontales.", svg:"cinturon", img:"https://cdn.pixabay.com/photo/2019/12/20/14/44/seatbelt-4709004_640.jpg"},
      {t:"Airbag", txt:"Complementario al cinturón, NO lo reemplaza. Sin cinturón = 'efecto rebote': airbag empuja cuerpo violentamente hacia atrás."},
      {t:"Sistema de Retención Infantil (SRI)", txt:"Obligatorio para niños. Compatible con vehículo (ISOFIX o cinturón) y adecuado al peso/talla. Ley 20.904. Asientos traseros.", svg:"sri", img:"https://cdn.pixabay.com/photo/2017/11/10/00/28/new-born-2935722_640.jpg"},
      {t:"Doble Puntaje en Examen", txt:"Preguntas sobre alcohol/drogas, velocidad y SRI valen DOBLE (2 pts c/u). 3 preguntas por examen. Fallar las 3 = reprobación automática."},
    ]},
  { id:"emergencias", titulo:"Emergencias y Primeros Auxilios", icono:"🚑", color:"#be185d", desc:"Conducta PAS, siniestros, documentación", svg:"primerAux",
    contenido:[
      {t:"Conducta PAS", txt:"Proteger (señalizar zona), Alertar (131/132/133), Socorrer (según capacidad). No mover heridos innecesariamente.", svg:"primerAux", img:"https://cdn.pixabay.com/photo/2012/04/14/14/04/emergency-34684_640.png"},
      {t:"Documentación Obligatoria", txt:"Licencia vigente, permiso de circulación, SOAP, revisión técnica al día."},
      {t:"Vehículos de Emergencia", txt:"Ambulancias, bomberos, policía con sirenas tienen preferencia absoluta. Desplazarse a la derecha y detenerse."},
    ]},
];

// ── BANCO DE PREGUNTAS (40+) ─────────────────────────────────────────
const PREGUNTAS = [
  // Convivencia (0-4)
  {id:"c1",tema:"convivencia",p:"¿Qué es la Convivencia Vial?",o:["Solo respetar semáforos","Interacción armoniosa y segura entre todos los usuarios de las vías","Conducir sin exceder velocidad máxima"],c:1,e:"La Convivencia Vial es la interacción armoniosa entre conductores, peatones, ciclistas, basada en respeto y tolerancia.",d:false},
  {id:"c2",tema:"convivencia",p:"¿Por qué se usa 'siniestro' y no 'accidente'?",o:["Suena más formal","Porque la mayoría son prevenibles y no casuales","Lo exige la ley internacional"],c:1,e:"El 90% ocurre por falla humana. 'Siniestro' refleja que son evitables.",d:false},
  {id:"c3",tema:"convivencia",p:"La Educación Vial busca inculcar:",o:["Solo conocimiento de señales","Valores de respeto, solidaridad y conocimiento de normas","Habilidades mecánicas"],c:1,e:"Incluye valores, normas de comportamiento (Ley de Tránsito) y conocimiento de señalización.",d:false},
  {id:"c4",tema:"convivencia",p:"¿Conducir ebrio es una decisión personal?",o:["Sí, solo afecta al conductor","No, afecta a toda la sociedad","Sí, si no causa siniestros"],c:1,e:"No es personal. Un siniestro afecta a todos con costos médicos, legales y emocionales.",d:false},
  {id:"c5",tema:"convivencia",p:"La meta de la Seguridad Vial es:",o:["Reducir la velocidad máxima","La eliminación total de los siniestros de tránsito","Aumentar las multas"],c:1,e:"Eliminar siniestros, partiendo de la reducción y minimización de consecuencias.",d:false},
  // Individuo (5-9)
  {id:"i1",tema:"individuo",p:"¿Cuál es el efecto del alcohol sobre la conducción?",o:["Mejora visión nocturna","Comportamiento impulsivo y agresivo","Aumenta concentración"],c:1,e:"El alcohol genera desinhibición, impulsividad, agresividad y falsa seguridad.",d:true,img:"https://upload.wikimedia.org/wikipedia/commons/thumb/a/a4/Alcohol_bottles_photographed_while_drunk.jpg/320px-Alcohol_bottles_photographed_while_drunk.jpg"},
  {id:"i2",tema:"individuo",p:"Con 0,3 g/l de alcohol en sangre:",o:["Condiciones normales","Estado de ebriedad","Bajo la influencia del alcohol"],c:2,e:"0,3 g/l = bajo la influencia. 0,8 g/l = ebriedad. Ambos son sancionados.",d:true,svg:"alcohol"},
  {id:"i3",tema:"individuo",p:"La Ley Emilia establece penas más severas para:",o:["Conductores sin licencia","Conductores ebrios que causen lesiones graves o muerte","No pagar TAG"],c:1,e:"Ley 20.770: cárcel efectiva para quien conduzca ebrio y cause lesiones gravísimas o muerte.",d:true},
  {id:"i4",tema:"individuo",p:"Conducir con fatiga puede provocar:",o:["Aumento de concentración","Dificultad para mantener la atención","Mejora en tiempos de reacción"],c:1,e:"La fatiga reduce atención, aumenta tiempos de reacción, puede provocar microsueños.",d:false,img:"https://cdn.pixabay.com/photo/2016/11/29/06/17/adult-1867889_640.jpg"},
  {id:"i5",tema:"individuo",p:"¿Qué sustancias además del alcohol alteran la conducción?",o:["Determinados medicamentos","Bebidas gaseosas","Agua mineral"],c:0,e:"Ansiolíticos, antihistamínicos y otros fármacos producen somnolencia y alteran reflejos.",d:false},
  // Vulnerables (10-13)
  {id:"v1",tema:"vulnerables",p:"Usuarios vulnerables son el 15% de siniestros pero casi el __% de muertes:",o:["10%","25%","40%"],c:2,e:"Representan casi el 40% de las muertes por su mayor exposición.",d:false,img:"https://cdn.pixabay.com/photo/2017/08/01/00/38/people-2562694_640.jpg"},
  {id:"v2",tema:"vulnerables",p:"Distancia lateral mínima al adelantar un ciclista:",o:["0,5 metros","1,0 metro","1,5 metros"],c:2,e:"Ley 21.088: mínimo 1,5 metros de distancia lateral.",d:false,img:"https://cdn.pixabay.com/photo/2015/07/31/14/59/cycling-869869_640.jpg"},
  {id:"v3",tema:"vulnerables",p:"Cuando un peatón cruza por paso de cebra, el conductor:",o:["Detenerse y ceder el paso","Tocar la bocina","Pasar rápido"],c:0,e:"Peatones tienen preferencia en cruces demarcados. Detenerse completamente (Art. 176).",d:false,img:"https://cdn.pixabay.com/photo/2016/11/22/21/57/crosswalk-1850688_640.jpg"},
  {id:"v4",tema:"vulnerables",p:"¿Por qué los conductores jóvenes tienen mayor riesgo?",o:["Baja percepción del riesgo","No saben manejar","Vehículos viejos"],c:0,e:"Subestiman riesgos, sobreestiman habilidades, se dejan influir por presión de pares.",d:false},
  // Normas (14-19)
  {id:"n1",tema:"normas",p:"Velocidad máxima en zona urbana para livianos:",o:["50 km/h","60 km/h","80 km/h"],c:1,e:"60 km/h, salvo señalización que indique otra (Art. 145).",d:false,img:"https://cdn.pixabay.com/photo/2018/01/28/10/59/speed-limit-3113592_640.jpg"},
  {id:"n2",tema:"normas",p:"¿Dónde se permite adelantar?",o:["Solo en zonas rurales","Donde la señalización lo permita","En intersecciones y pasos peatonales"],c:1,e:"Solo donde la demarcación lo permita (línea segmentada). Nunca en intersecciones.",d:false,img:"https://cdn.pixabay.com/photo/2016/11/18/13/02/asphalt-1834598_640.jpg"},
  {id:"n3",tema:"normas",p:"Si se equivoca de salida en autopista:",o:["Retroceder por berma","Viraje en U","Continuar hasta la siguiente salida autorizada"],c:2,e:"Nunca retroceder ni virar en U en autopista (Art. 113).",d:false,img:"https://cdn.pixabay.com/photo/2013/02/12/17/02/highway-80656_640.jpg"},
  {id:"n4",tema:"normas",p:"¿A qué distancia mínima de una esquina se prohíbe estacionar?",o:["5 metros","10 metros","20 metros"],c:1,e:"Prohibido a menos de 10 metros de esquinas y señales PARE/CEDA (Art. 153).",d:false},
  {id:"n5",tema:"normas",p:"Luces bajas durante el día son obligatorias:",o:["Solo en carreteras","En todo momento y todas las vías","Solo cuando llueve"],c:1,e:"Obligatorio las 24 horas, todas las vías, desde 2005 (Art. 68).",d:false,img:"https://cdn.pixabay.com/photo/2016/09/01/19/53/low-beam-1637096_640.jpg"},
  {id:"n6",tema:"normas",p:"La bocina debe usarse para:",o:["Apurar al vehículo delantero","Anunciar estacionamiento","Prevenir un siniestro si es estrictamente necesario"],c:2,e:"Solo para prevenir siniestros (Art. 78). No para apurar ni avisar.",d:false},
  // Conducción (20-25)
  {id:"d1",tema:"conduccion",p:"¿Qué es el 'efecto túnel'?",o:["Pérdida del campo visual lateral al aumentar velocidad","Dificultad para ver en túneles","Efecto de lluvia en parabrisas"],c:0,e:"A mayor velocidad, el campo visual se reduce. A 130 km/h = solo 30°.",d:false,img:"https://cdn.pixabay.com/photo/2016/01/19/17/53/car-1149997_640.jpg"},
  {id:"d2",tema:"conduccion",p:"Si se duplica la velocidad, la distancia de frenado:",o:["Se duplica","Se cuadruplica","Se mantiene igual"],c:1,e:"Energía cinética proporcional al cuadrado de la velocidad. Duplicar = ×4.",d:false,svg:"efectoTunel"},
  {id:"d3",tema:"conduccion",p:"Un conductor defensivo se caracteriza porque:",o:["Reacciona adecuadamente ante imprevistos","Hace maniobras sorpresivas","Conduce bloqueando tránsito"],c:0,e:"Conducción defensiva: anticiparse, mantener distancia, reaccionar correctamente.",d:false},
  {id:"d4",tema:"conduccion",p:"Bajo lluvia intensa, debe:",o:["Aumentar velocidad","Reducir velocidad, aumentar distancia y encender luces","Mantener misma velocidad"],c:1,e:"Reducir velocidad, aumentar distancia, encender luces bajas.",d:false,img:"https://cdn.pixabay.com/photo/2016/11/29/09/32/auto-1868726_640.jpg"},
  {id:"d5",tema:"conduccion",p:"Uso del celular al conducir:",o:["Permitido a baja velocidad","Prohibido, salvo manos libres","Permitido en autopistas"],c:1,e:"Prohibido manipular celular. Solo manos libres. Multa gravísima (Art. 107).",d:false,img:"https://cdn.pixabay.com/photo/2015/02/02/11/09/office-620822_640.jpg"},
  {id:"d6",tema:"conduccion",p:"¿Qué es la 'zona de incertidumbre'?",o:["Área donde otros podrían moverse impredeciblemente","Zona sin señalización","Interior del vehículo"],c:0,e:"Espacio alrededor de otros usuarios donde podrían moverse inesperadamente.",d:false},
  // Señales (26-30)
  {id:"s1",tema:"senales",p:"Las señales reglamentarias tienen forma:",o:["Rectangular","Circular","Romboidal"],c:1,e:"Reglamentarias = circulares (excepto PARE octógono y CEDA triángulo invertido).",d:false,img:"https://upload.wikimedia.org/wikipedia/commons/thumb/e/ef/Chile_road_sign_RPO-1.svg/240px-Chile_road_sign_RPO-1.svg.png"},
  {id:"s2",tema:"senales",p:"Las señales preventivas tienen forma de:",o:["Círculo","Rombo (diamante)","Octágono"],c:1,e:"Preventivas: romboidales, fondo amarillo, símbolo negro.",d:false,img:"https://upload.wikimedia.org/wikipedia/commons/thumb/0/09/Chile_road_sign_PG-1a.svg/240px-Chile_road_sign_PG-1a.svg.png"},
  {id:"s3",tema:"senales",p:"Un triángulo invertido indica:",o:["Pare obligatorio","Ceda el paso","Zona de peligro"],c:1,e:"Triángulo invertido = CEDA EL PASO. Reducir velocidad y ceder a vía preferente.",d:false,img:"https://upload.wikimedia.org/wikipedia/commons/thumb/e/e1/Chile_road_sign_RPO-2.svg/240px-Chile_road_sign_RPO-2.svg.png"},
  {id:"s4",tema:"senales",p:"Para ingresar a cruce con luz verde, verificar:",o:["Que haya luz amarilla antes","Que exista espacio para no bloquear el cruce","Que no haya paso de cebra"],c:1,e:"Verificar espacio al otro lado para no bloquear la intersección (Art. 131).",d:false,img:"https://cdn.pixabay.com/photo/2016/11/22/19/25/green-1850340_640.jpg"},
  {id:"s5",tema:"senales",p:"Línea amarilla continua en acera significa:",o:["Prohibido estacionar y detenerse","Estacionamiento nocturno","Zona carga/descarga"],c:0,e:"Línea amarilla continua = prohibición absoluta de estacionar y detenerse.",d:false},
  // Vehículo (31-34)
  {id:"m1",tema:"vehiculo",p:"¿Qué indica la luz de aceite en el tablero?",o:["Combustible bajo","Presión de aceite insuficiente, detenerse","Cambiar aceite de transmisión"],c:1,e:"Presión insuficiente. Detenerse y verificar nivel. Sin aceite se destruye el motor.",d:false,img:"https://cdn.pixabay.com/photo/2019/07/07/14/03/fiat-4322521_640.jpg"},
  {id:"m2",tema:"vehiculo",p:"Función del líquido de frenos:",o:["Lubricar motor","Transmitir presión del pedal a las ruedas","Enfriar escape"],c:1,e:"Fluido hidráulico que transmite la fuerza del pedal a pastillas/zapatas de freno.",d:false},
  {id:"m3",tema:"vehiculo",p:"Neumáticos desgastados provocan:",o:["Mayor agarre en mojado","Menor distancia de frenado","Mayor riesgo de aquaplaning"],c:2,e:"Pierden capacidad de evacuar agua. Profundidad mínima legal: 1,6 mm.",d:false,img:"https://cdn.pixabay.com/photo/2013/07/12/18/39/tire-153720_640.png"},
  {id:"m4",tema:"vehiculo",p:"¿Cada cuánto revisar presión de neumáticos?",o:["Cada 50.000 km","Cada 500 km o una vez al mes, en frío","Solo cuando se ven desinflados"],c:1,e:"Cada 500 km o mensualmente, siempre con neumáticos fríos.",d:false},
  // Seguridad (35-37)
  {id:"g1",tema:"seguridad",p:"Al elegir un SRI, lo más importante es:",o:["Que esté en oferta","Que sea compatible con el vehículo y adecuado al niño","Que combine con el interior"],c:1,e:"Compatible con vehículo (ISOFIX/cinturón) y adecuado al peso/talla del niño (Ley 20.904).",d:true,img:"https://cdn.pixabay.com/photo/2017/11/10/00/28/new-born-2935722_640.jpg"},
  {id:"g2",tema:"seguridad",p:"Respecto al cinturón, el conductor debe:",o:["Que todos los ocupantes lleven cinturón individual","Solo preocuparse del suyo","Permitir compartir cinturón"],c:0,e:"Responsabilidad del conductor que TODOS usen cinturón individual (Art. 75 bis).",d:false,img:"https://cdn.pixabay.com/photo/2019/12/20/14/44/seatbelt-4709004_640.jpg"},
  {id:"g3",tema:"seguridad",p:"Sin cinturón, el airbag puede causar:",o:["Protección extra","Efecto rebote con lesiones graves","No tiene efecto"],c:1,e:"Sin cinturón, el airbag empuja el cuerpo violentamente hacia atrás (efecto rebote).",d:false},
  // Emergencias (38-39)
  {id:"e1",tema:"emergencias",p:"Ante un siniestro, lo primero es:",o:["Mover heridos rápido","Conducta PAS: Proteger, Alertar, Socorrer","Continuar si no está involucrado"],c:1,e:"PAS: Proteger (señalizar), Alertar (131/132/133), Socorrer según capacidad.",d:false,img:"https://cdn.pixabay.com/photo/2012/04/14/14/04/emergency-34684_640.png"},
  {id:"e2",tema:"emergencias",p:"Ante vehículo de emergencia con sirenas:",o:["Aumentar velocidad","Continuar normalmente","Ceder paso y detenerse si es necesario"],c:2,e:"Preferencia absoluta. Desplazarse a la derecha y detenerse (Art. 65).",d:false,img:"https://cdn.pixabay.com/photo/2018/02/04/09/09/ambulance-3129542_640.jpg"},
  // Extra
  {id:"x1",tema:"individuo",p:"¿Por qué el exceso de velocidad es peligroso?",o:["Aumenta distancia de frenado y riesgo de siniestro","Solo afecta peatones","Consume menos combustible"],c:0,e:"Mayor distancia de frenado, menor campo visual, menor tiempo de reacción.",d:true,img:"https://cdn.pixabay.com/photo/2016/11/29/06/15/plans-1867745_640.jpg"},
  {id:"x2",tema:"normas",p:"Antes de virar en una intersección, el conductor debe:",o:["Aumentar velocidad antes de girar","Señalizar con anticipación suficiente","Encender luces bajas"],c:1,e:"Toda maniobra de viraje debe señalizarse con anticipación mínima de 30m urbano (Art. 142).",d:false},
  {id:"x3",tema:"conduccion",p:"¿Cuál es la regla para mantener distancia de seguimiento segura?",o:["Regla de 1 segundo","Regla de los 3 segundos","Regla de 10 metros"],c:1,e:"La regla de los 3 segundos permite calcular una distancia segura con el vehículo de adelante.",d:false},
  {id:"x4",tema:"senales",p:"Las señales informativas de tránsito tienen forma:",o:["Circular","Romboidal","Rectangular"],c:2,e:"Informativas: rectangulares, fondo verde con texto blanco. Guían rutas y destinos.",d:false,img:"https://upload.wikimedia.org/wikipedia/commons/thumb/1/1e/Chile_road_sign_ID-1.svg/320px-Chile_road_sign_ID-1.svg.png"},
  {id:"x5",tema:"seguridad",p:"¿Desde qué edad se puede obtener licencia Clase B?",o:["16 años","17 años con acompañante","18 años"],c:2,e:"18 años cumplidos. A los 17 se puede con acompañante que tenga 5+ años de licencia.",d:false},
];

// ── EXAM ALGORITHM (NEXTEO REPLICA) ──────────────────────────────────
function generarExamen() {
  const dobles = PREGUNTAS.filter(q => q.d);
  const normales = PREGUNTAS.filter(q => !q.d);
  const sd = shuffle(dobles).slice(0, 3);
  const sn = shuffle(normales).slice(0, 32);
  return shuffle([...sd, ...sn]);
}

function shuffle(a) { const b=[...a]; for(let i=b.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[b[i],b[j]]=[b[j],b[i]];} return b; }
function fmtTime(s) { return `${Math.floor(s/60).toString().padStart(2,'0')}:${(s%60).toString().padStart(2,'0')}`; }

// ═══════════════════════════════════════════════════════════════════════
// APP STATE & RENDER
// ═══════════════════════════════════════════════════════════════════════
const APP = {
  view: 'login', session: null,
  // exam
  qs: [], idx: 0, resp: {}, timer: 2700, done: false, mode: 'examen', navOpen: false, showExpl: false,
  timerInterval: null,
  // temario
  temario: null,
  // settings
  newUser: '', newPass: '',
};

function render() {
  const $=document.getElementById('app');
  if (!APP.session) { $.innerHTML = renderLogin(); return; }
  switch(APP.view) {
    case 'inicio': $.innerHTML = renderInicio(); break;
    case 'temarios': $.innerHTML = renderTemarios(); break;
    case 'temarioDetalle': $.innerHTML = renderTemarioDetalle(); break;
    case 'examen': $.innerHTML = renderExamen(); break;
    case 'resultado': $.innerHTML = renderResultado(); break;
    case 'revision': $.innerHTML = renderRevision(); break;
    case 'settings': $.innerHTML = renderSettings(); break;
    default: $.innerHTML = renderInicio();
  }
}

// ── LOGIN ────────────────────────────────────────────────────────────
function renderLogin() {
  return `<div class="login-screen fade-in">
    <div class="login-box">
      <div class="login-logo">${SVG.logo}</div>
      <div class="login-title">AutoEscuela Chile</div>
      <div class="login-sub">Simulador CONASET Clase B · 2026</div>
      <div class="form-group">
        <label class="form-label">Usuario</label>
        <input class="form-input" id="loginUser" type="text" placeholder="Ingresa tu usuario" autocomplete="username">
      </div>
      <div class="form-group">
        <label class="form-label">Contraseña</label>
        <input class="form-input" id="loginPass" type="password" placeholder="••••••" autocomplete="current-password">
      </div>
      <button class="login-btn" onclick="doLogin()">Ingresar</button>
      <div class="login-error" id="loginErr"></div>
    </div>
  </div>`;
}

function doLogin() {
  const u = document.getElementById('loginUser').value.trim();
  const p = document.getElementById('loginPass').value;
  const users = getUsers();
  const found = users.find(x => x.username === u && x.password === p);
  if (!found) { document.getElementById('loginErr').textContent = 'Usuario o contraseña incorrectos'; return; }
  APP.session = found;
  setSession(found);
  APP.view = 'inicio';
  render();
}

// ── PROGRESS CALC ────────────────────────────────────────────────────
function calcProgress() {
  const prog = getUserProgress(APP.session.username);
  const totalQ = PREGUNTAS.length;
  const correctas = Object.keys(prog.preguntasCorrectas || {}).length;
  const pct = Math.round((correctas / totalQ) * 100);
  const temasEst = Object.keys(prog.temasEstudiados || {}).length;
  const exams = prog.examenes || [];
  const aprobados = exams.filter(e => e.aprobado).length;
  const errores = prog.erroresPorTema || {};
  const topErrors = Object.entries(errores).sort((a,b)=>b[1]-a[1]).slice(0,3);
  const ultimo = exams.length ? exams[exams.length-1] : null;
  return { totalQ, correctas, pct, temasEst, totalTemas: TEMARIOS.length, exams: exams.length, aprobados, topErrors, ultimo, errores };
}

// ── INICIO ───────────────────────────────────────────────────────────
function renderInicio() {
  const gp = calcProgress();
  const initials = APP.session.username.slice(0,2).toUpperCase();
  
  let weakHTML = '';
  if (gp.topErrors.length > 0) {
    const chips = gp.topErrors.map(([tid,cnt]) => {
      const t = TEMARIOS.find(x=>x.id===tid);
      return `<span class="weak-chip" style="border-color:${t?.color||'#94a3b8'}">${t?.icono||''} ${t?.titulo||tid} (${cnt})</span>`;
    }).join('');
    weakHTML = `<div class="weak-box fade-in"><div class="weak-title">⚠️ Temas a reforzar</div><div class="weak-chips">${chips}</div><button class="refuerzo-btn" onclick="iniciarRefuerzo()">🎯 Practicar temas débiles</button></div>`;
  }

  // Progress message
  let progMsg = '';
  if (gp.pct === 0) progMsg = 'Comienza estudiando los temarios';
  else if (gp.pct < 30) progMsg = 'Buen inicio, sigue practicando';
  else if (gp.pct < 60) progMsg = 'Vas por buen camino';
  else if (gp.pct < 90) progMsg = '¡Casi listo para el examen real!';
  else if (gp.pct < 100) progMsg = '¡Excelente! Solo te faltan algunas';
  else progMsg = '🏆 ¡Dominas todas las preguntas!';

  return `
  <div class="home-header fade-in">
    <div>${SVG.logo}</div>
    <div style="flex:1"><div class="brand-title">AutoEscuela Chile</div><div class="brand-sub">Clase B · ${APP.session.username}</div></div>
    <button class="avatar-btn" onclick="goSettings()">${initials}</button>
  </div>
  <div class="prog-card fade-in">
    <div class="prog-top">
      <div><div class="prog-label">Progreso de aprendizaje</div><div class="prog-pct">${gp.pct}%</div></div>
      <div style="text-align:right"><div style="font-size:.7rem;color:#94a3b8">${gp.correctas}/${gp.totalQ}</div><div style="font-size:.65rem;color:#64748b">preguntas dominadas</div></div>
    </div>
    <div class="prog-bar-outer"><div class="prog-bar-inner" style="width:${gp.pct}%"></div></div>
    <div class="prog-msg">${progMsg}</div>
    <div class="prog-stats">
      <div class="prog-stat"><span class="stat-num">${gp.temasEst}/${gp.totalTemas}</span><span class="stat-label">Temas</span></div>
      <div class="prog-stat"><span class="stat-num">${gp.exams}</span><span class="stat-label">Exámenes</span></div>
      <div class="prog-stat"><span class="stat-num" style="color:${gp.aprobados>0?'#059669':'#94a3b8'}">${gp.aprobados}</span><span class="stat-label">Aprobados</span></div>
    </div>
    ${gp.ultimo ? `<div style="font-size:.68rem;color:#94a3b8;text-align:center;margin-top:10px">Último: <strong>${gp.ultimo.puntaje}/38</strong> — ${gp.ultimo.aprobado?'✅ Aprobado':'❌ Reprobado'}</div>` : ''}
  </div>
  ${weakHTML}
  <div class="actions">
    <button class="action-btn" onclick="goTemarios()"><span class="action-icon">📚</span><div><span class="action-label">Temarios Ilustrados</span><div class="action-desc">9 capítulos del Libro CONASET</div></div><span class="action-arrow">→</span></button>
    <button class="action-btn dark" onclick="iniciarExamen('examen')"><span class="action-icon">📝</span><div><span class="action-label">Examen Simulado</span><div class="action-desc" style="color:rgba(255,255,255,.6)">35 preguntas · 45 min · Formato NEXTEO</div></div><span class="action-arrow" style="color:rgba(255,255,255,.5)">→</span></button>
    <button class="action-btn" onclick="iniciarExamen('estudio')"><span class="action-icon">💡</span><div><span class="action-label">Modo Aprendizaje</span><div class="action-desc">Con explicaciones detalladas</div></div><span class="action-arrow">→</span></button>
  </div>
  <div class="info-bar">
    <div class="info-item"><span class="info-num">35</span>Preguntas</div>
    <div class="info-item"><span class="info-num">38</span>Pts máx</div>
    <div class="info-item"><span class="info-num">33</span>Aprueba</div>
    <div class="info-item"><span class="info-num">×2</span>3 doble</div>
  </div>
  <button class="logout-btn" onclick="doLogout()">Cerrar sesión</button>
  <div class="disclaimer">⚠️ Herramienta de práctica. No afiliada a CONASET ni a ningún organismo gubernamental.</div>`;
}

// ── TEMARIOS LIST ────────────────────────────────────────────────────
function renderTemarios() {
  const prog = getUserProgress(APP.session.username);
  const cards = TEMARIOS.map((t,i) => {
    const est = prog.temasEstudiados?.[t.id];
    const err = prog.erroresPorTema?.[t.id] || 0;
    return `<button class="tem-card fade-in" style="animation-delay:${i*.04}s" onclick="goTemarioDetalle('${t.id}')">
      <div class="tem-icon" style="background:${t.color}12">${svgHTML(t.svg, 42)}</div>
      <div style="flex:1;min-width:0">
        <div style="display:flex;align-items:center">${t.icono} <span class="tem-title" style="margin-left:4px">${t.titulo}</span>${est?'<span class="tem-studied">✓</span>':''}</div>
        <div class="tem-desc">${t.desc}</div>
        ${err?`<span class="tem-errors">${err} errores</span>`:''}
      </div>
      <span class="tem-arrow">›</span>
    </button>`;
  }).join('');
  return `<div class="top-bar"><button class="back-btn" onclick="goInicio()">←</button><span class="top-title">📚 Temarios Clase B</span></div>
  <div style="padding:10px 16px 4px;font-size:.8rem;color:var(--sub);line-height:1.5">9 capítulos del Libro para la Conducción en Chile (CONASET 2026)</div>
  <div class="tem-list">${cards}</div>`;
}

// ── TEMARIO DETALLE ──────────────────────────────────────────────────
function renderTemarioDetalle() {
  const t = APP.temario; if(!t) return renderTemarios();
  const secs = t.contenido.map((s,i) => {
    let ill = '';
    if (s.img) {
      ill = `<div class="tem-sec-illust"><img src="${s.img}" alt="${s.t}" style="max-width:100%;max-height:160px;border-radius:10px;object-fit:cover;box-shadow:0 2px 12px rgba(0,0,0,.08)"></div>`;
    } else if (s.svg) {
      ill = `<div class="tem-sec-illust">${svgHTML(s.svg, 65)}</div>`;
    }
    return `<div class="tem-section slide-up" style="animation-delay:${i*.06}s"><h3 class="tem-sec-title" style="color:${t.color}">${s.t}</h3>${ill}<p class="tem-sec-text">${s.txt}</p></div>`;
  }).join('');
  const qCount = PREGUNTAS.filter(q => q.tema === t.id).length;
  return `<div class="top-bar"><button class="back-btn" onclick="goTemarios()">←</button><span class="top-title">${t.icono} ${t.titulo}</span></div>
  <div class="tem-hero fade-in" style="background:linear-gradient(135deg,${t.color}15,${t.color}08)">${svgHTML(t.svg, 70)}<p style="font-size:.82rem;font-weight:500;margin-top:10px;color:${t.color}">${t.desc}</p></div>
  <div style="margin-top:12px">${secs}</div>
  <div class="tem-actions">
    <button class="tem-test-btn" style="background:${t.color}" onclick="practicarTema('${t.id}')">📝 Practicar (${qCount} preguntas)</button>
    <button class="tem-mark-btn" onclick="marcarEstudiado('${t.id}')">✅ Marcar como estudiado</button>
  </div>`;
}

// ── EXAMEN ───────────────────────────────────────────────────────────
function renderExamen() {
  const q = APP.qs[APP.idx]; if (!q) return '';
  const r = APP.resp[APP.idx];
  const answered = r !== undefined;
  const totalR = Object.keys(APP.resp).length;
  const pct = (totalR / APP.qs.length) * 100;
  const lowTime = APP.timer < 300;
  const t = TEMARIOS.find(x => x.id === q.tema);

  // Nav dots
  let dotsHTML = '';
  if (APP.navOpen) {
    const dots = APP.qs.map((dq, di) => {
      const dr = APP.resp[di];
      let cls = 'dot';
      if (di === APP.idx) cls += ' current';
      else if (dr !== undefined) {
        if (APP.mode !== 'examen') cls += (dr === dq.c ? ' ok' : ' bad');
        else cls += ' answered';
      }
      return `<button class="${cls}" onclick="goQ(${di})">${di+1}${dq.d?'<span class="dot-x2">×2</span>':''}</button>`;
    }).join('');
    dotsHTML = `<div class="dots-grid fade-in">${dots}</div>`;
  }

  // Opciones - en modo examen SIEMPRE se puede cambiar respuesta
  // en modo estudio se bloquea SOLO cuando showExpl es true
  const locked = APP.mode !== 'examen' && APP.showExpl;
  const opts = q.o.map((o, oi) => {
    const letra = String.fromCharCode(65+oi);
    let cls = 'opt';
    if (locked) {
      if (oi === q.c) cls += ' ok';
      else if (r === oi) cls += ' bad';
    } else if (r === oi) cls += ' sel';
    const letterLabel = locked ? (oi===q.c?'✓':(r===oi?'✗':letra)) : letra;
    return `<button class="${cls}" onclick="selectOpt(${oi})" ${locked?'disabled':''}><span class="opt-letter">${letterLabel}</span><span>${o}</span></button>`;
  }).join('');

  // Explicacion
  let explHTML = '';
  if (APP.mode !== 'examen' && APP.showExpl) {
    const ok = r === q.c;
    explHTML = `<div class="expl-box ${ok?'correct':'wrong'} slide-up"><div class="expl-head">${ok?'✅ ¡Correcto!':'❌ Incorrecto'}</div><p class="expl-text">${q.e}</p></div>`;
  }

  // Illustration - prefer real image (img), fallback to SVG
  let illust = '';
  if (q.img) {
    illust = `<div class="q-illust"><img src="${q.img}" alt="" style="max-width:100%;max-height:140px;border-radius:10px;object-fit:cover;box-shadow:0 2px 12px rgba(0,0,0,.1)"></div>`;
  } else if (q.svg) {
    illust = `<div class="q-illust">${svgHTML(q.svg, 65)}</div>`;
  }

  return `
  <div class="exam-top"><button class="back-btn" onclick="exitExam()">←</button><span class="exam-label">${APP.mode==='estudio'?'💡 Aprendizaje':'📝 Examen'}</span>${APP.mode==='examen'?`<span class="timer-badge${lowTime?' low':''}">${fmtTime(APP.timer)}</span>`:''}</div>
  <div class="prog-wrap"><div class="prog-fill" style="width:${pct}%"></div></div>
  <div class="prog-text">${totalR}/${APP.qs.length}</div>
  <button class="dots-toggle" onclick="toggleNav()">${APP.navOpen?'Ocultar mapa ▲':'Mapa de preguntas ▼'}</button>
  ${dotsHTML}
  <div class="q-box fade-in">
    <div class="q-meta">
      <span class="q-tema" style="background:${t?.color||'#6b7280'}12;color:${t?.color||'#6b7280'}">${t?.icono||''} ${t?.titulo||q.tema}</span>
      ${q.d?'<span class="q-doble">⚡ DOBLE PUNTAJE</span>':''}
    </div>
    ${illust}
    <div class="q-num">Pregunta ${APP.idx+1} de ${APP.qs.length}</div>
    <h3 class="q-text">${q.p}</h3>
    <div class="opts">${opts}</div>
    ${APP.mode==='examen' && r !== undefined && !APP.done ? '<div class="change-hint">💡 Puedes cambiar tu respuesta antes de avanzar</div>' : ''}
    ${explHTML}
  </div>
  <div class="nav-row">
    <button class="nav-btn" onclick="prevQ()" ${APP.idx===0?'disabled':''}>← Anterior</button>
    ${APP.idx===APP.qs.length-1 ? `<button class="nav-btn finish" onclick="finishExam()">Finalizar</button>` : `<button class="nav-btn next" onclick="nextQ()">Siguiente →</button>`}
  </div>`;
}

// ── RESULTADO ────────────────────────────────────────────────────────
function renderResultado() {
  const res = calcExamResult();
  const tiempoUsado = 2700 - APP.timer;
  
  let temaHTML = Object.entries(res.porTema).map(([tid,d]) => {
    const t = TEMARIOS.find(x=>x.id===tid);
    const p = Math.round((d.c/d.t)*100);
    const barColor = p>=80?'#059669':p>=50?'#f59e0b':'#dc2626';
    return `<div class="res-tema-row"><div class="res-tema-header"><span class="res-tema-name" style="color:${t?.color||'#6b7280'}">${t?.icono||''} ${t?.titulo||tid}</span><span class="res-tema-score">${d.c}/${d.t}</span></div><div class="res-tema-bar"><div class="res-tema-fill" style="width:${p}%;background:${barColor}"></div></div></div>`;
  }).join('');

  let weakHTML = '';
  if (Object.keys(res.erroresTema).length > 0) {
    const chips = Object.keys(res.erroresTema).map(tid => {
      const t = TEMARIOS.find(x=>x.id===tid);
      return `<span class="weak-chip" style="border-color:${t?.color}">${t?.icono} ${t?.titulo} (${res.erroresTema[tid].length})</span>`;
    }).join('');
    weakHTML = `<div class="weak-box" style="margin:12px 16px 0"><div class="weak-title">🎯 Refuerza estos temas:</div><div class="weak-chips">${chips}</div><button class="refuerzo-btn" onclick="practicarErrores()">🔄 Practicar solo mis errores</button></div>`;
  }

  return `
  <div class="res-banner ${res.aprobado?'pass':'fail'} fade-in">
    <div style="font-size:2.5rem">${res.aprobado?'🎉':'📚'}</div>
    <div class="res-title">${res.aprobado?'¡APROBADO!':'NO APROBADO'}</div>
    <div class="res-sub">${res.aprobado?'¡Felicidades! Estás listo para el examen real.':'Sigue practicando. ¡Puedes lograrlo!'}</div>
  </div>
  <div class="res-grid">
    <div class="res-card"><div class="res-num">${res.puntaje}</div><div class="res-label">Puntaje</div><div style="font-size:.6rem;color:var(--muted)">de 38</div></div>
    <div class="res-card"><div class="res-num">${res.correctas}</div><div class="res-label">Correctas</div><div style="font-size:.6rem;color:var(--muted)">de ${APP.qs.length}</div></div>
    <div class="res-card"><div class="res-num">${fmtTime(tiempoUsado)}</div><div class="res-label">Tiempo</div></div>
  </div>
  <div class="res-temas"><div style="font-size:.88rem;font-weight:700;margin-bottom:14px">Rendimiento por tema</div>${temaHTML}</div>
  ${weakHTML}
  <div class="res-actions">
    <button class="rev-btn" onclick="goRevision()">📋 Revisar</button>
    <button class="new-btn" onclick="goInicio()">🏠 Inicio</button>
  </div>`;
}

// ── REVISIÓN ─────────────────────────────────────────────────────────
function renderRevision() {
  const cards = APP.qs.map((q, i) => {
    const r = APP.resp[i];
    const ok = r === q.c;
    const noR = r === undefined;
    const t = TEMARIOS.find(x=>x.id===q.tema);
    const borderColor = noR?'#9ca3af':ok?'#059669':'#dc2626';
    const ill = q.img ? `<div style="display:flex;justify-content:center;margin:6px 0"><img src="${q.img}" alt="" style="max-width:100%;max-height:100px;border-radius:8px;object-fit:cover"></div>` : (q.svg ? `<div style="display:flex;justify-content:center;margin:6px 0">${svgHTML(q.svg, 50)}</div>` : '');
    const opts = q.o.map((o,oi) => {
      const l = String.fromCharCode(65+oi);
      const isC = oi===q.c, isS = oi===r;
      let cls = 'rev-opt'; if(isC) cls+=' ok'; if(isS&&!isC) cls+=' bad';
      const lBg = isC?'background:#059669;color:#fff':(isS?'background:#dc2626;color:#fff':'background:#e2e8f0;color:#64748b');
      return `<div class="${cls}"><span class="rev-letter" style="${lBg}">${isC?'✓':(isS?'✗':l)}</span><span>${o}</span></div>`;
    }).join('');
    return `<div class="rev-card fade-in" style="border-left:4px solid ${borderColor}">
      <div style="display:flex;justify-content:space-between;flex-wrap:wrap;gap:6px;margin-bottom:8px">
        <span style="font-size:.8rem;font-weight:700">${noR?'⬜':ok?'✅':'❌'} Pregunta ${i+1}</span>
        <div style="display:flex;gap:4px"><span style="font-size:.63rem;font-weight:600;padding:2px 8px;border-radius:5px;background:${t?.color||'#6b7280'}12;color:${t?.color}">${t?.icono} ${t?.titulo}</span>${q.d?'<span style="font-size:.63rem;font-weight:700;padding:2px 8px;border-radius:5px;background:#dc2626;color:#fff">×2</span>':''}</div>
      </div>
      ${ill}
      <p style="font-size:.85rem;font-weight:500;line-height:1.5;margin-bottom:10px">${q.p}</p>
      ${opts}
      <div class="rev-expl"><strong>Explicación:</strong> ${q.e}</div>
    </div>`;
  }).join('');
  return `<div class="top-bar"><button class="back-btn" onclick="APP.view='resultado';render()">←</button><span class="top-title">📋 Revisión</span></div>
  <div style="padding:8px 0 30px">${cards}</div>
  <div style="padding:0 16px 30px"><button class="new-btn" style="width:100%" onclick="goInicio()">🏠 Inicio</button></div>`;
}

// ── SETTINGS ─────────────────────────────────────────────────────────
function renderSettings() {
  const users = getUsers();
  const isAdmin = APP.session.role === 'admin';
  const userRows = users.map((u,i) => {
    const delBtn = isAdmin && u.username !== APP.session.username ? `<button class="del-user-btn" onclick="delUser(${i})">Eliminar</button>` : '';
    return `<div class="user-row"><div><span class="user-name">${u.username}</span><span class="user-role" style="margin-left:8px">${u.role||'usuario'}</span></div>${delBtn}</div>`;
  }).join('');

  const addForm = isAdmin ? `
    <div style="margin-top:16px;padding-top:14px;border-top:1px solid var(--border)">
      <div style="font-size:.78rem;font-weight:600;margin-bottom:8px">Agregar usuario</div>
      <div class="add-user-form">
        <input id="newUser" type="text" placeholder="Usuario">
        <input id="newPass" type="password" placeholder="Contraseña">
        <button class="add-user-btn" onclick="addUser()">Agregar</button>
      </div>
      <div id="addUserErr" style="font-size:.72rem;color:var(--bad);margin-top:6px"></div>
    </div>` : '';

  const prog = getUserProgress(APP.session.username);
  const resetBtn = `<button class="logout-btn" style="color:var(--bad)" onclick="resetProgress()">🗑️ Reiniciar mi progreso</button>`;

  return `<div class="top-bar"><button class="back-btn" onclick="goInicio()">←</button><span class="top-title">⚙️ Configuración</span></div>
  <div style="padding:16px 0">
    <div class="settings-section">
      <div class="settings-title">👤 Sesión actual</div>
      <div style="font-size:.85rem"><strong>${APP.session.username}</strong> <span style="font-size:.7rem;color:var(--muted)">(${APP.session.role||'usuario'})</span></div>
    </div>
    <div class="settings-section">
      <div class="settings-title">👥 Usuarios</div>
      ${userRows}
      ${addForm}
    </div>
    <div class="settings-section">
      <div class="settings-title">📊 Mi progreso</div>
      <div style="font-size:.82rem;color:var(--sub)">Preguntas dominadas: <strong>${Object.keys(prog.preguntasCorrectas||{}).length}/${PREGUNTAS.length}</strong></div>
      <div style="font-size:.82rem;color:var(--sub);margin-top:4px">Exámenes realizados: <strong>${(prog.examenes||[]).length}</strong></div>
      ${resetBtn}
    </div>
    <button class="logout-btn" onclick="doLogout()">Cerrar sesión</button>
  </div>`;
}

// ═══════════════════════════════════════════════════════════════════════
// ACTION HANDLERS
// ═══════════════════════════════════════════════════════════════════════
function goInicio() { clearInterval(APP.timerInterval); APP.view='inicio'; render(); }
function goTemarios() { APP.view='temarios'; render(); }
function goTemarioDetalle(id) { APP.temario = TEMARIOS.find(t=>t.id===id); APP.view='temarioDetalle'; render(); }
function goSettings() { APP.view='settings'; render(); }
function goRevision() { APP.view='revision'; render(); }
function doLogout() { clearSession(); APP.session=null; APP.view='login'; render(); }

function marcarEstudiado(id) {
  const prog = getUserProgress(APP.session.username);
  if (!prog.temasEstudiados) prog.temasEstudiados = {};
  prog.temasEstudiados[id] = true;
  saveUserProgress(APP.session.username, prog);
  goTemarios();
}

function iniciarExamen(mode) {
  clearInterval(APP.timerInterval);
  APP.qs = generarExamen();
  APP.idx = 0; APP.resp = {}; APP.timer = 2700; APP.done = false; APP.mode = mode; APP.navOpen = false; APP.showExpl = false;
  APP.view = 'examen';
  if (mode === 'examen') {
    APP.timerInterval = setInterval(() => {
      APP.timer--;
      if (APP.timer <= 0) { clearInterval(APP.timerInterval); APP.done = true; finishExam(); return; }
      // Update timer display only
      const el = document.querySelector('.timer-badge');
      if (el) { el.textContent = fmtTime(APP.timer); if(APP.timer<300) el.classList.add('low'); }
    }, 1000);
  }
  render();
}

function practicarTema(id) {
  marcarEstudiado(id);
  clearInterval(APP.timerInterval);
  APP.qs = shuffle(PREGUNTAS.filter(q => q.tema === id));
  APP.idx = 0; APP.resp = {}; APP.timer = 2700; APP.done = false; APP.mode = 'estudio'; APP.navOpen = false; APP.showExpl = false;
  APP.view = 'examen';
  render();
}

function iniciarRefuerzo() {
  const prog = getUserProgress(APP.session.username);
  const errores = prog.erroresPorTema || {};
  const sorted = Object.entries(errores).sort((a,b)=>b[1]-a[1]).slice(0,3).map(e=>e[0]);
  if (!sorted.length) { alert('Realiza un examen primero.'); return; }
  clearInterval(APP.timerInterval);
  APP.qs = shuffle(PREGUNTAS.filter(q => sorted.includes(q.tema)));
  APP.idx = 0; APP.resp = {}; APP.timer = 2700; APP.done = false; APP.mode = 'estudio'; APP.navOpen = false; APP.showExpl = false;
  APP.view = 'examen';
  render();
}

function practicarErrores() {
  const errorIndices = [];
  APP.qs.forEach((q,i) => { if(APP.resp[i] !== q.c) errorIndices.push(q); });
  if (!errorIndices.length) { goInicio(); return; }
  clearInterval(APP.timerInterval);
  APP.qs = shuffle(errorIndices);
  APP.idx = 0; APP.resp = {}; APP.timer = 2700; APP.done = false; APP.mode = 'estudio'; APP.navOpen = false; APP.showExpl = false;
  APP.view = 'examen';
  render();
}

function exitExam() { clearInterval(APP.timerInterval); goInicio(); }
function toggleNav() { APP.navOpen = !APP.navOpen; render(); }
function prevQ() { if(APP.idx>0) { APP.idx--; APP.showExpl=false; render(); } }
function nextQ() { if(APP.idx<APP.qs.length-1) { APP.idx++; APP.showExpl=false; render(); } }
function goQ(i) { APP.idx = i; APP.showExpl = false; APP.navOpen = false; render(); }

function selectOpt(oi) {
  if (APP.done) return;
  // En modo estudio, si ya se mostró la explicación, no permitir cambiar
  if (APP.mode !== 'examen' && APP.showExpl) return;
  // En modo examen: SIEMPRE permitir cambiar respuesta (toggle o cambiar a otra)
  if (APP.resp[APP.idx] === oi) {
    // Click en la misma opción = deseleccionar
    delete APP.resp[APP.idx];
  } else {
    // Seleccionar nueva opción (o cambiar de opción)
    APP.resp[APP.idx] = oi;
  }
  if (APP.mode !== 'examen' && APP.resp[APP.idx] !== undefined) APP.showExpl = true;
  render();
}

function calcExamResult() {
  let correctas=0, puntaje=0, porTema={}, erroresTema={};
  APP.qs.forEach((q,i) => {
    if(!porTema[q.tema]) porTema[q.tema]={c:0,t:0};
    porTema[q.tema].t++;
    if(APP.resp[i]===q.c){correctas++;puntaje+=q.d?2:1;porTema[q.tema].c++;}
    else { if(!erroresTema[q.tema]) erroresTema[q.tema]=[]; erroresTema[q.tema].push(i); }
  });
  // Check: if all 3 double-score wrong = fail
  const doublesWrong = APP.qs.filter((q,i) => q.d && APP.resp[i] !== q.c).length;
  const dobles3fail = APP.qs.filter(q=>q.d).length > 0 && doublesWrong >= 3;
  const aprobado = puntaje >= 33 && !dobles3fail;
  return { correctas, puntaje, porTema, erroresTema, aprobado, dobles3fail };
}

function finishExam() {
  clearInterval(APP.timerInterval);
  APP.done = true;
  // Save progress
  const res = calcExamResult();
  const prog = getUserProgress(APP.session.username);
  if (!prog.examenes) prog.examenes = [];
  prog.examenes.push({
    fecha: new Date().toISOString(),
    puntaje: res.puntaje,
    correctas: res.correctas,
    total: APP.qs.length,
    aprobado: res.aprobado,
  });
  // Track errors
  if (!prog.erroresPorTema) prog.erroresPorTema = {};
  if (!prog.preguntasCorrectas) prog.preguntasCorrectas = {};
  if (!prog.preguntasRespondidas) prog.preguntasRespondidas = {};
  APP.qs.forEach((q,i) => {
    prog.preguntasRespondidas[q.id] = true;
    if (APP.resp[i] === q.c) {
      prog.preguntasCorrectas[q.id] = true;
    } else {
      prog.erroresPorTema[q.tema] = (prog.erroresPorTema[q.tema] || 0) + 1;
      // If previously marked correct but now wrong, remove
      delete prog.preguntasCorrectas[q.id];
    }
  });
  saveUserProgress(APP.session.username, prog);
  APP.view = 'resultado';
  render();
}

// ── USER MANAGEMENT ──────────────────────────────────────────────────
function addUser() {
  const u = document.getElementById('newUser').value.trim();
  const p = document.getElementById('newPass').value;
  const err = document.getElementById('addUserErr');
  if (!u || !p) { err.textContent = 'Completa ambos campos'; return; }
  if (p.length < 4) { err.textContent = 'Contraseña mínimo 4 caracteres'; return; }
  const users = getUsers();
  if (users.find(x => x.username === u)) { err.textContent = 'Usuario ya existe'; return; }
  users.push({ username: u, password: p, role: 'usuario', created: new Date().toISOString() });
  saveUsers(users);
  render();
}

function delUser(i) {
  const users = getUsers();
  if (users[i].username === APP.session.username) return;
  if (!confirm(`¿Eliminar usuario "${users[i].username}"?`)) return;
  users.splice(i, 1);
  saveUsers(users);
  render();
}

function resetProgress() {
  if (!confirm('¿Borrar todo tu progreso? No se puede deshacer.')) return;
  LS.del('ae_prog_' + APP.session.username);
  render();
}

// ── INIT ─────────────────────────────────────────────────────────────
(function init() {
  const s = getSession();
  if (s) {
    // Verify user still exists
    const users = getUsers();
    const found = users.find(u => u.username === s.username && u.password === s.password);
    if (found) { APP.session = found; APP.view = 'inicio'; }
    else { clearSession(); }
  }
  render();
  // Handle Enter on login
  document.addEventListener('keydown', e => {
    if (e.key === 'Enter' && !APP.session) doLogin();
  });
})();
</script>
</body>
</html>
