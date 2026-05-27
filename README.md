
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Parche FAE — Externado</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=Manrope:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #070B14;
  --surface: #0D1526;
  --surface2: #111C30;
  --surface3: #162035;
  --border: rgba(255,255,255,0.07);
  --border2: rgba(255,255,255,0.12);
  --text: #E8EDF5;
  --muted: #5A6880;
  --muted2: #8898B0;
  --green: #00E5A0;
  --green-dim: rgba(0,229,160,0.12);
  --green-glow: rgba(0,229,160,0.25);
  --orange: #FF6B2B;
  --orange-dim: rgba(255,107,43,0.12);
  --blue-accent: #3B7FFF;
  --font-display: "Syne", sans-serif;
  --font-body: "Manrope", sans-serif;
}
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; }
body {
  font-family: var(--font-body);
  background: var(--bg);
  color: var(--text);
  min-height: 100vh;
  overflow-x: hidden;
  -webkit-font-smoothing: antialiased;
}
/* Noise grain overlay */
body::before {
  content: "";
  position: fixed;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='300' height='300'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='300' height='300' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
  pointer-events: none; z-index: 9998;
}
/* Ambient blobs */
.blob { position: fixed; border-radius: 50%; filter: blur(80px); pointer-events: none; z-index: 0; }
.b1 { width: 550px; height: 550px; top: -180px; left: -120px; background: rgba(0,229,160,0.06); animation: drift 20s ease-in-out infinite; }
.b2 { width: 450px; height: 450px; bottom: -100px; right: -80px; background: rgba(255,107,43,0.05); animation: drift 25s ease-in-out infinite reverse; }
@keyframes drift { 0%,100% { transform: translate(0,0); } 50% { transform: translate(24px,-18px); } }
::-webkit-scrollbar { width: 4px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb { background: var(--surface3); border-radius: 4px; }
 
/* ─── TOPNAV ─── */
#nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 500;
  height: 58px;
  background: rgba(7,11,20,0.85);
  backdrop-filter: blur(18px);
  -webkit-backdrop-filter: blur(18px);
  border-bottom: 1px solid var(--border);
  display: flex; align-items: center; justify-content: space-between;
  padding: 0 20px;
  transition: background 0.3s;
}
.nav-logo {
  display: flex; align-items: center; gap: 9px;
  cursor: pointer; text-decoration: none; user-select: none;
  flex-shrink: 0;
}
.nav-logo-icon {
  width: 32px; height: 32px; border-radius: 9px;
  background: linear-gradient(135deg, var(--green), #00A86B);
  display: flex; align-items: center; justify-content: center;
  box-shadow: 0 0 14px rgba(0,229,160,0.28);
  flex-shrink: 0;
}
.nav-logo-icon svg { width: 17px; height: 17px; }
.nav-logo-text { display: flex; flex-direction: column; line-height: 1; }
.nav-logo-text .t1 { font-family: var(--font-display); font-size: 0.95rem; font-weight: 800; color: #fff; letter-spacing: 0.04em; }
.nav-logo-text .t2 { font-size: 0.5rem; font-weight: 600; text-transform: uppercase; letter-spacing: 0.14em; color: var(--muted); margin-top: 1px; }
.nav-right { display: flex; align-items: center; gap: 8px; }
#nav-auth { display: none; align-items: center; gap: 8px; }
#nav-auth.show { display: flex; }
.nav-icon-btn {
  width: 36px; height: 36px; border-radius: 9px;
  background: rgba(255,255,255,0.05);
  border: 1px solid var(--border);
  display: flex; align-items: center; justify-content: center;
  cursor: pointer; color: var(--muted2);
  transition: all 0.2s; position: relative;
  flex-shrink: 0;
}
.nav-icon-btn:hover { background: rgba(255,255,255,0.09); color: #fff; border-color: var(--border2); }
.nav-icon-btn svg { width: 15px; height: 15px; }
.notif-dot {
  position: absolute; top: 7px; right: 7px;
  width: 6px; height: 6px; border-radius: 50%;
  background: var(--orange); border: 1.5px solid var(--bg);
  display: none;
}
.notif-dot.show { display: block; }
.nav-user-chip {
  display: flex; align-items: center; gap: 7px;
  padding: 4px 11px 4px 5px;
  background: rgba(255,255,255,0.05);
  border: 1px solid var(--border);
  border-radius: 9px; cursor: pointer;
  transition: all 0.2s;
}
.nav-user-chip:hover { background: rgba(255,255,255,0.08); border-color: var(--border2); }
.nav-user-av {
  width: 26px; height: 26px; border-radius: 7px;
  display: flex; align-items: center; justify-content: center;
  font-family: var(--font-display); font-size: 0.6rem; font-weight: 800; color: #fff;
  flex-shrink: 0;
}
.nav-user-info .name { font-size: 0.7rem; font-weight: 600; color: var(--text); max-width: 100px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
.nav-user-info .role-lbl { font-size: 0.52rem; font-weight: 600; text-transform: uppercase; letter-spacing: 0.1em; color: var(--muted); }
.nav-user-chip svg { width: 10px; height: 10px; color: var(--muted); margin-left: 2px; }
#nav-loginbtn { display: none; }
#nav-loginbtn.show { display: block; }
 
/* ─── PAGES ─── */
#app { padding-top: 58px; min-height: 100vh; position: relative; z-index: 1; }
.page { display: none; min-height: calc(100vh - 58px); }
.page.active { display: block; animation: pg-in 0.42s cubic-bezier(0.22,1,0.36,1); }
@keyframes pg-in { from { opacity: 0; transform: translateY(16px); } to { opacity: 1; transform: translateY(0); } }
 
/* ─── SHARED COMPONENTS ─── */
.btn {
  display: inline-flex; align-items: center; justify-content: center; gap: 7px;
  font-family: var(--font-display); font-weight: 700;
  font-size: 0.72rem; letter-spacing: 0.08em; text-transform: uppercase;
  border: none; cursor: pointer; border-radius: 11px;
  padding: 13px 22px; transition: all 0.2s;
  position: relative; overflow: hidden;
}
.btn::after { content: ""; position: absolute; inset: 0; background: rgba(255,255,255,0); transition: 0.15s; }
.btn:hover::after { background: rgba(255,255,255,0.07); }
.btn:active { transform: scale(0.98); }
.btn:disabled { opacity: 0.3; cursor: not-allowed; }
.btn svg { width: 15px; height: 15px; flex-shrink: 0; }
.btn-green { background: linear-gradient(135deg, var(--green) 0%, #00A86B 100%); color: #051a0e; box-shadow: 0 4px 18px rgba(0,229,160,0.22); }
.btn-green:hover { box-shadow: 0 6px 26px rgba(0,229,160,0.36); transform: translateY(-1px); }
.btn-orange { background: linear-gradient(135deg, var(--orange) 0%, #D4510A 100%); color: #fff; box-shadow: 0 4px 18px rgba(255,107,43,0.22); }
.btn-orange:hover { box-shadow: 0 6px 26px rgba(255,107,43,0.36); transform: translateY(-1px); }
.btn-ghost { background: rgba(255,255,255,0.05); border: 1px solid var(--border); color: var(--muted2); }
.btn-ghost:hover { background: rgba(255,255,255,0.09); border-color: var(--border2); color: #fff; }
.btn-sm { padding: 8px 14px; font-size: 0.65rem; border-radius: 8px; }
.btn-w { width: 100%; padding: 14px; }
 
.inp-wrap { position: relative; }
.inp-icon { position: absolute; left: 13px; top: 50%; transform: translateY(-50%); color: var(--muted); pointer-events: none; }
.inp-icon svg { width: 15px; height: 15px; }
.inp {
  width: 100%; padding: 12px 14px 12px 40px;
  background: rgba(255,255,255,0.04);
  border: 1.5px solid var(--border);
  border-radius: 11px; color: var(--text);
  font-family: var(--font-body); font-size: 0.875rem;
  outline: none; transition: all 0.2s;
}
.inp:focus { border-color: var(--green); background: rgba(0,229,160,0.04); box-shadow: 0 0 0 3px rgba(0,229,160,0.09); }
.inp::placeholder { color: var(--muted); }
.inp.err { border-color: #ef4444; }
.field-label { display: block; font-size: 0.6rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.12em; color: var(--muted); margin-bottom: 7px; }
 
.card { background: var(--surface); border: 1px solid var(--border); border-radius: 20px; }
.card2 { background: var(--surface2); border: 1px solid var(--border); border-radius: 14px; }
 
.badge {
  display: inline-flex; align-items: center; gap: 5px;
  padding: 4px 10px; border-radius: 99px;
  font-size: 0.58rem; font-weight: 700; letter-spacing: 0.08em; text-transform: uppercase;
  border: 1px solid currentColor;
}
.badge-green { color: var(--green); background: var(--green-dim); }
.badge-orange { color: var(--orange); background: var(--orange-dim); }
.badge-muted { color: var(--muted2); background: rgba(255,255,255,0.05); border-color: var(--border); }
 
.pill-row { display: flex; gap: 6px; flex-wrap: wrap; }
.pill {
  padding: 6px 14px; border-radius: 99px;
  border: 1.5px solid var(--border); background: transparent;
  font-family: var(--font-display); font-size: 0.62rem; font-weight: 700;
  text-transform: uppercase; letter-spacing: 0.07em;
  cursor: pointer; color: var(--muted); transition: all 0.2s; white-space: nowrap;
}
.pill:hover { border-color: rgba(255,255,255,0.18); color: var(--text); }
.pill.p-orange { background: var(--orange); border-color: var(--orange); color: #fff; }
.pill.p-green { background: var(--green); border-color: var(--green); color: #051a0e; }
 
.sem-strip { display: flex; gap: 5px; overflow-x: auto; scrollbar-width: none; padding-bottom: 2px; }
.sem-strip::-webkit-scrollbar { display: none; }
.sem-btn {
  padding: 5px 12px; border-radius: 7px; white-space: nowrap;
  border: 1px solid var(--border); background: transparent;
  font-family: var(--font-display); font-size: 0.6rem; font-weight: 700;
  text-transform: uppercase; letter-spacing: 0.07em;
  cursor: pointer; color: var(--muted); transition: all 0.2s;
}
.sem-btn:hover { background: rgba(255,255,255,0.06); color: var(--text); }
.sem-btn.on { background: rgba(0,229,160,0.1); border-color: rgba(0,229,160,0.35); color: var(--green); }
 
.section-label { font-size: 0.58rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.14em; color: var(--muted); margin-bottom: 10px; display: block; }
.back-btn {
  display: inline-flex; align-items: center; gap: 7px;
  padding: 7px 13px; border-radius: 9px;
  background: rgba(255,255,255,0.05); border: 1px solid var(--border);
  color: var(--muted2); font-family: var(--font-display);
  font-size: 0.6rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.08em;
  cursor: pointer; transition: all 0.2s; margin-bottom: 22px;
}
.back-btn:hover { background: rgba(255,255,255,0.09); color: #fff; }
.back-btn svg { width: 13px; height: 13px; }
 
.hr { height: 1px; background: var(--border); margin: 14px 0; }
 
/* ─── LOGIN PAGE ─── */
#pg-login {
  display: flex; align-items: center; justify-content: center;
  padding: 28px 16px;
}
.login-shell { display: grid; grid-template-columns: minmax(0,1fr) minmax(0,1fr); max-width: 820px; width: 100%; border-radius: 26px; overflow: hidden; border: 1px solid var(--border); }
@media (max-width: 600px) { .login-shell { grid-template-columns: 1fr; } }
.login-left {
  background: linear-gradient(150deg, #0C1C30 0%, #071520 100%);
  padding: 36px 30px; position: relative; overflow: hidden;
  min-width: 0;
  display: flex; flex-direction: column; justify-content: space-between;
}
.login-left::before {
  content: ""; position: absolute; top: -80px; right: -80px;
  width: 280px; height: 280px; border-radius: 50%;
  background: radial-gradient(circle, rgba(0,229,160,0.13), transparent 70%);
  pointer-events: none;
}
.login-left::after {
  content: ""; position: absolute; bottom: -60px; left: -40px;
  width: 230px; height: 230px; border-radius: 50%;
  background: radial-gradient(circle, rgba(255,107,43,0.08), transparent 70%);
  pointer-events: none;
}
.live-chip {
  display: inline-flex; align-items: center; gap: 6px;
  padding: 5px 11px; border-radius: 99px;
  background: rgba(0,229,160,0.1); border: 1px solid rgba(0,229,160,0.25);
  font-family: var(--font-display); font-size: 0.58rem; font-weight: 700;
  text-transform: uppercase; letter-spacing: 0.12em; color: var(--green);
  margin-bottom: 20px; position: relative; z-index: 1;
}
.live-chip::before { content: ""; width: 6px; height: 6px; border-radius: 50%; background: var(--green); animation: blink 2s infinite; }
@keyframes blink { 0%,100%{opacity:1;} 50%{opacity:0.35;} }
.login-headline { font-family: var(--font-display); font-size: 2.9rem; line-height: 0.88; color: #fff; font-weight: 800; position: relative; z-index: 1; }
.login-headline .accent { color: var(--green); }
.login-sub { font-size: 0.73rem; color: var(--muted2); margin-top: 14px; line-height: 1.65; max-width: 250px; position: relative; z-index: 1; }
.login-kpis { display: flex; gap: 20px; margin-top: 28px; position: relative; z-index: 1; }
.kpi p:first-child { font-family: var(--font-display); font-size: 1.35rem; font-weight: 800; color: #fff; }
.kpi p:last-child { font-size: 0.58rem; font-weight: 600; text-transform: uppercase; letter-spacing: 0.1em; color: var(--muted); }
.login-right { background: var(--surface); padding: 36px 30px; display: flex; flex-direction: column; justify-content: center; min-width: 0; }
.login-form-h { font-family: var(--font-display); font-size: 1.25rem; font-weight: 800; color: #fff; margin-bottom: 4px; }
.login-form-s { font-size: 0.73rem; color: var(--muted2); margin-bottom: 26px; }
.form-col { display: flex; flex-direction: column; gap: 14px; }
 
/* Recent users */
.recent-block { margin-bottom: 18px; }
.recent-hd { font-size: 0.58rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.12em; color: var(--muted); margin-bottom: 9px; }
.recent-list { display: flex; flex-direction: column; gap: 5px; }
.recent-item {
  display: flex; align-items: center; gap: 10px;
  padding: 9px 12px; border-radius: 10px;
  background: rgba(255,255,255,0.03); border: 1px solid var(--border);
  cursor: pointer; transition: all 0.2s;
}
.recent-item:hover { background: rgba(0,229,160,0.06); border-color: rgba(0,229,160,0.22); }
.rec-av { width: 28px; height: 28px; border-radius: 7px; flex-shrink: 0; display: flex; align-items: center; justify-content: center; font-family: var(--font-display); font-size: 0.65rem; font-weight: 800; color: #fff; }
.rec-info { flex: 1; min-width: 0; }
.rec-name { font-size: 0.78rem; font-weight: 600; color: var(--text); overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
.rec-role { font-size: 0.58rem; color: var(--muted); }
.rec-arr { color: var(--muted); flex-shrink: 0; }
.rec-arr svg { width: 12px; height: 12px; }
.or-row { display: flex; align-items: center; gap: 10px; margin: 12px 0; }
.or-row::before,.or-row::after { content:""; flex:1; height:1px; background:var(--border); }
.or-row span { font-size: 0.58rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.12em; color: var(--muted); }
 
/* ─── ROLE PAGE ─── */
#pg-role { display: flex; align-items: center; justify-content: center; padding: 36px 16px; }
.role-c { max-width: 500px; width: 100%; text-align: center; }
.role-eyebrow { font-size: 0.58rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.14em; color: var(--muted); margin-bottom: 10px; }
.role-h { font-family: var(--font-display); font-size: 2.3rem; font-weight: 800; color: #fff; margin-bottom: 7px; }
.role-s { font-size: 0.75rem; color: var(--muted2); margin-bottom: 28px; }
.role-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
.role-card {
  background: var(--surface); border: 2px solid var(--border);
  border-radius: 20px; padding: 26px 18px;
  cursor: pointer; transition: all 0.28s;
  position: relative; overflow: hidden; text-align: left;
}
.role-card:hover { transform: translateY(-3px); }
.role-card.rs:hover,.role-card.rs.sel { border-color: rgba(0,229,160,0.5); }
.role-card.rm:hover,.role-card.rm.sel { border-color: rgba(255,107,43,0.5); }
.role-card.sel { transform: translateY(-5px); }
.role-card-bg { position: absolute; top: -30px; right: -30px; width: 100px; height: 100px; border-radius: 50%; opacity: 0.08; transition: opacity 0.3s; }
.role-card:hover .role-card-bg,.role-card.sel .role-card-bg { opacity: 0.15; }
.role-ico { width: 48px; height: 48px; border-radius: 13px; display: flex; align-items: center; justify-content: center; margin-bottom: 14px; }
.role-ico svg { width: 22px; height: 22px; }
.role-card h3 { font-family: var(--font-display); font-size: 0.9rem; font-weight: 800; color: #fff; margin-bottom: 5px; text-transform: uppercase; letter-spacing: 0.04em; }
.role-card p { font-size: 0.7rem; color: var(--muted2); line-height: 1.55; }
.role-chk { position: absolute; top: 12px; right: 12px; width: 20px; height: 20px; border-radius: 6px; border: 1.5px solid var(--border); display: flex; align-items: center; justify-content: center; transition: all 0.25s; }
.role-card.rs.sel .role-chk { background: var(--green); border-color: var(--green); }
.role-card.rm.sel .role-chk { background: var(--orange); border-color: var(--orange); }
.role-chk svg { width: 10px; height: 10px; display: none; }
.role-card.sel .role-chk svg { display: block; }
 
/* ─── PRESENTATION PAGE ─── */
#pg-pres { padding: 30px 20px 60px; }
.pres-inner { max-width: 900px; margin: 0 auto; }
.pres-masthead { text-align: center; margin-bottom: 28px; }
.pres-tab-row { display: flex; justify-content: center; gap: 7px; flex-wrap: wrap; margin-bottom: 28px; }
.psec { display: none; }
.psec.on { display: block; animation: pg-in 0.38s ease; }
 
/* MVV */
.mvv-grid { display: grid; grid-template-columns: repeat(3,1fr); gap: 14px; }
@media (max-width:600px) { .mvv-grid { grid-template-columns:1fr; } }
.mvv-card { background: var(--surface); border: 1px solid var(--border); border-radius: 18px; padding: 22px; transition: all 0.28s; position: relative; overflow: hidden; }
.mvv-card::after { content:""; position:absolute; bottom:0; left:0; right:0; height:2px; opacity:0; transition:opacity 0.3s; }
.mvv-card:hover { transform: translateY(-3px); }
.mvv-card:hover::after { opacity:1; }
.mvv-card.cg::after { background:var(--green); }
.mvv-card.co::after { background:var(--orange); }
.mvv-card.cb::after { background:var(--blue-accent); }
.mvv-ico { width: 40px; height: 40px; border-radius: 11px; display: flex; align-items: center; justify-content: center; margin-bottom: 14px; }
.mvv-ico svg { width: 19px; height: 19px; }
.mvv-label { font-size: 0.56rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.12em; margin-bottom: 6px; }
.mvv-card h3 { font-family: var(--font-display); font-size: 0.92rem; font-weight: 800; color: #fff; margin-bottom: 7px; text-transform: uppercase; }
.mvv-card p { font-size: 0.72rem; color: var(--muted2); line-height: 1.65; }
 
/* Pipeline */
.pipe-row { display: flex; align-items: flex-start; gap: 0; overflow-x: auto; scrollbar-width: none; padding-bottom: 6px; margin: 22px 0; }
.pipe-row::-webkit-scrollbar { display: none; }
.pipe-node { display: flex; flex-direction: column; align-items: center; gap: 6px; min-width: 78px; cursor: pointer; }
.pipe-circle {
  width: 44px; height: 44px; border-radius: 50%;
  border: 2px solid var(--border); background: var(--surface2);
  display: flex; align-items: center; justify-content: center;
  font-family: var(--font-display); font-size: 0.78rem; font-weight: 800;
  color: var(--muted); transition: all 0.3s; flex-shrink: 0;
}
.pipe-circle.done { border-color: var(--orange); background: rgba(255,107,43,0.1); color: var(--orange); }
.pipe-circle.curr { border-color: var(--orange); background: var(--orange); color: #fff; box-shadow: 0 0 18px rgba(255,107,43,0.42); }
.pipe-lbl { font-size: 0.5rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.08em; color: var(--muted); text-align: center; }
.pipe-conn { flex: 1; height: 2px; background: var(--border); margin-top: 21px; min-width: 14px; position: relative; overflow: hidden; }
.pipe-fill { height: 100%; background: var(--orange); width: 0; transition: width 0.5s ease; }
.pipe-fill.done { width: 100%; }
.pipe-detail-card {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: 16px; padding: 22px;
  border-left: 3px solid var(--orange);
  animation: pg-in 0.3s ease;
}
.pipe-detail-cat { font-size: 0.58rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.12em; color: var(--orange); margin-bottom: 6px; }
.pipe-detail-card h3 { font-family: var(--font-display); font-size: 1.4rem; font-weight: 800; color: #fff; margin-bottom: 7px; letter-spacing: 0.02em; }
.pipe-detail-card p { font-size: 0.76rem; color: var(--muted2); line-height: 1.72; }
 
/* Stats */
.stat-row { display: grid; grid-template-columns: repeat(4,1fr); gap: 13px; }
@media (max-width:600px) { .stat-row { grid-template-columns: 1fr 1fr; } }
.stat-card { background: var(--surface); border: 1px solid var(--border); border-radius: 16px; padding: 18px; text-align: center; transition: all 0.25s; }
.stat-card:hover { border-color: rgba(255,255,255,0.12); transform: translateY(-2px); }
.stat-card .s-lbl { font-size: 0.54rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.12em; margin-bottom: 8px; }
.stat-card .s-val { font-family: var(--font-display); font-size: 2rem; font-weight: 800; color: #fff; }
.stat-card .s-desc { font-size: 0.62rem; color: var(--muted2); margin-top: 3px; }
 
/* Calendar */
.cal-grid { display: grid; grid-template-columns: repeat(3,1fr); gap: 11px; }
@media (max-width:640px) { .cal-grid { grid-template-columns: 1fr 1fr; } }
.cal-month-box { background: var(--surface); border: 1px solid var(--border); border-radius: 13px; padding: 13px; }
.cal-month-title { font-family: var(--font-display); font-size: 0.62rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.09em; color: #fff; text-align: center; margin-bottom: 9px; }
.cal-dow { display: grid; grid-template-columns: repeat(7,1fr); gap: 2px; margin-bottom: 3px; }
.cal-dow span { font-size: 0.44rem; font-weight: 700; text-transform: uppercase; color: var(--muted); text-align: center; }
.cal-days { display: grid; grid-template-columns: repeat(7,1fr); gap: 2px; }
.cd { aspect-ratio:1; display:flex; align-items:center; justify-content:center; font-size:0.54rem; font-weight:500; border-radius:4px; color:var(--muted2); }
.cd.induccion { background:rgba(0,200,100,0.2); color:#00C864; font-weight:700; }
.cd.inicio { background:rgba(59,127,255,0.2); color:#7EA8FF; font-weight:700; }
.cd.corte { background:rgba(255,107,43,0.24); color:var(--orange); font-weight:700; }
.cd.fin { background:rgba(245,158,11,0.2); color:#FBBF24; font-weight:700; }
.cd.examen { background:rgba(0,229,160,0.2); color:var(--green); font-weight:700; }
.cal-legend { display:flex; flex-wrap:wrap; gap:10px; justify-content:center; margin-top:16px; }
.cal-leg-item { display:flex; align-items:center; gap:5px; font-size:0.58rem; font-weight:600; color:var(--muted2); text-transform:uppercase; letter-spacing:0.07em; }
.cal-leg-dot { width:7px; height:7px; border-radius:50%; }
.alert-tl { display:flex; flex-direction:column; }
.al-row { display:flex; gap:14px; padding:14px 0; border-bottom:1px solid var(--border); }
.al-row:last-child { border-bottom:none; }
.al-dot-col { display:flex; flex-direction:column; align-items:center; gap:3px; padding-top:1px; }
.al-dot { width:9px; height:9px; border-radius:50%; flex-shrink:0; }
.al-line { width:1px; flex:1; min-height:16px; opacity:0.2; }
.al-body .al-date { font-size:0.57rem; font-weight:700; text-transform:uppercase; letter-spacing:0.1em; margin-bottom:3px; }
.al-body .al-title { font-size:0.86rem; font-weight:700; color:#fff; margin-bottom:3px; }
.al-body .al-desc { font-size:0.7rem; color:var(--muted2); line-height:1.6; }
 
/* ─── DASHBOARD ─── */
#pg-dash { padding: 26px 20px 60px; }
.dash-wrap { max-width: 1000px; margin: 0 auto; }
.dash-greeting .gr-eyebrow { font-size: 0.6rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.14em; color: var(--green); margin-bottom: 3px; }
.dash-greeting h2 { font-family: var(--font-display); font-size: 1.9rem; font-weight: 800; color: #fff; }
.dash-greeting .gr-sub { font-size: 0.72rem; color: var(--muted2); margin-top: 2px; }
.qs-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin: 18px 0; }
@media(max-width:500px) { .qs-grid { grid-template-columns:1fr; } }
.qs-card { background: var(--surface); border: 1px solid var(--border); border-radius: 13px; padding: 15px; display: flex; align-items: center; gap: 12px; transition: all 0.2s; }
.qs-card:hover { border-color: rgba(255,255,255,0.11); }
.qs-ico { width: 38px; height: 38px; border-radius: 10px; display: flex; align-items: center; justify-content: center; flex-shrink: 0; }
.qs-ico svg { width: 17px; height: 17px; }
.qs-num { font-family: var(--font-display); font-size: 1.35rem; font-weight: 800; color: #fff; line-height: 1; }
.qs-lbl { font-size: 0.57rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.09em; color: var(--muted); }
.sh-row { display:flex; align-items:center; justify-content:space-between; margin-bottom:11px; }
.sub-grid { display: grid; grid-template-columns: repeat(3,1fr); gap: 10px; }
@media(max-width:680px) { .sub-grid { grid-template-columns: 1fr 1fr; } }
@media(max-width:380px) { .sub-grid { grid-template-columns: 1fr; } }
.sub-card {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: 13px; padding: 14px;
  cursor: pointer; transition: all 0.2s;
  position: relative; overflow: hidden;
}
.sub-card::before { content:""; position:absolute; top:0; left:0; right:0; height:2px; background:linear-gradient(90deg,var(--green),#00A86B); transform:scaleX(0); transform-origin:left; transition:transform 0.3s; }
.sub-card:hover::before { transform:scaleX(1); }
.sub-card:hover { border-color:rgba(0,229,160,0.2); transform:translateY(-2px); }
.sub-card h4 { font-family: var(--font-display); font-size: 0.76rem; font-weight: 700; color: #fff; line-height: 1.38; margin-bottom: 9px; }
.sc-foot { display:flex; align-items:center; justify-content:space-between; }
.sc-cta { font-size: 0.53rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.08em; color: var(--muted); }
.sc-arrow { width: 21px; height: 21px; border-radius: 6px; background: rgba(255,255,255,0.05); display: flex; align-items: center; justify-content: center; transition: all 0.2s; }
.sc-arrow svg { width: 9px; height: 9px; color: var(--muted); }
.sub-card:hover .sc-arrow { background: rgba(0,229,160,0.15); }
.sub-card:hover .sc-arrow svg { color: var(--green); }
 
/* Filter panel */
.filter-panel { background: var(--surface); border: 1px solid var(--border); border-radius: 20px; padding: 24px; }
.filter-group-title { font-size: 0.58rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.12em; color: var(--muted); margin-bottom: 10px; }
.ftag {
  padding: 6px 12px; border-radius: 99px;
  border: 1.5px solid var(--border); background: transparent;
  font-family: var(--font-display); font-size: 0.6rem; font-weight: 700;
  text-transform: uppercase; letter-spacing: 0.07em;
  cursor: pointer; color: var(--muted); transition: all 0.2s;
}
.ftag:hover { border-color: rgba(255,255,255,0.16); color: var(--text); }
.ftag.on { background: var(--green); border-color: var(--green); color: #051a0e; }
 
/* Monitor cards */
.mon-card { background: var(--surface); border: 1px solid var(--border); border-radius: 18px; padding: 18px; transition: all 0.25s; }
.mon-card:hover { border-color: rgba(255,255,255,0.11); transform: translateY(-2px); }
.mon-card.ideal { border-color: rgba(0,229,160,0.38); background: rgba(0,229,160,0.03); }
.mon-av { width: 46px; height: 46px; border-radius: 12px; display: flex; align-items: center; justify-content: center; font-family: var(--font-display); font-size: 1rem; font-weight: 800; color: #fff; flex-shrink: 0; }
.mon-name { font-family: var(--font-display); font-size: 0.92rem; font-weight: 800; color: #fff; }
.mon-bio { font-size: 0.69rem; color: var(--muted2); line-height: 1.58; }
.mon-score { font-size: 0.62rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.09em; color: var(--green); }
.stars { color: #FBBF24; font-size: 0.82rem; letter-spacing: -1px; }
 
/* Detail view */
.det-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
@media(max-width:580px) { .det-grid { grid-template-columns:1fr; } }
.sess-row { display:flex; align-items:center; gap:10px; padding:10px; background:rgba(0,229,160,0.05); border:1px solid rgba(0,229,160,0.12); border-radius:10px; margin-bottom:6px; transition:all 0.2s; }
.sess-row:hover { background:rgba(0,229,160,0.09); }
.sess-ico { width:30px; height:30px; border-radius:8px; background:rgba(0,229,160,0.1); display:flex; align-items:center; justify-content:center; flex-shrink:0; }
.sess-ico svg { width:13px; height:13px; color:var(--green); }
.sess-name { font-size:0.7rem; font-weight:600; color:#fff; }
.sess-meta { font-size:0.6rem; color:var(--muted); }
.mat-row { display:flex; align-items:center; gap:9px; padding:9px; background:rgba(255,255,255,0.03); border:1px solid var(--border); border-radius:9px; margin-bottom:5px; cursor:pointer; transition:all 0.2s; }
.mat-row:hover { background:rgba(255,255,255,0.06); }
.mat-ico { width:27px; height:27px; border-radius:7px; background:rgba(0,229,160,0.1); display:flex; align-items:center; justify-content:center; flex-shrink:0; }
.mat-ico svg { width:12px; height:12px; color:var(--green); }
.mat-name { font-size:0.68rem; font-weight:600; color:var(--text); }
.mat-size { font-size:0.58rem; color:var(--muted); }
.upload-zone { border:2px dashed rgba(0,229,160,0.22); border-radius:12px; padding:22px; text-align:center; cursor:pointer; transition:all 0.3s; background:rgba(0,229,160,0.02); }
.upload-zone:hover,.upload-zone.dov { border-color:var(--green); background:rgba(0,229,160,0.06); }
.upload-zone svg { display:block; margin:0 auto 7px; color:var(--green); }
.upload-zone p { font-size:0.72rem; font-weight:600; color:var(--text); }
.upload-zone small { font-size:0.62rem; color:var(--muted); }
 
/* ─── PROFILE DROPDOWN ─── */
#pd {
  position: fixed; top: 65px; right: 14px; width: 320px;
  background: var(--surface); border: 1px solid var(--border2);
  border-radius: 18px; z-index: 600;
  box-shadow: 0 18px 55px rgba(0,0,0,0.5);
  display: none; overflow: hidden;
}
#pd.show { display: block; animation: dropIn 0.22s cubic-bezier(0.22,1,0.36,1); }
@keyframes dropIn { from{opacity:0;transform:translateY(-8px);} to{opacity:1;transform:translateY(0);} }
.pd-head { padding: 16px; border-bottom: 1px solid var(--border); display: flex; align-items: center; gap: 10px; }
.pd-av { width: 40px; height: 40px; border-radius: 10px; display: flex; align-items: center; justify-content: center; font-family: var(--font-display); font-size: 0.88rem; font-weight: 800; color: #fff; flex-shrink: 0; }
.pd-name { font-family: var(--font-display); font-size: 0.85rem; font-weight: 800; color: #fff; }
.pd-role-lbl { font-size: 0.56rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.1em; color: var(--muted); }
.pd-body { padding: 14px; max-height: 370px; overflow-y: auto; }
.pd-slbl { font-size: 0.54rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.12em; color: var(--muted); margin-bottom: 9px; }
.grade-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 6px; margin-bottom: 9px; }
.gi {
  background: rgba(255,255,255,0.04); border: 1px solid var(--border); border-radius: 8px;
  padding: 9px; color: #fff; text-align: center;
  font-family: var(--font-display); font-size: 0.98rem; font-weight: 800; letter-spacing: 0.03em;
  outline: none; width: 100%; transition: all 0.2s;
}
.gi:focus { border-color: var(--green); }
.gi::placeholder { font-family: var(--font-body); font-size: 0.65rem; font-weight: 500; color: var(--muted); letter-spacing: 0; }
.grade-res { background: rgba(255,255,255,0.03); border: 1px solid var(--border); border-radius: 9px; padding: 12px; text-align: center; margin-bottom: 14px; }
.gr-lbl { font-size: 0.52rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.12em; color: var(--muted); margin-bottom: 3px; }
.gr-val { font-family: var(--font-display); font-size: 1.8rem; font-weight: 800; letter-spacing: 0.04em; }
.gr-track { height: 3px; background: rgba(255,255,255,0.07); border-radius: 99px; overflow: hidden; margin-top: 7px; }
.gr-fill { height: 100%; background: linear-gradient(90deg,var(--green),#00A86B); width: 0; transition: width 0.4s ease; }
.sess-mini { display:flex; align-items:center; justify-content:space-between; padding:8px; background:rgba(255,255,255,0.03); border:1px solid var(--border); border-radius:8px; margin-bottom:5px; }
.sm-info .sm-sub { font-size:0.55rem; font-weight:700; text-transform:uppercase; letter-spacing:0.08em; color:var(--muted); }
.sm-info .sm-par { font-size:0.74rem; font-weight:600; color:var(--text); }
.sm-acts { display:flex; gap:4px; }
.sm-btn { width:24px; height:24px; border-radius:6px; display:flex; align-items:center; justify-content:center; cursor:pointer; border:none; transition:all 0.2s; }
.sm-btn svg { width:11px; height:11px; }
.sm-chat { background:rgba(0,229,160,0.1); color:var(--green); }
.sm-chat:hover { background:rgba(0,229,160,0.2); }
.sm-del { background:rgba(239,68,68,0.1); color:#ef4444; }
.sm-del:hover { background:rgba(239,68,68,0.2); }
.pd-foot { padding: 10px 14px; border-top: 1px solid var(--border); }
 
/* ─── INBOX MODAL ─── */
#inbox-modal { position:fixed; inset:0; background:rgba(7,11,20,0.9); backdrop-filter:blur(16px); z-index:700; display:none; align-items:center; justify-content:center; padding:14px; }
#inbox-modal.show { display:flex; animation:fadeIn 0.22s ease; }
@keyframes fadeIn { from{opacity:0;} to{opacity:1;} }
.inbox-box { background:var(--surface); border:1px solid var(--border2); border-radius:22px; width:100%; max-width:480px; max-height:76vh; display:flex; flex-direction:column; overflow:hidden; }
.inbox-head { padding:18px 20px; border-bottom:1px solid var(--border); display:flex; align-items:center; justify-content:space-between; flex-shrink:0; }
.inbox-head h3 { font-family:var(--font-display); font-size:1.05rem; font-weight:800; color:#fff; }
.inbox-head p { font-size:0.56rem; font-weight:700; text-transform:uppercase; letter-spacing:0.12em; color:var(--muted); margin-top:1px; }
.inbox-close { width:28px; height:28px; border-radius:7px; border:none; background:rgba(255,255,255,0.06); color:var(--muted2); cursor:pointer; display:flex; align-items:center; justify-content:center; transition:all 0.2s; }
.inbox-close:hover { background:rgba(255,255,255,0.1); color:#fff; }
.inbox-close svg { width:12px; height:12px; }
.inbox-body { padding:13px; overflow-y:auto; flex:1; }
.ib-item { display:flex; align-items:center; gap:10px; padding:12px; background:rgba(255,255,255,0.03); border:1px solid var(--border); border-radius:12px; cursor:pointer; transition:all 0.2s; margin-bottom:6px; }
.ib-item:hover { background:rgba(0,229,160,0.05); border-color:rgba(0,229,160,0.22); }
.ib-av { width:38px; height:38px; border-radius:10px; display:flex; align-items:center; justify-content:center; font-family:var(--font-display); font-size:0.72rem; font-weight:800; color:#fff; flex-shrink:0; }
.ib-name { font-family:var(--font-display); font-size:0.8rem; font-weight:800; color:#fff; }
.ib-sub { font-size:0.56rem; font-weight:700; text-transform:uppercase; letter-spacing:0.09em; color:var(--muted); }
.ib-prev { font-size:0.67rem; color:var(--muted2); overflow:hidden; white-space:nowrap; text-overflow:ellipsis; margin-top:1px; }
 
/* ─── CHAT ─── */
#chat-modal { position:fixed; inset:0; background:rgba(7,11,20,0.93); backdrop-filter:blur(20px); z-index:800; display:none; align-items:center; justify-content:center; padding:14px; }
#chat-modal.show { display:flex; animation:fadeIn 0.22s ease; }
.chat-win { width:100%; max-width:500px; height:min(78vh,660px); background:var(--surface); border:1px solid var(--border2); border-radius:22px; display:flex; flex-direction:column; overflow:hidden; box-shadow:0 26px 70px rgba(0,0,0,0.55); }
.chat-head { padding:14px 18px; border-bottom:1px solid var(--border); display:flex; align-items:center; gap:10px; flex-shrink:0; background:rgba(255,255,255,0.02); }
.chat-av { width:36px; height:36px; border-radius:9px; display:flex; align-items:center; justify-content:center; font-family:var(--font-display); font-size:0.88rem; font-weight:800; color:#fff; flex-shrink:0; }
.chat-nm { font-family:var(--font-display); font-size:0.8rem; font-weight:800; color:#fff; }
.chat-sub-lbl { font-size:0.54rem; font-weight:700; text-transform:uppercase; letter-spacing:0.1em; color:var(--green); }
.ai-dot { display:inline-flex; align-items:center; gap:3px; padding:2px 7px; background:rgba(0,229,160,0.08); border:1px solid rgba(0,229,160,0.2); border-radius:99px; font-size:0.5rem; font-weight:700; text-transform:uppercase; letter-spacing:0.09em; color:var(--green); }
.ai-dot::before { content:""; width:5px; height:5px; border-radius:50%; background:var(--green); animation:blink 2s infinite; }
.chat-close { margin-left:auto; width:28px; height:28px; border-radius:7px; border:none; background:rgba(255,255,255,0.05); color:var(--muted2); cursor:pointer; display:flex; align-items:center; justify-content:center; transition:all 0.2s; }
.chat-close:hover { background:rgba(255,255,255,0.1); color:#fff; }
.chat-close svg { width:12px; height:12px; }
.chat-msgs { flex:1; overflow-y:auto; padding:13px; display:flex; flex-direction:column; gap:9px; scroll-behavior:smooth; }
.chat-msgs::-webkit-scrollbar { width:2px; }
.chat-msgs::-webkit-scrollbar-thumb { background:var(--border); border-radius:2px; }
.bubble { max-width:80%; padding:9px 12px; border-radius:14px; line-height:1.55; font-size:0.79rem; word-break:break-word; }
.bubble.mine { align-self:flex-end; background:linear-gradient(135deg,#00A86B,#006644); color:#fff; border-radius:14px 14px 3px 14px; }
.bubble.theirs { align-self:flex-start; background:var(--surface2); border:1px solid var(--border); border-radius:14px 14px 14px 3px; }
.bubble-from { font-size:0.54rem; font-weight:700; text-transform:uppercase; letter-spacing:0.09em; opacity:0.5; margin-bottom:3px; }
.typing-ind { display:flex; align-items:center; gap:4px; padding:9px 12px; background:var(--surface2); border-radius:14px 14px 14px 3px; align-self:flex-start; border:1px solid var(--border); }
.td { width:5px; height:5px; border-radius:50%; background:var(--green); animation:tb 1.2s infinite; }
.td:nth-child(2){animation-delay:.2s;} .td:nth-child(3){animation-delay:.4s;}
@keyframes tb { 0%,60%,100%{transform:translateY(0);opacity:.5;} 30%{transform:translateY(-5px);opacity:1;} }
.chat-foot { padding:10px 12px; border-top:1px solid var(--border); background:rgba(0,0,0,0.18); flex-shrink:0; display:flex; gap:8px; }
.chat-inp { flex:1; background:rgba(255,255,255,0.04); border:1.5px solid var(--border); border-radius:10px; padding:9px 12px; color:var(--text); font-family:var(--font-body); font-size:0.79rem; outline:none; transition:all 0.2s; }
.chat-inp:focus { border-color:var(--green); }
.chat-inp::placeholder { color:var(--muted); }
.chat-send { width:36px; height:36px; border-radius:9px; background:var(--green); border:none; color:#051a0e; cursor:pointer; display:flex; align-items:center; justify-content:center; transition:all 0.2s; flex-shrink:0; }
.chat-send:hover { background:#00c48a; }
.chat-send svg { width:14px; height:14px; }
 
/* ─── TOAST ─── */
#toast { position:fixed; bottom:22px; left:50%; transform:translateX(-50%) translateY(60px); background:var(--surface); border:1px solid var(--border2); border-radius:10px; padding:10px 16px; z-index:900; font-size:0.74rem; font-weight:600; color:var(--text); display:flex; align-items:center; gap:8px; box-shadow:0 8px 28px rgba(0,0,0,0.4); transition:transform 0.3s cubic-bezier(0.22,1,0.36,1); white-space:nowrap; }
#toast.show { transform:translateX(-50%) translateY(0); }
#toast svg { width:14px; height:14px; flex-shrink:0; }
 
/* empty state */
.empty-st { text-align:center; padding:26px; color:var(--muted); }
.empty-st svg { width:30px; height:30px; margin:0 auto 8px; opacity:0.4; }
.empty-st p { font-size:0.76rem; }
</style>
</head>
<body>
<div class="blob b1"></div>
<div class="blob b2"></div>
 
<!-- ═══════ TOPNAV ═══════ -->
<nav id="nav">
  <div class="nav-logo" onclick="logoClick()">
    <div class="nav-logo-icon">
      <svg viewBox="0 0 24 24" fill="none" stroke="#051a0e" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
        <path d="M12 2L2 7l10 5 10-5-10-5z"/><path d="M2 17l10 5 10-5"/><path d="M2 12l10 5 10-5"/>
      </svg>
    </div>
    <div class="nav-logo-text"><span class="t1">Parche FAE</span><span class="t2">Externado · FAE</span></div>
  </div>
  <div class="nav-right">
    <div id="nav-auth">
      <button class="nav-icon-btn" onclick="toggleInbox()" title="Bandeja">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/></svg>
        <div class="notif-dot" id="notif-dot"></div>
      </button>
      <button class="nav-user-chip" onclick="togglePD()">
        <div class="nav-user-av" id="nav-av">?</div>
        <div class="nav-user-info">
          <div class="name" id="nav-name">—</div>
          <div class="role-lbl" id="nav-role">—</div>
        </div>
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polyline points="6 9 12 15 18 9"/></svg>
      </button>
    </div>
    <div id="nav-loginbtn">
      <button class="btn btn-ghost btn-sm" onclick="goPage('pg-login')">Iniciar sesión</button>
    </div>
  </div>
</nav>
 
<div id="app">
 
<!-- ═══════ LOGIN ═══════ -->
<div id="pg-login" class="page active" style="display:flex;align-items:center;justify-content:center;padding:28px 16px;">
  <div class="login-shell">
    <div class="login-left">
      <div style="position:relative;z-index:1">
        <div class="live-chip">Sistema activo</div>
        <div class="login-headline">PARCHE<br><span class="accent">FAE</span></div>
        <p class="login-sub">El ecosistema de monitorías académicas de la Facultad de Administración de Empresas.</p>
        <div class="login-kpis">
          <div class="kpi"><p>100+</p><p>Estudiantes</p></div>
          <div class="kpi"><p>70%</p><p>Participación</p></div>
          <div class="kpi"><p>+20%</p><p>Promedio</p></div>
        </div>
      </div>
      <p style="font-size:0.56rem;font-weight:600;text-transform:uppercase;letter-spacing:0.12em;color:var(--muted);position:relative;z-index:1;margin-top:24px">Universidad Externado de Colombia · 2026</p>
    </div>
    <div class="login-right">
      <div class="login-form-h">Acceso Institucional</div>
      <div class="login-form-s">Ingresa con tu nombre y PIN.</div>
      <div id="recent-wrap" style="display:none">
        <div class="recent-block">
          <div class="recent-hd">Accesos Recientes</div>
          <div id="recent-list" class="recent-list"></div>
        </div>
        <div class="or-row"><span>o ingresa manualmente</span></div>
      </div>
      <div class="form-col">
        <div>
          <label class="field-label">Nombre de usuario</label>
          <div class="inp-wrap">
            <span class="inp-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg></span>
            <input id="inp-u" class="inp" type="text" placeholder="Tu nombre completo" autocomplete="off">
          </div>
        </div>
        <div>
          <label class="field-label">PIN de acceso</label>
          <div class="inp-wrap">
            <span class="inp-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="11" width="18" height="11" rx="2" ry="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/></svg></span>
            <input id="inp-p" class="inp" type="password" placeholder="••••••">
          </div>
        </div>
        <button class="btn btn-green btn-w" onclick="doLogin()">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M15 3h4a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2h-4"/><polyline points="10 17 15 12 10 7"/><line x1="15" y1="12" x2="3" y2="12"/></svg>
          Ingresar al Parche
        </button>
        
      </div>
    </div>
  </div>
</div>
 
<!-- ═══════ ROLE ═══════ -->
<div id="pg-role" class="page" style="display:flex;align-items:center;justify-content:center;padding:36px 16px;">
  <div class="role-c">
    <div class="badge badge-green" style="margin-bottom:12px">Paso 1 de 2</div>
    <h2 class="role-h">¿Cuál es tu rol hoy?</h2>
    <p class="role-s">Selecciona cómo quieres participar en el Parche FAE.</p>
    <div class="role-grid">
      <div class="role-card rs" id="rc-a" onclick="pickRole('aprendiz')">
        <div class="role-chk" id="chk-a"><svg viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="3"><polyline points="20 6 9 17 4 12"/></svg></div>
        <div class="role-card-bg" style="background:var(--green)"></div>
        <div class="role-ico" style="background:rgba(0,229,160,0.1)">
          <svg viewBox="0 0 24 24" fill="none" stroke="#00E5A0" stroke-width="2"><path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"/><path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"/></svg>
        </div>
        <h3>Quiero Aprender</h3>
        <p>Busco un monitor que me ayude a preparar mis materias y superar los cortes.</p>
      </div>
      <div class="role-card rm" id="rc-m" onclick="pickRole('monitor')">
        <div class="role-chk" id="chk-m"><svg viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="3"><polyline points="20 6 9 17 4 12"/></svg></div>
        <div class="role-card-bg" style="background:var(--orange)"></div>
        <div class="role-ico" style="background:rgba(255,107,43,0.1)">
          <svg viewBox="0 0 24 24" fill="none" stroke="#FF6B2B" stroke-width="2"><circle cx="12" cy="12" r="10"/><path d="M12 8v4"/><path d="M12 16h.01"/></svg>
        </div>
        <h3>Soy Monitor</h3>
        <p>Comparto mi conocimiento con compañeros de semestres inferiores.</p>
      </div>
    </div>
    <button id="btn-role-cont" class="btn btn-green btn-w" style="margin-top:18px" onclick="goToPres()" disabled>Continuar →</button>
  </div>
</div>
 
<!-- ═══════ PRESENTATION ═══════ -->
<div id="pg-pres" class="page">
  <div class="pres-inner">
    <button class="back-btn" onclick="goPage('pg-role')">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polyline points="15 18 9 12 15 6"/></svg>
      Atrás
    </button>
    <div class="pres-masthead">
      <div class="badge badge-orange" style="margin-bottom:10px">Ecosistema Académico FAE</div>
      <h1 style="font-family:var(--font-display);font-size:2.6rem;font-weight:800;color:#fff;letter-spacing:0.03em">PARCHE FAE</h1>
      <p style="font-size:0.64rem;font-weight:600;text-transform:uppercase;letter-spacing:0.14em;color:var(--muted);margin-top:3px">Monitorías Colaborativas · Universidad Externado de Colombia</p>
    </div>
    <div class="pres-tab-row">
      <button class="pill p-orange" onclick="showPT('prop',this)">01 Propósito</button>
      <button class="pill" onclick="showPT('5as',this)">02 Las 5 A's</button>
      <button class="pill" onclick="showPT('imp',this)">03 Impacto</button>
      <button class="pill" onclick="showPT('cal',this)">04 Calendario</button>
    </div>
 
    <!-- Propósito -->
    <div id="pt-prop" class="psec on">
      <div class="mvv-grid">
        <div class="mvv-card cg">
          <div class="mvv-ico" style="background:rgba(0,229,160,0.1)"><svg viewBox="0 0 24 24" fill="none" stroke="#00E5A0" stroke-width="2"><polygon points="13 2 3 14 12 14 11 22 21 10 12 10 13 2"/></svg></div>
          <div class="mvv-label" style="color:var(--green)">Misión</div>
          <h3>Conectar para Transformar</h3>
          <p>Conectamos semestres para transformar el rendimiento académico y vencer el individualismo en la carrera FAE.</p>
        </div>
        <div class="mvv-card co">
          <div class="mvv-ico" style="background:rgba(255,107,43,0.1)"><svg viewBox="0 0 24 24" fill="none" stroke="#FF6B2B" stroke-width="2"><circle cx="12" cy="12" r="10"/><circle cx="12" cy="12" r="3"/><line x1="12" y1="2" x2="12" y2="5"/><line x1="12" y1="19" x2="12" y2="22"/><line x1="2" y1="12" x2="5" y2="12"/><line x1="19" y1="12" x2="22" y2="12"/></svg></div>
          <div class="mvv-label" style="color:var(--orange)">Visión</div>
          <h3>Ecosistema Líder FAE</h3>
          <p>Ser el ecosistema de referencia para monitorías colaborativas, respaldado por resultados reales y medibles.</p>
        </div>
        <div class="mvv-card cb">
          <div class="mvv-ico" style="background:rgba(59,127,255,0.1)"><svg viewBox="0 0 24 24" fill="none" stroke="#3B7FFF" stroke-width="2"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg></div>
          <div class="mvv-label" style="color:#3B7FFF">Valores</div>
          <h3>Lo que nos Mueve</h3>
          <p><strong style="color:#fff">Empatía · Colectividad · Excelencia</strong><br>Apoyo mutuo como cultura, no como favor aislado.</p>
        </div>
      </div>
    </div>
 
    <!-- 5 A's -->
    <div id="pt-5as" class="psec">
      <div style="padding:14px 18px;background:rgba(255,107,43,0.07);border:1px solid rgba(255,107,43,0.16);border-radius:13px;margin-bottom:18px">
        <span style="font-size:0.57rem;font-weight:700;text-transform:uppercase;letter-spacing:0.12em;color:var(--orange)">Campaña de Mercadeo</span>
        <h3 style="font-family:var(--font-display);font-size:1.5rem;font-weight:800;color:#fff;margin-top:3px">La Ruta de las 5 A's</h3>
        <p style="font-size:0.71rem;color:var(--muted2)">Haz clic en cada nodo para ver la táctica de cada etapa.</p>
      </div>
      <div class="pipe-row" id="pipe-row"></div>
      <div id="pipe-det-wrap"></div>
    </div>
 
    <!-- Impacto -->
    <div id="pt-imp" class="psec">
      <div class="stat-row">
        <div class="stat-card"><div class="s-lbl" style="color:var(--green)">Estudiantes</div><div class="s-val">100+</div><div class="s-desc">Registrados al lanzar</div></div>
        <div class="stat-card"><div class="s-lbl" style="color:var(--orange)">Participación</div><div class="s-val">70%</div><div class="s-desc">Activa en monitorías</div></div>
        <div class="stat-card"><div class="s-lbl" style="color:#3B7FFF">Promedio</div><div class="s-val">+20%</div><div class="s-desc">Incremento proyectado</div></div>
        <div class="stat-card"><div class="s-lbl" style="color:#FBBF24">Retención</div><div class="s-val">65%</div><div class="s-desc">Trimestral</div></div>
      </div>
    </div>
 
    <!-- Calendario -->
    <div id="pt-cal" class="psec">
      <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:13px">
        <button class="pill p-orange" onclick="switchCalSem(1,this)">Sem 2026-1</button>
        <button class="pill" onclick="switchCalSem(2,this)">Sem 2026-2</button>
      </div>
      <div style="display:flex;gap:7px;margin-bottom:16px">
        <button class="pill p-orange" id="cv-grid-btn" onclick="switchCalView('grid',this)">Vista Calendario</button>
        <button class="pill" id="cv-list-btn" onclick="switchCalView('list',this)">Línea de Alerta</button>
      </div>
      <div id="cal-grid-wrap"></div>
      <div id="cal-list-wrap" style="display:none"></div>
      <div class="cal-legend">
        <div class="cal-leg-item"><div class="cal-leg-dot" style="background:#00C864"></div>Inducción</div>
        <div class="cal-leg-item"><div class="cal-leg-dot" style="background:#7EA8FF"></div>Inicio clases</div>
        <div class="cal-leg-item"><div class="cal-leg-dot" style="background:#FF6B2B"></div>Corte / Alerta</div>
        <div class="cal-leg-item"><div class="cal-leg-dot" style="background:#FBBF24"></div>Fin de clases</div>
        <div class="cal-leg-item"><div class="cal-leg-dot" style="background:#00E5A0"></div>Exámenes</div>
      </div>
    </div>
 
    <button class="btn btn-green btn-w" style="margin-top:26px" onclick="goPage('pg-dash');renderDash()">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/></svg>
      Ir al Dashboard Académico
    </button>
  </div>
</div>
 
<!-- ═══════ DASHBOARD ═══════ -->
<div id="pg-dash" class="page">
  <div class="dash-wrap">
    <div class="dash-greeting" style="margin-bottom:18px">
      <div class="gr-eyebrow">Conectado al Parche</div>
      <h2>Hola, <span id="dn" style="color:var(--green)">—</span></h2>
      <p class="gr-sub" id="drl">—</p>
    </div>
    <div class="qs-grid">
      <div class="qs-card">
        <div class="qs-ico" style="background:rgba(0,229,160,0.1)"><svg viewBox="0 0 24 24" fill="none" stroke="#00E5A0" stroke-width="2"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></svg></div>
        <div><div class="qs-num" id="qs-n">0</div><div class="qs-lbl">Monitorías Activas</div></div>
      </div>
      <div class="qs-card">
        <div class="qs-ico" style="background:rgba(255,107,43,0.1)"><svg viewBox="0 0 24 24" fill="none" stroke="#FF6B2B" stroke-width="2"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/><line x1="16" y1="13" x2="8" y2="13"/><line x1="16" y1="17" x2="8" y2="17"/></svg></div>
        <div><div class="qs-num">9</div><div class="qs-lbl">Semestres disponibles</div></div>
      </div>
    </div>
 
    <!-- View: Subjects -->
    <div id="v-subs">
      <div class="sh-row">
        <span class="section-label" style="margin:0">Pensum Académico</span>
        <div class="sem-strip" id="sem-strip"></div>
      </div>
      <div id="sub-grid" class="sub-grid" style="margin-top:11px"></div>
    </div>
 
    <!-- View: Filter -->
    <div id="v-filter" style="display:none">
      <button class="back-btn" onclick="showView('v-subs')"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polyline points="15 18 9 12 15 6"/></svg>Volver</button>
      <div class="filter-panel">
        <h3 style="font-family:var(--font-display);font-size:1.6rem;font-weight:800;color:#fff;margin-bottom:5px">¿Qué monitor buscas?</h3>
        <p style="font-size:0.71rem;color:var(--muted2);margin-bottom:20px">Filtra por personalidad y disponibilidad.</p>
        <div style="display:grid;grid-template-columns:1fr 1fr;gap:18px;margin-bottom:20px">
          <div>
            <div class="filter-group-title">Personalidad</div>
            <div style="display:flex;flex-wrap:wrap;gap:6px" id="fg-pers">
              <button class="ftag" onclick="this.classList.toggle('on')">Extrovertido/a</button>
              <button class="ftag" onclick="this.classList.toggle('on')">Paciente</button>
              <button class="ftag" onclick="this.classList.toggle('on')">Explica Despacio</button>
              <button class="ftag" onclick="this.classList.toggle('on')">Directo al Punto</button>
              <button class="ftag" onclick="this.classList.toggle('on')">Chill</button>
            </div>
          </div>
          <div>
            <div class="filter-group-title">Disponibilidad</div>
            <div style="display:flex;flex-wrap:wrap;gap:6px" id="fg-avail">
              <button class="ftag" onclick="this.classList.toggle('on')">Presencial (U)</button>
              <button class="ftag" onclick="this.classList.toggle('on')">Virtual (Meet)</button>
              <button class="ftag" onclick="this.classList.toggle('on')">Tiene Tiempo</button>
              <button class="ftag" onclick="this.classList.toggle('on')">Fines de Semana</button>
              <button class="ftag" onclick="this.classList.toggle('on')">Noches</button>
            </div>
          </div>
        </div>
        <button class="btn btn-green btn-w" onclick="applyFilters()">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/></svg>
          Encontrar mi Monitor Ideal
        </button>
      </div>
    </div>
 
    <!-- View: Cast -->
    <div id="v-cast" style="display:none">
      <button class="back-btn" onclick="showView('v-filter')"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polyline points="15 18 9 12 15 6"/></svg>Ajustar filtros</button>
      <div style="margin-bottom:16px">
        <span class="section-label">Monitores disponibles</span>
        <h3 id="cast-title" style="font-family:var(--font-display);font-size:1.5rem;font-weight:800;color:#fff"></h3>
      </div>
      <div id="cast-list" style="display:flex;flex-direction:column;gap:11px"></div>
    </div>
 
    <!-- View: Detail -->
    <div id="v-det" style="display:none">
      <button class="back-btn" onclick="showView('v-cast')"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polyline points="15 18 9 12 15 6"/></svg>Volver a monitores</button>
      <h3 id="det-title" style="font-family:var(--font-display);font-size:1.5rem;font-weight:800;color:#fff;margin-bottom:16px"></h3>
      <div class="det-grid">
        <div>
          <span class="section-label">📅 Próximas Sesiones</span>
          <div class="sess-row"><div class="sess-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="4" width="18" height="18" rx="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg></div><div><div class="sess-name">Lunes · 10:00 AM</div><div class="sess-meta">Aula 305 — Presencial</div></div></div>
          <div class="sess-row"><div class="sess-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polygon points="23 7 16 12 23 17 23 7"/><rect x="1" y="5" width="15" height="14" rx="2"/></svg></div><div><div class="sess-name">Miércoles · 2:00 PM</div><div class="sess-meta">Google Meet — Virtual</div></div></div>
          <div class="sess-row"><div class="sess-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="4" width="18" height="18" rx="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg></div><div><div class="sess-name">Viernes · 3:00 PM</div><div class="sess-meta">Aula 305 — Presencial</div></div></div>
        </div>
        <div>
          <span class="section-label">📁 Materiales</span>
          <div id="mat-list"></div>
        </div>
      </div>
      <div style="margin-top:16px">
        <span class="section-label">📤 Subir apuntes o PDF</span>
        <div class="upload-zone" id="upload-zone" onclick="document.getElementById('file-inp').click()">
          <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="17 8 12 3 7 8"/><line x1="12" y1="3" x2="12" y2="15"/></svg>
          <p style="margin-top:6px">Arrastra o haz clic para subir</p>
          <small>PDF, Word, Imágenes — máx. 10 MB</small>
          <input type="file" id="file-inp" multiple style="display:none" onchange="handleUpload(event)">
        </div>
        <div id="upload-list" style="display:flex;flex-direction:column;gap:5px;margin-top:8px"></div>
      </div>
    </div>
  </div>
</div>
 
</div><!-- /app -->
 
<!-- ═══════ PROFILE DROPDOWN ═══════ -->
<div id="pd">
  <div class="pd-head">
    <div class="pd-av" id="pd-av">?</div>
    <div><div class="pd-name" id="pd-name">—</div><div class="pd-role-lbl" id="pd-role">—</div></div>
  </div>
  <div class="pd-body">
    <div class="pd-slbl" style="margin-bottom:9px">Calculadora de Notas</div>
    <div class="grade-grid">
      <input class="gi" id="g1" type="number" step="0.1" min="0" max="5" placeholder="Corte 1" oninput="calcG()">
      <input class="gi" id="g2" type="number" step="0.1" min="0" max="5" placeholder="Corte 2" oninput="calcG()">
      <input class="gi" id="g3" type="number" step="0.1" min="0" max="5" placeholder="Corte 3" oninput="calcG()">
      <input class="gi" id="g4" type="number" step="0.1" min="0" max="5" placeholder="Corte 4" oninput="calcG()">
    </div>
    <div class="grade-res">
      <div class="gr-lbl" id="gr-lbl">Necesitas en C4 para pasar (3.0)</div>
      <div class="gr-val" id="gr-val" style="color:var(--muted2)">—</div>
      <div class="gr-track"><div class="gr-fill" id="gr-fill"></div></div>
    </div>
    <div class="hr"></div>
    <div class="pd-slbl">Mis Monitorías</div>
    <div id="pd-sess"></div>
  </div>
  <div class="pd-foot">
    <button class="btn btn-ghost btn-w" style="padding:9px;font-size:0.62rem;color:#ef4444" onclick="doLogout()">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M9 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h4"/><polyline points="16 17 21 12 16 7"/><line x1="21" y1="12" x2="9" y2="12"/></svg>
      Cerrar Sesión
    </button>
  </div>
</div>
 
<!-- ═══════ INBOX ═══════ -->
<div id="inbox-modal">
  <div class="inbox-box">
    <div class="inbox-head">
      <div><h3>Tu Bandeja</h3><p>Conversaciones activas</p></div>
      <button class="inbox-close" onclick="toggleInbox()"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg></button>
    </div>
    <div class="inbox-body" id="inbox-body"></div>
  </div>
</div>
 
<!-- ═══════ CHAT ═══════ -->
<div id="chat-modal">
  <div class="chat-win">
    <div class="chat-head">
      <div class="chat-av" id="chat-av">?</div>
      <div style="flex:1;min-width:0">
        <div class="chat-nm" id="chat-nm">—</div>
        <div style="display:flex;align-items:center;gap:5px;margin-top:1px">
          <div class="chat-sub-lbl" id="chat-sub">—</div>
          <div class="ai-dot">IA Activa</div>
        </div>
      </div>
      <button class="chat-close" onclick="closeChat()"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg></button>
    </div>
    <div id="chat-msgs" class="chat-msgs"></div>
    <div id="typing-row" style="padding:4px 13px;display:none">
      <div class="typing-ind"><div class="td"></div><div class="td"></div><div class="td"></div>
      <span style="font-size:0.52rem;font-weight:700;text-transform:uppercase;color:var(--muted2);margin-left:5px">escribiendo...</span></div>
    </div>
    <div class="chat-foot">
      <input id="chat-inp" class="chat-inp" type="text" placeholder="Escribe tu pregunta…" onkeydown="if(event.key==='Enter')sendMsg()">
      <button class="chat-send" onclick="sendMsg()"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><line x1="22" y1="2" x2="11" y2="13"/><polygon points="22 2 15 22 11 13 2 9 22 2"/></svg></button>
    </div>
  </div>
</div>
 
<!-- ═══════ TOAST ═══════ -->
<div id="toast">
  <svg viewBox="0 0 24 24" fill="none" stroke="#00E5A0" stroke-width="2.5"><polyline points="20 6 9 17 4 12"/></svg>
  <span id="toast-msg">—</span>
</div>
 
<script>
// ─── DATA ───
const PENSUM = {
  1:['Pensamiento Estratégico','Liderazgo Personal','Fundamentos de Adm. y Org.','Tecnología y Sociedad','Fundamentos de Matemáticas','Introducción a la Economía','Ética y Comp. Ciudadanas','Pensamiento Crítico I','Idioma I'],
  2:['Fund. Estrategia y Prospectiva','Análisis Organizacional','Contabilidad Gerencial','Métodos Cuantitativos I','Microeconomía','Instituciones Políticas','Electiva I','DECAPE','Idioma II'],
  3:['Propuestas Gerenciales','Fundamentos de Marketing','Comportamiento Org.','Desarrollo Sostenible','Planeación Financiera y Costos','Sistemas de Información','Métodos Cuantitativos II','Política y Entorno Macro.','Idioma III'],
  4:['Prospectiva','Liderazgo de Equipos','Investigación de Mercados','Producción de Bienes y Serv.','Decisiones de Inv. y Finan.','Estadística y Programación','Pensamiento Crítico II','Seminario Legis. Comercial','Idioma IV'],
  5:['Comunicaciones Integradas','Gestión Humana','Logística','Creatividad','Mercados Financieros','Modelos de Optimización I','Diagnóstico Sectorial y Reg.','Seminario Laboral','Idioma V','Electiva II'],
  6:['Dirección Estratégica','Gerencia de Mercadeo','Gestión del Cambio','Innovación y Mod. Negocio','Gerencia Financiera','Formulac. y Des. Proyectos','Modelos de Optimización II','Seminario Legis. Tributaria','Idioma VI'],
  7:['Casos Empresariales','Liderazgo Directivo','Habilidades Profesionales','Simuladores Gerenciales','Taller RSE','Taller de Emprendimiento','Negocios Internacionales','Plan Padrinos'],
  8:['Énfasis 1','Énfasis 2','Electiva III'],
  9:['Alpina','Bavaria','Ecopetrol','Pepsi','Coca-Cola','P&G','Autogermana','Terpel','Davivienda','Alquería','Samsung','Oracle']
};
 
const MONITORS = [
  {n:'Santiago Vargas',i:'SV',b:'Finanzas corporativas y análisis cuantitativo.',t:['Directo al Punto','Presencial (U)','Tiene Tiempo'],s:[1,2,3,4,5,6]},
  {n:'Valentina Ospina',i:'VO',b:'Economía con casos cotidianos de Bogotá.',t:['Paciente','Explica Despacio','Virtual (Meet)'],s:[1,2,3]},
  {n:'Sebastián Ríos',i:'SR',b:'Mercados financieros y decisiones de inversión.',t:['Directo al Punto','Virtual (Meet)','Noches'],s:[4,5,6,7]},
  {n:'Isabella Gómez',i:'IG',b:'Contabilidad y finanzas paso a paso.',t:['Paciente','Presencial (U)','Fines de Semana'],s:[2,3,4,5]},
  {n:'Mateo Acosta',i:'MA',b:'Métodos cuantitativos y estadística aplicada.',t:['Directo al Punto','Virtual (Meet)','Tiene Tiempo'],s:[2,3,4,5,6]},
  {n:'Camila Herrera',i:'CH',b:'Marketing digital y estrategia de marca.',t:['Extrovertido/a','Presencial (U)','Tiene Tiempo'],s:[3,4,5,6,7]},
  {n:'Nicolás Bermúdez',i:'NB',b:'Dirección estratégica con casos reales.',t:['Chill','Virtual (Meet)','Noches'],s:[3,4,5,6]},
  {n:'Alejandra Rueda',i:'AR',b:'Gestión del cambio e innovación aplicada.',t:['Paciente','Presencial (U)','Fines de Semana'],s:[6,7,8]},
  {n:'Miguel Ángel Cano',i:'MC',b:'Simuladores gerenciales y toma de decisiones.',t:['Directo al Punto','Virtual (Meet)','Tiene Tiempo'],s:[7,8]},
  {n:'Laura Quintero',i:'LQ',b:'Gestión humana y cultura organizacional.',t:['Extrovertido/a','Presencial (U)','Noches'],s:[2,3,5,7]},
  {n:'Daniel Morales',i:'DM',b:'Comportamiento org. y liderazgo ágil.',t:['Chill','Virtual (Meet)','Tiene Tiempo'],s:[3,4,5,7]},
  {n:'Sofía Castellanos',i:'SC',b:'Liderazgo y comunicación estratégica.',t:['Paciente','Presencial (U)','Fines de Semana'],s:[1,4,5,6,7]},
  {n:'Andrés Montoya',i:'AM',b:'Matemáticas y métodos cuantitativos.',t:['Directo al Punto','Virtual (Meet)','Noches'],s:[1,2,3,4]},
  {n:'Paulina Vergara',i:'PV',b:'Sistemas de información y estadística.',t:['Paciente','Explica Despacio','Presencial (U)'],s:[3,4,5,6]},
  {n:'David Jiménez',i:'DJ',b:'Modelos de optimización con lógica aplicada.',t:['Directo al Punto','Tiene Tiempo','Virtual (Meet)'],s:[5,6,7]},
  {n:'María José Torres',i:'MJ',b:'Legislación comercial y tributaria clara.',t:['Paciente','Presencial (U)','Fines de Semana'],s:[4,6,7]},
  {n:'Felipe Cardona',i:'FC',b:'Seminarios legales sin tecnicismos.',t:['Explica Despacio','Virtual (Meet)','Noches'],s:[4,6,7,8]},
  {n:'Natalia Pardo',i:'NP',b:'Negocios internacionales y proyectos globales.',t:['Extrovertido/a','Virtual (Meet)','Tiene Tiempo'],s:[6,7,8,9]},
  {n:'Carlos Estrada',i:'CE',b:'Formulación de proyectos y Canvas.',t:['Chill','Presencial (U)','Fines de Semana'],s:[6,7,8,9]},
  {n:'Gabriela Soto',i:'GS',b:'RSE e innovación sostenible.',t:['Paciente','Presencial (U)','Noches'],s:[3,6,7,8]},
  {n:'Juliana Arias',i:'JA',b:'Idiomas y comunicación profesional.',t:['Extrovertido/a','Virtual (Meet)','Tiene Tiempo'],s:[1,2,3,4,5,6]},
  {n:'Tomás Becerra',i:'TB',b:'Pensamiento crítico y habilidades blandas.',t:['Chill','Presencial (U)','Fines de Semana'],s:[1,4,7]},
  {n:'Ximena Flórez',i:'XF',b:'Ha rotado por 3 empresas del listado FAE.',t:['Extrovertido/a','Virtual (Meet)','Noches'],s:[9]},
  {n:'Ricardo Lozano',i:'RL',b:'Redes de contacto en empresas aliadas.',t:['Directo al Punto','Presencial (U)','Tiene Tiempo'],s:[9]},
  {n:'Paola Fuentes',i:'PF',b:'Prepara CVs y entrevistas para prácticas.',t:['Paciente','Presencial (U)','Fines de Semana'],s:[8,9]}
];
 
const CINCO_AS = [
  {id:'A1',lb:'Awareness',cat:'01 · Reconocimiento',title:'AWARENESS — HACEMOS RUIDO',desc:'Activaciones en El Solar y campañas digitales para instalar "Parche FAE" en la mente de cada estudiante desde el primer día del semestre.'},
  {id:'A2',lb:'Appeal',cat:'02 · Atracción',title:'APPEAL — LA SOLUCIÓN EMPÁTICA',desc:'Estudiantes que superaron materias críticas comparten tips reales. El gancho: autenticidad de pares que vivieron lo mismo.'},
  {id:'A3',lb:'Ask',cat:'03 · Búsqueda',title:'ASK — CONSULTA RÁPIDA Y CENTRALIZADA',desc:'Un solo punto de acceso para encontrar monitores por materia, semestre y disponibilidad. Sin formularios eternos.'},
  {id:'A4',lb:'Act',cat:'04 · Acción',title:'ACT — AGENDA, APRENDE, AVANZA',desc:'Tarifas estandarizadas y transparentes. El apoyo mutuo primero, la transacción como herramienta.'},
  {id:'A5',lb:'Advocate',cat:'05 · Recomendación',title:'ADVOCATE — LA COMUNIDAD HABLA',desc:'Comunidad orgánica que crece por resultados: promedios mejorados y logros reales compartidos.'}
];
 
const CAL = {
  1: {months:[
    {n:'Enero 2026',y:2026,m:0,ev:{19:'induccion',20:'induccion',21:'induccion',22:'induccion',23:'induccion',26:'inicio',27:'inicio',28:'inicio',29:'inicio',30:'inicio',31:'inicio'}},
    {n:'Febrero 2026',y:2026,m:1,ev:{}},
    {n:'Marzo 2026',y:2026,m:2,ev:{3:'corte',22:'corte',23:'corte'}},
    {n:'Abril 2026',y:2026,m:3,ev:{7:'corte'}},
    {n:'Mayo 2026',y:2026,m:4,ev:{22:'corte',23:'corte',24:'fin',25:'fin',26:'fin',27:'fin',28:'fin',29:'fin',30:'fin'}},
    {n:'Junio 2026',y:2026,m:5,ev:{1:'examen',2:'examen',3:'examen',4:'examen',5:'examen'}}
  ]},
  2: {months:[
    {n:'Julio 2026',y:2026,m:6,ev:{20:'inicio',21:'inicio',22:'inicio',23:'inicio',24:'inicio',25:'inicio',26:'inicio',27:'inicio',28:'inicio',29:'inicio',30:'inicio',31:'inicio'}},
    {n:'Agosto 2026',y:2026,m:7,ev:{25:'corte'}},
    {n:'Septiembre 2026',y:2026,m:8,ev:{29:'corte'}},
    {n:'Octubre 2026',y:2026,m:9,ev:{}},
    {n:'Noviembre 2026',y:2026,m:10,ev:{13:'corte',17:'fin',18:'fin',19:'fin',20:'fin',21:'fin',22:'examen',23:'examen',24:'examen',25:'examen',26:'examen',27:'examen',28:'examen'}},
    {n:'Diciembre 2026',y:2026,m:11,ev:{}}
  ]}
};
 
const ALERTS = {
  1:[
    {date:'19–24 Ene',type:'induccion',title:'Semana de Inducción',desc:'Regístrate en Parche FAE y explora los monitores disponibles para tu semestre.'},
    {date:'3 Mar',type:'corte',title:'Corte 1 — ¡Pide tu Parche!',desc:'Primer parcial del semestre. Si tienes dudas acumuladas, este es el momento de actuar.'},
    {date:'7 Abr',type:'corte',title:'Corte 2 — Alerta Parche',desc:'Segundo corte. Refuerza los temas que más te costaron en el primero.'},
    {date:'22–23 May',type:'corte',title:'Corte 3 — Recta Final',desc:'Última oportunidad antes de finales. Máxima intensidad de monitorías.'},
    {date:'1–5 Jun',type:'examen',title:'Exámenes Finales',desc:'El parche ya debe estar activo y consolidado para esta semana.'}
  ],
  2:[
    {date:'20 Jul',type:'inicio',title:'Inicio Clases Sem 2',desc:'Empieza con el pie derecho: busca tu monitor desde el primer día.'},
    {date:'25 Ago',type:'corte',title:'Corte 1 — ¡Pide tu Parche!',desc:'Primer corte del segundo semestre. No lo dejes para el último momento.'},
    {date:'29 Sep',type:'corte',title:'Corte 2 — Alerta Parche',desc:'Evalúa tu situación y refuerza donde más necesitas apoyo.'},
    {date:'17–21 Nov',type:'fin',title:'Fin de Clases',desc:'Consolida todo el material antes de los exámenes finales.'},
    {date:'22–28 Nov',type:'examen',title:'Exámenes Finales',desc:'Sprint final. El parche marca la diferencia en estas semanas.'}
  ]
};
 
const AL_COLORS = {induccion:'#00C864',inicio:'#7EA8FF',corte:'#FF6B2B',fin:'#FBBF24',examen:'#00E5A0'};
 
const DEF_MATS = [
  {n:'Resumen_Capítulo_1.pdf',s:'12 KB'},
  {n:'Ejercicios_Resueltos.docx',s:'38 KB'},
  {n:'Guía_Parcial.pdf',s:'24 KB'}
];
 
 
const PRESET_CONV = {
  subject: 'Pensamiento Estratégico',
  monitorName: 'Andrés Montoya',
  messages: [
    {
      sender: '__monitor__',
      text: 'Hola, ¿cómo te encuentras? ¡Espero que estés muy bien! 😊\n\nMi nombre es Andrés Montoya y voy a ser tu monitor en la materia de Pensamiento Estratégico aquí en Parche FAE.\n\nCuéntame, ¿qué duda tienes o qué tema te gustaría reforzar hoy?'
    },
    {
      sender: '__user__',
      text: 'Vale, ¿según Daniel Kahneman de qué trata el sistema 1 y el sistema 2?'
    },
    {
      sender: '__monitor__',
      text: '¡Claro! Te explico 😊\n\nEn Pensamiento Estratégico, el "Sistema 1" y el "Sistema 2" son conceptos propuestos por el psicólogo Daniel Kahneman para entender cómo pensamos y tomamos decisiones.\n\n🔹 Sistema 1:\nEs rápido, automático e intuitivo. Funciona casi sin esfuerzo. Por ejemplo: cuando respondes una pregunta fácil inmediatamente o reconoces una cara conocida.\n\n🔹 Sistema 2:\nEs más lento, analítico y requiere concentración. Se usa cuando debes resolver un problema matemático, analizar una estrategia o tomar una decisión importante.\n\n📌 En términos estratégicos, muchas veces las personas toman decisiones usando el Sistema 1 porque es más rápido, pero eso puede generar errores o sesgos. Por eso, en administración y estrategia, es importante aprender a activar el Sistema 2 para analizar mejor las situaciones antes de decidir.\n\n¿Quieres que te dé un ejemplo aplicado a una empresa o a la vida cotidiana para entenderlo mejor?'
    },
    {
      sender: '__user__',
      text: 'Desarrolla el ejemplo.'
    },
    {
      sender: '__monitor__',
      text: '¡Con gusto! Aquí va un ejemplo aplicado a una empresa real:\n\n🏢 Caso: Un gerente de ventas en una empresa colombiana\n\nImagina que eres gerente de ventas y un cliente frecuente te llama pidiendo un descuento del 30% en un pedido grande. Tienes dos opciones de reacción:\n\n⚡ Reacción con Sistema 1 (rápido e intuitivo):\n"Este cliente siempre nos compra, es de confianza, démosle el descuento ya." — Decides en segundos basándote en la relación previa y el instinto. El problema: quizás ese descuento no es rentable para la empresa en este momento o abre la puerta para que otros clientes lo pidan también.\n\n🧠 Reacción con Sistema 2 (analítico y deliberado):\nTe tomas un momento, revisas los márgenes de ese producto, consultas con el área financiera, evalúas el impacto en otros clientes y propones un descuento del 15% con condiciones claras. Decisión más sólida, aunque tomó más tiempo.\n\n📊 ¿Qué nos enseña esto en estrategia?\nLas organizaciones exitosas diseñan procesos (como comités de aprobación, checklists o análisis de datos) precisamente para forzar el uso del Sistema 2 antes de tomar decisiones importantes, evitando que el instinto lleve a errores costosos.\n\n¿Quieres explorar cómo esto se relaciona con los sesgos cognitivos que vemos en el curso?'
    }
  ]
};
 
const AI_LINES = [
  '¡Claro! Vamos paso a paso. ¿Con qué parte específica tienes más dificultad?',
  'Ese concepto es clave. Te doy un ejemplo práctico que usé cuando tomé esa materia.',
  'Muchos compañeros tienen el mismo problema al inicio. La clave está en entender la lógica antes de memorizar.',
  '¿Tienes los apuntes del profesor a mano? Así lo vemos con la estructura que él maneja.',
  'Para ese parcial te recomiendo enfocarte en los tres temas que más pesan. ¿Sabes cuáles son?',
  'Ese error es muy común. No te preocupes, te explico la diferencia con un caso real del sector.',
  'Muy bien, vamos a hacer un plan de repaso. ¿Cuántos días tienes antes del corte?',
  'Ese tema lo dominas mejor practicando que leyendo. ¿Empezamos con un ejercicio resuelto?',
  'Toma nota: siempre entiende el "por qué" antes del "cómo". ¿Quieres que lo vemos así?',
  'Con gusto te ayudo. ¿Hay algún tema que el profesor haya enfatizado esta semana?'
];
 
// ─── STATE ───
const ST = {
  user:'', role:'', sem:1, selSub:'',
  sessions:[], activeChatId:null, calSem:1, calView:'grid', pipeIdx:0
};
 
// ─── PERSISTENCE ───
const SK = 'parche_fae_v6';
const UK = 'parche_fae_users_v2';
 
function save() {
  try { localStorage.setItem(SK, JSON.stringify({user:ST.user,role:ST.role,sessions:ST.sessions})); } catch(e){}
  if (ST.user) {
    let u = getRecent();
    u = u.filter(x=>x.n!==ST.user);
    u.unshift({n:ST.user,r:ST.role,ts:Date.now()});
    u = u.slice(0,5);
    try { localStorage.setItem(UK, JSON.stringify(u)); } catch(e){}
  }
}
 
function loadUser(name) {
  try {
    const d = JSON.parse(localStorage.getItem(SK)||'{}');
    return (d.user===name) ? (d.sessions||[]) : [];
  } catch(e){ return []; }
}
 
function getRecent() {
  try { return JSON.parse(localStorage.getItem(UK)||'[]'); } catch(e){ return []; }
}
 
// ─── NAV ───
function goPage(id) {
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  const el = document.getElementById(id);
  el.classList.add('active');
  el.style.display = '';
}
 
function logoClick() { ST.user ? goPage('pg-dash') : goPage('pg-login'); }
 
function updateNav() {
  const auth = document.getElementById('nav-auth');
  const lb = document.getElementById('nav-loginbtn');
  if (ST.user) {
    auth.classList.add('show'); lb.classList.remove('show');
    const ini = ST.user.substring(0,2).toUpperCase();
    const bg = avBg(ST.user);
    el('nav-av').textContent = ini; el('nav-av').style.background = bg;
    el('nav-name').textContent = ST.user;
    el('nav-role').textContent = ST.role==='monitor' ? 'Monitor' : 'Aprendiz';
    el('pd-av').textContent = ini; el('pd-av').style.background = bg;
    el('pd-name').textContent = ST.user;
    el('pd-role').textContent = ST.role==='monitor' ? 'Monitor Académico' : 'Aprendiz';
  } else {
    auth.classList.remove('show'); lb.classList.add('show');
  }
}
 
// ─── LOGIN ───
function initLogin() {
  const recent = getRecent();
  const wrap = el('recent-wrap');
  const list = el('recent-list');
  if (recent.length) {
    wrap.style.display = 'block';
    list.innerHTML = recent.map(u=>`
      <div class="recent-item" onclick="quickLogin('${u.n.replace(/'/g,"\'")}','${u.r}')">
        <div class="rec-av" style="background:${avBg(u.n)}">${u.n.substring(0,2).toUpperCase()}</div>
        <div class="rec-info">
          <div class="rec-name">${u.n}</div>
          <div class="rec-role">${u.r==='monitor'?'Monitor':'Aprendiz'}</div>
        </div>
        <div class="rec-arr"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polyline points="9 18 15 12 9 6"/></svg></div>
      </div>
    `).join('');
  } else {
    wrap.style.display = 'none';
  }
}
 
function quickLogin(name, role) {
  ST.user = name; ST.role = role;
  ST.sessions = loadUser(name);
  updateNav();
  // Still require role confirmation even for returning users
  // Pre-select their previous role but let them confirm
  if(role) {
    pickRole(role);
  }
  goPage('pg-role');
  toast('¡Bienvenido de vuelta, '+name.split(' ')[0]+'! Confirma tu rol para continuar.');
}
 
function doLogin() {
  const u = el('inp-u').value.trim();
  const p = el('inp-p').value;
  el('inp-u').classList.remove('err'); el('inp-p').classList.remove('err');
  if (!u || u.length<2) { el('inp-u').classList.add('err'); return; }
  if (!p) { el('inp-p').classList.add('err'); return; }
  ST.user = u; ST.sessions = loadUser(u); ST.role = '';
  updateNav(); goPage('pg-role');
}
 
function goToPres() {
  save(); goPage('pg-pres');
  buildPipeline(); buildCalendar();
}
 
function doLogout() {
  closePD(); ST.user=''; ST.role=''; ST.sessions=[];
  updateNav(); goPage('pg-login'); initLogin();
}
 
// ─── ROLE ───
function pickRole(r) {
  ST.role = r;
  ['aprendiz','monitor'].forEach(x => {
    const cid = x==='aprendiz'?'rc-a':'rc-m';
    const chk = x==='aprendiz'?'chk-a':'chk-m';
    document.getElementById(cid).classList.toggle('sel', x===r);
  });
  el('btn-role-cont').disabled = false;
  updateNav();
}
 
// ─── PRES TABS ───
function showPT(tab, btn) {
  document.querySelectorAll('.psec').forEach(s=>s.classList.remove('on'));
  document.querySelectorAll('.pres-tab-row .pill').forEach(b=>{b.classList.remove('p-orange','p-green');});
  el('pt-'+tab).classList.add('on');
  btn.classList.add('p-orange');
}
 
// ─── PIPELINE ───
function buildPipeline() {
  const row = el('pipe-row');
  row.innerHTML = CINCO_AS.map((a,i)=>`
    <div class="pipe-node" onclick="selPipe(${i})">
      <div class="pipe-circle ${i===0?'curr':''}" id="pc-${i}">${a.id}</div>
      <div class="pipe-lbl">${a.lb}</div>
    </div>
    ${i<CINCO_AS.length-1?`<div class="pipe-conn"><div class="pipe-fill" id="pf-${i}"></div></div>`:''}
  `).join('');
  selPipe(0);
}
 
function selPipe(idx) {
  ST.pipeIdx = idx;
  CINCO_AS.forEach((_,i)=>{
    const c = el('pc-'+i);
    if(c) c.className='pipe-circle '+(i<idx?'done':i===idx?'curr':'');
    const f = el('pf-'+i);
    if(f) f.className='pipe-fill '+(i<idx?'done':'');
  });
  const a = CINCO_AS[idx];
  el('pipe-det-wrap').innerHTML = `
    <div class="pipe-detail-card">
      <div class="pipe-detail-cat">${a.cat}</div>
      <h3>${a.title}</h3>
      <p>${a.desc}</p>
    </div>`;
}
 
// ─── CALENDAR ───
function buildCalendar() { renderCalGrid(); renderCalList(); }
 
function switchCalSem(sem, btn) {
  ST.calSem = sem;
  document.querySelectorAll('#pt-cal .pill').forEach(b=>{b.classList.remove('p-orange','p-green');});
  btn.classList.add('p-orange');
  renderCalGrid(); renderCalList();
}
 
function switchCalView(view, btn) {
  ST.calView = view;
  el('cal-grid-wrap').style.display = view==='grid'?'':'none';
  el('cal-list-wrap').style.display = view==='list'?'':'none';
  ['cv-grid-btn','cv-list-btn'].forEach(id=>el(id).classList.remove('p-orange','p-green'));
  btn.classList.add('p-orange');
}
 
function renderCalGrid() {
  const data = CAL[ST.calSem];
  const dow = ['DO','LU','MA','MI','JU','VI','SÁ'];
  el('cal-grid-wrap').innerHTML = `<div class="cal-grid">${data.months.map(mo=>{
    const fd = new Date(mo.y,mo.m,1).getDay();
    const dim = new Date(mo.y,mo.m+1,0).getDate();
    return `<div class="cal-month-box">
      <div class="cal-month-title">${mo.n}</div>
      <div class="cal-dow">${dow.map(d=>`<span>${d}</span>`).join('')}</div>
      <div class="cal-days">
        ${Array(fd).fill('<div></div>').join('')}
        ${Array.from({length:dim},(_,i)=>{const d=i+1;const ev=mo.ev[d]||'';return `<div class="cd${ev?' '+ev:''}">${d}</div>`;}).join('')}
      </div>
    </div>`;
  }).join('')}</div>`;
}
 
function renderCalList() {
  const alerts = ALERTS[ST.calSem];
  el('cal-list-wrap').innerHTML = `<div class="alert-tl">${alerts.map(a=>`
    <div class="al-row">
      <div class="al-dot-col">
        <div class="al-dot" style="background:${AL_COLORS[a.type]||'#888'}"></div>
        <div class="al-line" style="background:${AL_COLORS[a.type]||'#888'}"></div>
      </div>
      <div class="al-body">
        <div class="al-date" style="color:${AL_COLORS[a.type]||'#888'}">${a.date}</div>
        <div class="al-title">${a.title}</div>
        <div class="al-desc">${a.desc}</div>
      </div>
    </div>`).join('')}</div>`;
}
 
// ─── DASHBOARD ───
function renderDash() {
  el('dn').textContent = ST.user;
  el('drl').textContent = ST.role==='monitor'?'Monitor Académico · FAE':'Aprendiz · FAE';
  updateQS(); renderSemTabs(1); showView('v-subs');
}
 
function updateQS() {
  const mine = ST.sessions.filter(s=>s.u1===ST.user||s.u2===ST.user);
  el('qs-n').textContent = mine.length;
  const dot = el('notif-dot');
  if(dot) dot.classList.toggle('show', mine.length>0);
}
 
function renderSemTabs(n) {
  ST.sem = n;
  const strip = el('sem-strip');
  strip.innerHTML = Object.keys(PENSUM).map(s=>`
    <button class="sem-btn${s==n?' on':''}" onclick="renderSemTabs(${s})">${s==9?'PRÁCTICAS':'SEM '+s}</button>
  `).join('');
  renderSubGrid();
}
 
function renderSubGrid() {
  const subs = PENSUM[ST.sem]||[];
  el('sub-grid').innerHTML = subs.map(sub=>`
    <div class="sub-card" onclick="openSub('${sub.replace(/'/g,"\'")}')" title="${sub}">
      <h4>${sub}</h4>
      <div class="sc-foot">
        <span class="sc-cta">${ST.role==='monitor'?'Ver alumnos':'Ver monitores'}</span>
        <div class="sc-arrow"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polyline points="9 18 15 12 9 6"/></svg></div>
      </div>
    </div>`).join('');
}
 
function showView(id) {
  ['v-subs','v-filter','v-cast','v-det'].forEach(v=>{
    const x=el(v); if(x) x.style.display=(v===id?'':'none');
  });
}
 
function openSub(sub) {
  ST.selSub = sub;
  if (ST.role==='monitor') { renderCast(); showView('v-cast'); }
  else { showView('v-filter'); }
}
 
function applyFilters() { renderCast(); showView('v-cast'); }
 
function hash(s){return Math.abs(Array.from(s).reduce((h,c)=>((h<<5)-h)+c.charCodeAt(0),0));}
function shuffle(arr,seed){const a=[...arr];for(let i=a.length-1;i>0;i--){const j=(seed+i*7)%(i+1);[a[i],a[j]]=[a[j],a[i]];}return a;}
 
function getMonitors(sub) {
  const seed = hash(sub);
  let pool = MONITORS.filter(m=>m.s.includes(Number(ST.sem)));
  if(pool.length<4) pool = MONITORS;
  return shuffle(pool,seed).slice(0,4).map((m,i)=>({
    ...m, bio:`${m.b} Especialista en ${sub}.`,
    score:(4.5+((seed+i)%5)*0.1).toFixed(1), stars:4+((seed+i)%2)
  }));
}
 
function renderCast() {
  const selT = Array.from(document.querySelectorAll('.ftag.on')).map(e=>e.textContent.trim());
  const mons = getMonitors(ST.selSub);
  const sorted = [...mons].sort((a,b)=>{
    const mA=a.t.some(t=>selT.includes(t))?-1:1;
    const mB=b.t.some(t=>selT.includes(t))?-1:1;
    return mA-mB;
  });
  el('cast-title').textContent = (ST.sem==9?'Práctica: ':'')+ST.selSub;
  el('cast-list').innerHTML = sorted.map(m=>{
    const ideal = m.t.some(t=>selT.includes(t))&&selT.length>0;
    return `<div class="mon-card${ideal?' ideal':''}">
      <div style="display:flex;gap:14px;align-items:flex-start;flex-wrap:wrap">
        <div class="mon-av" style="background:${avBg(m.n)}">${m.i}</div>
        <div style="flex:1;min-width:0">
          <div style="display:flex;align-items:center;gap:8px;flex-wrap:wrap;margin-bottom:5px">
            <div class="mon-name">${m.n}</div>
            ${ideal?'<div class="badge badge-green">Tu Parche Ideal</div>':''}
          </div>
          <div class="mon-bio">"${m.bio}"</div>
          <div style="display:flex;flex-wrap:wrap;gap:5px;margin-top:9px">
            ${m.t.map(t=>`<div class="badge badge-muted">${t}</div>`).join('')}
          </div>
          <div style="display:flex;align-items:center;gap:10px;margin-top:8px">
            <span class="mon-score">Score ${m.score}</span>
            <span class="stars">${'★'.repeat(m.stars)}${'☆'.repeat(5-m.stars)}</span>
          </div>
        </div>
        <div style="display:flex;flex-direction:column;gap:7px;align-items:flex-end">
          <button class="btn btn-green btn-sm" onclick="startChat('${m.n.replace(/'/g,"\'")}')" style="white-space:nowrap">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/></svg>
            Pedir Monitoría
          </button>
          <button class="btn btn-ghost btn-sm" onclick="openDet('${ST.selSub.replace(/'/g,"\'")}')">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/></svg>
            Ver materiales
          </button>
        </div>
      </div>
    </div>`;
  }).join('');
}
 
function openDet(sub) {
  ST.selSub = sub;
  el('det-title').textContent = sub;
  el('mat-list').innerHTML = DEF_MATS.map(f=>`
    <div class="mat-row">
      <div class="mat-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M13 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V9z"/><polyline points="13 2 13 9 20 9"/></svg></div>
      <div style="flex:1;min-width:0"><div class="mat-name">${f.n}</div><div class="mat-size">${f.s}</div></div>
      <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="var(--green)" stroke-width="2"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
    </div>`).join('');
  el('upload-list').innerHTML = '';
  showView('v-det');
}
 
function handleUpload(event) {
  const files = Array.from(event.target.files);
  const matList = el('mat-list');
  const upList = el('upload-list');
  files.forEach(f=>{
    const rowH = `<div class="mat-row" style="border-color:rgba(0,229,160,0.2);background:rgba(0,229,160,0.04)">
      <div class="mat-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M13 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V9z"/><polyline points="13 2 13 9 20 9"/></svg></div>
      <div style="flex:1;min-width:0"><div class="mat-name">${f.name}</div><div class="mat-size">${(f.size/1024).toFixed(1)} KB</div></div>
      <span style="font-size:0.56rem;font-weight:700;color:var(--green);text-transform:uppercase">✓ Subido</span>
    </div>`;
    [matList,upList].forEach(c=>{const d=document.createElement('div');d.innerHTML=rowH;c&&c.appendChild(d.firstElementChild);});
  });
  toast('Archivo subido correctamente');
  event.target.value='';
}
 
// ─── DRAG & DROP ───
document.addEventListener('DOMContentLoaded',()=>{
  const z=el('upload-zone');
  if(z){
    z.addEventListener('dragover',e=>{e.preventDefault();z.classList.add('dov');});
    z.addEventListener('dragleave',()=>z.classList.remove('dov'));
    z.addEventListener('drop',e=>{e.preventDefault();z.classList.remove('dov');if(e.dataTransfer.files.length)handleUpload({target:{files:e.dataTransfer.files}});});
  }
  el('inp-p').addEventListener('keydown',e=>{if(e.key==='Enter')doLogin();});
  el('inp-u').addEventListener('keydown',e=>{if(e.key==='Enter')el('inp-p').focus();});
  el('chat-inp').addEventListener('keydown',e=>{if(e.key==='Enter')sendMsg();});
  initLogin(); updateNav();
});
 
// ─── PROFILE DROPDOWN ───
function togglePD() { el('pd').classList.toggle('show'); if(el('pd').classList.contains('show'))renderPdSess(); }
function closePD() { el('pd').classList.remove('show'); }
 
document.addEventListener('click',e=>{
  const pd=el('pd');
  if(pd.classList.contains('show')&&!pd.contains(e.target)&&!e.target.closest('.nav-user-chip'))closePD();
});
 
function renderPdSess() {
  const mine = ST.sessions.filter(s=>s.u1===ST.user||s.u2===ST.user);
  const c = el('pd-sess');
  if(!mine.length){c.innerHTML='<div class="empty-st"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/></svg><p>Sin monitorías activas</p></div>';return;}
  c.innerHTML = mine.map(s=>{
    const par=s.u1===ST.user?s.u2:s.u1;
    return `<div class="sess-mini">
      <div class="sm-info"><div class="sm-sub">${s.subject}</div><div class="sm-par">Con ${par}</div></div>
      <div class="sm-acts">
        <button class="sm-btn sm-chat" onclick="closePD();openChat(${s.id})" title="Chat"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/></svg></button>
        <button class="sm-btn sm-del" onclick="delSess(${s.id})" title="Eliminar"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="3 6 5 6 21 6"/><path d="M19 6l-1 14H6L5 6"/></svg></button>
      </div>
    </div>`;
  }).join('');
}
 
function calcG() {
  const g=id=>parseFloat(el(id).value)||0;
  const g1=g('g1'),g2=g('g2'),g3=g('g3'),raw=el('g4').value;
  const lbl=el('gr-lbl'),val=el('gr-val'),fill=el('gr-fill');
  if(raw!==''){
    const g4=parseFloat(raw)||0,avg=(g1+g2+g3+g4)/4;
    lbl.textContent='Promedio Final Proyectado';
    val.textContent=avg.toFixed(2);
    val.style.color=avg>=3?'var(--green)':'#ef4444';
    fill.style.width=Math.min(100,(avg/5)*100)+'%';
  } else {
    const need=12-(g1+g2+g3);
    lbl.textContent='Necesitas en C4 para pasar (3.0)';
    if(need<=0){val.textContent='✓ PASASTE';val.style.color='var(--green)';fill.style.width='100%';}
    else if(need>5){val.textContent=need.toFixed(1);val.style.color='#ef4444';fill.style.width='20%';}
    else{val.textContent=need.toFixed(1);val.style.color=var_muted2;fill.style.width=Math.min(100,((5-need)/5)*100)+'%';}
  }
}
const var_muted2 = '#8898B0';
 
// ─── INBOX ───
function toggleInbox() {
  el('inbox-modal').classList.toggle('show');
  if(el('inbox-modal').classList.contains('show'))renderInbox();
}
function renderInbox() {
  const mine=ST.sessions.filter(s=>s.u1===ST.user||s.u2===ST.user);
  const c=el('inbox-body');
  if(!mine.length){c.innerHTML='<div class="empty-st"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/></svg><p>Aún no hay parches activos</p></div>';return;}
  c.innerHTML=mine.map(s=>{
    const par=s.u1===ST.user?s.u2:s.u1;
    const last=s.messages.length?s.messages[s.messages.length-1].text.substring(0,55)+'…':'Nueva conversación';
    return `<div class="ib-item" onclick="toggleInbox();openChat(${s.id})">
      <div class="ib-av" style="background:${avBg(par)}">${par.substring(0,2).toUpperCase()}</div>
      <div style="flex:1;min-width:0">
        <div class="ib-name">${par}</div>
        <div class="ib-sub">${s.subject}</div>
        <div class="ib-prev">${last}</div>
      </div>
      <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="var(--muted)" stroke-width="2.5"><polyline points="9 18 15 12 9 6"/></svg>
    </div>`;
  }).join('');
}
 
// ─── CHAT ───
function startChat(name) {
  const sub=ST.selSub;
  let s=ST.sessions.find(x=>(x.u1===ST.user||x.u2===ST.user)&&(x.u1===name||x.u2===name)&&x.subject===sub);
  if(!s){
    const id=Date.now();
    let msgs=[];
    // Load preset conversation if subject and monitor match
    if(sub===PRESET_CONV.subject && name===PRESET_CONV.monitorName){
      msgs=PRESET_CONV.messages.map(m=>({
        sender: m.sender==='__monitor__' ? name : ST.user,
        text: m.text
      }));
    }
    s={id,u1:ST.user,u2:name,subject:sub,messages:msgs};
    ST.sessions.push(s);save();updateQS();
    toast('Monitoría creada con '+name.split(' ')[0]);
  }
  openChat(s.id);
}
 
function openChat(id) {
  ST.activeChatId=id;
  const s=ST.sessions.find(x=>x.id===id);if(!s)return;
  const par=s.u1===ST.user?s.u2:s.u1;
  const av=el('chat-av');av.textContent=par.substring(0,2).toUpperCase();av.style.background=avBg(par);
  el('chat-nm').textContent=par;el('chat-sub').textContent=s.subject;
  renderMsgs();el('chat-modal').classList.add('show');
  setTimeout(()=>el('chat-inp').focus(),100);
  if(!s.messages.length){setTimeout(()=>aiGreet(id),700);}else{setTimeout(()=>{const c=el('chat-msgs');if(c)c.scrollTop=c.scrollHeight;},150);}
}
 
function closeChat(){el('chat-modal').classList.remove('show');ST.activeChatId=null;}
 
function renderMsgs() {
  const s=ST.sessions.find(x=>x.id===ST.activeChatId);if(!s)return;
  const par=s.u1===ST.user?s.u2:s.u1;
  const c=el('chat-msgs');
  c.innerHTML=s.messages.map(m=>`
    <div class="bubble ${m.sender===ST.user?'mine':'theirs'}">
      <div class="bubble-from">${m.sender===ST.user?'Tú':par}</div>
      <div style="white-space:pre-wrap">${m.text}</div>
    </div>`).join('');
  c.scrollTop=c.scrollHeight;
}
 
async function sendMsg() {
  const inp=el('chat-inp');const text=inp.value.trim();
  if(!text||!ST.activeChatId)return;
  const s=ST.sessions.find(x=>x.id===ST.activeChatId);
  s.messages.push({sender:ST.user,text});inp.value='';
  inp.disabled=true;el('chat-modal').querySelector('.chat-send').disabled=true;
  renderMsgs();save();
  await aiReply(ST.activeChatId);
  inp.disabled=false;el('chat-modal').querySelector('.chat-send').disabled=false;inp.focus();
}
 
function showTyp(v){el('typing-row').style.display=v?'':'none';if(v)el('chat-msgs').scrollTop=99999;}
 
async function aiGreet(chatId) {
  const s=ST.sessions.find(x=>x.id===chatId);if(!s||ST.activeChatId!==chatId)return;
  const par=s.u1===ST.user?s.u2:s.u1;
  showTyp(true);await sleep(800+Math.random()*600);showTyp(false);
  const msg=`¡Hola! Soy ${par}, tu monitor en ${s.subject}. Estoy aquí para ayudarte a entender los temas y prepararte para los cortes. ¿Por dónde empezamos?`;
  s.messages.push({sender:par,text:msg});save();
  if(ST.activeChatId===chatId)renderMsgs();
}
 
async function aiReply(chatId) {
  const s=ST.sessions.find(x=>x.id===chatId);if(!s)return;
  const par=s.u1===ST.user?s.u2:s.u1;
  showTyp(true);await sleep(900+Math.random()*1100);showTyp(false);
  const msg=AI_LINES[Math.floor(Math.random()*AI_LINES.length)];
  s.messages.push({sender:par,text:msg});save();
  if(ST.activeChatId===chatId)renderMsgs();
}
 
function delSess(id) {
  ST.sessions=ST.sessions.filter(s=>s.id!==id);
  if(ST.activeChatId===id)closeChat();
  save();updateQS();renderPdSess();renderInbox();toast('Monitoría eliminada');
}
 
// ─── TOAST ───
let toastT=null;
function toast(msg) {
  el('toast-msg').textContent=msg;el('toast').classList.add('show');
  clearTimeout(toastT);toastT=setTimeout(()=>el('toast').classList.remove('show'),3000);
}
 
// ─── UTILS ───
function sleep(ms){return new Promise(r=>setTimeout(r,ms));}
function el(id){return document.getElementById(id);}
const AV_BKGS=['linear-gradient(135deg,#00A86B,#004D30)','linear-gradient(135deg,#FF6B2B,#B84D1A)','linear-gradient(135deg,#3B7FFF,#1A4DA8)','linear-gradient(135deg,#F59E0B,#B45309)','linear-gradient(135deg,#8B5CF6,#5B21B6)','linear-gradient(135deg,#06B6D4,#0284C7)'];
function avBg(name){return AV_BKGS[Math.abs(Array.from(name||'?').reduce((h,c)=>((h<<5)-h)+c.charCodeAt(0),0))%AV_BKGS.length];}
</script>
</body>
</html>
