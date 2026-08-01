<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Futur Caché — Tickets 2.5</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Space+Mono:wght@400;700&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#0A1410;
    --bg2:#0E1A15;
    --panel:#10201A;
    --panel-border:#24392E;
    --gold:#D9A94E;
    --gold-bright:#F2C868;
    --green:#34D399;
    --red:#E2564F;
    --text:#EDEAE0;
    --muted:#7C9186;
    --stitch: repeating-linear-gradient(90deg, var(--panel-border) 0 8px, transparent 8px 16px);
  }
  *{box-sizing:border-box;}
  body{
    margin:0;
    font-family:'Inter',-apple-system,sans-serif;
    background:
      radial-gradient(ellipse 900px 500px at 50% -10%, rgba(217,169,78,0.10), transparent 60%),
      radial-gradient(ellipse 700px 400px at 100% 30%, rgba(52,211,153,0.06), transparent 60%),
      var(--bg);
    color:var(--text);
    padding:18px 14px 40px;
    min-height:100vh;
  }

  /* ---- Header / hero ---- */
  header{ text-align:center; margin-bottom:20px; padding-top:6px; }
  .eyebrow{
    font-family:'Space Mono',monospace; font-size:0.7rem; letter-spacing:0.25em;
    color:var(--gold); text-transform:uppercase; opacity:0.85;
  }
  h1{
    font-family:'Bebas Neue',sans-serif;
    font-size:2.6rem; letter-spacing:0.05em; margin:2px 0 4px;
    background:linear-gradient(180deg, var(--gold-bright), var(--gold) 70%);
    -webkit-background-clip:text; background-clip:text; color:transparent;
    line-height:1;
  }
  h1 .glow{ animation:shimmer 2.8s ease-in-out 0.3s 1; background-size:200% 100%; }
  @keyframes shimmer{
    0%{ filter:brightness(1); }
    45%{ filter:brightness(1.5); }
    100%{ filter:brightness(1); }
  }
  p.sub{
    color:var(--muted); font-size:0.85rem; margin:0 auto; max-width:36ch; line-height:1.45;
  }

  /* ---- Ticket-stub cards ---- */
  .card{
    background:var(--panel);
    border:1px solid var(--panel-border);
    border-radius:14px;
    padding:18px 16px 16px;
    margin-bottom:16px;
    position:relative;
  }
  .card::before{
    content:""; position:absolute; top:0; left:16px; right:16px; height:1px;
    background:var(--stitch);
  }
  .card-label{
    font-family:'Space Mono',monospace; font-size:0.68rem; letter-spacing:0.15em;
    color:var(--gold); text-transform:uppercase; margin-bottom:12px; display:block;
  }

  .match-row{ display:flex; gap:10px; align-items:center; margin-bottom:9px; }
  .match-badge{
    width:26px; height:26px; flex-shrink:0; border-radius:50%;
    background:rgba(217,169,78,0.12); border:1px solid var(--panel-border);
    color:var(--gold-bright); font-family:'Space Mono',monospace; font-size:0.72rem;
    display:flex; align-items:center; justify-content:center;
  }
  .match-row input, .match-row select{
    flex:1; background:var(--bg2); border:1px solid var(--panel-border); color:var(--text);
    padding:9px 11px; border-radius:9px; font-size:0.88rem; font-family:'Inter',sans-serif;
  }
  .match-row input::placeholder{ color:#4d5f56; }
  .match-row select{ appearance:none; }

  #bonus-card{ border-color:rgba(217,169,78,0.35); }
  #bonus-card .match-badge{ background:rgba(217,169,78,0.22); color:var(--gold-bright); border-color:var(--gold); }

  button{
    background:linear-gradient(180deg, var(--gold-bright), var(--gold));
    color:#1a1204; border:none; border-radius:11px;
    padding:13px 16px; font-weight:700; font-size:0.92rem; cursor:pointer; width:100%;
    font-family:'Inter',sans-serif; letter-spacing:0.01em;
    box-shadow:0 4px 14px rgba(217,169,78,0.18);
  }
  button:active{ transform:translateY(1px); }
  button.secondary{
    background:var(--bg2); color:var(--text); border:1px solid var(--panel-border);
    margin-top:8px; box-shadow:none; font-weight:600;
  }
  #install-card{ display:none; padding:12px 16px; }
  #install-card button{ background:linear-gradient(180deg,#3fe5a3,var(--green)); color:#04231a; }

  /* ---- Stats / search ---- */
  .stats{
    display:flex; justify-content:space-between; align-items:center; margin-bottom:10px;
    color:var(--muted); font-size:0.78rem; font-family:'Space Mono',monospace; flex-wrap:wrap; gap:8px;
  }
  .search{
    width:100%; background:var(--bg2); border:1px solid var(--panel-border); color:var(--text);
    padding:9px 11px; border-radius:9px; margin-bottom:12px; font-size:0.88rem; font-family:'Inter',sans-serif;
  }

  /* ---- Table (receipt style) ---- */
  .table-wrap{
    max-height:58vh; overflow:auto; border:1px solid var(--panel-border); border-radius:10px;
    background:var(--bg2);
  }
  table{ width:100%; border-collapse:collapse; font-size:0.74rem; }
  thead th{
    position:sticky; top:0; background:#132720; color:var(--muted);
    padding:8px 4px; text-align:center; border-bottom:1px solid var(--panel-border);
    font-family:'Space Mono',monospace; font-weight:400; font-size:0.65rem;
    text-transform:uppercase; letter-spacing:0.04em;
  }
  tbody td{ padding:6px 3px; text-align:center; border-bottom:1px dashed var(--panel-border); }
  tbody tr:hover{ background:rgba(217,169,78,0.05); }
  .ticket-id{ color:var(--gold); font-family:'Space Mono',monospace; font-weight:700; }
  .pill{
    display:inline-block; min-width:44px; padding:2px 6px; border-radius:20px;
    font-family:'Space Mono',monospace; font-size:0.68rem; font-weight:700;
  }
  .pill.over{ background:rgba(52,211,153,0.14); color:var(--green); }
  .pill.under{ background:rgba(226,86,79,0.14); color:var(--red); }
  .banker-th{ background:rgba(217,169,78,0.14) !important; color:var(--gold-bright) !important; }
  .banker-td{
    font-family:'Space Mono',monospace; font-weight:700; color:#1a1204;
    background:linear-gradient(180deg, var(--gold-bright), var(--gold));
    border-radius:6px;
  }
  .play-th{ width:34px; }
  .play-td{ width:34px; }
  .play-check{
    width:18px; height:18px; accent-color:var(--green); cursor:pointer;
  }
  tbody tr.played{ background:rgba(52,211,153,0.06); }
  tbody tr.played td{ opacity:0.55; }
  tbody tr.played .ticket-id::after{ content:" ✓"; opacity:1; color:var(--green); }

  .progress-wrap{
    background:var(--bg2); border:1px solid var(--panel-border); border-radius:9px;
    height:8px; overflow:hidden; margin:4px 0 10px;
  }
  .progress-bar{
    height:100%; background:linear-gradient(90deg, var(--green), var(--gold)); width:0%;
    transition:width 0.3s ease;
  }
  .filter-row{ display:flex; gap:8px; margin-bottom:10px; }
  .filter-row select{
    flex:1; background:var(--bg2); border:1px solid var(--panel-border); color:var(--text);
    padding:9px 11px; border-radius:9px; font-size:0.85rem; font-family:'Inter',sans-serif;
  }
  .settings-note{
    color:var(--muted); font-size:0.74rem; line-height:1.5; margin-top:10px;
  }
  .entry-pick-row{
    display:flex; justify-content:space-between; align-items:center;
    background:var(--bg2); border:1px solid var(--panel-border); border-radius:9px;
    padding:10px 12px; font-size:0.9rem;
  }
  .entry-pick-row .m-name{ color:var(--text); }
  .entry-pick-row .m-pick{ font-family:'Space Mono',monospace; font-weight:700; }
  .entry-pick-row.banker{ border-color:var(--gold); background:rgba(217,169,78,0.1); }

  .pager{ display:flex; justify-content:space-between; align-items:center; margin-top:10px; gap:8px; }
  .pager button{ width:auto; padding:9px 16px; }
  .pager span{ color:var(--muted); font-size:0.8rem; font-family:'Space Mono',monospace; }

  .warn{
    background:rgba(226,86,79,0.08); border:1px solid rgba(226,86,79,0.3); color:#f0a29e;
    border-radius:10px; padding:11px 12px; font-size:0.76rem; margin-top:12px; line-height:1.5;
  }

  footer{ text-align:center; color:var(--muted); font-size:0.68rem; font-family:'Space Mono',monospace;
    margin-top:24px; letter-spacing:0.08em; text-transform:uppercase; opacity:0.6; }
</style>
<link rel="manifest" href="data:application/manifest+json;base64,eyJuYW1lIjogIkZ1dHVyIENhY2hcdTAwZTkiLCAic2hvcnRfbmFtZSI6ICJGdXR1ciBDYWNoXHUwMGU5IiwgImRlc2NyaXB0aW9uIjogIkdcdTAwZTluXHUwMGU5cmF0ZXVyIGRlIDEwMjQgdGlja2V0cyArMi41Ly0yLjUgYnV0cywgbGlcdTAwZTkgXHUwMGUwIHVuIDExXHUwMGU4bWUgbWF0Y2ggYmFua2VyIiwgInN0YXJ0X3VybCI6ICIuIiwgImRpc3BsYXkiOiAic3RhbmRhbG9uZSIsICJiYWNrZ3JvdW5kX2NvbG9yIjogIiMwQTE0MTAiLCAidGhlbWVfY29sb3IiOiAiIzBBMTQxMCIsICJpY29ucyI6IFt7InNyYyI6ICJkYXRhOmltYWdlL3N2Zyt4bWw7YmFzZTY0LFBITjJaeUI0Yld4dWN6MGlhSFIwY0RvdkwzZDNkeTUzTXk1dmNtY3ZNakF3TUM5emRtY2lJSGRwWkhSb1BTSTFNVElpSUdobGFXZG9kRDBpTlRFeUlqNEtQR1JsWm5NK0NqeHlZV1JwWVd4SGNtRmthV1Z1ZENCcFpEMGlaeUlnWTNnOUlqVXdKU0lnWTNrOUlqTTRKU0lnY2owaU56QWxJajRLUEhOMGIzQWdiMlptYzJWMFBTSXdKU0lnYzNSdmNDMWpiMnh2Y2owaUl6RmhNek15TnlJdlBnbzhjM1J2Y0NCdlptWnpaWFE5SWpFd01DVWlJSE4wYjNBdFkyOXNiM0k5SWlNd1lURTBNVEFpTHo0S1BDOXlZV1JwWVd4SGNtRmthV1Z1ZEQ0S1BDOWtaV1p6UGdvOGNtVmpkQ0IzYVdSMGFEMGlOVEV5SWlCb1pXbG5hSFE5SWpVeE1pSWdjbmc5SWprMklpQm1hV3hzUFNKMWNtd29JMmNwSWk4K0NqeGphWEpqYkdVZ1kzZzlJakkxTmlJZ1kzazlJakl4TUNJZ2NqMGlNVEl3SWlCbWFXeHNQU0p1YjI1bElpQnpkSEp2YTJVOUlpTkVPVUU1TkVVaUlITjBjbTlyWlMxM2FXUjBhRDBpTVRBaUlITjBjbTlyWlMxa1lYTm9ZWEp5WVhrOUlqWWdNVEFpTHo0S1BISmxZM1FnZUQwaU1UZzJJaUI1UFNJeE5UQWlJSGRwWkhSb1BTSXhOREFpSUdobGFXZG9kRDBpTVRJd0lpQnllRDBpTVRBaUlHWnBiR3c5SW01dmJtVWlJSE4wY205clpUMGlJMFl5UXpnMk9DSWdjM1J5YjJ0bExYZHBaSFJvUFNJNElpOCtDanhzYVc1bElIZ3hQU0l4T0RZaUlIa3hQU0l5TVRBaUlIZ3lQU0l6TWpZaUlIa3lQU0l5TVRBaUlITjBjbTlyWlQwaUl6TTBSRE01T1NJZ2MzUnliMnRsTFhkcFpIUm9QU0kySWlCemRISnZhMlV0WkdGemFHRnljbUY1UFNJMElEZ2lMejRLUEhSbGVIUWdlRDBpTWpVMklpQjVQU0kwTWpBaUlHWnZiblF0Wm1GdGFXeDVQU0pIWlc5eVoybGhMQ0J6WlhKcFppSWdabTl1ZEMxemFYcGxQU0kxT0NJZ1ptOXVkQzEzWldsbmFIUTlJbUp2YkdRaUlHWnBiR3c5SWlOR01rTTROamdpSUhSbGVIUXRZVzVqYUc5eVBTSnRhV1JrYkdVaUlHeGxkSFJsY2kxemNHRmphVzVuUFNJeUlqNUdRend2ZEdWNGRENEtQQzl6ZG1jKyIsICJzaXplcyI6ICI1MTJ4NTEyIiwgInR5cGUiOiAiaW1hZ2Uvc3ZnK3htbCJ9XX0=">
<link rel="icon" href="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSI1MTIiIGhlaWdodD0iNTEyIj4KPGRlZnM+CjxyYWRpYWxHcmFkaWVudCBpZD0iZyIgY3g9IjUwJSIgY3k9IjM4JSIgcj0iNzAlIj4KPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMzMyNyIvPgo8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTE0MTAiLz4KPC9yYWRpYWxHcmFkaWVudD4KPC9kZWZzPgo8cmVjdCB3aWR0aD0iNTEyIiBoZWlnaHQ9IjUxMiIgcng9Ijk2IiBmaWxsPSJ1cmwoI2cpIi8+CjxjaXJjbGUgY3g9IjI1NiIgY3k9IjIxMCIgcj0iMTIwIiBmaWxsPSJub25lIiBzdHJva2U9IiNEOUE5NEUiIHN0cm9rZS13aWR0aD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjYgMTAiLz4KPHJlY3QgeD0iMTg2IiB5PSIxNTAiIHdpZHRoPSIxNDAiIGhlaWdodD0iMTIwIiByeD0iMTAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iI0YyQzg2OCIgc3Ryb2tlLXdpZHRoPSI4Ii8+CjxsaW5lIHgxPSIxODYiIHkxPSIyMTAiIHgyPSIzMjYiIHkyPSIyMTAiIHN0cm9rZT0iIzM0RDM5OSIgc3Ryb2tlLXdpZHRoPSI2IiBzdHJva2UtZGFzaGFycmF5PSI0IDgiLz4KPHRleHQgeD0iMjU2IiB5PSI0MjAiIGZvbnQtZmFtaWx5PSJHZW9yZ2lhLCBzZXJpZiIgZm9udC1zaXplPSI1OCIgZm9udC13ZWlnaHQ9ImJvbGQiIGZpbGw9IiNGMkM4NjgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGxldHRlci1zcGFjaW5nPSIyIj5GQzwvdGV4dD4KPC9zdmc+">
<link rel="apple-touch-icon" href="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSI1MTIiIGhlaWdodD0iNTEyIj4KPGRlZnM+CjxyYWRpYWxHcmFkaWVudCBpZD0iZyIgY3g9IjUwJSIgY3k9IjM4JSIgcj0iNzAlIj4KPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMzMyNyIvPgo8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTE0MTAiLz4KPC9yYWRpYWxHcmFkaWVudD4KPC9kZWZzPgo8cmVjdCB3aWR0aD0iNTEyIiBoZWlnaHQ9IjUxMiIgcng9Ijk2IiBmaWxsPSJ1cmwoI2cpIi8+CjxjaXJjbGUgY3g9IjI1NiIgY3k9IjIxMCIgcj0iMTIwIiBmaWxsPSJub25lIiBzdHJva2U9IiNEOUE5NEUiIHN0cm9rZS13aWR0aD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjYgMTAiLz4KPHJlY3QgeD0iMTg2IiB5PSIxNTAiIHdpZHRoPSIxNDAiIGhlaWdodD0iMTIwIiByeD0iMTAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iI0YyQzg2OCIgc3Ryb2tlLXdpZHRoPSI4Ii8+CjxsaW5lIHgxPSIxODYiIHkxPSIyMTAiIHgyPSIzMjYiIHkyPSIyMTAiIHN0cm9rZT0iIzM0RDM5OSIgc3Ryb2tlLXdpZHRoPSI2IiBzdHJva2UtZGFzaGFycmF5PSI0IDgiLz4KPHRleHQgeD0iMjU2IiB5PSI0MjAiIGZvbnQtZmFtaWx5PSJHZW9yZ2lhLCBzZXJpZiIgZm9udC1zaXplPSI1OCIgZm9udC13ZWlnaHQ9ImJvbGQiIGZpbGw9IiNGMkM4NjgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGxldHRlci1zcGFjaW5nPSIyIj5GQzwvdGV4dD4KPC9zdmc+">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="Futur Caché">
<meta name="theme-color" content="#0A1410">
</head>
<body>

<div class="card" id="install-card">
  <button id="install-btn">📲 Installer Futur Caché</button>
</div>

<header>
  <div class="eyebrow">Générateur de tickets</div>
  <h1 class="glow">FUTUR&nbsp;CACHÉ</h1>
  <p class="sub">Dix matchs. Deux issues chacun. 1024 futurs possibles — révélés d'un coup, plus un pari banker qui les traverse tous.</p>
</header>

<div class="card" id="setup-card">
  <span class="card-label">01 — Les dix matchs</span>
  <div id="match-inputs"></div>
  <button id="generate-btn">Révéler les 1024 tickets</button>
</div>

<div class="card" id="bonus-card">
  <span class="card-label">02 — Le match banker</span>
  <p class="sub" style="margin:0 0 12px; max-width:none; text-align:left;">Un seul pronostic, appliqué automatiquement aux 1024 tickets.</p>
  <div class="match-row">
    <span class="match-badge">11</span>
    <input type="text" id="m10-name" placeholder="Nom du 11ème match (ex: PSG - Lens)">
  </div>
  <div class="match-row">
    <span class="match-badge">🔒</span>
    <select id="m10-pick">
      <option value="1">1 — Victoire équipe domicile</option>
      <option value="N">N — Match nul</option>
      <option value="2">2 — Victoire équipe extérieur</option>
    </select>
  </div>
</div>

<div class="card" id="results-card" style="display:none;">
  <span class="card-label">03 — Les tickets</span>
  <div class="stats">
    <span id="count-info">1024 tickets générés</span>
    <span id="filtered-info"></span>
  </div>
  <div class="progress-wrap"><div class="progress-bar" id="progress-bar"></div></div>
  <div class="stats" style="margin-top:-4px;">
    <span id="progress-info">0 / 1024 joués</span>
  </div>
  <input class="search" id="search" placeholder="Filtrer par n° ou motif (ex: OOOOOOOOOU)">
  <div class="filter-row">
    <select id="play-filter">
      <option value="all">Tous les tickets</option>
      <option value="played">Joués uniquement</option>
      <option value="unplayed">Non joués uniquement</option>
    </select>
  </div>
  <div class="table-wrap">
    <table>
      <thead><tr id="thead-row"></tr></thead>
      <tbody id="tbody"></tbody>
    </table>
  </div>
  <div class="pager">
    <button id="prev-btn" class="secondary">◀ Précédent</button>
    <span id="page-info"></span>
    <button id="next-btn" class="secondary">Suivant ▶</button>
  </div>
  <div class="warn">⚠️ Cet outil génère uniquement des combinaisons mathématiques possibles — il ne prédit aucun résultat et ne garantit aucun gain. Les paris sportifs comportent un risque financier réel : mise seulement ce que tu peux te permettre de perdre.</div>
</div>

<div class="card" id="settings-card" style="display:none;">
  <span class="card-label">⚙️ Paramètres</span>

  <div class="match-row">
    <span class="match-badge">💰</span>
    <input type="number" id="stake-input" placeholder="Mise par ticket (FCFA)" min="0" step="1">
  </div>
  <div class="stats" style="margin-bottom:14px;">
    <span id="stake-summary">Sélectionne des tickets pour voir la mise totale</span>
  </div>

  <button class="secondary" id="copy-selection-btn">📋 Copier / télécharger ma sélection (format texte)</button>
  <button id="entry-mode-btn">🎯 Mode saisie — un ticket à la fois</button>
  <button class="secondary" id="export-btn">📄 Télécharger la liste complète (CSV, avec le 11ème match)</button>
  <button class="secondary" id="export-progress-btn">✅ Exporter ma progression (tickets joués)</button>
  <label class="secondary" style="display:block; text-align:center; cursor:pointer;">
    📥 Importer une progression
    <input type="file" id="import-progress-input" accept=".json" style="display:none;">
  </label>
  <button class="secondary" id="reset-progress-btn">🗑️ Réinitialiser le suivi</button>
  <p class="settings-note">Coche les tickets que tu veux jouer dans le tableau ci-dessus : ils comptent dans la mise totale, dans la sélection à copier, et dans le mode saisie. Le suivi reste actif tant que la page est ouverte — exporte ta progression avant de fermer pour la retrouver à ta prochaine session.</p>
</div>

<div id="entry-mode-overlay" style="display:none; position:fixed; inset:0; background:var(--bg); z-index:50; padding:18px 16px; overflow-y:auto;">
  <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:16px;">
    <span class="eyebrow">Mode saisie</span>
    <button class="secondary" id="entry-close-btn" style="width:auto; padding:8px 14px;">✕ Fermer</button>
  </div>
  <div class="card" style="text-align:center;">
    <div class="card-label" id="entry-position-label">Ticket 1 / 1</div>
    <div style="font-family:'Space Mono',monospace; font-size:2.4rem; font-weight:700; color:var(--gold-bright); margin-bottom:14px;" id="entry-ticket-id">0000</div>
    <div id="entry-picks-list" style="text-align:left; display:flex; flex-direction:column; gap:8px; margin-bottom:16px;"></div>
    <div class="pager" style="margin-top:4px;">
      <button id="entry-prev-btn" class="secondary">◀ Précédent</button>
      <button id="entry-next-btn" class="secondary">Suivant ▶</button>
    </div>
  </div>
  <p class="settings-note" style="text-align:center;">Fais défiler tes tickets sélectionnés un par un pendant que tu les saisis toi-même dans l'appli du bookmaker.</p>
</div>

<footer>Futur Caché · 2¹⁰ = 1024</footer>

<script>
const N = 10;
const matchInputsDiv = document.getElementById('match-inputs');
for(let i=0;i<N;i++){
  const row = document.createElement('div');
  row.className = 'match-row';
  row.innerHTML = `<span class="match-badge">${i+1}</span><input type="text" id="m${i}" placeholder="Match ${i+1} (ex: PSG - OM)">`;
  matchInputsDiv.appendChild(row);
}

let allTickets = [];
let filteredTickets = [];
let matchNames = [];
let bankerName = '';
let bankerPick = '1';
let page = 0;
let playedSet = new Set();
let playFilter = 'all';
const PAGE_SIZE = 50;

document.getElementById('generate-btn').addEventListener('click', () => {
  matchNames = [];
  for(let i=0;i<N;i++){
    const v = document.getElementById('m' + i).value.trim();
    matchNames.push(v || `Match ${i+1}`);
  }

  bankerName = document.getElementById('m10-name').value.trim() || 'Match 11';
  bankerPick = document.getElementById('m10-pick').value;

  allTickets = [];
  const total = 1 << N; // 1024
  for(let n=0; n<total; n++){
    const picks = [];
    for(let b=0;b<N;b++){
      const bit = (n >> (N-1-b)) & 1;
      picks.push(bit === 1 ? 'O' : 'U');
    }
    allTickets.push({id: n+1, picks, code: picks.join(''), banker: bankerPick});
  }

  playedSet = new Set();
  playFilter = 'all';
  document.getElementById('play-filter').value = 'all';
  applyFilters();
  page = 0;

  buildHeader();
  document.getElementById('results-card').style.display = 'block';
  document.getElementById('settings-card').style.display = 'block';
  document.getElementById('count-info').textContent = `${allTickets.length} tickets · liés à "${bankerName}"`;
  updateProgress();
  renderPage();
  document.getElementById('results-card').scrollIntoView({behavior:'smooth', block:'start'});
});

function pad4(n){ return String(n).padStart(4,'0'); }

function buildHeader(){
  const thead = document.getElementById('thead-row');
  const bankerLabel = `${bankerName} (${bankerPick})`;
  thead.innerHTML = '<th class="play-th">✓</th><th>N°</th>' + matchNames.map(name => `<th title="${escapeHtml(name)}">${escapeHtml(shorten(name))}</th>`).join('')
    + `<th class="banker-th" title="${escapeHtml(bankerLabel)}">${escapeHtml(shorten(bankerName))}</th>`;
}

function applyFilters(){
  const q = document.getFree TV
=======

This is an M3U playlist for free TV channels around the World.

Either free locally (over the air):

[<img src="https://hatscripts.github.io/circle-flags/flags/us.svg" width="24">](lists/usa.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/ca.svg" width="24">](lists/canada.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/gb.svg" width="24">](lists/uk.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/ie.svg" width="24">](lists/ireland.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/au.svg" width="24">](lists/australia.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/in.svg" width="24">](lists/india.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/jp.svg" width="24">](lists/japan.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/cn.svg" width="24">](lists/china.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/hk.svg" width="24">](lists/hong_kong.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/mo.svg" width="24">](lists/macau.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/tw.svg" width="24">](lists/taiwan.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/kp.svg" width="24">](lists/north_korea.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/kr.svg" width="24">](lists/korea.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/dk.svg" width="24">](lists/denmark.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/fo.svg" width="24">](lists/faroe_islands.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/gl.svg" width="24">](lists/greenland.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/fi.svg" width="24">](lists/finland.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/is.svg" width="24">](lists/iceland.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/no.svg" width="24">](lists/norway.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/se.svg" width="24">](lists/sweden.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/ee.svg" width="24">](lists/estonia.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/lv.svg" width="24">](lists/latvia.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/lt.svg" width="24">](lists/lithuania.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/be.svg" width="24">](lists/belgium.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/nl.svg" width="24">](lists/netherlands.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/lu.svg" width="24">](lists/luxembourg.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/de.svg" width="24">](lists/germany.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/at.svg" width="24">](lists/austria.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/ch.svg" width="24">](lists/switzerland.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/pl.svg" width="24">](lists/poland.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/cz.svg" width="24">](lists/czech_republic.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/sk.svg" width="24">](lists/slovakia.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/hu.svg" width="24">](lists/hungary.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/ro.svg" width="24">](lists/romania.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/md.svg" width="24">](lists/moldova.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/bg.svg" width="24">](lists/bulgaria.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/fr.svg" width="24">](lists/france.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/it.svg" width="24">](lists/italy.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/pt.svg" width="24">](lists/portugal.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/es.svg" width="24">](lists/spain.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/ru.svg" width="24">](lists/russia.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/by.svg" width="24">](lists/belarus.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/ua.svg" width="24">](lists/ukraine.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/am.svg" width="24">](lists/armenia.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/az.svg" width="24">](lists/azerbaijan.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/ge.svg" width="24">](lists/georgia.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/ba.svg" width="24">](lists/bosnia_and_herzegovina.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/hr.svg" width="24">](lists/croatia.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/me.svg" width="24">](lists/montenegro.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/mk.svg" width="24">](lists/north_macedonia.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/rs.svg" width="24">](lists/serbia.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/si.svg" width="24">](lists/slovenia.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/al.svg" width="24">](lists/albania.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/xk.svg" width="24">](lists/kosovo.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/gr.svg" width="24">](lists/greece.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/cy.svg" width="24">](lists/cyprus.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/ad.svg" width="24">](lists/andorra.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/mt.svg" width="24">](lists/malta.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/mc.svg" width="24">](lists/monaco.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/sm.svg" width="24">](lists/san_marino.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/ir.svg" width="24">](lists/iran.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/iq.svg" width="24">](lists/iraq.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/il.svg" width="24">](lists/israel.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/qa.svg" width="24">](lists/qatar.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/tr.svg" width="24">](lists/turkey.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/ae.svg" width="24">](lists/united_arab_emirates.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/ar.svg" width="24">](lists/argentina.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/cr.svg" width="24">](lists/costa_rica.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/do.svg" width="24">](lists/dominican_republic.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/mx.svg" width="24">](lists/mexico.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/py.svg" width="24">](lists/paraguay.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/pe.svg" width="24">](lists/peru.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/ve.svg" width="24">](lists/venezuela.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/br.svg" width="24">](lists/brazil.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/tt.svg" width="24">](lists/trinidad.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/td.svg" width="24">](lists/chad.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/so.svg" width="24">](lists/somalia.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/id.svg" width="24">](lists/indonesia.md)
[<img src="https://hatscripts.github.io/circle-flags/flags/ke.svg" width="24">](lists/kenya.md)

Or free on the Internet:

- Plex TV
- Pluto TV (English, Spanish, French, Italian)
- Redbox Live TV
- Roku TV
- Samsung TV Plus
- Youtube live channels

To use it point your IPTV player to https://raw.githubusercontent.com/Free-TV/IPTV/master/playlist.m3u8.

Philosophy
==========

The main goals for this playlist are listed below.

**Quality over quantity**

The less channels we support the better.

- All channels should work well.
- As much as possible channels should be in HD, not SD.
- Only one URL per channel (no +1, no alternate feeds, no regional declinations)

**Only free channels**

If a channel is normally only available via commercial subscriptions it has nothing to do in this playlist. If on the other hand it is provided for free to everybody in a particular country, then it should be in this playlist.

- No paid channels
- Only channels which are officially provided for free (via DVB-S, DVB-T, analog, etc..)

**Only mainstream channels**

This is a playlist for everybody.

- No adult channels
- No channels dedicated to any particular religion
- No channels dedicated to any particular political party
- No channels made for a country and funded by a different country

Feed sources
============

It can be quite hard to find up to date URLs, here's a list of sources:

- https://github.com/iptv-org/iptv/tree/master/streams
- Youtube: As long as the channel is live and its URL doesn't change (check the age of the stream, the number of viewers..)
- Dailymotion: Same criteria as for youtube

Format
======

The m3u8 playlist is generated by `make_playlist.py`, using the `.md` files located in `lists`.

Each .md file represesnts a group. The `<h1>` line is used as the group title.

Only channels which URL column starts with `[>]` are included in the playlist.

Channels which are not in HD are marked with an `Ⓢ`.

Channels which use GeoIP blocking are marked with a `Ⓖ`.

Channels which are live Youtube channels are marked with a `Ⓨ`.

Issues
======

Only create issues for bugs and feature requests.

Do not create issues to add/edit or to remove channels. If you want to add/edit/remove channels, create a pull request directly.

Pull Requests
=============

**Only modify .md files**

If your Pull Request modifies channels, only modify .md files. Do not modify m3u8 files in your pull request.

**Adding a new Channel**

To add a new channel, make a Pull Request.

- In your Pull Request you need to provide information to show that the channel is free.
- Use imgur.com to host the channel logo and point to it.
- If you have a valid stream, add it and put `[>]` in front of it.
- If you don't have an stream for the channel, add `[x]()` in the url column and place your channel in the Invalid category.
- If you have a stream but it doesn't work well, put the channel in the Invalid category and put `[x]` in front of the url.
- If you're adding geoblocked URLs specify it in your PR and specify which country they're working in. The PR will only be merged if these URLs can be tested.

**Removing a Channel**

To remove a channel, make a Pull Request.

In your Pull Request you need to provide information to show that the channel is only available via a private paid subscription.

Note: Public taxes (whether national or regional, whether called TV License or not) do not constitute a private paid subscription.

If a stream is broken, simply move the channel to the invalid category and replace `[>]` with `[x]` in the url column.
