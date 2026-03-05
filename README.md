<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>WHITEGREENZONE</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=Outfit:wght@300;400;500;600;700&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>

<style>
/* ================================================================
   DESIGN TOKENS — Black & White Minimal Theme
================================================================ */
:root {
  /* Backgrounds */
  --bg:        #000000;
  --bg2:       #0a0a0a;
  --surface:   #111111;
  --surface2:  #1a1a1a;
  --surface3:  #222222;

  /* Borders */
  --border:    #1f1f1f;
  --border2:   #2e2e2e;
  --border3:   #3a3a3a;

  /* Text */
  --text:      #f5f5f5;
  --text-muted:#888888;
  --text-dim:  #3a3a3a;

  /* Accents — white-based */
  --accent:       #ffffff;
  --accent-sub:   rgba(255,255,255,0.07);
  --accent-glow:  rgba(255,255,255,0.12);

  /* Status */
  --danger:    #ef4444;
  --success:   #22c55e;
  --warning:   #f59e0b;

  /* Platform colors kept for recognition */
  --tiktok:    #00f2ea;
  --instagram: #f76a8a;
  --facebook:  #6a9bff;
  --youtube:   #ff6464;

  --r:    10px;
  --r-lg: 16px;
  --font-d: 'Syne', sans-serif;
  --font-b: 'Outfit', sans-serif;
  --font-m: 'DM Mono', monospace;
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; }

body {
  background: var(--bg);
  color: var(--text);
  font-family: var(--font-b);
  font-size: 15px;
  line-height: 1.6;
  min-height: 100vh;
  overflow-x: hidden;
}

/* Subtle dot-grid texture */
body::before {
  content: '';
  position: fixed; inset: 0;
  background-image: radial-gradient(rgba(255,255,255,0.04) 1px, transparent 1px);
  background-size: 32px 32px;
  pointer-events: none; z-index: 0;
}

::-webkit-scrollbar { width: 4px; height: 4px; }
::-webkit-scrollbar-track { background: var(--bg); }
::-webkit-scrollbar-thumb { background: var(--border3); border-radius: 4px; }
::-webkit-scrollbar-thumb:hover { background: #555; }

/* ================================================================
   SHARED INPUTS & BUTTONS
================================================================ */
.field-label {
  display: block; font-size: 0.68rem; font-weight: 600;
  letter-spacing: 0.1em; text-transform: uppercase;
  color: var(--text-muted); margin-bottom: 0.45rem;
}

.field-input {
  width: 100%;
  background: var(--bg2); border: 1px solid var(--border2);
  border-radius: var(--r); color: var(--text);
  font-family: var(--font-b); font-size: 0.88rem;
  padding: 0.72rem 1rem; outline: none;
  transition: border-color 0.2s, box-shadow 0.2s;
  -webkit-appearance: none;
}
.field-input:focus { border-color: #555; box-shadow: 0 0 0 3px rgba(255,255,255,0.06); }
.field-input.sm { padding: 0.56rem 0.85rem; font-size: 0.83rem; }
select.field-input option { background: var(--surface2); }
textarea.field-input { resize: vertical; font-family: var(--font-b); }
.form-group { display: flex; flex-direction: column; gap: 0.42rem; }
.form-grid  { display: grid; grid-template-columns: 1fr 1fr; gap: 1rem; }
.form-grid .full { grid-column: 1 / -1; }

/* Primary — white button, black text */
.btn-primary {
  background: #ffffff; color: #000000;
  font-family: var(--font-d); font-size: 0.95rem; font-weight: 700;
  letter-spacing: 0.04em; border: none; border-radius: var(--r);
  padding: 0.9rem; cursor: pointer; width: 100%;
  transition: background 0.2s, transform 0.15s, box-shadow 0.2s;
  box-shadow: 0 2px 16px rgba(255,255,255,0.08);
}
.btn-primary:hover { background: #e8e8e8; box-shadow: 0 4px 24px rgba(255,255,255,0.15); }
.btn-primary:active { transform: scale(0.98); }

/* Add button */
.btn-add {
  background: var(--accent); color: #000;
  font-family: var(--font-b); font-size: 0.83rem; font-weight: 700;
  border: none; border-radius: var(--r); padding: 0.56rem 1.15rem;
  cursor: pointer; white-space: nowrap;
  transition: background 0.2s, box-shadow 0.2s, transform 0.15s;
  display: inline-flex; align-items: center; gap: 0.3rem;
}
.btn-add:hover { background: #ddd; transform: translateY(-1px); box-shadow: 0 4px 16px rgba(255,255,255,0.1); }

/* Ghost button */
.btn-ghost {
  background: transparent; border: 1px solid var(--border2); color: var(--text-muted);
  font-family: var(--font-b); font-size: 0.83rem; font-weight: 600;
  border-radius: var(--r); padding: 0.56rem 1.1rem; cursor: pointer; transition: 0.2s;
}
.btn-ghost:hover { border-color: var(--border3); color: var(--text); }

/* Save button */
.btn-save {
  background: var(--accent); border: none; color: #000;
  font-family: var(--font-b); font-size: 0.875rem; font-weight: 700;
  border-radius: var(--r); padding: 0.65rem 1.5rem; cursor: pointer; transition: 0.2s;
}
.btn-save:hover { background: #ddd; }

/* Sort button */
.btn-sort {
  background: var(--surface); border: 1px solid var(--border2);
  color: var(--text-muted); font-family: var(--font-b);
  font-size: 0.78rem; font-weight: 600; border-radius: var(--r);
  padding: 0.56rem 0.9rem; cursor: pointer; transition: 0.2s; white-space: nowrap;
}
.btn-sort:hover, .btn-sort.asc { border-color: var(--border3); color: var(--text); }

/* Icon buttons */
.btn-icon {
  background: transparent; border: 1px solid var(--border);
  border-radius: 6px; color: var(--text-muted); font-size: 0.74rem;
  padding: 0.27rem 0.48rem; cursor: pointer; transition: 0.2s; margin-right: 0.2rem;
}
.btn-icon.edit:hover { border-color: var(--border3); color: var(--text); }
.btn-icon.del:hover  { border-color: var(--danger); color: var(--danger); }

/* Update follower btn */
.btn-update {
  background: var(--surface2); border: 1px solid var(--border2);
  color: var(--text-muted); font-family: var(--font-b); font-size: 0.77rem; font-weight: 600;
  border-radius: var(--r); padding: 0.56rem 0.85rem; cursor: pointer; white-space: nowrap; transition: 0.2s;
}
.btn-update:hover { background: var(--accent); color: #000; border-color: var(--accent); }

/* ================================================================
   HEADER
================================================================ */
.header {
  display: flex; align-items: center; justify-content: space-between;
  padding: 0 2rem; height: 60px;
  border-bottom: 1px solid var(--border);
  background: rgba(0,0,0,0.9); backdrop-filter: blur(16px); -webkit-backdrop-filter: blur(16px);
  position: sticky; top: 0; z-index: 100;
}
.header-logo {
  font-family: var(--font-d); font-size: 1rem; font-weight: 800;
  letter-spacing: 0.08em; color: var(--text);
  display: flex; align-items: center; gap: 0.45rem;
}
.header-logo .dot {
  width: 6px; height: 6px; border-radius: 50%; background: #fff;
  box-shadow: 0 0 6px rgba(255,255,255,0.6);
  animation: blink 2.5s ease-in-out infinite;
}
@keyframes blink { 0%,100% { opacity:1; } 50% { opacity:0.25; } }

.header-nav { display: flex; align-items: center; gap: 0.2rem; }
.nav-btn {
  background: transparent; border: none; color: var(--text-muted);
  font-family: var(--font-b); font-size: 0.8rem; font-weight: 500;
  padding: 0.38rem 0.8rem; border-radius: var(--r); cursor: pointer; transition: 0.2s;
}
.nav-btn:hover  { background: var(--surface2); color: var(--text); }
.nav-btn.active { background: var(--surface2); color: var(--text); border: 1px solid var(--border2); }

.btn-logout {
  background: transparent; border: 1px solid var(--border2); color: var(--text-muted);
  font-family: var(--font-b); font-size: 0.75rem; font-weight: 600;
  padding: 0.34rem 0.82rem; border-radius: var(--r); cursor: pointer; transition: 0.2s; margin-left: 0.7rem;
}
.btn-logout:hover { border-color: var(--danger); color: var(--danger); }

.btn-public-view {
  background: var(--surface2); border: 1px solid var(--border2); color: var(--text-muted);
  font-family: var(--font-b); font-size: 0.75rem; font-weight: 600;
  padding: 0.34rem 0.82rem; border-radius: var(--r); cursor: pointer; transition: 0.2s;
  margin-left: 0.5rem; display: inline-flex; align-items: center; gap: 0.3rem;
}
.btn-public-view:hover { background: var(--accent); color: #000; border-color: var(--accent); }

/* ================================================================
   PAGE SYSTEM
================================================================ */
.page { display: none; }
.page.active { display: block; animation: pageIn 0.25s ease; }
@keyframes pageIn { from { opacity:0; transform:translateY(6px); } to { opacity:1; transform:translateY(0); } }

.main { padding: 2rem; max-width: 1400px; margin: 0 auto; }

/* ================================================================
   HERO
================================================================ */
.hero {
  position: relative; overflow: hidden; border-radius: var(--r-lg);
  border: 1px solid var(--border2); min-height: 190px;
  display: flex; align-items: flex-end; padding: 2.5rem;
  margin-bottom: 2rem;
  background: linear-gradient(135deg, #0d0d0d 0%, #050505 100%);
}
.hero::before {
  content: ''; position: absolute; inset: 0;
  background:
    radial-gradient(ellipse at 8% 60%, rgba(255,255,255,0.04) 0%, transparent 50%),
    radial-gradient(ellipse at 85% 15%, rgba(255,255,255,0.02) 0%, transparent 45%);
}
.hero::after {
  content: ''; position: absolute; right: 0; top: 0; bottom: 0; width: 45%;
  background-image:
    repeating-linear-gradient(0deg, transparent, transparent 28px, rgba(255,255,255,0.025) 28px, rgba(255,255,255,0.025) 29px),
    repeating-linear-gradient(90deg, transparent, transparent 40px, rgba(255,255,255,0.015) 40px, rgba(255,255,255,0.015) 41px);
  mask-image: linear-gradient(90deg, transparent, black);
}
.hero-deco { position: absolute; right: 2.5rem; bottom: 2rem; opacity: 0.25; pointer-events: none; z-index: 1; }
.hero-content { position: relative; z-index: 2; max-width: 620px; }
.hero-tag {
  display: inline-flex; align-items: center; gap: 0.38rem;
  font-family: var(--font-m); font-size: 0.65rem; letter-spacing: 0.15em; text-transform: uppercase;
  color: #888; background: rgba(255,255,255,0.04); border: 1px solid rgba(255,255,255,0.1);
  border-radius: 999px; padding: 0.25rem 0.8rem; margin-bottom: 1rem;
}
.hero-tag::before { content: ''; width: 5px; height: 5px; background: var(--success); border-radius: 50%; box-shadow: 0 0 5px var(--success); animation: blink 2s ease-in-out infinite; }
.hero-quote { font-family: var(--font-d); font-size: clamp(1.2rem, 2.5vw, 1.85rem); line-height: 1.25; color: var(--text); margin-bottom: 0.7rem; }
.hero-quote em { color: #aaa; font-style: italic; }
.hero-sub { font-size: 0.8rem; color: var(--text-muted); font-weight: 300; }

/* ================================================================
   SECTION HEADS
================================================================ */
.section-head { display: flex; align-items: center; justify-content: space-between; margin-bottom: 1.2rem; }
.section-title { font-family: var(--font-d); font-size: 0.92rem; font-weight: 700; color: var(--text); }
.divider { height: 1px; background: var(--border); margin: 2rem 0; }
.toolbar { display: flex; flex-wrap: wrap; gap: 0.6rem; align-items: center; margin-bottom: 1rem; }
.toolbar-search { flex: 1; min-width: 175px; }

/* ================================================================
   STAT CARDS
================================================================ */
.stats-row {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(125px, 1fr));
  gap: 0.875rem; margin-bottom: 1.75rem;
}
.stat-card {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: var(--r); padding: 1.2rem 1.2rem 1rem;
  position: relative; overflow: hidden;
  transition: border-color 0.2s, transform 0.2s;
}
.stat-card:hover { border-color: var(--border2); transform: translateY(-2px); }
.stat-card::after {
  content: ''; position: absolute; bottom: 0; left: 0; right: 0; height: 1px;
  background: linear-gradient(90deg, rgba(255,255,255,0.15), transparent);
}
.stat-label { font-size: 0.64rem; font-weight: 600; letter-spacing: 0.1em; text-transform: uppercase; color: var(--text-muted); margin-bottom: 0.45rem; }
.stat-value { font-family: var(--font-m); font-size: 1.8rem; font-weight: 500; color: var(--text); line-height: 1; }
.stat-sub   { font-size: 0.68rem; color: var(--text-muted); margin-top: 0.28rem; }

/* ================================================================
   MONTHLY GOALS SECTION
================================================================ */
.goals-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1rem; margin-bottom: 2rem;
}

.goal-card {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: var(--r-lg); padding: 1.5rem;
  position: relative; overflow: hidden;
  transition: border-color 0.2s, transform 0.2s;
}
.goal-card:hover { border-color: var(--border2); transform: translateY(-2px); }

/* Top accent line — changes color based on completion */
.goal-card::before {
  content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px;
  background: var(--goal-color, #333);
  transition: background 0.4s;
}

.goal-header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 1.1rem; }
.goal-icon { font-size: 1.3rem; }
.goal-pct {
  font-family: var(--font-m); font-size: 0.8rem; font-weight: 500;
  color: var(--text-muted);
  background: var(--surface2); border: 1px solid var(--border);
  border-radius: 6px; padding: 0.18rem 0.55rem;
}
.goal-title { font-family: var(--font-d); font-size: 0.82rem; font-weight: 700; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.08em; margin-bottom: 0.4rem; }
.goal-numbers { display: flex; align-items: baseline; gap: 0.3rem; margin-bottom: 1rem; }
.goal-current { font-family: var(--font-m); font-size: 2rem; font-weight: 500; color: var(--text); line-height: 1; }
.goal-sep     { font-size: 1rem; color: var(--text-dim); }
.goal-target  { font-family: var(--font-m); font-size: 1rem; color: var(--text-muted); }
.goal-unit    { font-size: 0.75rem; color: var(--text-muted); margin-left: 0.4rem; }

/* Progress bar track */
.goal-bar-track {
  height: 6px; background: var(--surface3);
  border-radius: 999px; overflow: hidden; margin-bottom: 0.55rem;
}
.goal-bar-fill {
  height: 100%; border-radius: 999px;
  background: var(--goal-color, #333);
  transition: width 0.6s cubic-bezier(0.34,1.2,0.64,1);
  min-width: 0; max-width: 100%;
}
.goal-status { font-size: 0.72rem; color: var(--text-muted); }

/* ================================================================
   TABLE
================================================================ */
.table-wrap {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: var(--r-lg); overflow: hidden; overflow-x: auto;
}
table { width: 100%; border-collapse: collapse; min-width: 660px; }
thead { background: var(--surface2); }
th {
  text-align: left; font-size: 0.64rem; font-weight: 700;
  letter-spacing: 0.12em; text-transform: uppercase; color: var(--text-muted);
  padding: 0.85rem 1.2rem; border-bottom: 1px solid var(--border); white-space: nowrap;
}
td { padding: 0.78rem 1.2rem; font-size: 0.83rem; border-bottom: 1px solid var(--border); vertical-align: middle; }
tbody tr { transition: background 0.15s; }
tbody tr:hover { background: var(--surface2); }
tbody tr:last-child td { border-bottom: none; }

/* badges */
.badge { display: inline-block; font-size: 0.64rem; font-weight: 700; letter-spacing: 0.05em; text-transform: uppercase; padding: 0.18rem 0.46rem; border-radius: 5px; margin: 0.08rem 0.1rem 0.08rem 0; }
.badge-tiktok    { background: rgba(0,242,234,0.08);  color: var(--tiktok);    border: 1px solid rgba(0,242,234,0.18); }
.badge-instagram { background: rgba(247,106,138,0.08); color: var(--instagram); border: 1px solid rgba(247,106,138,0.18); }
.badge-facebook  { background: rgba(106,155,255,0.08); color: var(--facebook);  border: 1px solid rgba(106,155,255,0.18); }
.badge-youtube   { background: rgba(255,100,100,0.08); color: var(--youtube);   border: 1px solid rgba(255,100,100,0.18); }
.pill { display: inline-block; font-size: 0.7rem; font-weight: 500; padding: 0.2rem 0.55rem; border-radius: 5px; background: var(--accent-sub); border: 1px solid var(--border2); color: var(--text-muted); }

.content-link {
  color: #aaa; font-family: var(--font-m); font-size: 0.74rem;
  text-decoration: none; max-width: 145px; display: inline-block;
  overflow: hidden; text-overflow: ellipsis; white-space: nowrap; vertical-align: middle;
  opacity: 0.75; transition: opacity 0.2s;
}
.content-link:hover { opacity: 1; color: var(--text); text-decoration: underline; }

.empty-state { text-align: center; padding: 4rem 2rem; color: var(--text-muted); }
.empty-icon  { font-size: 2.2rem; margin-bottom: 0.7rem; opacity: 0.2; }
.empty-state p { font-size: 0.875rem; }

/* ================================================================
   CHART CARDS
================================================================ */
.chart-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px,1fr)); gap: 1.25rem; margin-bottom: 2rem; }
.chart-card {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: var(--r-lg); padding: 1.5rem; position: relative; overflow: hidden; transition: border-color 0.2s;
}
.chart-card:hover { border-color: var(--border2); }
.chart-card::before {
  content: ''; position: absolute; top: 0; left: 0; right: 0; height: 1px;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.12), transparent);
}
.chart-title { font-family: var(--font-d); font-size: 0.88rem; font-weight: 700; color: var(--text); margin-bottom: 0.25rem; }
.chart-sub   { font-size: 0.72rem; color: var(--text-muted); margin-bottom: 1.2rem; }
.chart-wrap  { position: relative; height: 215px; }

/* ================================================================
   PLATFORM GROWTH CARDS
================================================================ */
.platform-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(270px,1fr)); gap: 1.25rem; margin-bottom: 2rem; }
.platform-card {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: var(--r-lg); padding: 1.5rem;
  transition: border-color 0.2s, transform 0.2s;
}
.platform-card:hover { border-color: var(--border2); transform: translateY(-2px); }
.platform-card-header { display: flex; align-items: center; gap: 0.75rem; margin-bottom: 1.2rem; }
.platform-icon { width: 40px; height: 40px; border-radius: 10px; display: flex; align-items: center; justify-content: center; font-size: 1.1rem; }
.platform-card-name { font-family: var(--font-d); font-size: 0.95rem; font-weight: 700; }
.platform-card-link { font-size: 0.72rem; color: var(--text-muted); text-decoration: none; transition: color 0.2s; }
.platform-card-link:hover { color: var(--text); }
.follower-current { font-family: var(--font-m); font-size: 1.5rem; font-weight: 500; color: var(--text); margin-bottom: 0.18rem; }
.follower-label   { font-size: 0.68rem; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.08em; margin-bottom: 0.75rem; }
.follower-input-row { display: flex; gap: 0.5rem; margin-bottom: 1rem; }
.follower-input-row .field-input { flex: 1; }
.mini-chart-wrap { height: 75px; position: relative; }

/* ================================================================
   MODAL
================================================================ */
.modal-overlay {
  position: fixed; inset: 0;
  background: rgba(0,0,0,0.85); backdrop-filter: blur(8px); -webkit-backdrop-filter: blur(8px);
  z-index: 300; display: none; align-items: center; justify-content: center; padding: 1rem;
}
.modal-overlay.open { display: flex; }
.modal {
  background: var(--surface); border: 1px solid var(--border2);
  border-radius: 18px; padding: 2rem; width: 100%; max-width: 540px;
  max-height: 90vh; overflow-y: auto;
  animation: modalIn 0.22s cubic-bezier(0.34,1.4,0.64,1);
  box-shadow: 0 40px 100px rgba(0,0,0,0.8);
}
@keyframes modalIn { from { opacity:0; transform:translateY(16px) scale(0.97); } to { opacity:1; transform:translateY(0) scale(1); } }
.modal-header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 1.75rem; }
.modal-title  { font-family: var(--font-d); font-size: 1.15rem; color: var(--text); }
.btn-close { background: var(--surface2); border: 1px solid var(--border); border-radius: 6px; color: var(--text-muted); width: 30px; height: 30px; display: flex; align-items: center; justify-content: center; cursor: pointer; font-size: 0.85rem; transition: 0.2s; }
.btn-close:hover { border-color: var(--danger); color: var(--danger); }
.modal-actions { display: flex; justify-content: flex-end; gap: 0.75rem; margin-top: 1.75rem; }

/* Platform checkboxes */
.platform-checkboxes { display: flex; flex-wrap: wrap; gap: 0.5rem; padding: 0.72rem; background: var(--bg2); border: 1px solid var(--border2); border-radius: var(--r); }
.plat-label { display: flex; align-items: center; gap: 0.38rem; cursor: pointer; padding: 0.34rem 0.7rem; border-radius: 7px; border: 1px solid var(--border2); background: var(--surface2); font-size: 0.79rem; font-weight: 600; color: var(--text-muted); transition: 0.2s; user-select: none; }
.plat-label:hover { border-color: var(--border3); color: var(--text); }
.plat-label input { display: none; }
.plat-label.checked { background: var(--accent-sub); border-color: #555; color: var(--text); }

/* ================================================================
   INBOX
================================================================ */
.inbox-compose { background: var(--surface); border: 1px solid var(--border); border-radius: var(--r-lg); padding: 1.75rem; margin-bottom: 1.75rem; }
.inbox-plat-row { display: flex; flex-wrap: wrap; gap: 0.45rem; margin-bottom: 0.875rem; }
.inbox-plat-btn { background: var(--surface2); border: 1px solid var(--border2); color: var(--text-muted); font-size: 0.77rem; font-weight: 600; border-radius: 7px; padding: 0.33rem 0.7rem; cursor: pointer; transition: 0.2s; }
.inbox-plat-btn:hover { border-color: var(--border3); color: var(--text); }
.inbox-plat-btn.active { background: var(--accent-sub); border-color: #555; color: var(--text); }
.upload-area { border: 1.5px dashed var(--border2); border-radius: var(--r); padding: 1.4rem; text-align: center; cursor: pointer; transition: 0.2s; background: var(--bg2); position: relative; }
.upload-area:hover { border-color: #555; background: var(--surface2); }
.upload-area input[type="file"] { position: absolute; inset: 0; opacity: 0; cursor: pointer; width: 100%; height: 100%; }
.upload-icon { font-size: 1.6rem; margin-bottom: 0.35rem; opacity: 0.35; }
.upload-text { font-size: 0.74rem; color: var(--text-muted); }
.upload-preview { max-height: 130px; max-width: 100%; border-radius: 8px; margin-top: 0.72rem; display: none; }
.inbox-list { display: flex; flex-direction: column; gap: 1rem; }
.inbox-card { background: var(--surface); border: 1px solid var(--border); border-radius: var(--r-lg); padding: 1.35rem; display: flex; gap: 1.2rem; transition: border-color 0.2s; animation: fadeUp 0.25s ease; }
@keyframes fadeUp { from { opacity:0; transform:translateY(8px); } to { opacity:1; transform:translateY(0); } }
.inbox-card:hover { border-color: var(--border2); }
.inbox-thumb { width: 82px; height: 82px; min-width: 82px; border-radius: 10px; object-fit: cover; cursor: pointer; transition: transform 0.2s; border: 1px solid var(--border2); }
.inbox-thumb:hover { transform: scale(1.04); }
.inbox-thumb-empty { width: 82px; height: 82px; min-width: 82px; border-radius: 10px; background: var(--surface2); border: 1px dashed var(--border2); display: flex; align-items: center; justify-content: center; color: var(--text-dim); font-size: 1.1rem; }
.inbox-body { flex: 1; }
.inbox-meta { display: flex; align-items: center; gap: 0.6rem; margin-bottom: 0.38rem; flex-wrap: wrap; }
.inbox-date { font-family: var(--font-m); font-size: 0.68rem; color: var(--text-muted); }
.inbox-msg  { font-size: 0.86rem; color: var(--text); line-height: 1.5; }
.inbox-del  { background: transparent; border: 1px solid var(--border); border-radius: 6px; color: var(--text-muted); font-size: 0.72rem; padding: 0.24rem 0.44rem; cursor: pointer; transition: 0.2s; align-self: flex-start; }
.inbox-del:hover { border-color: var(--danger); color: var(--danger); }

/* ================================================================
   LIGHTBOX
================================================================ */
#lightbox { position: fixed; inset: 0; background: rgba(0,0,0,0.95); z-index: 500; display: none; align-items: center; justify-content: center; cursor: zoom-out; padding: 2rem; }
#lightbox.open { display: flex; animation: fadeUp 0.2s ease; }
#lightbox img  { max-width: 100%; max-height: 90vh; border-radius: 12px; object-fit: contain; }

/* ================================================================
   TOAST
================================================================ */
#toast { position: fixed; bottom: 2rem; right: 2rem; background: var(--surface2); border: 1px solid var(--border2); border-radius: var(--r); color: var(--text); font-size: 0.83rem; padding: 0.7rem 1.15rem; z-index: 999; opacity: 0; transform: translateY(8px); transition: opacity 0.25s, transform 0.25s; pointer-events: none; max-width: 300px; }
#toast.show { opacity: 1; transform: translateY(0); }

/* ================================================================
   LOGIN SCREEN
================================================================ */
#login-screen {
  position: fixed; inset: 0; display: flex; align-items: center; justify-content: center;
  z-index: 200; padding: 1.5rem; background: var(--bg);
}
.login-card {
  background: var(--surface); border: 1px solid var(--border2);
  border-radius: 22px; padding: 3rem 2.5rem;
  width: 100%; max-width: 400px;
  position: relative; overflow: hidden; text-align: center;
  box-shadow: 0 40px 80px rgba(0,0,0,0.6);
}
/* Top shimmer */
.login-card::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 1px; background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent); }

.login-icon {
  width: 52px; height: 52px; background: var(--surface2); border: 1px solid var(--border2);
  border-radius: 14px; display: flex; align-items: center; justify-content: center;
  font-size: 1.4rem; margin: 0 auto 1.4rem;
}
/* Responsive headline — scales down, never overflows the card */
.login-headline {
  font-family: var(--font-d);
  font-size: 0.95rem;
  font-weight: 800;
  letter-spacing: 0.01em;
  color: var(--text);
  margin-bottom: 0.4rem;
  white-space: normal;
  word-break: break-word;
  overflow-wrap: break-word;
  line-height: 1.2;
}
.login-sub { font-size: 0.82rem; color: var(--text-muted); margin-bottom: 2rem; }
.field-group { margin-bottom: 1.1rem; text-align: left; }
.login-error { margin-top: 0.85rem; background: rgba(239,68,68,0.08); border: 1px solid rgba(239,68,68,0.25); border-radius: var(--r); color: var(--danger); font-size: 0.8rem; padding: 0.55rem 1rem; display: none; }
.welcome-text { font-family: var(--font-d); font-size: 0.92rem; font-weight: 700; letter-spacing: 0.05em; }
.login-public-link { display: inline-block; margin-top: 1.2rem; font-size: 0.78rem; color: var(--text-muted); cursor: pointer; transition: color 0.2s; }
.login-public-link:hover { color: var(--text); }

/* ================================================================
   PUBLIC PAGE BADGE
================================================================ */
.public-badge {
  display: inline-flex; align-items: center; gap: 0.35rem;
  background: rgba(34,197,94,0.08); border: 1px solid rgba(34,197,94,0.2);
  color: var(--success); font-family: var(--font-m); font-size: 0.62rem;
  letter-spacing: 0.1em; text-transform: uppercase; border-radius: 999px;
  padding: 0.22rem 0.7rem; margin-left: 0.7rem;
}
.public-badge::before { content: ''; width: 5px; height: 5px; background: var(--success); border-radius: 50%; animation: blink 2s infinite; }

/* ================================================================
   RESPONSIVE
================================================================ */
@media (max-width: 768px) {
  .main { padding: 1.25rem 1rem 3rem; }
  .header { padding: 0 1rem; }
  .nav-btn span { display: none; }
  .form-grid { grid-template-columns: 1fr; }
  .stats-row { grid-template-columns: repeat(3, 1fr); }
  .hero { padding: 1.75rem 1.4rem; }
  .hero-deco { display: none; }
  .inbox-card { flex-direction: column; }
  .inbox-thumb, .inbox-thumb-empty { width: 100%; height: 150px; }
  .chart-grid, .goals-grid { grid-template-columns: 1fr; }
  .login-card { padding: 2rem 1.25rem; }
  .login-headline { font-size: 0.95rem; letter-spacing: 0.01em; }
}
</style>
</head>
<body>

<!-- ================================================================
     LOGIN SCREEN
================================================================ -->
<div id="login-screen">
  <div class="login-card">
    <div class="login-icon">⬜</div>
    <h1 class="login-headline">WHITEGREENZONE</h1>
    <p class="login-sub">Admin dashboard · Content &amp; growth</p>

    <div class="field-group">
      <label class="field-label">Admin Password</label>
      <input type="password" id="pw-input" class="field-input" placeholder="Enter password…" autocomplete="current-password"/>
    </div>

    <div class="login-error" id="login-error">Incorrect password. Please try again.</div>

    <button class="btn-primary" onclick="handleLogin()">
      <div class="welcome-text">Welcome WhiteGreenZone</div>
    </button>

    <div class="login-public-link" onclick="showPublicPage()">
      👁 View public progress page →
    </div>
  </div>
</div>

<!-- ================================================================
     ADMIN DASHBOARD
================================================================ -->
<div id="admin-app" style="display:none;">

  <header class="header">
    <div class="header-logo"><div class="dot"></div>WHITEGREENZONE</div>
    <nav class="header-nav">
      <button class="nav-btn active" id="nav-tracker"   onclick="switchAdminPage('tracker')"><span>📊 </span>Tracker</button>
      <button class="nav-btn"        id="nav-inbox"     onclick="switchAdminPage('inbox')"><span>📥 </span>Inbox</button>
      <button class="nav-btn"        id="nav-analytics" onclick="switchAdminPage('analytics')"><span>📈 </span>Analytics</button>
      <button class="btn-public-view" onclick="showPublicPage()">👁 Public</button>
      <button class="btn-logout" onclick="handleLogout()">Logout</button>
    </nav>
  </header>

  <!-- ==== ADMIN: TRACKER ==== -->
  <div id="admin-page-tracker" class="page active">
    <div class="main">

      <!-- Hero -->
      <div class="hero">
        <svg class="hero-deco" width="250" height="110" viewBox="0 0 250 110" fill="none">
          <polyline points="0,90 30,78 62,70 90,55 122,60 152,40 182,30 210,18 240,8 250,4"
            stroke="#fff" stroke-width="1.5" fill="none" stroke-linecap="round" stroke-linejoin="round" opacity="0.6"/>
          <polygon points="0,90 30,78 62,70 90,55 122,60 152,40 182,30 210,18 240,8 250,4 250,110 0,110"
            fill="url(#wg)" opacity="0.08"/>
          <circle cx="152" cy="40" r="3" fill="#fff" opacity="0.7"/>
          <circle cx="250" cy="4"  r="3" fill="#fff" opacity="0.7"/>
          <defs><linearGradient id="wg" x1="0" y1="0" x2="0" y2="1">
            <stop offset="0%" stop-color="#ffffff"/><stop offset="100%" stop-color="transparent"/>
          </linearGradient></defs>
        </svg>
        <div class="hero-content">
          <div class="hero-tag">Admin Dashboard</div>
          <h2 class="hero-quote">"Green Zone for Investors —<br><em>The place that keeps you safe</em><br>from the Red Zone."</h2>
          <p class="hero-sub">Track your content. Stay consistent. Build your empire.</p>
        </div>
      </div>

      <!-- ── MONTHLY GOALS ── -->
      <div class="section-head">
        <div class="section-title">🎯 Monthly Goals</div>
        <span style="font-size:0.75rem;color:var(--text-muted);font-family:var(--font-m);" id="goals-month-label"></span>
      </div>
      <div class="goals-grid" id="goals-grid">
        <!-- Rendered by JS -->
      </div>

      <!-- Stats -->
      <div class="section-head" style="margin-top:0.5rem;"><div class="section-title">📊 Overview</div></div>
      <div class="stats-row">
        <div class="stat-card"><div class="stat-label">Total Posts</div><div class="stat-value" id="stat-total">0</div></div>
        <div class="stat-card"><div class="stat-label">TikTok</div><div class="stat-value" id="stat-tiktok">0</div></div>
        <div class="stat-card"><div class="stat-label">Instagram</div><div class="stat-value" id="stat-insta">0</div></div>
        <div class="stat-card"><div class="stat-label">YouTube</div><div class="stat-value" id="stat-yt">0</div></div>
        <div class="stat-card"><div class="stat-label">Facebook</div><div class="stat-value" id="stat-fb">0</div></div>
      </div>

      <!-- Toolbar -->
      <div class="toolbar">
        <div class="toolbar-search"><input type="text" id="search-input" class="field-input sm" placeholder="🔍  Search entries…" oninput="renderTable()"/></div>
        <select id="filter-platform" class="field-input sm" style="min-width:132px" onchange="renderTable()">
          <option value="">All Platforms</option>
          <option>TikTok</option><option>Instagram</option><option>Facebook</option><option>YouTube</option>
        </select>
        <select id="filter-type" class="field-input sm" style="min-width:132px" onchange="renderTable()">
          <option value="">All Types</option>
          <option>Livestream</option><option>Normal Post</option><option>Short Video</option><option>Other</option>
        </select>
        <button id="sort-btn" class="btn-sort" onclick="toggleSort()">↓ Newest</button>
        <button class="btn-add" onclick="openEntryModal()">+ Add Entry</button>
      </div>

      <!-- Table -->
      <div class="table-wrap">
        <table>
          <thead><tr><th>Date</th><th>Platforms</th><th>Work Type</th><th>Content Link</th><th>Notes</th><th>Actions</th></tr></thead>
          <tbody id="entries-tbody"></tbody>
        </table>
        <div class="empty-state" id="empty-state" style="display:none;"><div class="empty-icon">📋</div><p>No entries yet — hit <strong>+ Add Entry</strong>.</p></div>
      </div>

    </div>
  </div><!-- /tracker -->

  <!-- ==== ADMIN: INBOX ==== -->
  <div id="admin-page-inbox" class="page">
    <div class="main">

      <div class="section-head"><div class="section-title">📬 Monthly Inbox Summary</div></div>
      <div class="stats-row">
        <div class="stat-card"><div class="stat-label">This Month</div><div class="stat-value" id="ib-stat-total">0</div><div class="stat-sub">messages</div></div>
        <div class="stat-card"><div class="stat-label">TikTok</div><div class="stat-value" id="ib-stat-tiktok">0</div></div>
        <div class="stat-card"><div class="stat-label">Instagram</div><div class="stat-value" id="ib-stat-insta">0</div></div>
        <div class="stat-card"><div class="stat-label">YouTube</div><div class="stat-value" id="ib-stat-yt">0</div></div>
        <div class="stat-card"><div class="stat-label">Facebook</div><div class="stat-value" id="ib-stat-fb">0</div></div>
      </div>

      <div class="chart-card" style="margin-bottom:2rem;">
        <div class="chart-title">Monthly Inbox by Platform</div>
        <div class="chart-sub">Messages per platform this month</div>
        <div class="chart-wrap"><canvas id="inboxMonthChart"></canvas></div>
      </div>

      <div class="section-head"><div class="section-title">✍️ New Message</div></div>
      <div class="inbox-compose">
        <div class="form-group" style="margin-bottom:0.75rem;">
          <label class="field-label">Platform</label>
          <div class="inbox-plat-row" id="inbox-plat-row">
            <button class="inbox-plat-btn" data-p="TikTok"    onclick="toggleInboxPlat(this)">TikTok</button>
            <button class="inbox-plat-btn" data-p="Instagram" onclick="toggleInboxPlat(this)">Instagram</button>
            <button class="inbox-plat-btn" data-p="YouTube"   onclick="toggleInboxPlat(this)">YouTube</button>
            <button class="inbox-plat-btn" data-p="Facebook"  onclick="toggleInboxPlat(this)">Facebook</button>
          </div>
        </div>
        <div class="form-group" style="margin-bottom:0.875rem;">
          <label class="field-label">Message</label>
          <textarea id="inbox-msg-input" class="field-input" rows="3" placeholder="Write your message or evidence note…"></textarea>
        </div>
        <div class="form-group" style="margin-bottom:1.2rem;">
          <label class="field-label">Image Evidence (optional)</label>
          <div class="upload-area" id="upload-area">
            <input type="file" id="inbox-img-input" accept="image/*" onchange="previewImage(event)"/>
            <div class="upload-icon">🖼️</div>
            <div class="upload-text">Click to upload image</div>
            <img id="upload-preview" class="upload-preview" alt="preview"/>
          </div>
        </div>
        <div style="display:flex;gap:0.75rem;flex-wrap:wrap;">
          <button class="btn-add" onclick="saveInboxEntry()">Save Message</button>
          <button class="btn-ghost" onclick="clearInboxForm()">Clear</button>
        </div>
      </div>

      <div class="section-head"><div class="section-title">📥 All Messages</div></div>
      <div class="inbox-list" id="inbox-list"></div>
      <div class="empty-state" id="inbox-empty" style="display:none;"><div class="empty-icon">📭</div><p>No messages yet.</p></div>

    </div>
  </div><!-- /inbox -->

  <!-- ==== ADMIN: ANALYTICS ==== -->
  <div id="admin-page-analytics" class="page">
    <div class="main">

      <div class="section-head" style="margin-bottom:1.5rem;"><div class="section-title">📊 Productivity Overview</div></div>

      <div class="chart-grid">
        <div class="chart-card"><div class="chart-title">Content Activity</div><div class="chart-sub">Posts created per month</div><div class="chart-wrap"><canvas id="contentActivityChart"></canvas></div></div>
        <div class="chart-card"><div class="chart-title">Inbox Growth</div><div class="chart-sub">Messages per platform per month</div><div class="chart-wrap"><canvas id="inboxGrowthChart"></canvas></div></div>
      </div>

      <div class="chart-card" style="margin-bottom:2rem;">
        <div class="chart-title">Platform Content Distribution</div>
        <div class="chart-sub">Total content entries per platform all-time</div>
        <div class="chart-wrap"><canvas id="platformDistChart"></canvas></div>
      </div>

      <div class="divider"></div>

      <div class="section-head" style="margin-bottom:1.5rem;"><div class="section-title">🚀 Platform Growth Tracker</div></div>
      <div class="platform-grid">

        <div class="platform-card">
          <div class="platform-card-header">
            <div class="platform-icon" style="background:rgba(255,100,100,0.1);color:var(--youtube);">▶️</div>
            <div>
              <div class="platform-card-name" style="color:var(--youtube);">YouTube</div>
              <a class="platform-card-link" href="https://youtube.com/@startwithmindset?si=fvzqKPwS2Zw5k6fm" target="_blank" rel="noopener">@startwithmindset ↗</a>
            </div>
          </div>
          <div class="follower-current" id="yt-follower-display">—</div>
          <div class="follower-label">Subscribers</div>
          <div class="follower-input-row">
            <input type="number" id="yt-follower-input" class="field-input sm" placeholder="Enter count"/>
            <button class="btn-update" onclick="updateFollowers('youtube')">Update</button>
          </div>
          <div class="mini-chart-wrap"><canvas id="ytGrowthChart"></canvas></div>
        </div>

        <div class="platform-card">
          <div class="platform-card-header">
            <div class="platform-icon" style="background:rgba(247,106,138,0.1);color:var(--instagram);">📸</div>
            <div>
              <div class="platform-card-name" style="color:var(--instagram);">Instagram</div>
              <a class="platform-card-link" href="https://www.instagram.com/whitegreenzone/" target="_blank" rel="noopener">@whitegreenzone ↗</a>
            </div>
          </div>
          <div class="follower-current" id="ig-follower-display">—</div>
          <div class="follower-label">Followers</div>
          <div class="follower-input-row">
            <input type="number" id="ig-follower-input" class="field-input sm" placeholder="Enter count"/>
            <button class="btn-update" onclick="updateFollowers('instagram')">Update</button>
          </div>
          <div class="mini-chart-wrap"><canvas id="igGrowthChart"></canvas></div>
        </div>

        <div class="platform-card">
          <div class="platform-card-header">
            <div class="platform-icon" style="background:rgba(0,242,234,0.08);color:var(--tiktok);">🎵</div>
            <div>
              <div class="platform-card-name" style="color:var(--tiktok);">TikTok</div>
              <a class="platform-card-link" href="https://www.tiktok.com/@white_green_zone?is_from_webapp=1&sender_device=pc" target="_blank" rel="noopener">@white_green_zone ↗</a>
            </div>
          </div>
          <div class="follower-current" id="tt-follower-display">—</div>
          <div class="follower-label">Followers</div>
          <div class="follower-input-row">
            <input type="number" id="tt-follower-input" class="field-input sm" placeholder="Enter count"/>
            <button class="btn-update" onclick="updateFollowers('tiktok')">Update</button>
          </div>
          <div class="mini-chart-wrap"><canvas id="ttGrowthChart"></canvas></div>
        </div>

      </div>
    </div>
  </div><!-- /analytics -->

</div><!-- /admin-app -->


<!-- ================================================================
     PUBLIC PROGRESS PAGE
================================================================ -->
<div id="public-app" style="display:none;">

  <header class="header">
    <div class="header-logo"><div class="dot"></div>WHITEGREENZONE<span class="public-badge">Public</span></div>
    <div class="header-nav">
      <button class="btn-logout" onclick="backToLogin()">← Back</button>
    </div>
  </header>

  <div class="main">

    <!-- Hero -->
    <div class="hero">
      <svg class="hero-deco" width="250" height="110" viewBox="0 0 250 110" fill="none">
        <polyline points="0,90 30,78 62,70 90,55 122,60 152,40 182,30 210,18 240,8 250,4"
          stroke="#fff" stroke-width="1.5" fill="none" stroke-linecap="round" stroke-linejoin="round" opacity="0.5"/>
        <polygon points="0,90 30,78 62,70 90,55 122,60 152,40 182,30 210,18 240,8 250,4 250,110 0,110"
          fill="url(#wg2)" opacity="0.07"/>
        <circle cx="152" cy="40" r="3" fill="#fff" opacity="0.6"/>
        <circle cx="250" cy="4"  r="3" fill="#fff" opacity="0.6"/>
        <defs><linearGradient id="wg2" x1="0" y1="0" x2="0" y2="1">
          <stop offset="0%" stop-color="#ffffff"/><stop offset="100%" stop-color="transparent"/>
        </linearGradient></defs>
      </svg>
      <div class="hero-content">
        <div class="hero-tag">Progress Page · Live</div>
        <h2 class="hero-quote">"Green Zone for Investors —<br><em>The place that keeps you safe</em><br>from the Red Zone."</h2>
        <p class="hero-sub">Follow the journey. Real work. Real results. Updated regularly.</p>
      </div>
    </div>

    <!-- Public Monthly Goals -->
    <div class="section-head">
      <div class="section-title">🎯 Monthly Goals</div>
      <span style="font-size:0.75rem;color:var(--text-muted);font-family:var(--font-m);" id="pub-goals-month-label"></span>
    </div>
    <div class="goals-grid" id="pub-goals-grid"></div>

    <div class="divider"></div>

    <!-- Content stats -->
    <div class="section-head"><div class="section-title">📊 Content Overview</div></div>
    <div class="stats-row">
      <div class="stat-card"><div class="stat-label">Total Posts</div><div class="stat-value" id="pub-stat-total">0</div></div>
      <div class="stat-card"><div class="stat-label">TikTok</div><div class="stat-value" id="pub-stat-tiktok">0</div></div>
      <div class="stat-card"><div class="stat-label">Instagram</div><div class="stat-value" id="pub-stat-insta">0</div></div>
      <div class="stat-card"><div class="stat-label">YouTube</div><div class="stat-value" id="pub-stat-yt">0</div></div>
      <div class="stat-card"><div class="stat-label">Facebook</div><div class="stat-value" id="pub-stat-fb">0</div></div>
    </div>

    <!-- Content Table -->
    <div class="section-head" style="margin-bottom:1rem;"><div class="section-title">📋 All Content Posted</div></div>
    <div class="table-wrap" style="margin-bottom:2rem;">
      <table>
        <thead><tr><th>Date</th><th>Platforms</th><th>Work Type</th><th>Content Link</th><th>Notes</th></tr></thead>
        <tbody id="pub-entries-tbody"></tbody>
      </table>
      <div class="empty-state" id="pub-empty" style="display:none;"><div class="empty-icon">📋</div><p>No content posted yet.</p></div>
    </div>

    <div class="divider"></div>

    <!-- Inbox stats -->
    <div class="section-head"><div class="section-title">📥 Inbox Activity</div></div>
    <div class="stats-row">
      <div class="stat-card"><div class="stat-label">This Month</div><div class="stat-value" id="pub-ib-total">0</div><div class="stat-sub">messages</div></div>
      <div class="stat-card"><div class="stat-label">TikTok</div><div class="stat-value" id="pub-ib-tiktok">0</div></div>
      <div class="stat-card"><div class="stat-label">Instagram</div><div class="stat-value" id="pub-ib-insta">0</div></div>
      <div class="stat-card"><div class="stat-label">YouTube</div><div class="stat-value" id="pub-ib-yt">0</div></div>
      <div class="stat-card"><div class="stat-label">Facebook</div><div class="stat-value" id="pub-ib-fb">0</div></div>
    </div>

    <div class="divider"></div>

    <!-- Productivity charts -->
    <div class="section-head" style="margin-bottom:1.5rem;"><div class="section-title">📈 Productivity Charts</div></div>
    <div class="chart-grid">
      <div class="chart-card"><div class="chart-title">Content per Month</div><div class="chart-sub">Posts created over the last 6 months</div><div class="chart-wrap"><canvas id="pub-contentChart"></canvas></div></div>
      <div class="chart-card"><div class="chart-title">Inbox per Month</div><div class="chart-sub">Messages per platform over last 6 months</div><div class="chart-wrap"><canvas id="pub-inboxChart"></canvas></div></div>
    </div>

    <div class="divider"></div>

    <!-- Platform growth (public, read-only) -->
    <div class="section-head" style="margin-bottom:1.5rem;"><div class="section-title">🚀 Platform Growth</div></div>
    <div class="platform-grid">

      <div class="platform-card">
        <div class="platform-card-header">
          <div class="platform-icon" style="background:rgba(255,100,100,0.1);color:var(--youtube);">▶️</div>
          <div><div class="platform-card-name" style="color:var(--youtube);">YouTube</div>
            <a class="platform-card-link" href="https://youtube.com/@startwithmindset?si=fvzqKPwS2Zw5k6fm" target="_blank" rel="noopener">@startwithmindset ↗</a></div>
        </div>
        <div class="follower-current" id="pub-yt-display">—</div>
        <div class="follower-label">Subscribers</div>
        <div class="mini-chart-wrap"><canvas id="pub-ytChart"></canvas></div>
      </div>

      <div class="platform-card">
        <div class="platform-card-header">
          <div class="platform-icon" style="background:rgba(247,106,138,0.1);color:var(--instagram);">📸</div>
          <div><div class="platform-card-name" style="color:var(--instagram);">Instagram</div>
            <a class="platform-card-link" href="https://www.instagram.com/whitegreenzone/" target="_blank" rel="noopener">@whitegreenzone ↗</a></div>
        </div>
        <div class="follower-current" id="pub-ig-display">—</div>
        <div class="follower-label">Followers</div>
        <div class="mini-chart-wrap"><canvas id="pub-igChart"></canvas></div>
      </div>

      <div class="platform-card">
        <div class="platform-card-header">
          <div class="platform-icon" style="background:rgba(0,242,234,0.08);color:var(--tiktok);">🎵</div>
          <div><div class="platform-card-name" style="color:var(--tiktok);">TikTok</div>
            <a class="platform-card-link" href="https://www.tiktok.com/@white_green_zone?is_from_webapp=1&sender_device=pc" target="_blank" rel="noopener">@white_green_zone ↗</a></div>
        </div>
        <div class="follower-current" id="pub-tt-display">—</div>
        <div class="follower-label">Followers</div>
        <div class="mini-chart-wrap"><canvas id="pub-ttChart"></canvas></div>
      </div>

    </div>
  </div><!-- /public .main -->
</div><!-- /public-app -->


<!-- ================================================================
     ENTRY MODAL
================================================================ -->
<div class="modal-overlay" id="entry-modal" onclick="closeModalOnOverlay(event,'entry-modal')">
  <div class="modal">
    <div class="modal-header">
      <h2 class="modal-title" id="modal-title">Add Entry</h2>
      <button class="btn-close" onclick="closeModal('entry-modal')">✕</button>
    </div>
    <div class="form-grid">
      <div class="form-group"><label class="field-label">Date</label><input type="date" id="f-date" class="field-input sm"/></div>
      <div class="form-group"><label class="field-label">Work Type</label>
        <select id="f-type" class="field-input sm">
          <option value="">Select…</option><option>Livestream</option><option>Normal Post</option><option>Short Video</option><option>Other</option>
        </select>
      </div>
      <div class="form-group full">
        <label class="field-label">Platforms (select all that apply)</label>
        <div class="platform-checkboxes" id="plat-checks">
          <label class="plat-label"><input type="checkbox" value="TikTok"    onchange="syncPlat(this)"/> TikTok</label>
          <label class="plat-label"><input type="checkbox" value="Instagram" onchange="syncPlat(this)"/> Instagram</label>
          <label class="plat-label"><input type="checkbox" value="Facebook"  onchange="syncPlat(this)"/> Facebook</label>
          <label class="plat-label"><input type="checkbox" value="YouTube"   onchange="syncPlat(this)"/> YouTube</label>
        </div>
      </div>
      <div class="form-group full"><label class="field-label">Content Link</label><input type="url" id="f-link" class="field-input sm" placeholder="https://…"/></div>
      <div class="form-group full"><label class="field-label">Notes (optional)</label><input type="text" id="f-notes" class="field-input sm" placeholder="Any extra details…"/></div>
    </div>
    <div class="modal-actions">
      <button class="btn-ghost" onclick="closeModal('entry-modal')">Cancel</button>
      <button class="btn-save" onclick="saveEntry()">Save Entry</button>
    </div>
  </div>
</div>

<!-- Lightbox -->
<div id="lightbox" onclick="closeLightbox()"><img id="lightbox-img" src="" alt="enlarged"/></div>
<!-- Toast -->
<div id="toast"></div>


<!-- ================================================================
     JAVASCRIPT
================================================================ -->
<script>
/* ================================================================
   CONFIG
================================================================ */
const APP_PASSWORD = "whitegreenzone130748";

/* ================================================================
   MONTHLY GOAL DEFINITIONS
   Targets: Content=12, Livestream=16, Inbox=100
================================================================ */
const GOALS = [
  {
    id:      "content",
    icon:    "🎬",
    title:   "Content Goal",
    target:  12,
    unit:    "clips",
    color:   "#ffffff",       // white bar for on-track
    getProgress: () => {
      // Count all entries in the current month
      const ym = currentYM();
      return entries.filter(e => toYM(e.date) === ym).length;
    }
  },
  {
    id:      "livestream",
    icon:    "🔴",
    title:   "Livestream Goal",
    target:  16,
    unit:    "livestreams",
    color:   "#ff6464",       // red-ish for livestream
    getProgress: () => {
      const ym = currentYM();
      return entries.filter(e => toYM(e.date) === ym && e.type === "Livestream").length;
    }
  },
  {
    id:      "inbox",
    icon:    "📬",
    title:   "Inbox Goal",
    target:  100,
    unit:    "messages",
    color:   "#22c55e",       // green for inbox/engagement
    getProgress: () => {
      const ym = currentYM();
      return inbox.filter(e => e.ym === ym).length;
    }
  }
];

/* ================================================================
   Chart.js global defaults — B&W palette
================================================================ */
Chart.defaults.color       = '#666';
Chart.defaults.borderColor = '#1f1f1f';
Chart.defaults.font.family = "'DM Mono', monospace";
Chart.defaults.font.size   = 11;

/* ================================================================
   STATE
================================================================ */
let entries   = [];
let inbox     = [];
let followers = { youtube: [], instagram: [], tiktok: [] };
let editingId = null;
let sortAsc   = false;
let selectedInboxPlat = null;
const charts  = {};

/* ================================================================
   LOCAL STORAGE
================================================================ */
function loadAll() {
  entries   = JSON.parse(localStorage.getItem("wgz_entries")   || "[]");
  inbox     = JSON.parse(localStorage.getItem("wgz_inbox")     || "[]");
  followers = JSON.parse(localStorage.getItem("wgz_followers") || '{"youtube":[],"instagram":[],"tiktok":[]}');
}

function saveEntries()   { localStorage.setItem("wgz_entries",   JSON.stringify(entries)); }
function saveInbox()     { localStorage.setItem("wgz_inbox",     JSON.stringify(inbox)); }
function saveFollowers() { localStorage.setItem("wgz_followers", JSON.stringify(followers)); }

/* ================================================================
   LOGIN / LOGOUT
================================================================ */
function handleLogin() {
  if (document.getElementById("pw-input").value === APP_PASSWORD) {
    document.getElementById("login-screen").style.display = "none";
    document.getElementById("admin-app").style.display    = "block";
    loadAll();
    renderTable();
    updateStats();
    renderGoals("goals-grid", "goals-month-label");
    refreshFollowerDisplays("admin");
  } else {
    const el = document.getElementById("login-error");
    el.style.display = "block";
    el.animate([
      {transform:"translateX(-5px)"},{transform:"translateX(5px)"},
      {transform:"translateX(-3px)"},{transform:"translateX(3px)"},{transform:"translateX(0)"}
    ],{duration:280});
  }
}

document.getElementById("pw-input").addEventListener("keydown", e => { if (e.key === "Enter") handleLogin(); });

function handleLogout() {
  document.getElementById("admin-app").style.display = "none";
  document.getElementById("login-screen").style.display = "flex";
  document.getElementById("pw-input").value = "";
  document.getElementById("login-error").style.display = "none";
}

/* ================================================================
   PUBLIC PAGE
================================================================ */
function showPublicPage() {
  document.getElementById("login-screen").style.display = "none";
  document.getElementById("admin-app").style.display    = "none";
  document.getElementById("public-app").style.display   = "block";
  loadAll();
  renderPublicPage();
}

function backToLogin() {
  document.getElementById("public-app").style.display  = "none";
  document.getElementById("login-screen").style.display = "flex";
}

/* ================================================================
   ADMIN PAGE NAVIGATION
================================================================ */
function switchAdminPage(page) {
  document.querySelectorAll("#admin-app .page").forEach(p => p.classList.remove("active"));
  document.getElementById("admin-page-" + page).classList.add("active");
  document.querySelectorAll("#admin-app .nav-btn").forEach(b => b.classList.remove("active"));
  document.getElementById("nav-" + page).classList.add("active");

  if (page === "inbox")     { renderInbox(); updateInboxStats(); refreshAdminInboxChart(); }
  if (page === "analytics") { refreshAnalyticsCharts(); }
}

/* ================================================================
   UTILITIES
================================================================ */
function uid() { return Date.now().toString(36) + Math.random().toString(36).slice(2); }

function escapeHtml(s) {
  if (!s) return "";
  return String(s).replace(/&/g,"&amp;").replace(/</g,"&lt;").replace(/>/g,"&gt;").replace(/"/g,"&quot;").replace(/'/g,"&#x27;");
}

function showToast(msg) {
  const t = document.getElementById("toast");
  t.textContent = msg; t.classList.add("show");
  setTimeout(() => t.classList.remove("show"), 2700);
}

function currentYM() {
  const n = new Date();
  return `${n.getFullYear()}-${String(n.getMonth()+1).padStart(2,'0')}`;
}

function currentMonthLabel() {
  return new Date().toLocaleString("default",{month:"long",year:"numeric"});
}

function lastNMonths(n) {
  const months = []; const d = new Date();
  for (let i = n-1; i >= 0; i--) {
    const m = new Date(d.getFullYear(), d.getMonth() - i, 1);
    months.push(`${m.getFullYear()}-${String(m.getMonth()+1).padStart(2,'0')}`);
  }
  return months;
}

function toYM(dateStr) { return dateStr ? dateStr.slice(0,7) : ""; }

function fmtFollowers(n) {
  if (!n && n !== 0) return "—";
  return n >= 1000000 ? (n/1000000).toFixed(1)+"M" : n >= 1000 ? (n/1000).toFixed(1)+"K" : String(n);
}

function destroyChart(key) { if (charts[key]) { charts[key].destroy(); delete charts[key]; } }

function whiteGradient(ctx, h = 220) {
  const g = ctx.createLinearGradient(0, 0, 0, h);
  g.addColorStop(0, "rgba(255,255,255,0.2)");
  g.addColorStop(1, "rgba(255,255,255,0)");
  return g;
}

const BCLS = { TikTok:"badge-tiktok", Instagram:"badge-instagram", Facebook:"badge-facebook", YouTube:"badge-youtube" };
const PLAT_COLORS = { TikTok:"#00f2ea", Instagram:"#f76a8a", Facebook:"#6a9bff", YouTube:"#ff6464" };

/* ================================================================
   MONTHLY GOALS — render goal cards
   gridId  = the goals-grid element id
   labelId = month label element id
================================================================ */
function renderGoals(gridId, labelId) {
  const grid = document.getElementById(gridId);
  const lbl  = document.getElementById(labelId);
  if (!grid) return;

  if (lbl) lbl.textContent = currentMonthLabel();

  grid.innerHTML = GOALS.map(g => {
    const current = g.getProgress();
    const pct     = Math.min(Math.round((current / g.target) * 100), 100);
    const done    = current >= g.target;

    // Status text
    const remaining = g.target - current;
    const statusText = done
      ? `✓ Goal reached!`
      : `${remaining} more to go`;

    // Bar color: green if done, goal color otherwise
    const barColor = done ? "#22c55e" : g.color;

    return `
      <div class="goal-card" style="--goal-color:${barColor}">
        <div class="goal-header">
          <span class="goal-icon">${g.icon}</span>
          <span class="goal-pct">${pct}%</span>
        </div>
        <div class="goal-title">${g.title}</div>
        <div class="goal-numbers">
          <span class="goal-current">${current}</span>
          <span class="goal-sep">/</span>
          <span class="goal-target">${g.target}</span>
          <span class="goal-unit">${g.unit}</span>
        </div>
        <div class="goal-bar-track">
          <div class="goal-bar-fill" style="width:${pct}%;background:${barColor};"></div>
        </div>
        <div class="goal-status" style="color:${done ? '#22c55e' : 'var(--text-muted)'};">${statusText}</div>
      </div>`;
  }).join("");
}

/* ================================================================
   SORT
================================================================ */
function toggleSort() {
  sortAsc = !sortAsc;
  const btn = document.getElementById("sort-btn");
  btn.textContent = sortAsc ? "↑ Oldest" : "↓ Newest";
  btn.classList.toggle("asc", sortAsc);
  renderTable();
}

/* ================================================================
   PLATFORM CHECKBOXES
================================================================ */
function syncPlat(cb) { cb.closest(".plat-label").classList.toggle("checked", cb.checked); }

function getCheckedPlats() {
  return Array.from(document.querySelectorAll("#plat-checks input:checked")).map(c => c.value);
}

function setCheckedPlats(plats = []) {
  document.querySelectorAll("#plat-checks input").forEach(cb => {
    cb.checked = plats.includes(cb.value);
    cb.closest(".plat-label").classList.toggle("checked", cb.checked);
  });
}

/* ================================================================
   ENTRY MODAL
================================================================ */
function openEntryModal(id = null) {
  editingId = id;
  document.getElementById("entry-modal").classList.add("open");
  if (id) {
    document.getElementById("modal-title").textContent = "Edit Entry";
    const e = entries.find(x => x.id === id);
    document.getElementById("f-date").value  = e.date;
    document.getElementById("f-type").value  = e.type;
    document.getElementById("f-link").value  = e.link;
    document.getElementById("f-notes").value = e.notes;
    setCheckedPlats(e.platforms || []);
  } else {
    document.getElementById("modal-title").textContent = "Add Entry";
    document.getElementById("f-date").value  = new Date().toISOString().slice(0,10);
    document.getElementById("f-type").value  = "";
    document.getElementById("f-link").value  = "";
    document.getElementById("f-notes").value = "";
    setCheckedPlats([]);
  }
}

function closeModal(id)  { document.getElementById(id).classList.remove("open"); editingId = null; }
function closeModalOnOverlay(e, id) { if (e.target === document.getElementById(id)) closeModal(id); }

function saveEntry() {
  const date      = document.getElementById("f-date").value.trim();
  const type      = document.getElementById("f-type").value;
  const link      = document.getElementById("f-link").value.trim();
  const notes     = document.getElementById("f-notes").value.trim();
  const platforms = getCheckedPlats();

  if (!date || !type || platforms.length === 0) {
    showToast("⚠️  Fill in Date, Work Type & at least one Platform."); return;
  }

  if (editingId) {
    const idx = entries.findIndex(e => e.id === editingId);
    entries[idx] = { id: editingId, date, platforms, type, link, notes };
    showToast("✏️  Entry updated.");
  } else {
    entries.push({ id: uid(), date, platforms, type, link, notes });
    showToast("✅  Entry added.");
  }

  saveEntries();
  renderTable();
  updateStats();
  renderGoals("goals-grid", "goals-month-label"); // refresh goals after adding
  closeModal("entry-modal");
}

function deleteEntry(id) {
  if (!confirm("Delete this entry?")) return;
  entries = entries.filter(e => e.id !== id);
  saveEntries(); renderTable(); updateStats();
  renderGoals("goals-grid", "goals-month-label");
  showToast("🗑️  Deleted.");
}

/* ================================================================
   RENDER TABLE
================================================================ */
function renderTable() {
  const search = document.getElementById("search-input").value.toLowerCase();
  const pfilt  = document.getElementById("filter-platform").value;
  const tfilt  = document.getElementById("filter-type").value;

  let filtered = entries.filter(e => {
    const matchP = !pfilt || (e.platforms||[]).includes(pfilt);
    const matchT = !tfilt || e.type === tfilt;
    const matchS = !search ||
      (e.notes||"").toLowerCase().includes(search) ||
      (e.link||"").toLowerCase().includes(search)  ||
      (e.platforms||[]).join(" ").toLowerCase().includes(search) ||
      (e.type||"").toLowerCase().includes(search);
    return matchP && matchT && matchS;
  });

  filtered.sort((a,b) => {
    const d = new Date(a.date) - new Date(b.date); return sortAsc ? d : -d;
  });

  const tbody = document.getElementById("entries-tbody");
  const empty = document.getElementById("empty-state");
  if (filtered.length === 0) { tbody.innerHTML = ""; empty.style.display = "block"; return; }
  empty.style.display = "none";

  tbody.innerHTML = filtered.map(e => buildEntryRow(e, true)).join("");
}

/* Reusable row builder */
function buildEntryRow(e, admin = false) {
  const badges   = (e.platforms||[]).map(p => `<span class="badge ${BCLS[p]||''}">${escapeHtml(p)}</span>`).join("");
  const linkHtml = e.link
    ? `<a class="content-link" href="${escapeHtml(e.link)}" target="_blank" rel="noopener" title="${escapeHtml(e.link)}">${escapeHtml(e.link)}</a>`
    : `<span style="color:var(--text-dim)">—</span>`;
  const actions = admin
    ? `<td><button class="btn-icon edit" onclick="openEntryModal('${e.id}')">✏️</button><button class="btn-icon del" onclick="deleteEntry('${e.id}')">🗑️</button></td>`
    : "";
  return `
    <tr>
      <td style="font-family:var(--font-m);font-size:0.75rem;color:var(--text-muted);">${escapeHtml(e.date)}</td>
      <td style="min-width:140px;">${badges||`<span style="color:var(--text-dim)">—</span>`}</td>
      <td><span class="pill">${escapeHtml(e.type)}</span></td>
      <td>${linkHtml}</td>
      <td style="color:var(--text-muted);max-width:175px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;" title="${escapeHtml(e.notes)}">${escapeHtml(e.notes)||`<span style="color:var(--text-dim)">—</span>`}</td>
      ${actions}
    </tr>`;
}

/* ================================================================
   STATS
================================================================ */
function updateStats() {
  document.getElementById("stat-total").textContent  = entries.length;
  document.getElementById("stat-tiktok").textContent = entries.filter(e=>(e.platforms||[]).includes("TikTok")).length;
  document.getElementById("stat-insta").textContent  = entries.filter(e=>(e.platforms||[]).includes("Instagram")).length;
  document.getElementById("stat-yt").textContent     = entries.filter(e=>(e.platforms||[]).includes("YouTube")).length;
  document.getElementById("stat-fb").textContent     = entries.filter(e=>(e.platforms||[]).includes("Facebook")).length;
}

/* ================================================================
   INBOX — PLATFORM TOGGLE
================================================================ */
function toggleInboxPlat(btn) {
  const p = btn.dataset.p;
  if (selectedInboxPlat === p) {
    selectedInboxPlat = null; btn.classList.remove("active");
  } else {
    selectedInboxPlat = p;
    document.querySelectorAll(".inbox-plat-btn").forEach(b => b.classList.remove("active"));
    btn.classList.add("active");
  }
}

/* ================================================================
   INBOX — IMAGE PREVIEW
================================================================ */
function previewImage(event) {
  const file = event.target.files[0]; if (!file) return;
  const reader = new FileReader();
  reader.onload = ev => {
    const img = document.getElementById("upload-preview");
    img.src = ev.target.result; img.style.display = "block";
    document.querySelector(".upload-icon").style.display = "none";
    document.querySelector(".upload-text").style.display = "none";
  };
  reader.readAsDataURL(file);
}

/* ================================================================
   INBOX — SAVE / CLEAR / DELETE
================================================================ */
function saveInboxEntry() {
  const msg = document.getElementById("inbox-msg-input").value.trim();
  const imgEl = document.getElementById("upload-preview");
  const img = imgEl.style.display === "block" ? imgEl.src : null;
  if (!msg) { showToast("⚠️  Write a message first."); return; }

  const now = new Date();
  const dateStr = now.toLocaleDateString("en-GB",{year:"numeric",month:"short",day:"numeric",hour:"2-digit",minute:"2-digit"});
  const ym = `${now.getFullYear()}-${String(now.getMonth()+1).padStart(2,'0')}`;

  inbox.unshift({ id: uid(), date: dateStr, ym, platform: selectedInboxPlat, msg, img });
  saveInbox(); renderInbox(); updateInboxStats();
  renderGoals("goals-grid", "goals-month-label"); // refresh inbox goal
  clearInboxForm();
  showToast("📥  Message saved.");
}

function clearInboxForm() {
  document.getElementById("inbox-msg-input").value = "";
  document.getElementById("inbox-img-input").value = "";
  const img = document.getElementById("upload-preview");
  img.src = ""; img.style.display = "none";
  document.querySelector(".upload-icon").style.display = "block";
  document.querySelector(".upload-text").style.display = "block";
  selectedInboxPlat = null;
  document.querySelectorAll(".inbox-plat-btn").forEach(b => b.classList.remove("active"));
}

function deleteInboxEntry(id) {
  if (!confirm("Delete this message?")) return;
  inbox = inbox.filter(e => e.id !== id);
  saveInbox(); renderInbox(); updateInboxStats();
  renderGoals("goals-grid", "goals-month-label");
  showToast("🗑️  Deleted.");
}

/* ================================================================
   INBOX — RENDER
================================================================ */
function renderInbox() {
  const list  = document.getElementById("inbox-list");
  const empty = document.getElementById("inbox-empty");
  if (inbox.length === 0) { list.innerHTML = ""; empty.style.display = "block"; return; }
  empty.style.display = "none";
  list.innerHTML = inbox.map(e => {
    const thumb = e.img
      ? `<img class="inbox-thumb" src="${e.img}" alt="evidence" onclick="openLightbox('${e.id}')" title="Enlarge"/>`
      : `<div class="inbox-thumb-empty">🖼️</div>`;
    const platBadge = e.platform ? `<span class="badge ${BCLS[e.platform]||''}">${escapeHtml(e.platform)}</span>` : "";
    return `
      <div class="inbox-card">
        ${thumb}
        <div class="inbox-body">
          <div class="inbox-meta"><span class="inbox-date">${escapeHtml(e.date)}</span>${platBadge}</div>
          <div class="inbox-msg">${escapeHtml(e.msg)}</div>
        </div>
        <button class="inbox-del" onclick="deleteInboxEntry('${e.id}')">🗑️</button>
      </div>`;
  }).join("");
}

function updateInboxStats() {
  const ym = currentYM();
  const tm = inbox.filter(e => e.ym === ym);
  document.getElementById("ib-stat-total").textContent  = tm.length;
  document.getElementById("ib-stat-tiktok").textContent = tm.filter(e=>e.platform==="TikTok").length;
  document.getElementById("ib-stat-insta").textContent  = tm.filter(e=>e.platform==="Instagram").length;
  document.getElementById("ib-stat-yt").textContent     = tm.filter(e=>e.platform==="YouTube").length;
  document.getElementById("ib-stat-fb").textContent     = tm.filter(e=>e.platform==="Facebook").length;
}

/* ================================================================
   LIGHTBOX
================================================================ */
function openLightbox(id) {
  const e = inbox.find(x => x.id === id);
  if (!e || !e.img) return;
  document.getElementById("lightbox-img").src = e.img;
  document.getElementById("lightbox").classList.add("open");
}
function closeLightbox() { document.getElementById("lightbox").classList.remove("open"); }

/* ================================================================
   FOLLOWERS
================================================================ */
function updateFollowers(platform) {
  const inputId = { youtube:"yt-follower-input", instagram:"ig-follower-input", tiktok:"tt-follower-input" }[platform];
  const val = parseInt(document.getElementById(inputId).value);
  if (!val || val < 0) { showToast("⚠️  Enter a valid count."); return; }
  const now = new Date();
  const label = `${now.toLocaleString("default",{month:"short"})} '${String(now.getFullYear()).slice(2)}`;
  followers[platform].push({ label, count: val, ts: Date.now() });
  if (followers[platform].length > 12) followers[platform] = followers[platform].slice(-12);
  saveFollowers();
  refreshFollowerDisplays("admin");
  refreshMiniCharts("admin");
  document.getElementById(inputId).value = "";
  showToast("✅  Updated!");
}

function refreshFollowerDisplays(mode) {
  const last = arr => arr.length > 0 ? fmtFollowers(arr[arr.length-1].count) : "—";
  if (mode === "admin") {
    document.getElementById("yt-follower-display").textContent = last(followers.youtube);
    document.getElementById("ig-follower-display").textContent = last(followers.instagram);
    document.getElementById("tt-follower-display").textContent = last(followers.tiktok);
  } else {
    document.getElementById("pub-yt-display").textContent = last(followers.youtube);
    document.getElementById("pub-ig-display").textContent = last(followers.instagram);
    document.getElementById("pub-tt-display").textContent = last(followers.tiktok);
  }
}

/* ================================================================
   ADMIN INBOX MONTH CHART
================================================================ */
function refreshAdminInboxChart() {
  const ym = currentYM();
  const tm = inbox.filter(e => e.ym === ym);
  const plats = ["TikTok","Instagram","YouTube","Facebook"];
  const counts = plats.map(p => tm.filter(e => e.platform === p).length);
  destroyChart("adminInboxMonth");
  const ctx = document.getElementById("inboxMonthChart");
  if (!ctx) return;
  charts.adminInboxMonth = new Chart(ctx, {
    type: "bar",
    data: {
      labels: plats,
      datasets: [{ label:"Messages", data: counts,
        backgroundColor: ["rgba(0,242,234,0.6)","rgba(247,106,138,0.6)","rgba(255,100,100,0.6)","rgba(106,155,255,0.6)"],
        borderColor:     ["#00f2ea","#f76a8a","#ff6464","#6a9bff"],
        borderWidth: 1, borderRadius: 6 }]
    },
    options: { responsive:true, maintainAspectRatio:false, plugins:{legend:{display:false}},
      scales: { x:{grid:{color:"rgba(255,255,255,0.04)"}}, y:{grid:{color:"rgba(255,255,255,0.04)"},beginAtZero:true,ticks:{precision:0}} } }
  });
}

/* ================================================================
   ANALYTICS CHARTS
================================================================ */
function refreshAnalyticsCharts() {
  const months = lastNMonths(6);
  const labels = months.map(ym => {
    const [y,m] = ym.split("-");
    return new Date(+y,+m-1).toLocaleString("default",{month:"short"});
  });

  // Content Activity
  destroyChart("contentActivity");
  const ca = document.getElementById("contentActivityChart");
  if (ca) {
    const ctx = ca.getContext("2d");
    charts.contentActivity = new Chart(ctx, {
      type: "line",
      data: { labels, datasets: [{ label:"Posts", data: months.map(ym=>entries.filter(e=>toYM(e.date)===ym).length),
        borderColor:"#fff", backgroundColor: whiteGradient(ctx), borderWidth:1.5, pointRadius:3, pointBackgroundColor:"#fff", fill:true, tension:0.4 }] },
      options: { responsive:true, maintainAspectRatio:false, plugins:{legend:{display:false}},
        scales: { x:{grid:{color:"rgba(255,255,255,0.04)"}}, y:{grid:{color:"rgba(255,255,255,0.04)"},beginAtZero:true,ticks:{precision:0}} } }
    });
  }

  // Inbox Growth
  destroyChart("inboxGrowth");
  const ig = document.getElementById("inboxGrowthChart");
  if (ig) {
    const plats = ["TikTok","Instagram","YouTube","Facebook"];
    charts.inboxGrowth = new Chart(ig, {
      type: "line",
      data: { labels, datasets: plats.map(p => ({
        label: p,
        data: months.map(ym => inbox.filter(e=>e.ym===ym&&e.platform===p).length),
        borderColor: PLAT_COLORS[p], backgroundColor:"transparent", borderWidth:1.5, pointRadius:2, tension:0.4
      })) },
      options: { responsive:true, maintainAspectRatio:false,
        plugins:{ legend:{position:"bottom",labels:{boxWidth:10,padding:12}} },
        scales: { x:{grid:{color:"rgba(255,255,255,0.04)"}}, y:{grid:{color:"rgba(255,255,255,0.04)"},beginAtZero:true,ticks:{precision:0}} } }
    });
  }

  // Platform Dist
  destroyChart("platDist");
  const pd = document.getElementById("platformDistChart");
  if (pd) {
    const plats = ["TikTok","Instagram","Facebook","YouTube"];
    charts.platDist = new Chart(pd, {
      type: "bar",
      data: { labels: plats, datasets:[{ label:"Entries",
        data: plats.map(p=>entries.filter(e=>(e.platforms||[]).includes(p)).length),
        backgroundColor: ["rgba(0,242,234,0.6)","rgba(247,106,138,0.6)","rgba(106,155,255,0.6)","rgba(255,100,100,0.6)"],
        borderColor: ["#00f2ea","#f76a8a","#6a9bff","#ff6464"],
        borderWidth:1, borderRadius:8
      }] },
      options: { responsive:true, maintainAspectRatio:false, plugins:{legend:{display:false}},
        scales: { x:{grid:{color:"rgba(255,255,255,0.04)"}}, y:{grid:{color:"rgba(255,255,255,0.04)"},beginAtZero:true,ticks:{precision:0}} } }
    });
  }

  refreshFollowerDisplays("admin");
  refreshMiniCharts("admin");
}

/* ================================================================
   MINI FOLLOWER CHARTS
================================================================ */
function refreshMiniCharts(mode) {
  const cfg = {
    admin: [
      { key:"ytGrowth",  data: followers.youtube,   color:"#ff6464", id:"ytGrowthChart" },
      { key:"igGrowth",  data: followers.instagram,  color:"#f76a8a", id:"igGrowthChart" },
      { key:"ttGrowth",  data: followers.tiktok,    color:"#00f2ea", id:"ttGrowthChart" }
    ],
    pub: [
      { key:"pubYt", data: followers.youtube,   color:"#ff6464", id:"pub-ytChart" },
      { key:"pubIg", data: followers.instagram,  color:"#f76a8a", id:"pub-igChart" },
      { key:"pubTt", data: followers.tiktok,    color:"#00f2ea", id:"pub-ttChart" }
    ]
  };

  (cfg[mode] || []).forEach(({ key, data, color, id }) => {
    destroyChart(key);
    const el = document.getElementById(id); if (!el) return;
    const ctx = el.getContext("2d");
    const g = ctx.createLinearGradient(0,0,0,75);
    g.addColorStop(0, color+"44"); g.addColorStop(1, color+"00");
    charts[key] = new Chart(ctx, {
      type:"line",
      data: {
        labels: data.map(d=>d.label),
        datasets:[{ data:data.map(d=>d.count), borderColor:color, backgroundColor:g, borderWidth:1.5, pointRadius:2, fill:true, tension:0.4 }]
      },
      options: { responsive:true, maintainAspectRatio:false,
        plugins:{legend:{display:false}, tooltip:{callbacks:{label:c=>`${c.parsed.y.toLocaleString()}`}}},
        scales:{x:{display:false},y:{display:false,beginAtZero:false}} }
    });
  });
}

/* ================================================================
   PUBLIC PAGE — render everything
================================================================ */
function renderPublicPage() {
  // Goals
  renderGoals("pub-goals-grid", "pub-goals-month-label");

  // Content stats
  document.getElementById("pub-stat-total").textContent  = entries.length;
  document.getElementById("pub-stat-tiktok").textContent = entries.filter(e=>(e.platforms||[]).includes("TikTok")).length;
  document.getElementById("pub-stat-insta").textContent  = entries.filter(e=>(e.platforms||[]).includes("Instagram")).length;
  document.getElementById("pub-stat-yt").textContent     = entries.filter(e=>(e.platforms||[]).includes("YouTube")).length;
  document.getElementById("pub-stat-fb").textContent     = entries.filter(e=>(e.platforms||[]).includes("Facebook")).length;

  // Content table
  const sorted = [...entries].sort((a,b) => new Date(b.date) - new Date(a.date));
  const tbody = document.getElementById("pub-entries-tbody");
  const empty = document.getElementById("pub-empty");
  if (sorted.length === 0) { tbody.innerHTML = ""; empty.style.display = "block"; }
  else { empty.style.display = "none"; tbody.innerHTML = sorted.map(e => buildEntryRow(e, false)).join(""); }

  // Inbox stats
  const ym = currentYM();
  const tm = inbox.filter(e => e.ym === ym);
  document.getElementById("pub-ib-total").textContent   = tm.length;
  document.getElementById("pub-ib-tiktok").textContent  = tm.filter(e=>e.platform==="TikTok").length;
  document.getElementById("pub-ib-insta").textContent   = tm.filter(e=>e.platform==="Instagram").length;
  document.getElementById("pub-ib-yt").textContent      = tm.filter(e=>e.platform==="YouTube").length;
  document.getElementById("pub-ib-fb").textContent      = tm.filter(e=>e.platform==="Facebook").length;

  // Follower displays
  refreshFollowerDisplays("pub");

  // Charts
  renderPublicCharts();
  refreshMiniCharts("pub");
}

function renderPublicCharts() {
  const months = lastNMonths(6);
  const labels = months.map(ym => {
    const [y,m] = ym.split("-");
    return new Date(+y,+m-1).toLocaleString("default",{month:"short"});
  });

  destroyChart("pubContent");
  const cc = document.getElementById("pub-contentChart");
  if (cc) {
    const ctx = cc.getContext("2d");
    charts.pubContent = new Chart(ctx, {
      type:"line",
      data: { labels, datasets:[{ label:"Posts", data:months.map(ym=>entries.filter(e=>toYM(e.date)===ym).length),
        borderColor:"#fff", backgroundColor:whiteGradient(ctx), borderWidth:1.5, pointRadius:3, pointBackgroundColor:"#fff", fill:true, tension:0.4 }] },
      options: { responsive:true, maintainAspectRatio:false, plugins:{legend:{display:false}},
        scales:{ x:{grid:{color:"rgba(255,255,255,0.04)"}}, y:{grid:{color:"rgba(255,255,255,0.04)"},beginAtZero:true,ticks:{precision:0}} } }
    });
  }

  destroyChart("pubInbox");
  const ic = document.getElementById("pub-inboxChart");
  if (ic) {
    const plats = ["TikTok","Instagram","YouTube","Facebook"];
    charts.pubInbox = new Chart(ic, {
      type:"line",
      data: { labels, datasets: plats.map(p => ({
        label:p, data:months.map(ym=>inbox.filter(e=>e.ym===ym&&e.platform===p).length),
        borderColor:PLAT_COLORS[p], backgroundColor:"transparent", borderWidth:1.5, pointRadius:2, tension:0.4
      })) },
      options: { responsive:true, maintainAspectRatio:false,
        plugins:{legend:{position:"bottom",labels:{boxWidth:10,padding:12}}},
        scales:{ x:{grid:{color:"rgba(255,255,255,0.04)"}}, y:{grid:{color:"rgba(255,255,255,0.04)"},beginAtZero:true,ticks:{precision:0}} } }
    });
  }
}
</script>
</body>
</html>
