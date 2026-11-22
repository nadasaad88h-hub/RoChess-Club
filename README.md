<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>RoChess Club — Official Portal &amp; Club System</title>
  <style>
    :root {
      --bg: #070a10;
      --surface: #0e1420;
      --surface-2: #141d2e;
      --surface-3: #1b273d;
      --text: #f8fafc;
      --muted: #94a3b8;
      --soft: #cbd5e1;
      --accent: #7aa246;
      --accent-hover: #8ec052;
      --gold: #eab308;
      --gold-soft: rgba(234, 179, 8, 0.13);
      --emerald: #34d399;
      --emerald-soft: rgba(52, 211, 153, 0.13);
      --sky: #38bdf8;
      --sky-soft: rgba(56, 189, 248, 0.13);
      --danger: #f87171;
      --border: rgba(148, 163, 184, 0.14);
      --border-strong: rgba(148, 163, 184, 0.28);
      --radius: clamp(8px, 1vw, 12px);
      --radius-sm: clamp(6px, 0.75vw, 9px);
      --shadow: 0 14px 34px rgba(0, 0, 0, 0.48);
    }

    body.theme-white {
      --bg: #f1f5f9;
      --surface: #ffffff;
      --surface-2: #e2e8f0;
      --surface-3: #cbd5e1;
      --text: #0f172a;
      --muted: #475569;
      --soft: #1e293b;
      --border: rgba(15, 23, 42, 0.14);
      --border-strong: rgba(15, 23, 42, 0.28);
      --shadow: 0 10px 26px rgba(15, 23, 42, 0.12);
      background: linear-gradient(180deg, rgba(122, 162, 70, 0.08), transparent 220px), var(--bg);
    }

    body.theme-black-blue {
      --bg: #040811;
      --surface: #070e1c;
      --surface-2: #0b1528;
      --surface-3: #101e38;
      --text: #eef4ff;
      --muted: #7c8fb0;
      --soft: #c5d4f0;
      --border: rgba(56, 97, 168, 0.18);
      --border-strong: rgba(56, 97, 168, 0.34);
      --shadow: 0 14px 34px rgba(1, 4, 12, 0.65);
      background:
        linear-gradient(180deg, rgba(15, 35, 72, 0.28), transparent 240px),
        radial-gradient(circle at 85% 0%, rgba(18, 46, 96, 0.22), transparent 360px),
        var(--bg);
    }

    body.signed-in .guest-only {
      display: none !important;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body {
      background:
        linear-gradient(180deg, rgba(122, 162, 70, 0.06), transparent 240px),
        radial-gradient(circle at 85% 0%, rgba(56, 189, 248, 0.06), transparent 360px),
        var(--bg);
      color: var(--text);
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Inter, sans-serif;
      font-size: clamp(13px, 1vw, 15px);
      line-height: 1.48;
      min-height: 100vh;
      overflow-x: hidden;
    }

    button, input, select, textarea { font-family: inherit; color: inherit; }
    a { color: var(--emerald); text-decoration: none; }
    a:hover { text-decoration: underline; }
    code {
      background: var(--surface-3);
      border: 1px solid var(--border);
      padding: 1px 5px;
      border-radius: 5px;
      font-size: 0.9em;
    }

    .container {
      width: 100%;
      max-width: 1280px;
      margin: 0 auto;
      padding: 0 clamp(12px, 1.8vw, 24px);
    }

    header {
      position: sticky;
      top: 0;
      z-index: 40;
      background: var(--surface);
      backdrop-filter: blur(14px);
      border-bottom: 1px solid var(--border);
    }
    .header-inner {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: clamp(8px, 1vw, 14px);
      flex-wrap: wrap;
      min-height: clamp(48px, 5vw, 60px);
      padding: clamp(6px, 0.7vw, 9px) 0;
    }
    .brand {
      display: inline-flex;
      align-items: center;
      gap: 9px;
      font-weight: 800;
      font-size: clamp(0.95rem, 1.15vw, 1.1rem);
      cursor: pointer;
    }
    .brand-mark {
      width: clamp(28px, 2.5vw, 34px);
      height: clamp(28px, 2.5vw, 34px);
      border-radius: var(--radius-sm);
      background: linear-gradient(145deg, var(--surface-3), var(--surface-2));
      border: 1px solid var(--border-strong);
      display: grid;
      place-items: center;
      font-size: clamp(1rem, 1.2vw, 1.2rem);
      color: var(--gold);
    }
    .brand-sub {
      display: block;
      font-size: clamp(0.58rem, 0.68vw, 0.68rem);
      font-weight: 700;
      color: var(--muted);
      letter-spacing: 0.07em;
      text-transform: uppercase;
    }

    .nav-tabs {
      display: flex;
      align-items: center;
      gap: clamp(4px, 0.6vw, 7px);
      flex-wrap: wrap;
    }
    .nav-btn {
      background: var(--surface);
      border: 1px solid var(--border);
      color: var(--muted);
      padding: clamp(5px, 0.55vw, 7px) clamp(8px, 0.9vw, 12px);
      border-radius: var(--radius-sm);
      font-size: clamp(0.72rem, 0.84vw, 0.84rem);
      font-weight: 600;
      cursor: pointer;
      transition: all 0.15s ease;
    }
    .nav-btn:hover {
      color: var(--text);
      border-color: var(--border-strong);
      background: var(--surface-2);
    }
    .nav-btn.active {
      background: var(--accent);
      color: #070a10;
      border-color: var(--accent);
    }
    .nav-btn.locked-tab { opacity: 0.62; }

    .header-actions {
      display: flex;
      align-items: center;
      gap: 7px;
      flex-wrap: wrap;
    }
    .status-chip {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      background: var(--surface);
      border: 1px solid var(--border);
      padding: clamp(4px, 0.5vw, 6px) clamp(9px, 0.9vw, 12px);
      border-radius: 999px;
      font-size: clamp(0.7rem, 0.82vw, 0.8rem);
      color: var(--soft);
    }
    .dot {
      width: 7px;
      height: 7px;
      border-radius: 50%;
      background: var(--muted);
    }
    .dot.online { background: var(--emerald); }

    .btn {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
      padding: clamp(6px, 0.65vw, 8px) clamp(10px, 1.05vw, 14px);
      border-radius: var(--radius-sm);
      border: 1px solid transparent;
      font-size: clamp(0.75rem, 0.86vw, 0.86rem);
      font-weight: 600;
      cursor: pointer;
      transition: all 0.15s ease;
    }
    .btn-primary { background: var(--accent); color: #070a10; }
    .btn-primary:hover:not(:disabled) { background: var(--accent-hover); }
    .btn-gold { background: var(--gold); color: #070a10; }
    .btn-gold:hover:not(:disabled) { filter: brightness(1.06); }
    .btn-secondary { background: var(--surface-2); border-color: var(--border-strong); color: var(--text); }
    .btn-secondary:hover:not(:disabled) { background: var(--surface-3); }
    .btn-ghost { background: transparent; border-color: var(--border); color: var(--muted); }
    .btn-ghost:hover:not(:disabled) { color: var(--text); border-color: var(--border-strong); }
    .btn-sm {
      padding: clamp(4px, 0.5vw, 6px) clamp(8px, 0.8vw, 10px);
      font-size: clamp(0.7rem, 0.78vw, 0.78rem);
    }
    .btn:disabled { opacity: 0.45; cursor: not-allowed; }

    main { padding: clamp(10px, 1.4vw, 20px) 0 clamp(16px, 2.2vw, 30px); }
    .view { display: none; }
    .view.active { display: block; animation: fadeIn 0.16s ease; }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(3px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: clamp(12px, 1.4vw, 20px);
      box-shadow: var(--shadow);
    }
    .card + .card { margin-top: clamp(10px, 1.1vw, 16px); }

    .eyebrow {
      display: inline-block;
      font-size: clamp(0.62rem, 0.7vw, 0.7rem);
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.08em;
      color: var(--gold);
      background: var(--gold-soft);
      border: 1px solid rgba(234, 179, 8, 0.25);
      padding: 2px 8px;
      border-radius: 999px;
      margin-bottom: 6px;
    }

    h1 { font-size: clamp(1.2rem, 2vw, 1.8rem); line-height: 1.16; letter-spacing: -0.02em; margin-bottom: 6px; }
    h2 { font-size: clamp(0.96rem, 1.2vw, 1.16rem); letter-spacing: -0.01em; margin-bottom: 5px; }
    h3 { font-size: clamp(0.84rem, 0.98vw, 0.96rem); margin-bottom: 4px; }
    .muted { color: var(--muted); font-size: clamp(0.76rem, 0.9vw, 0.88rem); }
    .small { font-size: clamp(0.7rem, 0.8vw, 0.78rem); color: var(--muted); }
    .err-text { color: var(--danger); font-size: 0.75rem; margin-top: 3px; white-space: pre-wrap; word-break: break-word; }

    .grid-2 { display: grid; grid-template-columns: repeat(auto-fit, minmax(290px, 1fr)); gap: clamp(10px, 1.2vw, 16px); align-items: start; }
    .grid-3 { display: grid; grid-template-columns: repeat(auto-fit, minmax(205px, 1fr)); gap: clamp(8px, 1vw, 12px); }
    .grid-4 { display: grid; grid-template-columns: repeat(auto-fit, minmax(125px, 1fr)); gap: clamp(7px, 0.85vw, 10px); }

    .hero {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(310px, 1fr));
      gap: clamp(10px, 1.2vw, 16px);
      margin-bottom: clamp(10px, 1.2vw, 16px);
    }
    .hero-main {
      background: linear-gradient(155deg, rgba(122, 162, 70, 0.12), var(--surface) 52%), var(--surface);
      border: 1px solid var(--border-strong);
      border-radius: var(--radius);
      padding: clamp(14px, 1.6vw, 22px);
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      gap: clamp(10px, 1.2vw, 16px);
      box-shadow: var(--shadow);
    }
    .hero-actions { display: flex; gap: 8px; flex-wrap: wrap; }

    .kpi-box {
      background: var(--surface-2);
      border: 1px solid var(--border);
      border-radius: var(--radius-sm);
      padding: clamp(8px, 0.9vw, 12px);
    }
    .kpi-val { font-size: clamp(0.95rem, 1.25vw, 1.2rem); font-weight: 800; }
    .kpi-lbl { font-size: clamp(0.6rem, 0.68vw, 0.68rem); color: var(--muted); text-transform: uppercase; letter-spacing: 0.05em; }

    .meta-list { display: grid; gap: 6px; margin: 8px 0; }
    .meta-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 8px;
      flex-wrap: wrap;
      padding: clamp(6px, 0.65vw, 8px) clamp(9px, 0.9vw, 12px);
      background: var(--surface-2);
      border: 1px solid var(--border);
      border-radius: var(--radius-sm);
      font-size: clamp(0.72rem, 0.84vw, 0.82rem);
    }

    .field { display: flex; flex-direction: column; gap: 4px; margin-bottom: 9px; }
    .field label { font-size: clamp(0.72rem, 0.82vw, 0.8rem); font-weight: 600; color: var(--soft); }
    .field input, .field select, .field textarea {
      background: var(--surface-2);
      border: 1px solid var(--border);
      border-radius: var(--radius-sm);
      padding: clamp(6px, 0.7vw, 9px) clamp(9px, 0.9vw, 11px);
      font-size: clamp(0.76rem, 0.86vw, 0.86rem);
      width: 100%;
    }
    .field input:focus, .field select:focus, .field textarea:focus {
      outline: none;
      border-color: var(--accent);
    }
    .field textarea { min-height: 58px; resize: vertical; }

    .pay-panel {
      background: var(--surface-2);
      border: 1px solid var(--border-strong);
      border-radius: var(--radius-sm);
      padding: 10px;
      margin-bottom: 9px;
    }

    .plan-card, .box-item {
      background: var(--surface-2);
      border: 1px solid var(--border);
      border-radius: var(--radius-sm);
      padding: clamp(9px, 1vw, 12px);
    }
    .box-item + .box-item { margin-top: 7px; }
    .price { font-size: clamp(1.02rem, 1.3vw, 1.25rem); font-weight: 800; color: var(--gold); margin: 3px 0; }
    .row-between {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 8px;
      flex-wrap: wrap;
    }
    .badge {
      display: inline-block;
      padding: 2px 7px;
      border-radius: 999px;
      font-size: clamp(0.64rem, 0.74vw, 0.72rem);
      font-weight: 700;
      background: var(--surface-3);
      border: 1px solid var(--border);
      color: var(--soft);
    }
    .badge-ok {
      background: var(--emerald-soft);
      border-color: rgba(52, 211, 153, 0.35);
      color: var(--emerald);
    }
    .badge-info {
      background: var(--sky-soft);
      border-color: rgba(56, 189, 248, 0.35);
      color: var(--sky);
    }
    .badge-warn {
      background: var(--gold-soft);
      border-color: rgba(234, 179, 8, 0.35);
      color: var(--gold);
    }
    .badge-danger {
      background: rgba(248, 113, 113, 0.14);
      border-color: rgba(248, 113, 113, 0.35);
      color: var(--danger);
    }

    .dm-feed {
      max-height: clamp(140px, 22vh, 210px);
      overflow-y: auto;
      background: var(--surface-2);
      border: 1px solid var(--border);
      border-radius: var(--radius-sm);
      padding: 8px 10px;
      margin-bottom: 9px;
      display: flex;
      flex-direction: column;
      gap: 6px;
    }
    .dm-msg {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius-sm);
      padding: 7px 9px;
      font-size: clamp(0.74rem, 0.84vw, 0.82rem);
    }

    .announce-img {
      max-width: 100%;
      max-height: 280px;
      border-radius: var(--radius-sm);
      border: 1px solid var(--border);
      object-fit: contain;
      background: var(--bg);
      margin-top: 6px;
    }
    .attach-chip {
      display: inline-flex;
      align-items: center;
      gap: 5px;
      padding: 4px 9px;
      border-radius: var(--radius-sm);
      background: var(--surface);
      border: 1px solid var(--border-strong);
      font-size: 0.76rem;
      color: var(--sky);
      margin-top: 6px;
    }

    .clock-bar {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 8px;
      margin-bottom: 8px;
    }
    .clock-box {
      background: var(--surface-2);
      border: 1px solid var(--border);
      border-radius: var(--radius-sm);
      padding: 7px 10px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 8px;
    }
    .clock-box.active-clock {
      border-color: var(--gold);
      box-shadow: inset 0 0 0 1px rgba(234, 179, 8, 0.35);
    }
    .clock-time {
      font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
      font-size: 0.96rem;
      font-weight: 800;
      color: var(--text);
    }

    /* Realistic Chess Board & Coordinates */
    .board-wrap {
      display: block;
      background: #1b1d1c;
      border: 2px solid var(--border-strong);
      border-radius: var(--radius-sm);
      padding: 8px;
      max-width: 420px;
      width: 100%;
    }
    .board-grid-row {
      display: grid;
      grid-template-columns: 20px 1fr;
      align-items: stretch;
    }
    .rank-labels {
      display: grid;
      grid-template-rows: repeat(8, 1fr);
      place-items: center;
      font-size: 0.75rem;
      font-weight: 700;
      color: #cbd5e1;
      padding-right: 4px;
      user-select: none;
    }
    .board {
      display: grid;
      grid-template-columns: repeat(8, 1fr);
      grid-template-rows: repeat(8, 1fr);
      aspect-ratio: 1 / 1;
      width: 100%;
      border-radius: 4px;
      overflow: hidden;
      border: 1px solid rgba(0, 0, 0, 0.5);
    }
    .file-labels {
      display: grid;
      grid-template-columns: repeat(8, 1fr);
      padding-left: 20px;
      padding-top: 5px;
      font-size: 0.75rem;
      font-weight: 700;
      color: #cbd5e1;
      user-select: none;
    }
    .file-labels span { text-align: center; }

    .sq {
      position: relative;
      display: flex;
      align-items: center;
      justify-content: center;
      width: 100%;
      height: 100%;
      padding: 6%;
      cursor: pointer;
      user-select: none;
      border: none;
      background: transparent;
      transition: filter 0.12s ease;
    }
    .sq svg {
      width: 100%;
      height: 100%;
      display: block;
      overflow: visible;
      position: relative;
      z-index: 2;
    }
    .sq.legal-dot::after {
      content: "";
      position: absolute;
      width: 28%;
      height: 28%;
      border-radius: 50%;
      background: rgba(15, 23, 42, 0.36);
      z-index: 1;
      pointer-events: none;
    }
    .sq.legal-capture::after {
      content: "";
      position: absolute;
      inset: 8%;
      border-radius: 50%;
      border: 3px solid rgba(220, 38, 38, 0.65);
      z-index: 1;
      pointer-events: none;
    }

    .cap-line {
      display: inline-flex;
      align-items: center;
      flex-wrap: wrap;
      gap: 4px;
      vertical-align: middle;
    }
    .cap-piece-svg {
      width: 20px;
      height: 20px;
      display: inline-block;
      vertical-align: middle;
    }

    .board.mat-classic .sq.light { background: #edeed1; }
    .board.mat-classic .sq.dark { background: #779952; }
    .board.mat-walnut .sq.light { background: repeating-linear-gradient(12deg, #deb887 0px, #d5ab76 6px, #e3bf91 12px); }
    .board.mat-walnut .sq.dark { background: repeating-linear-gradient(12deg, #6b3e26 0px, #5e351f 6px, #75442a 12px); }
    .board.mat-mahogany .sq.light { background: repeating-linear-gradient(88deg, #f3d5a5 0px, #ebd09e 5px, #f7ddb0 10px); }
    .board.mat-mahogany .sq.dark { background: repeating-linear-gradient(88deg, #7c2d12 0px, #6c250e 5px, #883316 10px); }
    .board.mat-slate .sq.light { background: #dce6f1; }
    .board.mat-slate .sq.dark { background: #3b526b; }
    .board.mat-obsidian .sq.light { background: #d8dee9; }
    .board.mat-obsidian .sq.dark { background: #1e293b; }

    .sq.selected { box-shadow: inset 0 0 0 3px #facc15; filter: brightness(1.06); }
    .sq.in-check { box-shadow: inset 0 0 0 3px #ef4444; background: rgba(239, 68, 68, 0.35) !important; }
    .custom-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 8px; margin-top: 8px; }

    .gate-card {
      background: var(--surface);
      border: 1px solid var(--border-strong);
      border-radius: var(--radius);
      padding: clamp(16px, 2vw, 24px);
      text-align: center;
      max-width: 560px;
      margin: clamp(12px, 2vw, 24px) auto;
      box-shadow: var(--shadow);
    }

    details {
      background: var(--surface-2);
      border: 1px solid var(--border);
      border-radius: var(--radius-sm);
      padding: clamp(7px, 0.8vw, 10px);
    }
    details + details { margin-top: 6px; }
    summary { cursor: pointer; font-weight: 700; font-size: clamp(0.76rem, 0.86vw, 0.84rem); color: var(--text); }
    details p { margin-top: 4px; font-size: clamp(0.72rem, 0.82vw, 0.78rem); color: var(--muted); }

    .monitor-bar {
      background: var(--surface);
      border-top: 1px solid var(--border);
      padding: clamp(7px, 0.8vw, 10px) 0 clamp(10px, 1.2vw, 14px);
    }
    .monitor-log {
      margin-top: 5px;
      max-height: clamp(95px, 16vh, 140px);
      overflow-y: auto;
      background: var(--surface-2);
      border: 1px solid var(--border);
      border-radius: var(--radius-sm);
      padding: 6px 9px;
      font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
      font-size: clamp(0.66rem, 0.76vw, 0.74rem);
      color: var(--soft);
      white-space: pre-wrap;
      word-break: break-word;
    }

    .modal-backdrop {
      position: fixed;
      inset: 0;
      background: rgba(0, 0, 0, 0.78);
      backdrop-filter: blur(6px);
      display: none;
      align-items: center;
      justify-content: center;
      padding: 14px;
      z-index: 60;
    }
    .modal-backdrop.open { display: flex; }
    .modal-card {
      width: 100%;
      max-width: 470px;
      max-height: 92vh;
      overflow-y: auto;
      background: var(--surface);
      border: 1px solid var(--border-strong);
      border-radius: var(--radius);
      padding: clamp(14px, 1.8vw, 22px);
      box-shadow: var(--shadow);
    }

    .toast {
      position: fixed;
      bottom: 14px;
      right: 14px;
      background: var(--surface-2);
      border: 1px solid var(--accent);
      color: var(--text);
      padding: 8px 13px;
      border-radius: var(--radius-sm);
      font-size: clamp(0.74rem, 0.85vw, 0.82rem);
      font-weight: 600;
      box-shadow: var(--shadow);
      opacity: 0;
      transform: translateY(8px);
      transition: all 0.2s ease;
      pointer-events: none;
      z-index: 80;
    }
    .toast.show { opacity: 1; transform: translateY(0); }
  </style>
</head>
<body>
  <header>
    <div class="container header-inner">
      <div class="brand" id="brand-home">
        <div class="brand-mark">♔</div>
        <div>
          RoChess Club
          <span class="brand-sub">Official Club &amp; Tournament System</span>
        </div>
      </div>

      <nav class="nav-tabs" aria-label="Primary Navigation">
        <button class="nav-btn active" data-view="lobby">Club Lobby</button>
        <button class="nav-btn" data-view="memberships">Memberships</button>
        <button class="nav-btn locked-tab" data-view="chess-tournaments" data-auth-only="true">1v1 &amp; Tournaments</button>
        <button class="nav-btn locked-tab" data-view="puzzles" data-auth-only="true">Tactics Trainer</button>
        <button class="nav-btn locked-tab" data-view="announcements" data-auth-only="true">Announcements</button>
        <button class="nav-btn locked-tab" data-view="mgmt-dm" data-auth-only="true">Requests &amp; Mgmt DMs</button>
        <button class="nav-btn locked-tab" data-view="standings" data-auth-only="true">Standings &amp; Status</button>
      </nav>

      <div class="header-actions">
        <button class="btn btn-ghost btn-sm" id="sound-toggle-btn" title="Toggle Chess Sound Effects">🔊 Sound On</button>
        <span class="status-chip" id="header-session-chip">
          <span class="dot" id="header-dot"></span>
          <span id="header-session-text">Guest Mode</span>
        </span>
        <button class="btn btn-primary btn-sm guest-only" id="header-auth-btn">Sign In with Discord</button>
        <button class="btn btn-secondary btn-sm member-only" id="header-profile-btn" style="display: none;">Profile</button>
      </div>
    </div>
  </header>

  <main class="container">
    <!-- CLUB LOBBY -->
    <section id="view-lobby" class="view active">
      <div class="hero">
        <div class="hero-main">
          <div>
            <span class="eyebrow">RoChess Club • Discord Member System</span>
            <h1>Competitive Chess, Verified Discord Accounts &amp; Whop Club Passes</h1>
            <p class="muted" style="max-width: 68ch;">
              <strong>RoChess Club</strong> coordinates organized tournaments, full-rules 1v1 matches with 10-minute clocks, tactical drills,
              governance requests, and verified memberships. Sign up with your <strong>Discord</strong> account,
              confirm your DM verification code, and route membership checkouts through your backend to Whop.
            </p>
          </div>

          <div class="grid-4">
            <div class="kpi-box">
              <div class="kpi-val">$1.99+</div>
              <div class="kpi-lbl">Starting Tier</div>
            </div>
            <div class="kpi-box">
              <div class="kpi-val">10:00</div>
              <div class="kpi-lbl">1v1 Clock / Side</div>
            </div>
            <div class="kpi-box">
              <div class="kpi-val">+8 / -8</div>
              <div class="kpi-lbl">Win / Loss ELO</div>
            </div>
            <div class="kpi-box">
              <div class="kpi-val">6,000 : 1</div>
              <div class="kpi-lbl">Çess per Token</div>
            </div>
          </div>

          <div class="hero-actions">
            <a class="btn btn-gold" id="join-server-btn" href="https://discord.gg/pVYUX5ahPc" target="_blank" rel="noopener noreferrer">
              Join RoChess Server
            </a>
            <button class="btn btn-primary guest-only" id="lobby-signin-btn">Sign In with Discord</button>
            <button class="btn btn-secondary" data-jump-view="memberships">Browse Memberships</button>
          </div>
        </div>

        <div class="card">
          <span class="eyebrow">Server &amp; Account Sync</span>
          <h2>RoChess Club Connection</h2>
          <p class="small">Club server details and Discord DM verification flow:</p>

          <div class="meta-list">
            <div class="meta-row">
              <span class="muted">Discord Invite</span>
              <a href="https://discord.gg/pVYUX5ahPc" target="_blank" rel="noopener noreferrer">discord.gg/pVYUX5ahPc</a>
            </div>
            <div class="meta-row">
              <span class="muted">Main Guild ID</span>
              <code>1563916314790072403</code>
            </div>
            <div class="meta-row">
              <span class="muted">Backend API</span>
              <code id="lobby-api-url">https://rochesswispuno.wispbyte.app</code>
            </div>
            <div class="meta-row">
              <span class="muted">New Member Plans</span>
              <span>$1.99 Mo · $5.99 Yr · $8.99 Perm</span>
            </div>
            <div class="meta-row">
              <span class="muted">Renewal Plans</span>
              <span>$2.49 Mo · $6.49 Yr</span>
            </div>
            <div class="meta-row">
              <span class="muted">Whop Destination</span>
              <code id="lobby-whop-dest">rochess-club</code>
            </div>
          </div>

          <div class="box-item" id="lobby-account-box">
            <div class="row-between">
              <strong id="lobby-account-title">Guest Mode (Unverified)</strong>
              <span class="badge" id="lobby-account-badge">Guest</span>
            </div>
            <p class="small" id="lobby-account-desc" style="margin-top: 4px;">
              Sign up with your Discord username to check server membership and receive a 6-digit code in Discord DMs.
            </p>
            <div id="lobby-account-meta" class="small" style="margin-top: 4px;"></div>
            <div style="margin-top: 8px; display: flex; gap: 6px; flex-wrap: wrap;" id="lobby-account-actions">
              <button class="btn btn-primary btn-sm guest-only" id="lobby-card-signin-btn">Sign In with Discord</button>
            </div>
          </div>
        </div>
      </div>

      <div class="grid-2">
        <div class="card">
          <h2>Public Schedule &amp; Club Highlights</h2>
          <p class="small" style="margin-bottom: 7px;">Upcoming club events visible to visitors. Sign in to register or host.</p>
          <div id="public-schedule-list"></div>
        </div>

        <div class="card">
          <h2>1v1 Challenge, ELO &amp; Rules</h2>
          <details open>
            <summary>How do 1v1 user challenges &amp; cooldowns work?</summary>
            <p>Click <strong>1v1 User</strong> in the chess section and enter the target Discord user. A Discord DM embed with <strong>Challenge</strong> and <strong>Deny</strong> buttons is sent with a <strong>3-minute</strong> response window (if unanswered after 3 reminders/minutes, it counts as denied). Challenge requests have a <strong>5-minute</strong> cooldown per target user stored on the backend by user ID so clearing or re-uploading the website cannot bypass it.</p>
          </details>
          <details>
            <summary>How do 10-minute clocks, ELO changes &amp; draws work?</summary>
            <p>Each side gets <strong>10:00</strong> on their clock (White moves first). Winning or opponent flag/loss gives <strong>+8 ELO</strong> to the winner and <strong>-8 ELO</strong> to the loser. Both players agreeing to a draw gives <strong>0 ELO</strong> change. <strong>Stalemate</strong>, <strong>threefold repetition</strong>, or <strong>only two kings remaining</strong> counts as a draw with <strong>-1 ELO</strong> to each user.</p>
          </details>
          <details>
            <summary>Are all chess rules enforced?</summary>
            <p>Yes: legal piece movement, self-check blocking, check detection, checkmate, stalemate, en passant, castling (kingside &amp; queenside), pawn promotion, and repetition/insufficient-material draw detection.</p>
          </details>
        </div>
      </div>
    </section>

    <!-- MEMBERSHIPS VIEW -->
    <section id="view-memberships" class="view">
      <div class="grid-2">
        <div class="card">
          <div class="row-between" style="margin-bottom: 6px;">
            <div>
              <span class="eyebrow" style="margin-bottom: 3px;">Club Membership Tiers</span>
              <h1 id="membership-heading" style="margin: 0;">RoChess Club Memberships</h1>
            </div>
            <span class="badge" id="membership-mode-badge">Standard Plans</span>
          </div>
          <p class="muted" id="membership-subtitle" style="margin-bottom: 10px;">
            Browse tiers anytime. Sign in with Discord first before submitting payment details to Whop.
          </p>
          <div id="membership-status-banner" class="box-item" style="display: none; margin-bottom: 10px;"></div>
          <div class="grid-3" id="membership-list"></div>
        </div>

        <div class="card">
          <div class="row-between" style="margin-bottom: 6px;">
            <h2 style="margin: 0;">Membership Cart &amp; Whop Checkout</h2>
            <span class="badge" id="checkout-auth-badge">Discord Sign-In Required</span>
          </div>

          <div id="checkout-lock-banner" class="box-item guest-only" style="margin-bottom: 9px;">
            <div class="row-between">
              <strong style="color: var(--gold);">Discord Sign-In Required</strong>
              <button class="btn btn-primary btn-sm guest-only" id="checkout-signin-btn">Sign In Now</button>
            </div>
            <p class="small" style="margin-top: 3px;">
              Sign in with your verified Discord account first so your order links to your profile before sending payment details to Whop.
            </p>
          </div>

          <div id="cart-items"></div>

          <div class="field" style="margin-top: 9px;">
            <label for="pay-method">Payment Method (Forwards via Backend to Whop)</label>
            <select id="pay-method">
              <option value="Debit">Debit Card</option>
              <option value="Apple">Apple Pay</option>
              <option value="Play Store">Play Store (Google Play)</option>
            </select>
          </div>

          <div id="pay-fields-debit" class="pay-panel">
            <div class="row-between" style="margin-bottom: 6px;">
              <strong>Debit Card Details</strong>
              <span class="badge badge-info">Whop Card Route</span>
            </div>
            <div class="field">
              <label for="debit-name">Cardholder Name</label>
              <input id="debit-name" type="text" placeholder="Full name on card" />
            </div>
            <div class="field">
              <label for="debit-number">Debit Card Number</label>
              <input id="debit-number" type="text" inputmode="numeric" maxlength="23" placeholder="1234 5678 1234 5678" />
            </div>
            <div class="grid-2">
              <div class="field" style="margin-bottom: 0;">
                <label for="debit-exp">Expiry (MM/YY)</label>
                <input id="debit-exp" type="text" inputmode="numeric" maxlength="5" placeholder="08/28" />
              </div>
              <div class="field" style="margin-bottom: 0;">
                <label for="debit-cvc">Security Code (CVC)</label>
                <input id="debit-cvc" type="password" inputmode="numeric" maxlength="4" placeholder="123" />
              </div>
            </div>
          </div>

          <div id="pay-fields-apple" class="pay-panel" style="display: none;">
            <div class="row-between" style="margin-bottom: 6px;">
              <strong>Apple Pay Details</strong>
              <span class="badge badge-info">Whop Apple Pay Route</span>
            </div>
            <div class="field">
              <label for="apple-email">Apple ID / Billing Email</label>
              <input id="apple-email" type="email" placeholder="member@icloud.com" />
            </div>
            <div class="field" style="margin-bottom: 0;">
              <label for="apple-device-tag">Apple Pay Pass / Wallet Label</label>
              <input id="apple-device-tag" type="text" placeholder="e.g. iPhone Apple Pay Debit" />
            </div>
          </div>

          <div id="pay-fields-play" class="pay-panel" style="display: none;">
            <div class="row-between" style="margin-bottom: 6px;">
              <strong>Play Store (Google Play) Details</strong>
              <span class="badge badge-info">Whop Play Route</span>
            </div>
            <div class="field">
              <label for="play-email">Google Play Account Email</label>
              <input id="play-email" type="email" placeholder="member@gmail.com" />
            </div>
            <div class="field" style="margin-bottom: 0;">
              <label for="play-token">Play Billing Receipt / Account Tag</label>
              <input id="play-token" type="text" placeholder="e.g. GPA-1234-5678" />
            </div>
          </div>

          <div class="field">
            <label for="pay-proof">Whop / Transaction Reference Note (Optional)</label>
            <input id="pay-proof" type="text" placeholder="Optional note for Whop dispatch" />
          </div>

          <div id="checkout-error" class="err-text" style="margin-bottom: 6px;"></div>

          <div class="row-between" style="margin: 7px 0;">
            <span class="muted">Order Total</span>
            <strong id="cart-total" class="price" style="margin: 0;">$0.00</strong>
          </div>

          <button class="btn btn-gold" id="checkout-btn" style="width: 100%;" disabled>Sign In First to Submit to Whop</button>

          <div style="margin-top: 12px;">
            <h3>Whop Order &amp; Dispatch Log</h3>
            <div id="orders-log" class="small" style="margin-top: 5px;">No Whop orders submitted yet.</div>
          </div>
        </div>
      </div>
    </section>

    <!-- SIGNED-IN ONLY VIEWS -->
    <section id="view-chess-tournaments" class="view"></section>
    <section id="view-puzzles" class="view"></section>
    <section id="view-announcements" class="view"></section>
    <section id="view-mgmt-dm" class="view"></section>
    <section id="view-standings" class="view"></section>
  </main>

  <!-- SERVER / BOT CONSOLE & ERROR BRIDGE MONITOR -->
  <div class="monitor-bar">
    <div class="container">
      <div class="row-between">
        <div class="row-between" style="gap: 6px;">
          <strong class="small" style="color: var(--text);">Server &amp; Error Bridge:</strong>
          <span class="badge" id="bridge-status-badge">Checking /api/rochess/log</span>
        </div>
        <div style="display: flex; gap: 6px; flex-wrap: wrap;">
          <button class="btn btn-secondary btn-sm" id="copy-log-btn">Copy Log</button>
          <button class="btn btn-ghost btn-sm" id="test-server-log-btn">Test Server Log</button>
          <button class="btn btn-ghost btn-sm" id="clear-monitor-btn">Clear Log</button>
        </div>
      </div>
      <div class="monitor-log" id="monitor-log">Initializing error &amp; event bridge...</div>
    </div>
  </div>

  <!-- 1V1 USER CHALLENGE MODAL -->
  <div class="modal-backdrop" id="challenge-modal" role="dialog" aria-modal="true" aria-labelledby="challenge-modal-title">
    <div class="modal-card">
      <div class="row-between" style="margin-bottom: 6px;">
        <h2 id="challenge-modal-title" style="margin: 0;">1v1 User Challenge</h2>
        <button class="btn btn-ghost btn-sm" id="close-challenge-modal">Close</button>
      </div>
      <p class="small" style="margin-bottom: 10px;">
        Send a 1v1 chess challenge via Discord DM embed with <strong>Challenge</strong> and <strong>Deny</strong> buttons.
        3-minute response window (3 reminders before auto-deny) and a <strong>5-minute</strong> per-user cooldown tracked by user on the backend.
      </p>

      <div class="field">
        <label for="challenge-target-input">Target Discord Username or ID *</label>
        <input id="challenge-target-input" type="text" placeholder="e.g. opponent_handle or 123456789012345678" />
      </div>

      <div class="box-item" id="challenge-status-box" style="margin-bottom: 10px;">
        <div class="small">Ready to send challenge. White always moves first once accepted.</div>
      </div>

      <div id="challenge-error-msg" class="err-text" style="margin-bottom: 8px;"></div>

      <div class="row-between">
        <button class="btn btn-gold" id="send-1v1-challenge-btn">Send Discord Challenge</button>
        <button class="btn btn-ghost btn-sm" id="cancel-challenge-btn">Cancel</button>
      </div>
    </div>
  </div>

  <!-- PROFILE SUMMARY MODAL -->
  <div class="modal-backdrop" id="profile-modal" role="dialog" aria-modal="true" aria-labelledby="profile-modal-title">
    <div class="modal-card">
      <div class="row-between" style="margin-bottom: 8px;">
        <h2 id="profile-modal-title" style="margin: 0;">Verified Discord Member</h2>
        <button class="btn btn-ghost btn-sm" id="close-profile-modal">Close</button>
      </div>
      <div id="profile-modal-body" class="box-item" style="margin-bottom: 12px;"></div>
      <div class="row-between">
        <button class="btn btn-secondary btn-sm" id="open-reverify-btn">Re-Verify / Edit Username</button>
        <button class="btn btn-ghost btn-sm" id="profile-signout-btn">Sign Out</button>
      </div>
    </div>
  </div>

  <!-- DISCORD SIGN-UP / VERIFY MODAL -->
  <div class="modal-backdrop" id="auth-modal" role="dialog" aria-modal="true" aria-labelledby="auth-modal-title">
    <div class="modal-card">
      <div class="row-between" style="margin-bottom: 6px;">
        <h2 id="auth-modal-title" style="margin: 0;">Discord Sign-Up &amp; DM Code</h2>
        <button class="btn btn-ghost btn-sm" id="close-auth-modal">Close</button>
      </div>
      <p class="small" style="margin-bottom: 10px;">
        Enter your Discord username. The bot checks if you are in the server first and sends a 6-digit code in a Discord DM embed.
      </p>

      <div class="field">
        <label for="auth-handle">Discord Username *</label>
        <input id="auth-handle" type="text" placeholder="e.g. unbreakilo" />
      </div>

      <div class="field">
        <label for="auth-discord-id">Discord User ID (Optional — Helps Exact Server Lookup)</label>
        <input id="auth-discord-id" type="text" inputmode="numeric" placeholder="e.g. 1390750820953231381" />
      </div>

      <div class="pay-panel">
        <div class="row-between" style="margin-bottom: 6px;">
          <strong>Discord DM Verification</strong>
          <button type="button" class="btn btn-secondary btn-sm" id="send-proof-code-btn">Send Code</button>
        </div>
        <div id="proof-dispatch-status" class="small" style="margin-bottom: 6px;">
          Enter your Discord username and click <strong>Send Code</strong>.
        </div>
        <div class="field" style="margin-bottom: 0;">
          <label for="auth-proof-input">Enter 6-Digit Code from Discord DM *</label>
          <input id="auth-proof-input" type="text" inputmode="numeric" maxlength="6" placeholder="6-digit code from DM embed" />
        </div>
      </div>

      <div id="auth-error-msg" class="err-text" style="margin-bottom: 8px;"></div>

      <div class="row-between" style="margin-top: 10px;">
        <button class="btn btn-primary" id="submit-signin-btn">Verify &amp; Sign In</button>
        <button class="btn btn-ghost btn-sm" id="signout-btn">Sign Out</button>
      </div>
    </div>
  </div>

  <div class="toast" id="toast" role="status" aria-live="polite"></div>

  <script>
    const API_BASE_URL = 'https://rochesswispuno.wispbyte.app';
    const ACTIVE_VIEW_STORAGE_KEY = 'rochess_active_view';
    const OWNER_DISCORD_ID = '1390750820953231381';
    const DEVICE_STORAGE_KEY = 'rochess_device_v1';
    const ANNOUNCEMENTS_STORAGE_KEY = 'rochess_site_announcements_v1';
    const SOUND_PREF_KEY = 'rochess_sound_enabled_v1';

    function apiUrl(path) {
      const base = String(API_BASE_URL || '').trim().replace(/\/+$/, '');
      return base ? `${base}${path}` : path;
    }

    const CLUB_CONFIG = {
      DISCORD_INVITE_URL: 'https://discord.gg/pVYUX5ahPc',
      MAIN_GUILD_ID: '1563916314790072403',
      MANAGEMENT_ROLE_IDS: [
        '1563922003008692244',
        '1563919061203816580',
        '1565240522237550612',
        '1565241085389701191'
      ],
      ENTERTAINMENT_ROLE_IDS: [
        '1565324754846752798',
        '1565349575898960003'
      ],
      HOST_EVENT_ROLE_ID: '1565324754846752798',
      SUBSCRIBER_ROLE_ID: '1568268164309983264',
      WHOP_DESTINATION_ACCOUNT: 'rochess-club',
      CHESS_PER_TOKEN: 6000,
      DEFAULT_ELO: 1200,
      INITIAL_CLOCK_MS: 10 * 60 * 1000,
      CHALLENGE_COOLDOWN_MS: 5 * 60 * 1000,
      CHALLENGE_WINDOW_MS: 3 * 60 * 1000,
      RESEND_COOLDOWN_MS: 30 * 1000,
      MAX_RESENDS_BEFORE_LOCK: 3,
      LOCK_DURATION_MS: 3 * 60 * 60 * 1000
    };

    /* ==================== SOUND ENGINE (WEB AUDIO API) ==================== */
    let soundEnabled = localStorage.getItem(SOUND_PREF_KEY) !== 'false';
    let audioCtx = null;

    function getAudioCtx() {
      if (!soundEnabled) return null;
      const Ctx = window.AudioContext || window.webkitAudioContext;
      if (!Ctx) return null;
      if (!audioCtx) audioCtx = new Ctx();
      if (audioCtx.state === 'suspended') {
        audioCtx.resume().catch(() => {});
      }
      return audioCtx;
    }

    function playTone(freq, duration = 0.09, type = 'triangle', gainPeak = 0.14, delay = 0) {
      const ctx = getAudioCtx();
      if (!ctx) return;
      const startAt = ctx.currentTime + delay;
      const osc = ctx.createOscillator();
      const gain = ctx.createGain();
      osc.type = type;
      osc.frequency.setValueAtTime(freq, startAt);
      gain.gain.setValueAtTime(0.0001, startAt);
      gain.gain.exponentialRampToValueAtTime(gainPeak, startAt + 0.012);
      gain.gain.exponentialRampToValueAtTime(0.0001, startAt + duration);
      osc.connect(gain);
      gain.connect(ctx.destination);
      osc.start(startAt);
      osc.stop(startAt + duration + 0.02);
    }

    function playChessSound(kind) {
      if (!soundEnabled) return;
      switch (kind) {
        case 'select':
          playTone(520, 0.04, 'sine', 0.06, 0);
          break;
        case 'move':
          playTone(210, 0.075, 'triangle', 0.16, 0);
          playTone(145, 0.06, 'sine', 0.1, 0.015);
          break;
        case 'capture':
          playTone(320, 0.07, 'sawtooth', 0.13, 0);
          playTone(135, 0.11, 'square', 0.11, 0.03);
          break;
        case 'castle':
          playTone(220, 0.07, 'triangle', 0.15, 0);
          playTone(290, 0.07, 'triangle', 0.15, 0.065);
          break;
        case 'check':
          playTone(660, 0.09, 'sawtooth', 0.14, 0);
          playTone(880, 0.12, 'sawtooth', 0.14, 0.08);
          break;
        case 'notify':
          playTone(587.33, 0.09, 'sine', 0.12, 0);
          playTone(783.99, 0.14, 'sine', 0.12, 0.09);
          break;
        case 'gameover':
          playTone(392, 0.14, 'triangle', 0.15, 0);
          playTone(329.63, 0.14, 'triangle', 0.15, 0.13);
          playTone(261.63, 0.24, 'triangle', 0.16, 0.26);
          break;
        default:
          playTone(300, 0.06, 'sine', 0.1, 0);
      }
    }

    function updateSoundButtonUI() {
      const btn = document.getElementById('sound-toggle-btn');
      if (!btn) return;
      btn.textContent = soundEnabled ? '🔊 Sound On' : '🔇 Muted';
    }

    document.getElementById('sound-toggle-btn').addEventListener('click', () => {
      soundEnabled = !soundEnabled;
      localStorage.setItem(SOUND_PREF_KEY, String(soundEnabled));
      updateSoundButtonUI();
      if (soundEnabled) playChessSound('notify');
      showToast(soundEnabled ? 'Chess sound effects enabled' : 'Chess sound effects muted');
    });

    const STANDARD_PLANS = [
      { id: 'mem_monthly', name: 'Monthly Membership', price: 1.99, note: 'New member monthly tier ($2.49 renewal after trial).' },
      { id: 'mem_yearly', name: 'Yearly Membership', price: 5.99, note: 'New member yearly tier ($6.49 renewal after trial).' },
      { id: 'mem_permanent', name: 'Permanent Membership', price: 8.99, note: 'One-time permanent club membership.' }
    ];

    const RENEWAL_PLANS = [
      { id: 'renew_monthly', name: 'Monthly Renewal', price: 2.49, note: 'Renewal plan after trial/subscription period.' },
      { id: 'renew_yearly', name: 'Yearly Renewal', price: 6.49, note: 'Renewal plan after trial/subscription period.' }
    ];

    const DEFAULT_TOURNAMENTS = [
      { id: 't_swiss_1', title: 'RoChess Open Swiss #1', format: 'Swiss Tournament', hostName: 'RoChess Management', link: '', description: '5 rounds · 10+0 Rapid · Open to club members.' },
      { id: 't_arena_2', title: 'Gambit & Tactics Arena', format: 'Rapid Arena', hostName: 'RoChess Management', link: '', description: 'Fast rapid matches highlighting sharp openings.' },
      { id: 't_simul_3', title: 'Club Night Simul & Ladder', format: 'Team / Simul Event', hostName: 'RoChess Management', link: '', description: 'Structured club night matchups and rating progression.' }
    ];

    const TACTICAL_PUZZLES = [
      {
        id: 'puz_1',
        title: 'Back-Rank Finish',
        prompt: 'White to move. Move the Rook on a1 to a8 to deliver back-rank checkmate.',
        hint: 'Click the Rook at a1, then click a8.',
        from: [7, 0],
        to: [0, 0],
        board: [
          ['','','','','','♜','♚',''],
          ['','','','','','♟','♟','♟'],
          ['','','','','','','',''],
          ['','','','','','','',''],
          ['','','','','','','',''],
          ['','','','','','','',''],
          ['','','','','','','',''],
          ['♖','','','','','','♔','']
        ]
      },
      {
        id: 'puz_2',
        title: 'Queen Strike on f7',
        prompt: 'White to move. Capture on f7 with the Queen to strike near Black’s king.',
        hint: 'Click the Queen at d3, then click f7.',
        from: [5, 3],
        to: [1, 5],
        board: [
          ['♜','','♝','♛','♚','♝','♞','♜'],
          ['♟','♟','♟','♟','','♟','♟','♟'],
          ['','','♞','','','','',''],
          ['','','','','','','',''],
          ['','','♝','','','','',''],
          ['','','','♕','','','',''],
          ['♙','♙','♙','♙','♙','♙','♙','♙'],
          ['♖','♘','♗','','♔','','♘','♖']
        ]
      },
      {
        id: 'puz_3',
        title: 'Knight Fork Setup',
        prompt: 'White to move. Jump the Knight from f3 to g5 to press f7 and h7.',
        hint: 'Click the Knight at f3, then click g5.',
        from: [5, 5],
        to: [3, 6],
        board: [
          ['♜','','♝','♛','♚','♝','','♜'],
          ['♟','♟','♟','♟','','♟','♟','♟'],
          ['','','♞','','','','',''],
          ['','','','','','','',''],
          ['','','','','♙','','',''],
          ['','','','','','♘','',''],
          ['♙','♙','♙','♙','','♙','♙','♙'],
          ['♖','♘','♗','♕','♔','♗','','♖']
        ]
      }
    ];

    const RATING_BANDS = [
      { band: 'Pawn', range: '0 – 999', role: 'New to Tournament Play' },
      { band: 'Knight', range: '1000 – 1199', role: 'Developing Club Player' },
      { band: 'Bishop', range: '1200 – 1399', role: 'Intermediate Competitor' },
      { band: 'Rook', range: '1400 – 1599', role: 'Upper-Intermediate' },
      { band: 'Queen', range: '1600 – 1799', role: 'Expert Club Contender' },
      { band: 'King / Master', range: '1800+', role: 'Senior Club Standard' }
    ];

    const START_1V1 = [
      ['♜','♞','♝','♛','♚','♝','♞','♜'],
      ['♟','♟','♟','♟','♟','♟','♟','♟'],
      ['','','','','','','',''],
      ['','','','','','','',''],
      ['','','','','','','',''],
      ['','','','','','','',''],
      ['♙','♙','♙','♙','♙','♙','♙','♙'],
      ['♖','♘','♗','♕','♔','♗','♘','♖']
    ];

    const WHITE_PIECES = new Set(['♙','♖','♘','♗','♕','♔']);
    const BLACK_PIECES = new Set(['♟','♜','♞','♝','♛','♚']);

    function isWhite(p) { return WHITE_PIECES.has(p); }
    function isBlack(p) { return BLACK_PIECES.has(p); }
    function pieceColor(p) {
      if (!p) return null;
      return WHITE_PIECES.has(p) ? 'white' : (BLACK_PIECES.has(p) ? 'black' : null);
    }
    function pieceType(p) {
      const map = { '♙':'P','♟':'P','♖':'R','♜':'R','♘':'N','♞':'N','♗':'B','♝':'B','♕':'Q','♛':'Q','♔':'K','♚':'K' };
      return map[p] || null;
    }

    function isOwnerAccount() {
      const uid = String(session?.discordId || session?.userId || '').trim();
      return uid === OWNER_DISCORD_ID;
    }

    function sanitizePublicText(text) {
      if (isOwnerAccount()) return String(text || '');
      return String(text || '').replace(/wisp(?:byte)?/gi, 'rochess-hub');
    }

    function detectDeviceLabel(ua = navigator.userAgent) {
      const lower = String(ua || '').toLowerCase();
      let deviceType = 'Desktop';
      if (/ipad/.test(lower)) deviceType = 'iPad';
      else if (/iphone/.test(lower)) deviceType = 'iPhone';
      else if (/android/.test(lower) && /mobile/.test(lower)) deviceType = 'Android Phone';
      else if (/android/.test(lower)) deviceType = 'Android Tablet';

      let browser = 'Browser';
      if (/edg\//.test(lower)) browser = 'Edge';
      else if (/opr\/|opera/.test(lower)) browser = 'Opera';
      else if (/chrome\//.test(lower)) browser = 'Chrome';
      else if (/safari\//.test(lower) && !/chrome/.test(lower)) browser = 'Safari';
      else if (/firefox\//.test(lower)) browser = 'Firefox';

      return `${deviceType} / ${browser}`;
    }

    function getOrCreateDevice() {
      const now = new Date().toISOString();
      let saved = null;
      try {
        saved = JSON.parse(localStorage.getItem(DEVICE_STORAGE_KEY) || 'null');
      } catch (_) {}

      const randomId =
        'dev_' +
        (crypto.randomUUID
          ? crypto.randomUUID().replace(/-/g, '').slice(0, 14)
          : Math.random().toString(36).slice(2, 12) + Date.now().toString(36));

      const device = {
        deviceId: saved?.deviceId || randomId,
        label: detectDeviceLabel(navigator.userAgent),
        platform: navigator.platform || 'unknown',
        screen: `${window.screen.width}x${window.screen.height}`,
        userAgent: navigator.userAgent,
        firstSeenAt: saved?.firstSeenAt || now,
        lastSeenAt: now
      };
      localStorage.setItem(DEVICE_STORAGE_KEY, JSON.stringify(device));
      return device;
    }

    function loadSavedSession() {
      try {
        const raw = localStorage.getItem('rochess_web_session');
        if (!raw) return null;
        const parsed = JSON.parse(raw);
        if (parsed && parsed.handle) {
          parsed.verified = true;
          return parsed;
        }
      } catch (_) {}
      return null;
    }

    let currentDevice = getOrCreateDevice();
    let session = loadSavedSession();
    let cart = JSON.parse(localStorage.getItem('rochess_web_cart') || '[]');
    let localOrders = JSON.parse(localStorage.getItem('rochess_web_orders') || '[]');
    let localDmThreads = JSON.parse(localStorage.getItem('rochess_web_dm_threads') || '[]');
    let localRequests = JSON.parse(localStorage.getItem('rochess_web_requests') || '[]');
    let joinedTournamentIds = JSON.parse(localStorage.getItem('rochess_web_joined_tournaments') || '[]');
    let puzzleStats = JSON.parse(localStorage.getItem('rochess_web_puzzle_stats') || '{"solved":0,"streak":0}');
    let localAnnouncements = JSON.parse(localStorage.getItem(ANNOUNCEMENTS_STORAGE_KEY) || '[]');
    let localTournaments = JSON.parse(localStorage.getItem('rochess_web_tournaments') || 'null');
    if (!Array.isArray(localTournaments)) {
      localTournaments = [...DEFAULT_TOURNAMENTS];
      localStorage.setItem('rochess_web_tournaments', JSON.stringify(localTournaments));
    }

    let boardPrefs = JSON.parse(localStorage.getItem('rochess_board_prefs') || JSON.stringify({
      siteTheme: 'black',
      material: 'classic',
      pieceStyle: 'classic',
      pieceColors: 'classic'
    }));

    const DISCORD_RESEND_KEY = 'rochess_discord_resend_state_v1';
    let resendStateMap = JSON.parse(localStorage.getItem(DISCORD_RESEND_KEY) || '{}');
    let codeSentOnceForCurrentTarget = false;
    let activeTargetKey = '';
    let resendIntervalId = null;

    function getTargetKey(username, discordId) {
      const cleanId = String(discordId || '').trim();
      const cleanName = String(username || '').trim().toLowerCase().replace(/^@+/, '');
      return cleanId ? `id:${cleanId}` : `user:${cleanName}`;
    }

    function getTargetResendInfo(targetKey) {
      const now = Date.now();
      const rec = resendStateMap[targetKey] || {
        initialSent: false,
        lastSentAt: 0,
        resendCount: 0,
        lockedUntil: 0
      };
      if (rec.lockedUntil && now >= rec.lockedUntil) {
        rec.lockedUntil = 0;
        rec.resendCount = 0;
        resendStateMap[targetKey] = rec;
        localStorage.setItem(DISCORD_RESEND_KEY, JSON.stringify(resendStateMap));
      }
      return rec;
    }

    function saveTargetResendInfo(targetKey, rec) {
      resendStateMap[targetKey] = rec;
      localStorage.setItem(DISCORD_RESEND_KEY, JSON.stringify(resendStateMap));
    }

    function formatRemaining(ms) {
      const totalSec = Math.max(1, Math.ceil(ms / 1000));
      const hrs = Math.floor(totalSec / 3600);
      const mins = Math.floor((totalSec % 3600) / 60);
      const secs = totalSec % 60;
      if (hrs > 0) return `${hrs}h ${mins}m ${secs}s`;
      if (mins > 0) return `${mins}m ${secs}s`;
      return `${secs}s`;
    }

    function formatClock(ms) {
      const safe = Math.max(0, Math.floor(ms / 1000));
      const mins = Math.floor(safe / 60);
      const secs = safe % 60;
      return `${String(mins).padStart(2, '0')}:${String(secs).padStart(2, '0')}`;
    }

    function updateSendCodeButtonState() {
      const btn = document.getElementById('send-proof-code-btn');
      const statusEl = document.getElementById('proof-dispatch-status');
      if (!btn || !statusEl) return;

      const handle = document.getElementById('auth-handle').value.trim();
      const discordId = document.getElementById('auth-discord-id').value.trim();
      const key = getTargetKey(handle, discordId);
      const info = getTargetResendInfo(key);
      const now = Date.now();

      if (info.lockedUntil && now < info.lockedUntil) {
        btn.disabled = true;
        btn.textContent = 'Locked (3h)';
        statusEl.innerHTML = `<span style="color: var(--danger);">Too many resends for this user (3/3). Locked for <strong>${formatRemaining(info.lockedUntil - now)}</strong>.</span>`;
        return;
      }

      if (info.initialSent && info.lastSentAt && (now - info.lastSentAt) < CLUB_CONFIG.RESEND_COOLDOWN_MS) {
        const waitMs = CLUB_CONFIG.RESEND_COOLDOWN_MS - (now - info.lastSentAt);
        btn.disabled = true;
        btn.textContent = `Resend in ${Math.ceil(waitMs / 1000)}s`;
        return;
      }

      btn.disabled = false;
      btn.textContent = info.initialSent ? `Resend Code (${info.resendCount}/${CLUB_CONFIG.MAX_RESENDS_BEFORE_LOCK})` : 'Send Code';
    }

    function startResendTicker() {
      if (resendIntervalId) clearInterval(resendIntervalId);
      resendIntervalId = setInterval(() => {
        if (document.getElementById('auth-modal').classList.contains('open')) {
          updateSendCodeButtonState();
        }
      }, 500);
    }

    /* ==================== FULL CHESS RULES ENGINE ==================== */
    function cloneBoard(b) {
      return b.map(row => [...row]);
    }

    function boardPositionKey(game) {
      const rows = game.board.map(r => r.map(c => c || '.').join('')).join('/');
      const castling = [
        game.castling.wK ? 'K' : '',
        game.castling.wQ ? 'Q' : '',
        game.castling.bK ? 'k' : '',
        game.castling.bQ ? 'q' : ''
      ].join('') || '-';
      const ep = game.enPassantTarget ? `${game.enPassantTarget.r},${game.enPassantTarget.c}` : '-';
      return `${rows}|${game.turn}|${castling}|${ep}`;
    }

    function findKing(board, color) {
      const target = color === 'white' ? '♔' : '♚';
      for (let r = 0; r < 8; r++) {
        for (let c = 0; c < 8; c++) {
          if (board[r][c] === target) return { r, c };
        }
      }
      return null;
    }

    function isSquareAttacked(board, tr, tc, byColor) {
      // Pawn attacks
      const pawnDir = byColor === 'white' ? 1 : -1;
      const pawnChar = byColor === 'white' ? '♙' : '♟';
      for (const dc of [-1, 1]) {
        const pr = tr + pawnDir;
        const pc = tc + dc;
        if (pr >= 0 && pr < 8 && pc >= 0 && pc < 8 && board[pr][pc] === pawnChar) {
          return true;
        }
      }

      // Knight attacks
      const knightChar = byColor === 'white' ? '♘' : '♞';
      const kJumps = [[-2,-1],[-2,1],[-1,-2],[-1,2],[1,-2],[1,2],[2,-1],[2,1]];
      for (const [dr, dc] of kJumps) {
        const nr = tr + dr;
        const nc = tc + dc;
        if (nr >= 0 && nr < 8 && nc >= 0 && nc < 8 && board[nr][nc] === knightChar) {
          return true;
        }
      }

      // King attacks (adjacent)
      const kingChar = byColor === 'white' ? '♔' : '♚';
      for (let dr = -1; dr <= 1; dr++) {
        for (let dc = -1; dc <= 1; dc++) {
          if (!dr && !dc) continue;
          const kr = tr + dr;
          const kc = tc + dc;
          if (kr >= 0 && kr < 8 && kc >= 0 && kc < 8 && board[kr][kc] === kingChar) {
            return true;
          }
        }
      }

      // Orthogonal sliders (Rook / Queen)
      const rookChar = byColor === 'white' ? '♖' : '♜';
      const queenChar = byColor === 'white' ? '♕' : '♛';
      for (const [dr, dc] of [[-1,0],[1,0],[0,-1],[0,1]]) {
        let nr = tr + dr;
        let nc = tc + dc;
        while (nr >= 0 && nr < 8 && nc >= 0 && nc < 8) {
          const p = board[nr][nc];
          if (p) {
            if (p === rookChar || p === queenChar) return true;
            break;
          }
          nr += dr;
          nc += dc;
        }
      }

      // Diagonal sliders (Bishop / Queen)
      const bishopChar = byColor === 'white' ? '♗' : '♝';
      for (const [dr, dc] of [[-1,-1],[-1,1],[1,-1],[1,1]]) {
        let nr = tr + dr;
        let nc = tc + dc;
        while (nr >= 0 && nr < 8 && nc >= 0 && nc < 8) {
          const p = board[nr][nc];
          if (p) {
            if (p === bishopChar || p === queenChar) return true;
            break;
          }
          nr += dr;
          nc += dc;
        }
      }

      return false;
    }

    function isInCheck(board, color) {
      const king = findKing(board, color);
      if (!king) return false;
      const opp = color === 'white' ? 'black' : 'white';
      return isSquareAttacked(board, king.r, king.c, opp);
    }

    function getPseudoLegalMovesForSquare(game, r, c) {
      const piece = game.board[r][c];
      const color = pieceColor(piece);
      const type = pieceType(piece);
      if (!piece || !color || !type) return [];

      const moves = [];
      const opp = color === 'white' ? 'black' : 'white';

      const pushIfValid = (tr, tc, extra = {}) => {
        if (tr < 0 || tr > 7 || tc < 0 || tc > 7) return false;
        const occupant = game.board[tr][tc];
        const occColor = pieceColor(occupant);
        if (occColor === color) return false;
        moves.push({
          from: { r, c },
          to: { r: tr, c: tc },
          capture: !!occupant,
          ...extra
        });
        return !occupant;
      };

      if (type === 'P') {
        const dir = color === 'white' ? -1 : 1;
        const startRow = color === 'white' ? 6 : 1;
        const promoRow = color === 'white' ? 0 : 7;

        // 1 square forward
        const f1 = r + dir;
        if (f1 >= 0 && f1 <= 7 && !game.board[f1][c]) {
          moves.push({
            from: { r, c },
            to: { r: f1, c },
            capture: false,
            promotion: f1 === promoRow ? 'Q' : null
          });
          // 2 squares forward from starting rank
          const f2 = r + dir * 2;
          if (r === startRow && !game.board[f2][c]) {
            moves.push({
              from: { r, c },
              to: { r: f2, c },
              capture: false,
              doubleStep: true
            });
          }
        }

        // Diagonal captures & En Passant
        for (const dc of [-1, 1]) {
          const tr = r + dir;
          const tc = c + dc;
          if (tr < 0 || tr > 7 || tc < 0 || tc > 7) continue;
          const target = game.board[tr][tc];
          if (target && pieceColor(target) === opp) {
            moves.push({
              from: { r, c },
              to: { r: tr, c: tc },
              capture: true,
              promotion: tr === promoRow ? 'Q' : null
            });
          } else if (
            game.enPassantTarget &&
            game.enPassantTarget.r === tr &&
            game.enPassantTarget.c === tc
          ) {
            const capPawnRow = r;
            const capPawnCol = tc;
            const adjPawn = game.board[capPawnRow][capPawnCol];
            if (adjPawn && pieceType(adjPawn) === 'P' && pieceColor(adjPawn) === opp) {
              moves.push({
                from: { r, c },
                to: { r: tr, c: tc },
                capture: true,
                enPassant: true,
                epCaptureSq: { r: capPawnRow, c: capPawnCol }
              });
            }
          }
        }
      } else if (type === 'N') {
        for (const [dr, dc] of [[-2,-1],[-2,1],[-1,-2],[-1,2],[1,-2],[1,2],[2,-1],[2,1]]) {
          pushIfValid(r + dr, c + dc);
        }
      } else if (type === 'B') {
        for (const [dr, dc] of [[-1,-1],[-1,1],[1,-1],[1,1]]) {
          let nr = r + dr, nc = c + dc;
          while (pushIfValid(nr, nc)) { nr += dr; nc += dc; }
        }
      } else if (type === 'R') {
        for (const [dr, dc] of [[-1,0],[1,0],[0,-1],[0,1]]) {
          let nr = r + dr, nc = c + dc;
          while (pushIfValid(nr, nc)) { nr += dr; nc += dc; }
        }
      } else if (type === 'Q') {
        for (const [dr, dc] of [[-1,-1],[-1,1],[1,-1],[1,1],[-1,0],[1,0],[0,-1],[0,1]]) {
          let nr = r + dr, nc = c + dc;
          while (pushIfValid(nr, nc)) { nr += dr; nc += dc; }
        }
      } else if (type === 'K') {
        for (let dr = -1; dr <= 1; dr++) {
          for (let dc = -1; dc <= 1; dc++) {
            if (dr || dc) pushIfValid(r + dr, c + dc);
          }
        }

        // Castling (King must not currently be in check, path empty, squares not attacked)
        const homeRow = color === 'white' ? 7 : 0;
        const canK = color === 'white' ? game.castling.wK : game.castling.bK;
        const canQ = color === 'white' ? game.castling.wQ : game.castling.bQ;
        const expectedKing = color === 'white' ? '♔' : '♚';
        const expectedRook = color === 'white' ? '♖' : '♜';

        if (r === homeRow && c === 4 && game.board[homeRow][4] === expectedKing && !isInCheck(game.board, color)) {
          // Kingside (e -> g, rook h -> f)
          if (
            canK &&
            !game.board[homeRow][5] &&
            !game.board[homeRow][6] &&
            game.board[homeRow][7] === expectedRook &&
            !isSquareAttacked(game.board, homeRow, 5, opp) &&
            !isSquareAttacked(game.board, homeRow, 6, opp)
          ) {
            moves.push({
              from: { r: homeRow, c: 4 },
              to: { r: homeRow, c: 6 },
              capture: false,
              castle: 'K'
            });
          }
          // Queenside (e -> c, rook a -> d)
          if (
            canQ &&
            !game.board[homeRow][1] &&
            !game.board[homeRow][2] &&
            !game.board[homeRow][3] &&
            game.board[homeRow][0] === expectedRook &&
            !isSquareAttacked(game.board, homeRow, 3, opp) &&
            !isSquareAttacked(game.board, homeRow, 2, opp)
          ) {
            moves.push({
              from: { r: homeRow, c: 4 },
              to: { r: homeRow, c: 2 },
              capture: false,
              castle: 'Q'
            });
          }
        }
      }

      return moves;
    }

    function applyMoveToBoardState(game, move) {
      const nextBoard = cloneBoard(game.board);
      const movingPiece = nextBoard[move.from.r][move.from.c];
      const moverColor = pieceColor(movingPiece);
      const moverType = pieceType(movingPiece);
      const nextCastling = { ...game.castling };
      let capturedPiece = nextBoard[move.to.r][move.to.c] || '';

      if (move.enPassant && move.epCaptureSq) {
        capturedPiece = nextBoard[move.epCaptureSq.r][move.epCaptureSq.c] || '';
        nextBoard[move.epCaptureSq.r][move.epCaptureSq.c] = '';
      }

      nextBoard[move.to.r][move.to.c] = movingPiece;
      nextBoard[move.from.r][move.from.c] = '';

      if (move.castle === 'K') {
        const row = moverColor === 'white' ? 7 : 0;
        nextBoard[row][5] = nextBoard[row][7];
        nextBoard[row][7] = '';
      } else if (move.castle === 'Q') {
        const row = moverColor === 'white' ? 7 : 0;
        nextBoard[row][3] = nextBoard[row][0];
        nextBoard[row][0] = '';
      }

      if (move.promotion) {
        const promoChar = move.promotion || 'Q';
        const promoMap = moverColor === 'white'
          ? { Q: '♕', R: '♖', B: '♗', N: '♘' }
          : { Q: '♛', R: '♜', B: '♝', N: '♞' };
        nextBoard[move.to.r][move.to.c] = promoMap[promoChar] || (moverColor === 'white' ? '♕' : '♛');
      }

      if (moverType === 'K') {
        if (moverColor === 'white') { nextCastling.wK = false; nextCastling.wQ = false; }
        else { nextCastling.bK = false; nextCastling.bQ = false; }
      }
      if (move.from.r === 7 && move.from.c === 7) nextCastling.wK = false;
      if (move.from.r === 7 && move.from.c === 0) nextCastling.wQ = false;
      if (move.from.r === 0 && move.from.c === 7) nextCastling.bK = false;
      if (move.from.r === 0 && move.from.c === 0) nextCastling.bQ = false;
      if (move.to.r === 7 && move.to.c === 7) nextCastling.wK = false;
      if (move.to.r === 7 && move.to.c === 0) nextCastling.wQ = false;
      if (move.to.r === 0 && move.to.c === 7) nextCastling.bK = false;
      if (move.to.r === 0 && move.to.c === 0) nextCastling.bQ = false;

      let nextEnPassant = null;
      if (moverType === 'P' && move.doubleStep) {
        nextEnPassant = {
          r: (move.from.r + move.to.r) / 2,
          c: move.from.c
        };
      }

      return {
        board: nextBoard,
        castling: nextCastling,
        enPassantTarget: nextEnPassant,
        capturedPiece
      };
    }

    function getLegalMovesForSquare(game, r, c) {
      const piece = game.board[r][c];
      const color = pieceColor(piece);
      if (!color || color !== game.turn) return [];
      const pseudo = getPseudoLegalMovesForSquare(game, r, c);
      return pseudo.filter(m => {
        const sim = applyMoveToBoardState(game, m);
        return !isInCheck(sim.board, color);
      });
    }

    function getAllLegalMoves(game, color = game.turn) {
      const all = [];
      for (let r = 0; r < 8; r++) {
        for (let c = 0; c < 8; c++) {
          if (pieceColor(game.board[r][c]) === color) {
            const ms = getPseudoLegalMovesForSquare(game, r, c).filter(m => {
              const sim = applyMoveToBoardState(game, m);
              return !isInCheck(sim.board, color);
            });
            all.push(...ms);
          }
        }
      }
      return all;
    }

    function isOnlyTwoKingsRemaining(board) {
      const pieces = [];
      for (let r = 0; r < 8; r++) {
        for (let c = 0; c < 8; c++) {
          if (board[r][c]) pieces.push(pieceType(board[r][c]));
        }
      }
      return pieces.length === 2 && pieces[0] === 'K' && pieces[1] === 'K';
    }

    function sqName(r, c) {
      return `${String.fromCharCode(97 + c)}${8 - r}`;
    }

    function createFreshChessState(matchInfo = null) {
      const initial = {
        board: cloneBoard(START_1V1),
        turn: 'white',
        selected: null,
        legalTargets: [],
        moves: 0,
        capturedByWhite: [],
        capturedByBlack: [],
        moveLog: [],
        history: [],
        castling: { wK: true, wQ: true, bK: true, bQ: true },
        enPassantTarget: null,
        positionCounts: {},
        whiteTimeMs: CLUB_CONFIG.INITIAL_CLOCK_MS,
        blackTimeMs: CLUB_CONFIG.INITIAL_CLOCK_MS,
        gameOver: false,
        statusText: 'White to Move (1v1)',
        eloDeltaApplied: false,
        drawOfferedBy: null,
        match: matchInfo || {
          matchId: null,
          mode: 'practice_1v1',
          whiteUser: null,
          blackUser: null,
          userRole: 'both'
        }
      };
      const startKey = boardPositionKey(initial);
      initial.positionCounts[startKey] = 1;
      return initial;
    }

    let chess1v1 = createFreshChessState();
    let clockTimerId = null;

    function applyMatchEloOutcome(outcomeType, winnerColor = null, reasonText = '') {
      if (chess1v1.eloDeltaApplied) return;
      chess1v1.eloDeltaApplied = true;
      chess1v1.gameOver = true;
      playChessSound('gameover');

      const uid = session?.discordId || session?.userId || 'guest';
      const st = getUserEloConnectState(uid);
      const currentElo = getCurrentUserElo();

      const match = chess1v1.match || {};
      const mySide = match.userRole === 'black' ? 'black' : (match.userRole === 'white' ? 'white' : 'white');

      let myDelta = 0;
      let oppDelta = 0;

      if (outcomeType === 'win') {
        const iWon = winnerColor === mySide;
        myDelta = iWon ? 8 : -8;
        oppDelta = iWon ? -8 : 8;
      } else if (outcomeType === 'agreed_draw') {
        myDelta = 0;
        oppDelta = 0;
      } else if (outcomeType === 'draw_penalty') {
        // Stalemate, threefold repetition, or two kings only
        myDelta = -1;
        oppDelta = -1;
      }

      const nextMyElo = Math.max(100, currentElo + myDelta);
      saveUserEloConnectState(uid, { ...st, elo: nextMyElo });

      const deltaLabel = myDelta > 0 ? `+${myDelta}` : `${myDelta}`;
      chess1v1.statusText = `${reasonText} (Your ELO: ${deltaLabel} → ${nextMyElo})`;

      if (match.matchId) {
        detailedApiRequest('/api/rochess/match/result', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({
            matchId: match.matchId,
            userId: uid,
            handle: session?.handle || 'Member',
            outcomeType,
            winnerColor,
            reason: reasonText,
            myDelta,
            oppDelta,
            newElo: nextMyElo
          })
        });
      }

      pushMonitorLine('INFO', `match_end: type=${outcomeType} reason="${reasonText}" myDelta=${deltaLabel} newElo=${nextMyElo}`);
      renderOpponentAndEloBar();
    }

    function startClockLoop() {
      if (clockTimerId) clearInterval(clockTimerId);
      clockTimerId = setInterval(() => {
        if (!isSignedIn() || chess1v1.gameOver) {
          updateClockDisplay();
          return;
        }
        if (chess1v1.turn === 'white') {
          chess1v1.whiteTimeMs = Math.max(0, chess1v1.whiteTimeMs - 250);
          if (chess1v1.whiteTimeMs <= 0) {
            applyMatchEloOutcome('win', 'black', 'White ran out of time — Black wins');
            render1v1Board();
          }
        } else {
          chess1v1.blackTimeMs = Math.max(0, chess1v1.blackTimeMs - 250);
          if (chess1v1.blackTimeMs <= 0) {
            applyMatchEloOutcome('win', 'white', 'Black ran out of time — White wins');
            render1v1Board();
          }
        }
        updateClockDisplay();
      }, 250);
    }

    function updateClockDisplay() {
      const wClock = document.getElementById('white-clock-val');
      const bClock = document.getElementById('black-clock-val');
      const wBox = document.getElementById('white-clock-box');
      const bBox = document.getElementById('black-clock-box');
      if (wClock) wClock.textContent = formatClock(chess1v1.whiteTimeMs);
      if (bClock) bClock.textContent = formatClock(chess1v1.blackTimeMs);
      if (wBox) wBox.classList.toggle('active-clock', !chess1v1.gameOver && chess1v1.turn === 'white');
      if (bBox) bBox.classList.toggle('active-clock', !chess1v1.gameOver && chess1v1.turn === 'black');
    }

    /* ==================== 1V1 CHALLENGE & COOLDOWNS ==================== */
    const CHALLENGE_COOLDOWN_KEY = 'rochess_challenge_cooldowns_v1';
    let localChallengeCooldowns = JSON.parse(localStorage.getItem(CHALLENGE_COOLDOWN_KEY) || '{}');
    let activeChallengePollId = null;

    function getChallengeCooldownForTarget(targetRaw) {
      const norm = String(targetRaw || '').trim().toLowerCase().replace(/^@+/, '');
      if (!norm) return 0;
      const now = Date.now();
      const serverMap = liveState?.challengeCooldownsByTarget || {};
      const serverUntil = Number(serverMap[norm] || 0);
      const localUntil = Number(localChallengeCooldowns[norm] || 0);
      const until = Math.max(serverUntil, localUntil);
      return until > now ? until : 0;
    }

    function setChallengeCooldownForTarget(targetRaw, untilTs) {
      const norm = String(targetRaw || '').trim().toLowerCase().replace(/^@+/, '');
      if (!norm) return;
      localChallengeCooldowns[norm] = untilTs;
      localStorage.setItem(CHALLENGE_COOLDOWN_KEY, JSON.stringify(localChallengeCooldowns));
    }

    function openChallengeModal() {
      if (!isSignedIn()) return openAuthModal();
      document.getElementById('challenge-error-msg').textContent = '';
      document.getElementById('challenge-target-input').value = '';
      document.getElementById('challenge-status-box').innerHTML =
        `<div class="small">Enter target Discord username or ID. 3-minute response window (3 reminders before deny) &amp; 5-minute per-user cooldown.</div>`;
      document.getElementById('challenge-modal').classList.add('open');
      playChessSound('notify');
    }

    function closeChallengeModal() {
      document.getElementById('challenge-modal').classList.remove('open');
    }

    document.getElementById('close-challenge-modal').addEventListener('click', closeChallengeModal);
    document.getElementById('cancel-challenge-btn').addEventListener('click', closeChallengeModal);
    document.getElementById('challenge-modal').addEventListener('click', (e) => {
      if (e.target === document.getElementById('challenge-modal')) closeChallengeModal();
    });

    document.getElementById('send-1v1-challenge-btn').addEventListener('click', async () => {
      const errEl = document.getElementById('challenge-error-msg');
      const statusBox = document.getElementById('challenge-status-box');
      errEl.textContent = '';

      if (!isSignedIn()) return openAuthModal();
      const target = document.getElementById('challenge-target-input').value.trim();
      if (!target) {
        errEl.textContent = 'Enter a Discord username or Discord user ID to challenge.';
        return;
      }

      const existingUntil = getChallengeCooldownForTarget(target);
      if (existingUntil > Date.now()) {
        errEl.textContent = `5-minute cooldown active for "${target}". Wait ${formatRemaining(existingUntil - Date.now())}.`;
        return;
      }

      const res = await detailedApiRequest('/api/rochess/challenge/create', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          challengerId: session.discordId || session.userId,
          challengerHandle: session.handle,
          target,
          guildId: CLUB_CONFIG.MAIN_GUILD_ID,
          cooldownMs: CLUB_CONFIG.CHALLENGE_COOLDOWN_MS,
          responseWindowMs: CLUB_CONFIG.CHALLENGE_WINDOW_MS,
          maxRemindersBeforeDeny: 3
        })
      });

      if (!res.ok) {
        if (res.data?.cooldownUntil) {
          setChallengeCooldownForTarget(target, Number(res.data.cooldownUntil));
        }
        errEl.textContent = res.data?.error || res.errorMessage || 'Could not send 1v1 challenge.';
        return;
      }

      const cooldownUntil = Number(res.data?.cooldownUntil || (Date.now() + CLUB_CONFIG.CHALLENGE_COOLDOWN_MS));
      setChallengeCooldownForTarget(target, cooldownUntil);

      const challengeId = res.data?.challengeId || `chal_${Date.now()}`;
      statusBox.innerHTML = `
        <strong style="color: var(--emerald);">Challenge Sent via Discord DM!</strong>
        <div class="small" style="margin-top: 3px;">
          Target: <strong>${escapeHtml(target)}</strong> · Window: <strong>3m</strong> (auto-denies after 3 unanswered reminders) · Cooldown: <strong>5m</strong>.
        </div>
      `;
      playChessSound('notify');
      showToast(`1v1 challenge sent to ${target}`);
      pushMonitorLine('INFO', `1v1_challenge_sent: ${session.handle} -> ${target} (id=${challengeId})`);

      if (activeChallengePollId) clearInterval(activeChallengePollId);
      let polls = 0;
      activeChallengePollId = setInterval(async () => {
        polls += 1;
        if (polls > 72) {
          clearInterval(activeChallengePollId);
          return;
        }
        const stRes = await detailedApiRequest(`/api/rochess/challenge/status?challengeId=${encodeURIComponent(challengeId)}`);
        if (!stRes.ok || !stRes.data?.status) return;
        const st = stRes.data.status;
        if (st === 'DENIED' || st === 'TIMED_OUT') {
          clearInterval(activeChallengePollId);
          playChessSound('gameover');
          showToast(`${target} denied the 1v1 challenge.`);
          pushMonitorLine('INFO', `1v1_challenge_denied: ${target} (${st})`);
        } else if (st === 'ACCEPTED') {
          clearInterval(activeChallengePollId);
          const matchId = stRes.data.matchId || `match_${Date.now()}`;
          const role = stRes.data.challengerRole || 'white';
          chess1v1 = createFreshChessState({
            matchId,
            mode: 'rated_1v1',
            whiteUser: stRes.data.whiteUser || session.handle,
            blackUser: stRes.data.blackUser || target,
            userRole: role
          });
          closeChallengeModal();
          setActiveView('chess-tournaments');
          render1v1Board();
          playChessSound('notify');
          showToast(`Challenge accepted! Match ${matchId} started — White moves first.`);
          pushMonitorLine('INFO', `1v1_challenge_accepted: matchId=${matchId} role=${role}`);
        }
      }, 2500);
    });

    function checkUrlMatchInvite() {
      const params = new URLSearchParams(window.location.search);
      const matchId = params.get('match');
      if (!matchId) return;
      const role = params.get('role') === 'black' ? 'black' : 'white';
      const opp = params.get('opp') || 'Discord Challenger';
      chess1v1 = createFreshChessState({
        matchId,
        mode: 'rated_1v1',
        whiteUser: role === 'white' ? (session?.handle || 'White Player') : opp,
        blackUser: role === 'black' ? (session?.handle || 'Black Player') : opp,
        userRole: role
      });
      localStorage.setItem(ACTIVE_VIEW_STORAGE_KEY, 'chess-tournaments');
      pushMonitorLine('INFO', `match_link_opened: matchId=${matchId} role=${role}`);
    }

    function isOwnerAccount() {
      const uid = String(session?.discordId || session?.userId || '').trim();
      return uid === OWNER_DISCORD_ID;
    }

    function sanitizePublicText(text) {
      if (isOwnerAccount()) return String(text || '');
      return String(text || '').replace(/wisp(?:byte)?/gi, 'rochess-hub');
    }

    function getUserRoleFlags() {
      const uid = String(session?.discordId || session?.userId || '').trim();
      const roleSet = new Set();

      const fromSession = Array.isArray(session?.roles) ? session.roles : [];
      fromSession.forEach(r => roleSet.add(String(r)));

      const fromRoleInfo = Array.isArray(liveState?.roleInfo?.roles) ? liveState.roleInfo.roles : [];
      fromRoleInfo.forEach(r => roleSet.add(String(r)));

      const fromProfileRoles = Array.isArray(liveState?.userProfile?.roles) ? liveState.userProfile.roles : [];
      fromProfileRoles.forEach(r => roleSet.add(String(r)));

      const guildsObj = liveState?.userProfile?.guilds || liveState?.member?.guilds || {};
      if (guildsObj && typeof guildsObj === 'object') {
        Object.values(guildsObj).forEach(g => {
          if (g && Array.isArray(g.roles)) g.roles.forEach(r => roleSet.add(String(r)));
        });
      }

      const isManagement =
        uid === OWNER_DISCORD_ID ||
        CLUB_CONFIG.MANAGEMENT_ROLE_IDS.some(id => roleSet.has(id)) ||
        Boolean(liveState?.roleInfo?.isManagement);

      const isEntertainment =
        CLUB_CONFIG.ENTERTAINMENT_ROLE_IDS.some(id => roleSet.has(id)) ||
        Boolean(liveState?.roleInfo?.isEntertainment);

      const isSubscriber = roleSet.has(CLUB_CONFIG.SUBSCRIBER_ROLE_ID) || isManagement;
      const canHostEvent = isManagement || isEntertainment || Boolean(liveState?.roleInfo?.canHostEvent);

      return { isManagement, isEntertainment, isSubscriber, canHostEvent, roles: Array.from(roleSet) };
    }

    function hasSubscriberPerks() {
      return getUserRoleFlags().isSubscriber;
    }

    function getSubStatusFromDb() {
      const up = liveState?.userProfile || liveState?.subscription || null;
      const now = Date.now();

      const hasActiveSub = !!(
        up?.hasActiveSubscription ||
        up?.subscriptionActive ||
        (up?.subscriptionExpiresAt && Number(new Date(up.subscriptionExpiresAt).getTime()) > now) ||
        (up?.plan_type && ['MONTHLY', 'YEARLY', 'PERMANENT', 'SUBSCRIBER'].includes(String(up.plan_type).toUpperCase()))
      );

      const trialEnded = !hasActiveSub && !!(
        up?.trialEnded ||
        up?.freeTrialEnded ||
        String(up?.trial_status || '').toUpperCase() === 'ENDED' ||
        String(up?.plan_type || '').toUpperCase() === 'TRIAL_ENDED' ||
        (up?.trialExpiresAt && Number(new Date(up.trialExpiresAt).getTime()) <= now)
      );

      return {
        hasActiveSub,
        trialEnded,
        planLabel: up?.plan_name || up?.plan_type || (hasActiveSub ? 'Active Subscription' : (trialEnded ? 'Free Trial Ended' : 'Standard')),
        expiresAt: up?.subscriptionExpiresAt || up?.expiresAt || null
      };
    }

    function getActivePlansForUser() {
      const sub = getSubStatusFromDb();
      return sub.trialEnded ? RENEWAL_PLANS : STANDARD_PLANS;
    }

    function getPiecePalette() {
      const sub = hasSubscriberPerks();
      const paletteKey = sub ? boardPrefs.pieceColors : 'classic';
      if (paletteKey === 'crimson') {
        return { wFill: '#fffbeb', wStroke: '#1c1917', wShade: '#fde68a', bFill: '#991b1b', bStroke: '#450a0a', bShade: '#7f1d1d' };
      }
      if (paletteKey === 'navy') {
        return { wFill: '#f0f9ff', wStroke: '#0f172a', wShade: '#bae6fd', bFill: '#1e3a8a', bStroke: '#0f172a', bShade: '#172554' };
      }
      return {
        wFill: '#ffffff',
        wStroke: '#1e242b',
        wShade: '#e2e8f0',
        bFill: '#3a3d42',
        bStroke: '#111315',
        bShade: '#26292e'
      };
    }

    function renderPieceSvg(piece, extraClass = '') {
      if (!piece) return '';
      const isWhite = WHITE_PIECES.has(piece);
      const pal = getPiecePalette();
      const fill = isWhite ? pal.wFill : pal.bFill;
      const stroke = isWhite ? pal.wStroke : pal.bStroke;
      const shade = isWhite ? pal.wShade : pal.bShade;
      const sw = hasSubscriberPerks() && boardPrefs.pieceStyle === 'modern' ? '3.4' : '4';
      const code = pieceType(piece);

      const base = `
        <path d="M22 86 C22 82, 26 80, 32 80 L68 80 C74 80, 78 82, 78 86 L78 90 L22 90 Z" fill="${fill}"/>
        <rect x="27" y="75" width="46" height="5.5" rx="2.5" fill="${shade}"/>
      `;

      const art = {
        P: `
          <path d="M36 75 C39 65, 43 58, 43 52 L57 52 C57 58, 61 65, 64 75 Z" fill="${fill}"/>
          <rect x="37" y="48" width="26" height="5.5" rx="2.7" fill="${shade}"/>
          <circle cx="50" cy="34" r="13" fill="${fill}"/>
          <path d="M41 28 C44 23, 52 22, 57 26" fill="none" stroke="${shade}" stroke-width="3" stroke-linecap="round"/>
          ${base}
        `,
        R: `
          <path d="M33 75 L36 41 L64 41 L67 75 Z" fill="${fill}"/>
          <path d="M35 66 L65 66 L66 72 L34 72 Z" fill="${shade}"/>
          <path d="M31 41 L31 21 L40 21 L40 28 L45.5 28 L45.5 21 L54.5 21 L54.5 28 L60 28 L60 21 L69 21 L69 41 Z" fill="${fill}"/>
          <rect x="31" y="38" width="38" height="4.5" rx="2" fill="${shade}"/>
          ${base}
        `,
        N: `
          <path d="M31 75 C32 61, 36 52, 43 44 C36 43, 30 45, 26 42 C23 39, 25 32, 31 27 L44 17 L48 11 L54 17 C65 20, 72 30, 72 44 C72 57, 68 67, 68 75 Z" fill="${fill}"/>
          <path d="M51 18 C60 22, 65 31, 65 44 C65 55, 62 65, 62 74 L68 74 C68 67, 72 57, 72 44 C72 30, 65 20, 54 17 Z" fill="${shade}" stroke="none"/>
          <circle cx="38" cy="28" r="3.1" fill="${stroke}" stroke="none"/>
          <path d="M27 40 C31 41, 35 40, 38 38" fill="none" stroke="${stroke}" stroke-width="2.6" stroke-linecap="round"/>
          ${base}
        `,
        B: `
          <path d="M35 75 C37 64, 41 56, 42 50 L58 50 C59 56, 63 64, 65 75 Z" fill="${fill}"/>
          <rect x="38" y="47" width="24" height="5" rx="2.5" fill="${shade}"/>
          <path d="M50 18 C62 24, 66 33, 63 42 C61 46, 56 48, 50 48 C44 48, 39 46, 37 42 C34 33, 38 24, 50 18 Z" fill="${fill}"/>
          <path d="M56 23 C60 28, 61 35, 58 42" fill="none" stroke="${shade}" stroke-width="3" stroke-linecap="round"/>
          <line x1="44" y1="31" x2="56" y2="39" stroke="${stroke}" stroke-width="2.6" stroke-linecap="round"/>
          <line x1="56" y1="31" x2="44" y2="39" stroke="${stroke}" stroke-width="2.6" stroke-linecap="round"/>
          <circle cx="50" cy="14" r="4.2" fill="${fill}"/>
          ${base}
        `,
        Q: `
          <path d="M33 75 L38 44 L62 44 L67 75 Z" fill="${fill}"/>
          <rect x="36" y="42" width="28" height="5" rx="2.5" fill="${shade}"/>
          <path d="M36 42 L20 22 L34 31 L42 17 L50 30 L58 17 L66 31 L80 22 L64 42 Z" fill="${fill}"/>
          <circle cx="20" cy="20" r="3.4" fill="${fill}"/>
          <circle cx="42" cy="15" r="3.4" fill="${fill}"/>
          <circle cx="50" cy="12.5" r="3.8" fill="${fill}"/>
          <circle cx="58" cy="15" r="3.4" fill="${fill}"/>
          <circle cx="80" cy="20" r="3.4" fill="${fill}"/>
          ${base}
        `,
        K: `
          <line x1="50" y1="9" x2="50" y2="25" stroke="${stroke}" stroke-width="${sw}" stroke-linecap="round"/>
          <line x1="42" y1="16" x2="58" y2="16" stroke="${stroke}" stroke-width="${sw}" stroke-linecap="round"/>
          <path d="M32 75 L36 44 L64 44 L68 75 Z" fill="${fill}"/>
          <rect x="35" y="42" width="30" height="5" rx="2.5" fill="${shade}"/>
          <path d="M35 42 C27 36, 28 25, 38 24 C44 23.5, 48 27, 50 31 C52 27, 56 23.5, 62 24 C72 25, 73 36, 65 42 Z" fill="${fill}"/>
          <path d="M58 26 C65 28, 66 36, 60 42" fill="none" stroke="${shade}" stroke-width="3" stroke-linecap="round"/>
          ${base}
        `
      };

      const clsAttr = extraClass ? ` class="${extraClass}"` : '';
      return `<svg${clsAttr} viewBox="0 0 100 100" aria-hidden="true"><g fill="none" stroke="${stroke}" stroke-width="${sw}" stroke-linejoin="round" stroke-linecap="round">${art[code] || ''}</g></svg>`;
    }

    function renderCapturedList(pieces) {
      if (!Array.isArray(pieces) || !pieces.length) return 'None';
      return `<span class="cap-line">${pieces.map(p => renderPieceSvg(p, 'cap-piece-svg')).join('')}</span>`;
    }

    function isSignedIn() {
      return !!(session && session.handle);
    }

    function getMergedTournaments() {
      const map = new Map();
      const serverList = (backendReachable && Array.isArray(liveState?.tournaments)) ? liveState.tournaments : [];
      for (const t of serverList) {
        if (t && t.id) map.set(String(t.id), t);
      }
      for (const t of localTournaments) {
        if (t && t.id && !map.has(String(t.id))) map.set(String(t.id), t);
      }
      return Array.from(map.values());
    }

    function getMergedAnnouncements() {
      const serverList = (backendReachable && Array.isArray(liveState?.announcements)) ? liveState.announcements : [];
      return serverList.length ? serverList : localAnnouncements;
    }

    const ELO_DAILY_LIMIT_KEY = 'rochess_elo_connect_state_v1';
    function getTodayKey() { return new Date().toISOString().slice(0, 10); }

    function getUserEloConnectState(uid) {
      const all = JSON.parse(localStorage.getItem(ELO_DAILY_LIMIT_KEY) || '{}');
      const today = getTodayKey();
      const entry = all[uid] || { date: today, usedToday: false, randomStrikes: 0, lockedToday: false, elo: null };
      if (entry.date !== today) {
        return { date: today, usedToday: false, randomStrikes: 0, lockedToday: false, elo: entry.elo ?? null };
      }
      return entry;
    }

    function saveUserEloConnectState(uid, nextEntry) {
      const all = JSON.parse(localStorage.getItem(ELO_DAILY_LIMIT_KEY) || '{}');
      all[uid] = nextEntry;
      localStorage.setItem(ELO_DAILY_LIMIT_KEY, JSON.stringify(all));
    }

    function getCurrentUserElo() {
      const uid = session?.discordId || session?.userId || 'guest';
      const localEntry = getUserEloConnectState(uid);
      if (typeof localEntry.elo === 'number') return localEntry.elo;
      if (typeof liveState?.userProfile?.rochess_elo === 'number') return liveState.userProfile.rochess_elo;
      if (typeof liveState?.userProfile?.elo === 'number') return liveState.userProfile.elo;
      return CLUB_CONFIG.DEFAULT_ELO;
    }

    function getOpponentDisplay() {
      if (chess1v1.match?.mode === 'rated_1v1') {
        const oppName = chess1v1.match.userRole === 'black'
          ? (chess1v1.match.whiteUser || 'White Challenger')
          : (chess1v1.match.blackUser || 'Black Challenger');
        return { name: oppName, elo: CLUB_CONFIG.DEFAULT_ELO };
      }
      const opp = liveState?.activeMatch?.opponent || liveState?.opponent || null;
      return {
        name: opp?.handle || opp?.username || 'Black Opponent (1v1)',
        elo: typeof opp?.elo === 'number' ? opp.elo : (typeof opp?.rochess_elo === 'number' ? opp.rochess_elo : CLUB_CONFIG.DEFAULT_ELO)
      };
    }

    function renderOpponentAndEloBar() {
      const oppEl = document.getElementById('opponent-name-label');
      const oppEloEl = document.getElementById('opponent-elo-badge');
      const myEloEl = document.getElementById('user-rochess-elo-label');
      const btn = document.getElementById('connect-elo-btn');
      const limitTxt = document.getElementById('elo-daily-limit-text');
      if (!oppEl || !oppEloEl || !myEloEl || !btn || !limitTxt) return;

      const opp = getOpponentDisplay();
      const myElo = getCurrentUserElo();
      const uid = session?.discordId || session?.userId || 'guest';
      const st = getUserEloConnectState(uid);
      const isSub = hasSubscriberPerks();

      oppEl.textContent = opp.name;
      oppEloEl.textContent = `RoChess ELO: ${opp.elo}`;
      myEloEl.textContent = String(myElo);

      if (!isSub) {
        btn.disabled = true;
        limitTxt.textContent = 'Subscriber role required';
        return;
      }
      if (st.lockedToday) {
        btn.disabled = true;
        limitTxt.innerHTML = `<span style="color: var(--danger);">Locked for today (3 random images sent)</span>`;
        return;
      }
      if (st.usedToday) {
        btn.disabled = true;
        limitTxt.textContent = 'Already used today (1/1 per day)';
        return;
      }

      btn.disabled = false;
      limitTxt.textContent = `1/day · Random strikes: ${st.randomStrikes}/3`;
    }

    function fileToBase64(file) {
      return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.onload = () => {
          const result = String(reader.result || '');
          resolve(result.includes(',') ? result.split(',')[1] : result);
        };
        reader.onerror = reject;
        reader.readAsDataURL(file);
      });
    }

    function readFilesAsAttachments(fileList) {
      const files = Array.from(fileList || []);
      return Promise.all(
        files.map(file => new Promise((resolve) => {
          const reader = new FileReader();
          reader.onload = () => resolve({
            name: file.name,
            type: file.type,
            size: file.size,
            isImage: /^image\//i.test(file.type),
            dataUrl: String(reader.result || '')
          });
          reader.readAsDataURL(file);
        }))
      );
    }

    function bindEloProofEvents() {
      const btn = document.getElementById('connect-elo-btn');
      const fileInput = document.getElementById('elo-proof-file-input');
      if (!btn || !fileInput) return;

      btn.addEventListener('click', () => {
        const uid = session?.discordId || session?.userId;
        if (!uid) return openAuthModal();
        if (!hasSubscriberPerks()) return showToast('Subscriber role required to connect ELO');

        const st = getUserEloConnectState(uid);
        if (st.lockedToday) return showToast('Connect ELO is locked for the rest of today due to random images.');
        if (st.usedToday) return showToast('You can only connect ELO once per day.');

        fileInput.value = '';
        fileInput.click();
      });

      fileInput.addEventListener('change', async () => {
        const file = fileInput.files && fileInput.files[0];
        if (!file) return;
        const uid = session?.discordId || session?.userId;
        if (!uid) return openAuthModal();

        const st = getUserEloConnectState(uid);
        if (st.lockedToday || st.usedToday) return renderOpponentAndEloBar();

        showToast('Analyzing ELO proof image with AI...');
        pushMonitorLine('INFO', `elo_proof_submitted: ${session.handle} (${file.name})`);

        const base64Data = await fileToBase64(file);
        const res = await detailedApiRequest('/api/rochess/elo/verify-proof', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({
            userId: uid,
            handle: session.handle,
            mimeType: file.type || 'image/png',
            imageBase64: base64Data
          })
        });

        if (!res.ok) {
          showToast(res.errorMessage || 'Could not verify proof image');
          return;
        }

        const data = res.data || {};
        if (data.verdict === 'RANDOM_IMAGE') {
          const nextStrikes = (st.randomStrikes || 0) + 1;
          const lockedNow = nextStrikes >= 3 || !!data.lockedToday;
          saveUserEloConnectState(uid, { ...st, randomStrikes: nextStrikes, lockedToday: lockedNow });
          renderOpponentAndEloBar();
          if (lockedNow) {
            showToast('3 random images sent: Connect ELO locked for the rest of today.');
            pushMonitorLine('WARN', `elo_connect_locked: ${session.handle} locked for today`);
          } else {
            showToast(`Not a chess ELO proof image! Warning ${nextStrikes}/3 (locks at 3).`);
          }
          return;
        }

        if (data.verdict === 'FAKE_PROOF') {
          saveUserEloConnectState(uid, { ...st, usedToday: true });
          renderOpponentAndEloBar();
          showToast('Fake ELO proof detected! Alert sent to logs.');
          pushMonitorLine('ERROR', `fake_elo_proof: ${session.handle} (${uid}) platform=${data.platform || 'unknown'}`);
          return;
        }

        if (data.verdict === 'LEGIT' && typeof data.newElo === 'number') {
          saveUserEloConnectState(uid, { ...st, usedToday: true, elo: data.newElo });
          renderOpponentAndEloBar();
          showToast(`Verified ${data.platform} ELO! RoChess ELO updated to ${data.newElo}.`);
          pushMonitorLine('INFO', `elo_updated: ${session.handle} -> ${data.newElo} (${data.platform})`);
          return;
        }

        showToast(data.message || 'Proof could not be verified.');
      });
    }

    function renderLockedGate(viewId, title, desc) {
      document.getElementById(viewId).innerHTML = `
        <div class="gate-card">
          <span class="eyebrow">Verified Discord Member Required</span>
          <h2>${escapeHtml(title)}</h2>
          <p class="muted" style="margin: 7px 0 13px;">${escapeHtml(desc)}</p>
          <div style="display: flex; gap: 7px; justify-content: center; flex-wrap: wrap;">
            <button class="btn btn-primary guest-only" onclick="openAuthModal()">Sign In with Discord</button>
            <button class="btn btn-secondary" onclick="setActiveView('memberships')">View Memberships</button>
            <a class="btn btn-ghost" href="${escapeHtml(CLUB_CONFIG.DISCORD_INVITE_URL)}" target="_blank" rel="noopener noreferrer">Join Server</a>
          </div>
        </div>
      `;
    }

    function buildMemberViews() {
      if (!isSignedIn()) {
        renderLockedGate(
          'view-chess-tournaments',
          '1v1 Chess Board & Tournaments (Discord Members Only)',
          'Sign up with your Discord username and verify your DM code to challenge users or host tournaments.'
        );
        renderLockedGate(
          'view-puzzles',
          'Tactical Puzzle Trainer (Discord Members Only)',
          'Sign in with Discord to solve tactical chess puzzles and save your session progress.'
        );
        renderLockedGate(
          'view-announcements',
          'Official Announcements Channel (Discord Members Only)',
          'Sign in with Discord to read official club announcements. Only Management Team members can post.'
        );
        renderLockedGate(
          'view-mgmt-dm',
          'Requests & Management DMs (Discord Members Only)',
          'Sign in with Discord so role requests, username requests, and management DMs attach to your account.'
        );
        renderLockedGate(
          'view-standings',
          'Club Standings, Economy & Status (Discord Members Only)',
          'Sign in with Discord to inspect your linked profile, rating bands, Çess-to-Token converter, and live bot status.'
        );
        return;
      }

      const flags = getUserRoleFlags();
      const isSub = flags.isSubscriber;

      document.getElementById('view-chess-tournaments').innerHTML = `
        <div class="grid-2">
          <div class="card">
            <div class="row-between" style="margin-bottom: 6px;">
              <div>
                <span class="eyebrow" style="margin-bottom: 3px;">Full-Rules 1v1 Arena</span>
                <h2 style="margin: 0;">1v1 Chess Board</h2>
              </div>
              <div style="display: flex; gap: 6px; align-items: center; flex-wrap: wrap;">
                <button type="button" class="btn btn-gold btn-sm" id="open-1v1-challenge-btn">1v1 User</button>
                <span class="badge badge-ok" id="turn-label">${escapeHtml(chess1v1.statusText)}</span>
              </div>
            </div>
            <p class="small" style="margin-bottom: 8px;">
              Playing as <strong>${escapeHtml(session.handle)}</strong> · Full rules (en passant, castling, promotion, check/checkmate, stalemate, threefold repetition, king-vs-king) · 10:00 clock per side.
            </p>

            <div class="clock-bar">
              <div class="clock-box active-clock" id="white-clock-box">
                <div>
                  <div class="small"><strong>White Clock</strong></div>
                  <div class="small" id="white-player-label">${escapeHtml(chess1v1.match?.whiteUser || session.handle)}</div>
                </div>
                <span class="clock-time" id="white-clock-val">10:00</span>
              </div>
              <div class="clock-box" id="black-clock-box">
                <div>
                  <div class="small"><strong>Black Clock</strong></div>
                  <div class="small" id="black-player-label">${escapeHtml(chess1v1.match?.blackUser || 'Black Challenger')}</div>
                </div>
                <span class="clock-time" id="black-clock-val">10:00</span>
              </div>
            </div>

            <div class="box-item" id="match-opponent-box" style="margin-bottom: 8px;">
              <div class="row-between">
                <div>
                  <strong>Opponent:</strong> <span id="opponent-name-label">Black Challenger (1v1)</span>
                </div>
                <span class="badge badge-info" id="opponent-elo-badge">RoChess ELO: 1200</span>
              </div>
              <div class="small" style="margin-top: 4px;">
                <strong>Your RoChess ELO:</strong> <span id="user-rochess-elo-label">1200</span>
                ${chess1v1.match?.matchId ? ` · <strong>Match:</strong> <code>${escapeHtml(chess1v1.match.matchId)}</code>` : ''}
              </div>
              <div style="margin-top: 8px; display: flex; gap: 6px; flex-wrap: wrap; align-items: center;">
                <button type="button" class="btn btn-gold btn-sm" id="connect-elo-btn" ${isSub ? '' : 'disabled'}>
                  Connect ELO to RoChess
                </button>
                <input type="file" id="elo-proof-file-input" accept="image/*" style="display: none;" />
                <span class="small" id="elo-daily-limit-text"></span>
              </div>
            </div>

            <div class="board-wrap">
              <div class="board-grid-row">
                <div class="rank-labels">
                  <span>8</span><span>7</span><span>6</span><span>5</span><span>4</span><span>3</span><span>2</span><span>1</span>
                </div>
                <div class="board mat-classic" id="board-1v1" role="grid" aria-label="1v1 Chess Board"></div>
              </div>
              <div class="file-labels">
                <span>a</span><span>b</span><span>c</span><span>d</span><span>e</span><span>f</span><span>g</span><span>h</span>
              </div>
            </div>

            <div class="row-between" style="margin-top: 8px;">
              <div style="display: flex; gap: 6px; flex-wrap: wrap;">
                <button class="btn btn-secondary btn-sm" id="reset-1v1-btn">New Round</button>
                <button class="btn btn-ghost btn-sm" id="undo-1v1-btn">Undo Move</button>
                <button class="btn btn-ghost btn-sm" id="agree-draw-btn">Agree Draw (0 ELO)</button>
              </div>
              <span class="small" id="move-count-label">0 moves</span>
            </div>

            <div class="pay-panel" style="margin-top: 10px; margin-bottom: 0;">
              <div class="row-between" style="margin-bottom: 6px;">
                <strong>Theme &amp; Board Customization</strong>
                <span class="badge ${isSub ? 'badge-ok' : ''}">
                  ${isSub ? 'Subscriber Perks Active' : 'Free Theme · Sub for Board/Pieces'}
                </span>
              </div>

              <div class="custom-grid">
                <div class="field" style="margin-bottom: 0;">
                  <label for="site-theme-select">Site Theme (All Members)</label>
                  <select id="site-theme-select">
                    <option value="black">Black (Default)</option>
                    <option value="white">White</option>
                    <option value="black-blue">Black-Blue (Dark)</option>
                  </select>
                </div>

                <div class="field" style="margin-bottom: 0;">
                  <label for="board-material-select">Board Material (Subscriber)</label>
                  <select id="board-material-select" ${isSub ? '' : 'disabled'}>
                    <option value="classic">Classic Cream &amp; Green (Default)</option>
                    <option value="walnut">Walnut Wood</option>
                    <option value="mahogany">Maple &amp; Mahogany Wood</option>
                    <option value="slate">Slate &amp; Frost</option>
                    <option value="obsidian">Obsidian &amp; Steel</option>
                  </select>
                </div>

                <div class="field" style="margin-bottom: 0;">
                  <label for="piece-style-select">Piece Style (Subscriber)</label>
                  <select id="piece-style-select" ${isSub ? '' : 'disabled'}>
                    <option value="classic">Staunton Classic</option>
                    <option value="modern">Modern Sleek</option>
                  </select>
                </div>

                <div class="field" style="margin-bottom: 0;">
                  <label for="piece-color-select">Piece Colors (Subscriber)</label>
                  <select id="piece-color-select" ${isSub ? '' : 'disabled'}>
                    <option value="classic">Ivory &amp; Charcoal (Default)</option>
                    <option value="crimson">Ivory &amp; Crimson</option>
                    <option value="navy">Ice &amp; Deep Navy</option>
                  </select>
                </div>
              </div>
            </div>

            <div class="box-item" style="margin-top: 8px;">
              <div class="small"><strong>Captured by White:</strong> <span id="cap-white">None</span></div>
              <div class="small" style="margin-top: 4px;"><strong>Captured by Black:</strong> <span id="cap-black">None</span></div>
              <div class="small" style="margin-top: 6px;"><strong>Move Log:</strong> <span id="move-log">No moves yet</span></div>
            </div>
          </div>

          <div>
            <div class="card">
              <div class="row-between" style="margin-bottom: 6px;">
                <h2 style="margin: 0;">Club Tournaments</h2>
                <select id="tourn-filter" style="background: var(--surface-2); border: 1px solid var(--border); border-radius: var(--radius-sm); padding: 5px 8px; font-size: 0.78rem;">
                  <option value="ALL">All Formats</option>
                  <option value="Swiss Tournament">Swiss Tournament</option>
                  <option value="Rapid Arena">Rapid Arena</option>
                  <option value="Team / Simul Event">Team / Simul Event</option>
                  <option value="1v1 Bracket">1v1 Bracket</option>
                </select>
              </div>
              <div id="tournaments-list"></div>
            </div>

            <div class="card">
              <div class="row-between" style="margin-bottom: 4px;">
                <h2 style="margin: 0;">Host Event / Tournament</h2>
                <span class="badge" id="host-status-badge">Checking</span>
              </div>
              <p class="small" id="host-gate-msg" style="margin-bottom: 8px;"></p>

              <form id="host-event-form">
                <div class="field">
                  <label for="ev-title">Event Title</label>
                  <input id="ev-title" type="text" required placeholder="e.g. RoChess Rapid Championship" />
                </div>
                <div class="field">
                  <label for="ev-format">Format</label>
                  <select id="ev-format">
                    <option value="Swiss Tournament">Swiss Tournament</option>
                    <option value="Rapid Arena">Rapid Arena</option>
                    <option value="Team / Simul Event">Team / Simul Event</option>
                    <option value="1v1 Bracket">1v1 Bracket</option>
                  </select>
                </div>
                <div class="field">
                  <label for="ev-link">Match / Bracket Link (Optional)</label>
                  <input id="ev-link" type="url" placeholder="https://..." />
                </div>
                <div class="field">
                  <label for="ev-desc">Details &amp; Time Control</label>
                  <textarea id="ev-desc" placeholder="Rounds, time control, or entry notes..."></textarea>
                </div>
                <button class="btn btn-primary" type="submit" id="host-submit-btn">Publish Event</button>
              </form>
            </div>
          </div>
        </div>
      `;

      document.getElementById('view-puzzles').innerHTML = `
        <div class="grid-2">
          <div class="card">
            <div class="row-between" style="margin-bottom: 6px;">
              <div>
                <span class="eyebrow" style="margin-bottom: 3px;">Interactive Drills</span>
                <h2 style="margin: 0;" id="puzzle-title"></h2>
              </div>
              <select id="puzzle-select" style="background: var(--surface-2); border: 1px solid var(--border); border-radius: var(--radius-sm); padding: 5px 8px; font-size: 0.78rem;">
                ${TACTICAL_PUZZLES.map((p, idx) => `<option value="${idx}">Puzzle ${idx + 1}: ${escapeHtml(p.title)}</option>`).join('')}
              </select>
            </div>
            <p class="muted" id="puzzle-prompt" style="margin-bottom: 8px;"></p>

            <div class="board-wrap">
              <div class="board-grid-row">
                <div class="rank-labels">
                  <span>8</span><span>7</span><span>6</span><span>5</span><span>4</span><span>3</span><span>2</span><span>1</span>
                </div>
                <div class="board mat-classic" id="puzzle-board" role="grid" aria-label="Tactical Puzzle Board"></div>
              </div>
              <div class="file-labels">
                <span>a</span><span>b</span><span>c</span><span>d</span><span>e</span><span>f</span><span>g</span><span>h</span>
              </div>
            </div>

            <div class="row-between" style="margin-top: 8px;">
              <div style="display: flex; gap: 6px; flex-wrap: wrap;">
                <button class="btn btn-secondary btn-sm" id="puzzle-hint-btn">Show Hint</button>
                <button class="btn btn-ghost btn-sm" id="puzzle-reset-btn">Reset Position</button>
              </div>
              <button class="btn btn-primary btn-sm" id="puzzle-next-btn">Next Puzzle →</button>
            </div>
          </div>

          <div class="card">
            <h2>Tactics Session Progress</h2>
            <p class="small">Linked to <strong>${escapeHtml(session.handle)}</strong></p>
            <div class="grid-2" style="margin: 8px 0;">
              <div class="kpi-box">
                <div class="kpi-val" id="puz-solved-val">${puzzleStats.solved}</div>
                <div class="kpi-lbl">Drills Solved</div>
              </div>
              <div class="kpi-box">
                <div class="kpi-val" id="puz-streak-val">${puzzleStats.streak}</div>
                <div class="kpi-lbl">Current Streak</div>
              </div>
            </div>
            <div class="box-item" id="puzzle-feedback">
              Select the piece to move on the board, then click its target square.
            </div>
          </div>
        </div>
      `;

      document.getElementById('view-announcements').innerHTML = `
        <div class="grid-2">
          <div class="card">
            <div class="row-between" style="margin-bottom: 6px;">
              <div>
                <span class="eyebrow" style="margin-bottom: 3px;">Management-Only Posting</span>
                <h2 style="margin: 0;">Post Official Announcement</h2>
              </div>
              <span class="badge ${flags.isManagement ? 'badge-ok' : 'badge-warn'}">
                ${flags.isManagement ? 'Management Authorized' : 'Read-Only'}
              </span>
            </div>
            <p class="small" style="margin-bottom: 9px;">
              Only members with a <strong>Management</strong> role can publish announcements. Supports text, links, image URLs, and file attachments.
            </p>
            ${flags.isManagement ? `
              <form id="announcement-post-form">
                <div class="field">
                  <label for="ann-text">Announcement Text &amp; Links *</label>
                  <textarea id="ann-text" placeholder="Write announcement text or paste https:// links..."></textarea>
                </div>
                <div class="field">
                  <label for="ann-image-url">Image URL (Optional)</label>
                  <input id="ann-image-url" type="url" placeholder="https://example.com/banner.png" />
                </div>
                <div class="field">
                  <label for="ann-files">Attachments / Images (Optional)</label>
                  <input id="ann-files" type="file" multiple />
                </div>
                <button class="btn btn-primary" type="submit" id="ann-submit-btn">Publish Announcement</button>
              </form>
            ` : `
              <div class="box-item">
                <strong style="color: var(--gold);">Posting Restricted to Management</strong>
                <p class="small" style="margin-top: 3px;">
                  You can read all announcements on the right, but only Management Team members can post new messages, images, or attachments.
                </p>
              </div>
            `}
          </div>

          <div class="card">
            <h2>Official Announcements Feed</h2>
            <p class="small" style="margin-bottom: 8px;">Latest club announcements, links, images, and files.</p>
            <div id="announcements-list"></div>
          </div>
        </div>
      `;

      document.getElementById('view-mgmt-dm').innerHTML = `
        <div class="grid-2">
          <div class="card">
            <span class="eyebrow">Club Desk</span>
            <h2>Role / Username Request &amp; Management DM</h2>
            <p class="muted" style="margin-bottom: 9px;">
              Verified as <strong>${escapeHtml(session.handle)}</strong> on Discord. Management role assignment is restricted to Management staff.
            </p>

            <form id="mgmt-dm-form">
              <div class="field">
                <label for="req-type">Request / Message Type</label>
                <select id="req-type">
                  <option value="Role Request">Role Request</option>
                  <option value="Username Request">Username Request</option>
                  <option value="Management DM">Direct Message to Management</option>
                </select>
              </div>
              <div class="field">
                <label for="req-value">Requested Role or Username</label>
                <input id="req-value" type="text" placeholder="e.g. Verified, Event Host, or new_handle" />
              </div>
              <div class="field">
                <label for="req-msg">Message to Management</label>
                <textarea id="req-msg" required placeholder="Write your request or message..."></textarea>
              </div>
              <label style="display: flex; align-items: center; gap: 6px; font-size: 0.78rem; color: var(--soft); margin-bottom: 9px; cursor: pointer;">
                <input type="checkbox" id="also-discord-dm" />
                <span>Forward to Owner via Discord DM (when bot bridge is active)</span>
              </label>
              <button class="btn btn-primary" type="submit">Send to Management</button>
            </form>
          </div>

          <div class="card">
            <div class="row-between" style="margin-bottom: 6px;">
              <h2 style="margin: 0;">Management Thread</h2>
              <button class="btn btn-ghost btn-sm" id="clear-local-dm-btn">Clear Local Feed</button>
            </div>
            <div class="dm-feed" id="dm-feed"></div>
            <h3>Logged Requests</h3>
            <div id="requests-log" style="margin-top: 5px;"></div>
          </div>
        </div>
      `;

      document.getElementById('view-standings').innerHTML = `
        <div class="grid-2">
          <div>
            <div class="card">
              <span class="eyebrow">Verified Discord Member</span>
              <h2>Linked Discord Account</h2>
              <div class="box-item">
                <div><strong>Discord Username:</strong> ${escapeHtml(session.handle)} <span class="badge badge-ok">Verified</span></div>
                <div class="small" style="margin-top: 2px;"><strong>Discord ID:</strong> <code>${escapeHtml(session.discordId || session.userId)}</code> · <strong>RoChess ELO:</strong> <strong>${getCurrentUserElo()}</strong></div>
                <div class="small" style="margin-top: 2px;"><strong>Access Tier:</strong> ${flags.isManagement ? '<span class="badge badge-ok">Management Team</span>' : (flags.isEntertainment ? '<span class="badge badge-info">Entertainment Team</span>' : '<span class="badge">Member</span>')}</div>
              </div>
            </div>

            <div class="card">
              <div class="row-between" style="margin-bottom: 6px;">
                <div>
                  <span class="eyebrow" style="margin-bottom: 3px;">Live Telemetry</span>
                  <h2 style="margin: 0;">Bot &amp; Database Status</h2>
                </div>
                <button class="btn btn-secondary btn-sm" id="refresh-state-btn">Refresh</button>
              </div>
              <div id="live-db-summary" class="muted">Checking status...</div>
            </div>

            <div class="card">
              <h2>Çess-to-Token Converter (6,000 : 1)</h2>
              <p class="small" style="margin-bottom: 7px;">Calculate how many Tokens a Çess balance converts to at 6,000 Çess per Token.</p>
              <div class="field">
                <label for="chess-coins-input">Çess Amount</label>
                <input id="chess-coins-input" type="number" min="0" step="100" value="18000" />
              </div>
              <div class="box-item" id="token-calc-output">
                <strong>Tokens:</strong> 3 Tokens <span class="small">(0 Çess remainder)</span>
              </div>
            </div>
          </div>

          <div class="card">
            <h2>Club Rating Bands</h2>
            <p class="small" style="margin-bottom: 7px;">Standard club progression tiers for internal play and events.</p>
            ${RATING_BANDS.map(r => `
              <div class="meta-row" style="margin-bottom: 5px;">
                <div><strong>${escapeHtml(r.band)}</strong> <span class="small">(${escapeHtml(r.role)})</span></div>
                <span class="badge">${escapeHtml(r.range)}</span>
              </div>
            `).join('')}
          </div>
        </div>
      `;

      bindMemberListeners();
      bindEloProofEvents();
      renderOpponentAndEloBar();
      render1v1Board();
      updateClockDisplay();
      loadPuzzle(activePuzzleIdx);
      renderTokenConverter();
      renderConnectedViews();
    }

    function renderTokenConverter() {
      const input = document.getElementById('chess-coins-input');
      const out = document.getElementById('token-calc-output');
      if (!input || !out) return;
      const amt = Math.max(0, Math.floor(Number(input.value) || 0));
      const tokens = Math.floor(amt / CLUB_CONFIG.CHESS_PER_TOKEN);
      const rem = amt % CLUB_CONFIG.CHESS_PER_TOKEN;
      out.innerHTML = `<strong>Tokens:</strong> ${tokens.toLocaleString()} ${tokens === 1 ? 'Token' : 'Tokens'} <span class="small">(${rem.toLocaleString()} Çess remainder)</span>`;
    }

    function renderAnnouncementsFeed() {
      const listEl = document.getElementById('announcements-list');
      if (!listEl) return;
      const items = getMergedAnnouncements();
      if (!items.length) {
        listEl.innerHTML = `<p class="small">No official announcements posted yet.</p>`;
        return;
      }

      listEl.innerHTML = items.map(a => {
        const imgHtml = a.imageUrl
          ? `<img class="announce-img" src="${escapeHtml(a.imageUrl)}" alt="Announcement banner" />`
          : '';
        const filesHtml = Array.isArray(a.attachments) && a.attachments.length
          ? `<div style="display: flex; gap: 6px; flex-wrap: wrap;">${a.attachments.map(att =>
              att.isImage && att.dataUrl
                ? `<img class="announce-img" src="${escapeHtml(att.dataUrl)}" alt="${escapeHtml(att.name || 'Attachment')}" />`
                : `<a class="attach-chip" href="${escapeHtml(att.dataUrl || '#')}" download="${escapeHtml(att.name || 'file')}">📎 ${escapeHtml(att.name || 'Attachment')}</a>`
            ).join('')}</div>`
          : '';

        return `
          <div class="box-item">
            <div class="row-between">
              <strong>📢 ${escapeHtml(a.authorName || 'Management')}</strong>
              <span class="small">${a.createdAt ? escapeHtml(new Date(a.createdAt).toLocaleString()) : ''}</span>
            </div>
            ${a.text ? `<div style="margin-top: 4px;">${linkifyEscapedText(a.text)}</div>` : ''}
            ${imgHtml}
            ${filesHtml}
          </div>
        `;
      }).join('');
    }

    function bindMemberListeners() {
      const themeSel = document.getElementById('site-theme-select');
      const matSel = document.getElementById('board-material-select');
      const pStyleSel = document.getElementById('piece-style-select');
      const pColorSel = document.getElementById('piece-color-select');

      if (themeSel) {
        themeSel.value = boardPrefs.siteTheme;
        themeSel.addEventListener('change', () => {
          boardPrefs.siteTheme = themeSel.value;
          applySiteTheme();
        });
      }
      if (matSel) {
        matSel.value = hasSubscriberPerks() ? boardPrefs.material : 'classic';
        matSel.addEventListener('change', () => {
          if (!hasSubscriberPerks()) return showToast('Subscriber role required');
          boardPrefs.material = matSel.value;
          localStorage.setItem('rochess_board_prefs', JSON.stringify(boardPrefs));
          render1v1Board();
        });
      }
      if (pStyleSel) {
        pStyleSel.value = hasSubscriberPerks() ? boardPrefs.pieceStyle : 'classic';
        pStyleSel.addEventListener('change', () => {
          if (!hasSubscriberPerks()) return showToast('Subscriber role required');
          boardPrefs.pieceStyle = pStyleSel.value;
          localStorage.setItem('rochess_board_prefs', JSON.stringify(boardPrefs));
          render1v1Board();
          renderPuzzleBoard();
        });
      }
      if (pColorSel) {
        pColorSel.value = hasSubscriberPerks() ? boardPrefs.pieceColors : 'classic';
        pColorSel.addEventListener('change', () => {
          if (!hasSubscriberPerks()) return showToast('Subscriber role required');
          boardPrefs.pieceColors = pColorSel.value;
          localStorage.setItem('rochess_board_prefs', JSON.stringify(boardPrefs));
          render1v1Board();
          renderPuzzleBoard();
        });
      }

      const chalBtn = document.getElementById('open-1v1-challenge-btn');
      if (chalBtn) {
        chalBtn.addEventListener('click', openChallengeModal);
      }

      const reset1v1 = document.getElementById('reset-1v1-btn');
      if (reset1v1) {
        reset1v1.addEventListener('click', () => {
          chess1v1 = createFreshChessState(chess1v1.match?.mode === 'rated_1v1' ? chess1v1.match : null);
          render1v1Board();
          updateClockDisplay();
          playChessSound('notify');
          showToast('New 1v1 round started — White to move');
          pushMonitorLine('INFO', '1v1_board_reset');
        });
      }

      const undo1v1 = document.getElementById('undo-1v1-btn');
      if (undo1v1) {
        undo1v1.addEventListener('click', () => {
          if (chess1v1.gameOver) return showToast('Match is finished. Start a New Round.');
          const prev = chess1v1.history.pop();
          if (!prev) return showToast('No moves to undo');
          chess1v1.board = prev.board;
          chess1v1.turn = prev.turn;
          chess1v1.moves = prev.moves;
          chess1v1.capturedByWhite = prev.capturedByWhite;
          chess1v1.capturedByBlack = prev.capturedByBlack;
          chess1v1.moveLog = prev.moveLog;
          chess1v1.castling = prev.castling;
          chess1v1.enPassantTarget = prev.enPassantTarget;
          chess1v1.positionCounts = prev.positionCounts;
          chess1v1.selected = null;
          chess1v1.legalTargets = [];
          chess1v1.statusText = `${chess1v1.turn === 'white' ? 'White' : 'Black'} to Move (1v1)`;
          render1v1Board();
          playChessSound('move');
          showToast('Undid last move');
          pushMonitorLine('INFO', '1v1_board_undo');
        });
      }

      const drawBtn = document.getElementById('agree-draw-btn');
      if (drawBtn) {
        drawBtn.addEventListener('click', () => {
          if (chess1v1.gameOver) return showToast('Game already ended.');
          applyMatchEloOutcome('agreed_draw', null, 'Draw agreed by both players');
          render1v1Board();
          updateClockDisplay();
          showToast('Agreed draw: 0 ELO change for both players');
        });
      }

      const tournFilter = document.getElementById('tourn-filter');
      if (tournFilter) {
        tournFilter.addEventListener('change', () => {
          renderConnectedViews();
          pushMonitorLine('INFO', `tournament_filter: ${tournFilter.value}`);
        });
      }

      const hostForm = document.getElementById('host-event-form');
      if (hostForm) {
        hostForm.addEventListener('submit', async (e) => {
          e.preventDefault();
          const flags = getUserRoleFlags();
          if (!flags.canHostEvent) {
            return showToast('Blocked: Only Management or Entertainment Team can host events.');
          }
          const title = document.getElementById('ev-title').value.trim();
          const format = document.getElementById('ev-format').value;
          const link = document.getElementById('ev-link').value.trim();
          const description = document.getElementById('ev-desc').value.trim();
          if (!title) return showToast('Enter an event title');

          const res = await detailedApiRequest('/api/rochess/events/host', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({
              userId: session?.discordId || session?.userId || '',
              handle: session?.handle || '',
              title,
              format,
              link,
              description,
              announceInDiscord: true
            })
          });

          if (!res.ok) {
            if (backendReachable) {
              return showToast(res.data?.error || res.errorMessage || 'Host role required');
            }
            localTournaments.unshift({
              id: `t_${Date.now()}`,
              title,
              format,
              hostName: session?.handle || 'Club Host',
              link,
              description
            });
            localStorage.setItem('rochess_web_tournaments', JSON.stringify(localTournaments));
          }

          hostForm.reset();
          renderConnectedViews();
          renderPublicSchedule();
          await fetchLiveState();
          showToast('Event published');
          pushMonitorLine('INFO', `event_hosted: ${title} (${format})`);
        });
      }

      const annForm = document.getElementById('announcement-post-form');
      if (annForm) {
        annForm.addEventListener('submit', async (e) => {
          e.preventDefault();
          const flags = getUserRoleFlags();
          if (!flags.isManagement) {
            return showToast('Blocked: Only Management Team members can post announcements.');
          }

          const text = document.getElementById('ann-text').value.trim();
          const imageUrl = document.getElementById('ann-image-url').value.trim();
          const fileInput = document.getElementById('ann-files');
          const attachments = await readFilesAsAttachments(fileInput?.files);

          if (!text && !imageUrl && !attachments.length) {
            return showToast('Add text, a link, an image URL, or an attachment first.');
          }

          const entry = {
            id: `ann_${Date.now()}`,
            text,
            imageUrl,
            attachments,
            authorName: session.handle,
            authorId: session.discordId || session.userId,
            createdAt: new Date().toISOString()
          };

          const res = await detailedApiRequest('/api/rochess/announcements/post', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({
              userId: session.discordId || session.userId,
              handle: session.handle,
              announcement: entry
            })
          });

          if (!res.ok && backendReachable) {
            return showToast(res.data?.error || res.errorMessage || 'Management role required');
          }

          if (!Array.isArray(res.data?.announcements)) {
            localAnnouncements.unshift(entry);
            localStorage.setItem(ANNOUNCEMENTS_STORAGE_KEY, JSON.stringify(localAnnouncements));
          }

          annForm.reset();
          renderAnnouncementsFeed();
          if (res.ok) await fetchLiveState();
          showToast('Announcement published');
          pushMonitorLine('INFO', `announcement_posted: by ${session.handle}`);
        });
      }

      const puzSelect = document.getElementById('puzzle-select');
      if (puzSelect) {
        puzSelect.value = String(activePuzzleIdx);
        puzSelect.addEventListener('change', () => loadPuzzle(Number(puzSelect.value)));
      }

      const puzHint = document.getElementById('puzzle-hint-btn');
      if (puzHint) {
        puzHint.addEventListener('click', () => {
          document.getElementById('puzzle-feedback').innerHTML = `<strong>Hint:</strong> ${escapeHtml(TACTICAL_PUZZLES[activePuzzleIdx].hint)}`;
          pushMonitorLine('INFO', `puzzle_hint: ${TACTICAL_PUZZLES[activePuzzleIdx].id}`);
        });
      }

      const puzReset = document.getElementById('puzzle-reset-btn');
      if (puzReset) {
        puzReset.addEventListener('click', () => {
          loadPuzzle(activePuzzleIdx);
          showToast('Puzzle reset');
        });
      }

      const puzNext = document.getElementById('puzzle-next-btn');
      if (puzNext) {
        puzNext.addEventListener('click', () => {
          loadPuzzle((activePuzzleIdx + 1) % TACTICAL_PUZZLES.length);
        });
      }

      const mgmtForm = document.getElementById('mgmt-dm-form');
      if (mgmtForm) {
        mgmtForm.addEventListener('submit', async (e) => {
          e.preventDefault();
          const requestType = document.getElementById('req-type').value;
          const requestedValue = document.getElementById('req-value').value.trim();
          const messageText = document.getElementById('req-msg').value.trim();
          if (!messageText) return showToast('Enter a message first');

          const flags = getUserRoleFlags();
          if (requestType === 'Role Request' && /management|founder|admin|head of moderation/i.test(requestedValue) && !flags.isManagement) {
            return showToast('Blocked: Only Management staff can assign or approve management roles.');
          }

          const sendToDiscordDm = document.getElementById('also-discord-dm').checked;
          const senderHandle = session.handle;
          const senderId = session.discordId || session.userId;

          await detailedApiRequest('/api/rochess/management-dm', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({
              senderId,
              senderHandle,
              provider: 'discord',
              requestType,
              requestedValue,
              messageText,
              sendToDiscordDm
            })
          });

          localDmThreads.push({
            id: `dm_${Date.now()}`,
            senderHandle,
            requestType,
            requestedValue,
            text: messageText,
            time: new Date().toISOString()
          });
          localStorage.setItem('rochess_web_dm_threads', JSON.stringify(localDmThreads));

          if (requestType === 'Role Request' || requestType === 'Username Request') {
            localRequests.unshift({
              id: `REQ-${Math.floor(1000 + Math.random() * 9000)}`,
              type: requestType,
              requestedValue: requestedValue || messageText.slice(0, 50),
              handle: senderHandle,
              status: 'Submitted'
            });
            localStorage.setItem('rochess_web_requests', JSON.stringify(localRequests));
          }

          mgmtForm.reset();
          renderConnectedViews();
          await fetchLiveState();
          showToast('Sent to management');
          pushMonitorLine('INFO', `mgmt_dm_sent: ${requestType} (${requestedValue || 'general'})`);
        });
      }

      const clearDmBtn = document.getElementById('clear-local-dm-btn');
      if (clearDmBtn) {
        clearDmBtn.addEventListener('click', () => {
          localDmThreads = [];
          localRequests = [];
          localStorage.setItem('rochess_web_dm_threads', '[]');
          localStorage.setItem('rochess_web_requests', '[]');
          renderConnectedViews();
          showToast('Local thread cleared');
        });
      }

      const refreshBtn = document.getElementById('refresh-state-btn');
      if (refreshBtn) {
        refreshBtn.addEventListener('click', async () => {
          await fetchLiveState();
          showToast('Status refreshed');
          pushMonitorLine('INFO', 'status_refresh: refreshed bot & DB state');
        });
      }

      const chessCoinsInput = document.getElementById('chess-coins-input');
      if (chessCoinsInput) {
        chessCoinsInput.addEventListener('input', renderTokenConverter);
      }
    }

    function render1v1Board() {
      const boardEl = document.getElementById('board-1v1');
      if (!boardEl) return;
      const matClass = hasSubscriberPerks() ? `mat-${boardPrefs.material}` : 'mat-classic';
      boardEl.className = `board ${matClass}`;
      boardEl.innerHTML = '';

      const turnBadge = document.getElementById('turn-label');
      if (turnBadge) {
        turnBadge.textContent = chess1v1.statusText;
        turnBadge.className = `badge ${chess1v1.gameOver ? 'badge-warn' : 'badge-ok'}`;
      }
      document.getElementById('move-count-label').textContent = `${chess1v1.moves} ${chess1v1.moves === 1 ? 'move' : 'moves'}`;
      document.getElementById('cap-white').innerHTML = renderCapturedList(chess1v1.capturedByWhite);
      document.getElementById('cap-black').innerHTML = renderCapturedList(chess1v1.capturedByBlack);
      document.getElementById('move-log').textContent = chess1v1.moveLog.length ? chess1v1.moveLog.slice(-10).join(', ') : 'No moves yet';

      const checkedKing = !chess1v1.gameOver && isInCheck(chess1v1.board, chess1v1.turn)
        ? findKing(chess1v1.board, chess1v1.turn)
        : null;

      for (let r = 0; r < 8; r++) {
        for (let c = 0; c < 8; c++) {
          const sq = document.createElement('button');
          sq.type = 'button';
          const isLight = (r + c) % 2 === 0;
          const isSelected = chess1v1.selected && chess1v1.selected.r === r && chess1v1.selected.c === c;
          const legalMove = chess1v1.legalTargets.find(m => m.to.r === r && m.to.c === c);
          const isCheckedSq = checkedKing && checkedKing.r === r && checkedKing.c === c;

          let cls = `sq ${isLight ? 'light' : 'dark'}`;
          if (isSelected) cls += ' selected';
          if (isCheckedSq) cls += ' in-check';
          if (legalMove) cls += legalMove.capture ? ' legal-capture' : ' legal-dot';

          sq.className = cls;
          sq.innerHTML = renderPieceSvg(chess1v1.board[r][c]);
          sq.setAttribute('aria-label', sqName(r, c));
          sq.addEventListener('click', () => on1v1Click(r, c));
          boardEl.appendChild(sq);
        }
      }
    }

    function on1v1Click(r, c) {
      if (chess1v1.gameOver) {
        return showToast('This round has ended. Click "New Round" or "1v1 User".');
      }

      const cell = chess1v1.board[r][c];
      const cellColor = pieceColor(cell);

      // Clicking a legal target square for the selected piece
      if (chess1v1.selected) {
        const chosen = chess1v1.legalTargets.find(m => m.to.r === r && m.to.c === c);
        if (chosen) {
          executeLegal1v1Move(chosen);
          return;
        }
      }

      // Clicking a friendly piece of the active turn selects it and highlights legal moves
      if (cellColor === chess1v1.turn) {
        const legal = getLegalMovesForSquare(chess1v1, r, c);
        chess1v1.selected = { r, c };
        chess1v1.legalTargets = legal;
        playChessSound('select');
        render1v1Board();
        return;
      }

      chess1v1.selected = null;
      chess1v1.legalTargets = [];
      render1v1Board();
      if (cell) {
        showToast(`Illegal square or ${chess1v1.turn === 'white' ? 'White' : 'Black'}'s turn`);
      }
    }

    function executeLegal1v1Move(move) {
      chess1v1.history.push({
        board: cloneBoard(chess1v1.board),
        turn: chess1v1.turn,
        moves: chess1v1.moves,
        capturedByWhite: [...chess1v1.capturedByWhite],
        capturedByBlack: [...chess1v1.capturedByBlack],
        moveLog: [...chess1v1.moveLog],
        castling: { ...chess1v1.castling },
        enPassantTarget: chess1v1.enPassantTarget ? { ...chess1v1.enPassantTarget } : null,
        positionCounts: { ...chess1v1.positionCounts }
      });

      const moverColor = chess1v1.turn;
      const sim = applyMoveToBoardState(chess1v1, move);
      chess1v1.board = sim.board;
      chess1v1.castling = sim.castling;
      chess1v1.enPassantTarget = sim.enPassantTarget;

      if (sim.capturedPiece) {
        if (moverColor === 'white') chess1v1.capturedByWhite.push(sim.capturedPiece);
        else chess1v1.capturedByBlack.push(sim.capturedPiece);
      }

      chess1v1.selected = null;
      chess1v1.legalTargets = [];
      chess1v1.moves += 1;

      const suffix = move.castle ? ` (${move.castle === 'K' ? 'O-O' : 'O-O-O'})` : (move.enPassant ? ' e.p.' : (move.promotion ? '=Q' : ''));
      const moveNotation = `${sqName(move.from.r, move.from.c)}→${sqName(move.to.r, move.to.c)}${suffix}`;
      chess1v1.moveLog.push(moveNotation);

      const nextTurn = moverColor === 'white' ? 'black' : 'white';
      chess1v1.turn = nextTurn;

      const posKey = boardPositionKey(chess1v1);
      chess1v1.positionCounts[posKey] = (chess1v1.positionCounts[posKey] || 0) + 1;

      const oppHasLegal = getAllLegalMoves(chess1v1, nextTurn).length > 0;
      const oppInCheck = isInCheck(chess1v1.board, nextTurn);

      if (!oppHasLegal && oppInCheck) {
        const winnerName = moverColor === 'white' ? 'White' : 'Black';
        applyMatchEloOutcome('win', moverColor, `Checkmate — ${winnerName} wins`);
      } else if (!oppHasLegal && !oppInCheck) {
        applyMatchEloOutcome('draw_penalty', null, 'Stalemate — Draw (-1 ELO each)');
      } else if (chess1v1.positionCounts[posKey] >= 3) {
        applyMatchEloOutcome('draw_penalty', null, 'Threefold Repetition — Draw (-1 ELO each)');
      } else if (isOnlyTwoKingsRemaining(chess1v1.board)) {
        applyMatchEloOutcome('draw_penalty', null, 'Only Two Kings Remain — Draw (-1 ELO each)');
      } else {
        chess1v1.statusText = oppInCheck
          ? `Check! ${nextTurn === 'white' ? 'White' : 'Black'} to Move`
          : `${nextTurn === 'white' ? 'White' : 'Black'} to Move (1v1)`;
        if (oppInCheck) playChessSound('check');
        else if (move.castle) playChessSound('castle');
        else if (move.capture) playChessSound('capture');
        else playChessSound('move');
      }

      render1v1Board();
      updateClockDisplay();
      pushMonitorLine('INFO', `1v1_legal_move: ${moveNotation} -> ${chess1v1.statusText}`);
    }

    function loadPuzzle(idx) {
      activePuzzleIdx = ((idx % TACTICAL_PUZZLES.length) + TACTICAL_PUZZLES.length) % TACTICAL_PUZZLES.length;
      const p = TACTICAL_PUZZLES[activePuzzleIdx];
      puzzleBoard = p.board.map(r => [...r]);
      puzzleSelected = null;

      const titleEl = document.getElementById('puzzle-title');
      const promptEl = document.getElementById('puzzle-prompt');
      if (titleEl) titleEl.textContent = p.title;
      if (promptEl) promptEl.textContent = p.prompt;
      renderPuzzleBoard();
    }

    function renderPuzzleBoard() {
      const el = document.getElementById('puzzle-board');
      if (!el) return;
      const matClass = hasSubscriberPerks() ? `mat-${boardPrefs.material}` : 'mat-classic';
      el.className = `board ${matClass}`;
      el.innerHTML = '';
      for (let r = 0; r < 8; r++) {
        for (let c = 0; c < 8; c++) {
          const sq = document.createElement('button');
          sq.type = 'button';
          const isLight = (r + c) % 2 === 0;
          const isSel = puzzleSelected && puzzleSelected.r === r && puzzleSelected.c === c;
          sq.className = `sq ${isLight ? 'light' : 'dark'}${isSel ? ' selected' : ''}`;
          sq.innerHTML = renderPieceSvg(puzzleBoard[r][c]);
          sq.addEventListener('click', () => onPuzzleClick(r, c));
          el.appendChild(sq);
        }
      }
    }

    function onPuzzleClick(r, c) {
      const p = TACTICAL_PUZZLES[activePuzzleIdx];
      const fb = document.getElementById('puzzle-feedback');
      if (!puzzleSelected) {
        if (r === p.from[0] && c === p.from[1]) {
          puzzleSelected = { r, c };
          playChessSound('select');
          renderPuzzleBoard();
        } else {
          fb.innerHTML = `<span style="color: var(--gold);">Select the intended piece first, or click <strong>Show Hint</strong>.</span>`;
        }
        return;
      }

      if (r === p.to[0] && c === p.to[1]) {
        const hadTarget = !!puzzleBoard[r][c];
        puzzleBoard[r][c] = puzzleBoard[puzzleSelected.r][puzzleSelected.c];
        puzzleBoard[puzzleSelected.r][puzzleSelected.c] = '';
        puzzleSelected = null;
        renderPuzzleBoard();
        playChessSound(hadTarget ? 'capture' : 'move');

        puzzleStats.solved += 1;
        puzzleStats.streak += 1;
        localStorage.setItem('rochess_web_puzzle_stats', JSON.stringify(puzzleStats));
        document.getElementById('puz-solved-val').textContent = puzzleStats.solved;
        document.getElementById('puz-streak-val').textContent = puzzleStats.streak;
        fb.innerHTML = `<span style="color: var(--emerald);"><strong>Solved!</strong> Great tactical move. Click <strong>Next Puzzle</strong> for another drill.</span>`;
        showToast('Puzzle solved!');
        pushMonitorLine('INFO', `puzzle_solved: ${p.id} (streak ${puzzleStats.streak})`);
      } else {
        puzzleSelected = null;
        puzzleStats.streak = 0;
        localStorage.setItem('rochess_web_puzzle_stats', JSON.stringify(puzzleStats));
        document.getElementById('puz-streak-val').textContent = '0';
        renderPuzzleBoard();
        fb.innerHTML = `<span style="color: var(--danger);">Not that square. Try again or click <strong>Show Hint</strong>.</span>`;
      }
    }

    window.toggleJoinTournament = function(id) {
      if (!isSignedIn()) return openAuthModal();
      let statusLabel = 'Registered';
      if (joinedTournamentIds.includes(id)) {
        joinedTournamentIds = joinedTournamentIds.filter(x => x !== id);
        statusLabel = 'Withdrew';
        showToast('Withdrew registration');
      } else {
        joinedTournamentIds.push(id);
        showToast('Registered for tournament');
      }
      localStorage.setItem('rochess_web_joined_tournaments', JSON.stringify(joinedTournamentIds));
      renderConnectedViews();
      pushMonitorLine('INFO', `tournament_reg: ${statusLabel} for ${id}`);
    };

    function escapeHtml(str) {
      return String(str || '')
        .replace(/&/g, '&amp;')
        .replace(/</g, '&lt;')
        .replace(/>/g, '&gt;')
        .replace(/"/g, '&quot;');
    }

    function linkifyEscapedText(text) {
      const safe = escapeHtml(text);
      return safe.replace(
        /(https?:\/\/[^\s<]+)/g,
        '<a href="$1" target="_blank" rel="noopener noreferrer">$1</a>'
      );
    }

    function showToast(msg) {
      const el = document.getElementById('toast');
      if (!el) return;
      el.textContent = sanitizePublicText(msg);
      el.classList.add('show');
      clearTimeout(showToast._t);
      showToast._t = setTimeout(() => el.classList.remove('show'), 2800);
    }

    function pushMonitorLine(level, text) {
      const ts = new Date().toLocaleTimeString();
      const safeText = sanitizePublicText(text);
      monitorLines.push(`[${ts}] [${level}] ${safeText}`);
      monitorLines = monitorLines.slice(-60);
      const logEl = document.getElementById('monitor-log');
      if (logEl) {
        logEl.textContent = monitorLines.join('\n');
        logEl.scrollTop = logEl.scrollHeight;
      }
    }

    async function copyLogToClipboard() {
      const logEl = document.getElementById('monitor-log');
      const text = monitorLines.length ? monitorLines.join('\n') : (logEl ? logEl.textContent : '');
      if (!text || text === 'Log cleared.') {
        return showToast('No log lines to copy');
      }

      try {
        if (navigator.clipboard && window.isSecureContext) {
          await navigator.clipboard.writeText(text);
        } else {
          const ta = document.createElement('textarea');
          ta.value = text;
          ta.setAttribute('readonly', '');
          ta.style.position = 'fixed';
          ta.style.left = '-9999px';
          document.body.appendChild(ta);
          ta.select();
          document.execCommand('copy');
          document.body.removeChild(ta);
        }
        showToast('Log copied to clipboard!');
      } catch (_) {
        showToast('Could not copy log automatically');
      }
    }

    function setBridgeBadge(connected, reasonText) {
      const badge = document.getElementById('bridge-status-badge');
      if (!badge) return;
      if (connected) {
        badge.textContent = `Connected (${sanitizePublicText(API_BASE_URL || 'same-origin')})`;
        badge.className = 'badge badge-ok';
      } else {
        badge.textContent = reasonText ? `Offline: ${sanitizePublicText(reasonText)}` : 'Local Mode (API Unreachable)';
        badge.className = 'badge';
      }
    }

    async function detailedApiRequest(path, options = {}) {
      const fullUrl = apiUrl(path);
      const method = options.method || 'GET';
      const displayUrl = sanitizePublicText(fullUrl);
      try {
        const res = await fetch(fullUrl, options);
        const rawText = await res.text().catch(() => '');
        let parsed = null;
        if (rawText) {
          try {
            parsed = JSON.parse(rawText);
          } catch (_) {
            parsed = null;
          }
        }
        if (!res.ok) {
          const serverErr = sanitizePublicText(parsed?.error || parsed?.message || rawText.slice(0, 220) || 'No response body');
          const detail = `${method} ${displayUrl} -> HTTP ${res.status} ${res.statusText}: ${serverErr}`;
          pushMonitorLine('ERROR', detail);
          return {
            ok: false,
            status: res.status,
            statusText: res.statusText,
            data: parsed || {},
            rawText,
            errorMessage: detail
          };
        }
        return {
          ok: true,
          status: res.status,
          statusText: res.statusText,
          data: parsed || {},
          rawText,
          errorMessage: ''
        };
      } catch (err) {
        const isCrossOrigin = window.location.origin !== 'null' && !fullUrl.startsWith(window.location.origin);
        const hint = isCrossOrigin
          ? 'Possible CORS block, SSL/TLS failure, host container stopped, or wrong port'
          : 'Network error or server unreachable';
        const detail = `${method} ${displayUrl} -> Fetch failed: ${sanitizePublicText(err?.message || String(err))} (${hint}; origin=${window.location.origin})`;
        pushMonitorLine('ERROR', detail);
        return {
          ok: false,
          status: 0,
          statusText: 'NETWORK_ERROR',
          data: {},
          rawText: '',
          errorMessage: detail
        };
      }
    }

    async function sendServerLog(level, eventName, detail) {
      const payload = {
        level,
        event: eventName,
        detail,
        userId: session?.discordId || session?.userId || 'guest',
        handle: session?.handle || 'Guest',
        device: currentDevice,
        url: window.location.href,
        timestamp: new Date().toISOString()
      };

      pushMonitorLine(level, `${eventName}: ${detail}`);
      if (level === 'ERROR') console.error('[RoChess Web]', eventName, sanitizePublicText(detail));
      else console.log('[RoChess Web]', eventName, sanitizePublicText(detail));

      const res = await detailedApiRequest('/api/rochess/log', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        keepalive: true,
        body: JSON.stringify(payload)
      });
      if (res.ok) {
        setBridgeBadge(true);
      } else {
        setBridgeBadge(false, `HTTP ${res.status || 'ERR'}`);
      }
    }

    window.addEventListener('error', (event) => {
      const msg = event?.message || 'Unknown window error';
      const src = event?.filename ? `${event.filename}:${event.lineno}` : 'inline';
      pushMonitorLine('ERROR', `window.onerror: ${msg} (${src})`);
    });

    window.addEventListener('unhandledrejection', (event) => {
      const reason = event?.reason?.message || String(event?.reason || 'Unhandled promise rejection');
      pushMonitorLine('ERROR', `unhandledrejection: ${reason}`);
    });

    function applySiteTheme() {
      document.body.classList.remove('theme-white', 'theme-black-blue');
      if (boardPrefs.siteTheme === 'white') document.body.classList.add('theme-white');
      else if (boardPrefs.siteTheme === 'black-blue') document.body.classList.add('theme-black-blue');
      localStorage.setItem('rochess_board_prefs', JSON.stringify(boardPrefs));
    }

    function setActiveView(viewName, persist = true) {
      const target = document.getElementById(`view-${viewName}`);
      if (!target) return;
      if (persist) {
        localStorage.setItem(ACTIVE_VIEW_STORAGE_KEY, viewName);
      }
      document.querySelectorAll('.nav-btn').forEach(b => b.classList.toggle('active', b.dataset.view === viewName));
      document.querySelectorAll('.view').forEach(v => v.classList.toggle('active', v.id === `view-${viewName}`));
      window.scrollTo({ top: 0, behavior: 'smooth' });
      buildMemberViews();
      renderMemberships();
      updateCheckoutGateUI();
      fetchLiveState();
      pushMonitorLine('INFO', `view_change: ${viewName}`);
    }

    document.querySelectorAll('.nav-btn').forEach(btn => {
      btn.addEventListener('click', () => setActiveView(btn.dataset.view));
    });
    document.querySelectorAll('[data-jump-view]').forEach(el => {
      el.addEventListener('click', () => setActiveView(el.dataset.jumpView));
    });
    document.getElementById('brand-home').addEventListener('click', () => setActiveView('lobby'));

    const joinServerBtn = document.getElementById('join-server-btn');
    if (joinServerBtn) {
      joinServerBtn.addEventListener('click', () => {
        pushMonitorLine('INFO', `join_server_click: ${CLUB_CONFIG.DISCORD_INVITE_URL}`);
      });
    }

    document.getElementById('copy-log-btn').addEventListener('click', copyLogToClipboard);

    document.getElementById('test-server-log-btn').addEventListener('click', () => {
      sendServerLog('INFO', 'manual_test_log', `Testing connection to ${sanitizePublicText(apiUrl('/api/rochess/log'))}`);
      showToast('Sent test log to server bridge');
    });

    document.getElementById('clear-monitor-btn').addEventListener('click', () => {
      monitorLines = [];
      const el = document.getElementById('monitor-log');
      if (el) el.textContent = 'Log cleared.';
    });

    const profileModal = document.getElementById('profile-modal');
    const authModal = document.getElementById('auth-modal');

    function openProfileModal() {
      if (!isSignedIn()) return openAuthModal();
      const flags = getUserRoleFlags();
      const roleLabel = flags.isManagement ? 'Management Team' : (flags.isEntertainment ? 'Entertainment Team' : 'Club Member');
      document.getElementById('profile-modal-body').innerHTML = `
        <div><strong>Discord Username:</strong> ${escapeHtml(session.handle)} <span class="badge badge-ok">Verified</span></div>
        <div class="small" style="margin-top: 4px;"><strong>Platform:</strong> DISCORD · <strong>Role Tier:</strong> ${escapeHtml(roleLabel)}</div>
        <div class="small" style="margin-top: 2px;"><strong>Discord ID:</strong> <code>${escapeHtml(session.discordId || session.userId)}</code></div>
        <div class="small" style="margin-top: 2px;"><strong>Device:</strong> ${escapeHtml(currentDevice.label)} (<code>${escapeHtml(currentDevice.deviceId)}</code>)</div>
        <div class="small" style="margin-top: 2px;"><strong>RoChess ELO:</strong> <strong>${getCurrentUserElo()}</strong></div>
      `;
      profileModal.classList.add('open');
      pushMonitorLine('INFO', `profile_modal_open: ${session.handle}`);
    }

    function closeProfileModal() { profileModal.classList.remove('open'); }

    window.openAuthModal = function() {
      if (isSignedIn()) {
        openProfileModal();
        return;
      }
      closeProfileModal();
      document.getElementById('auth-error-msg').textContent = '';
      if (session) {
        document.getElementById('auth-handle').value = session.handle || '';
        document.getElementById('auth-discord-id').value = session.discordId || '';
      }
      document.getElementById('auth-proof-input').value = '';
      codeSentOnceForCurrentTarget = false;
      activeTargetKey = '';
      document.getElementById('proof-dispatch-status').innerHTML = 'Enter your Discord username and click <strong>Send Code</strong>.';
      updateSendCodeButtonState();
      authModal.classList.add('open');
      pushMonitorLine('INFO', 'auth_modal_open');
    };

    function closeAuthModal() { authModal.classList.remove('open'); }

    document.getElementById('auth-handle').addEventListener('input', updateSendCodeButtonState);
    document.getElementById('auth-discord-id').addEventListener('input', updateSendCodeButtonState);

    document.getElementById('header-auth-btn').addEventListener('click', () => {
      if (isSignedIn()) openProfileModal();
      else openAuthModal();
    });
    document.getElementById('header-profile-btn').addEventListener('click', openProfileModal);
    document.getElementById('close-profile-modal').addEventListener('click', closeProfileModal);
    profileModal.addEventListener('click', (e) => { if (e.target === profileModal) closeProfileModal(); });
    document.getElementById('open-reverify-btn').addEventListener('click', () => {
      closeProfileModal();
      document.getElementById('auth-error-msg').textContent = '';
      document.getElementById('auth-handle').value = session?.handle || '';
      document.getElementById('auth-discord-id').value = session?.discordId || '';
      document.getElementById('auth-proof-input').value = '';
      codeSentOnceForCurrentTarget = false;
      activeTargetKey = '';
      document.getElementById('proof-dispatch-status').innerHTML = 'Enter your Discord username and click <strong>Send Code</strong>.';
      updateSendCodeButtonState();
      authModal.classList.add('open');
    });
    document.getElementById('profile-signout-btn').addEventListener('click', () => {
      closeProfileModal();
      document.getElementById('signout-btn').click();
    });

    document.getElementById('lobby-signin-btn').addEventListener('click', openAuthModal);
    document.getElementById('lobby-card-signin-btn').addEventListener('click', openAuthModal);
    document.getElementById('checkout-signin-btn').addEventListener('click', openAuthModal);
    document.getElementById('close-auth-modal').addEventListener('click', closeAuthModal);
    authModal.addEventListener('click', (e) => { if (e.target === authModal) closeAuthModal(); });

    document.getElementById('send-proof-code-btn').addEventListener('click', async () => {
      const handle = document.getElementById('auth-handle').value.trim();
      const discordId = document.getElementById('auth-discord-id').value.trim();
      const statusEl = document.getElementById('proof-dispatch-status');
      const errEl = document.getElementById('auth-error-msg');
      const sendBtn = document.getElementById('send-proof-code-btn');
      errEl.textContent = '';

      if (!handle) {
        errEl.textContent = 'Enter your Discord username first.';
        return;
      }

      const targetKey = getTargetKey(handle, discordId);
      const info = getTargetResendInfo(targetKey);
      const now = Date.now();

      if (info.lockedUntil && now < info.lockedUntil) {
        errEl.textContent = `Locked from sending more DMs to this user for ${formatRemaining(info.lockedUntil - now)}.`;
        updateSendCodeButtonState();
        return;
      }

      const isResend = info.initialSent;
      if (isResend && info.lastSentAt && (now - info.lastSentAt) < CLUB_CONFIG.RESEND_COOLDOWN_MS) {
        const waitSec = Math.ceil((CLUB_CONFIG.RESEND_COOLDOWN_MS - (now - info.lastSentAt)) / 1000);
        errEl.textContent = `Please wait ${waitSec}s before resending the code.`;
        updateSendCodeButtonState();
        return;
      }

      sendBtn.disabled = true;
      document.getElementById('auth-proof-input').value = '';
      pushMonitorLine('INFO', `send_code_attempt: handle="${handle}" discordId="${discordId || 'none'}" guild=${CLUB_CONFIG.MAIN_GUILD_ID} api=${apiUrl('/api/rochess/auth/challenge')}`);

      const checkRes = await detailedApiRequest('/api/rochess/auth/check-user', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ handle, discordId, guildId: CLUB_CONFIG.MAIN_GUILD_ID })
      });
      if (checkRes.ok && checkRes.data?.inServer === false) {
        alert('This Discord user is not in the RoChess server. Join the server first before requesting a code.');
        errEl.textContent = `check-user reported inServer=false for "${handle}". No DM was sent.`;
        updateSendCodeButtonState();
        return;
      }

      const res = await detailedApiRequest('/api/rochess/auth/challenge', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          provider: 'discord',
          handle,
          discordId,
          guildId: CLUB_CONFIG.MAIN_GUILD_ID,
          dmEmbed: true
        })
      });

      if (!res.ok) {
        codeSentOnceForCurrentTarget = false;
        const data = res.data || {};
        if (data.inServer === false || /not in.*server|member not found|not found in guild/i.test(String(data.error || ''))) {
          alert('This Discord user was not found in the RoChess server. Join the server first!');
        }
        errEl.textContent = res.errorMessage;
        updateSendCodeButtonState();
        return;
      }

      const nextResendCount = isResend ? (info.resendCount || 0) + 1 : 0;
      const shouldLockNow = isResend && nextResendCount >= CLUB_CONFIG.MAX_RESENDS_BEFORE_LOCK;
      const nextInfo = {
        initialSent: true,
        lastSentAt: Date.now(),
        resendCount: nextResendCount,
        lockedUntil: shouldLockNow ? (Date.now() + CLUB_CONFIG.LOCK_DURATION_MS) : 0
      };
      saveTargetResendInfo(targetKey, nextInfo);

      codeSentOnceForCurrentTarget = true;
      activeTargetKey = targetKey;

      if (shouldLockNow) {
        statusEl.innerHTML = `<span style="color: var(--danger);">Code sent (${nextResendCount}/${CLUB_CONFIG.MAX_RESENDS_BEFORE_LOCK} resends). Further DMs to this user are locked for <strong>3 hours</strong>.</span>`;
        alert('You reached 3 resends for this user. Sending more DMs to this user is locked for 3 hours.');
      } else {
        statusEl.innerHTML = `<span style="color: var(--emerald);">6-digit code sent in a Discord DM embed to <strong>${escapeHtml(handle)}</strong>. Resend unlocks in 30s.</span>`;
      }

      playChessSound('notify');
      showToast('Discord DM code sent');
      pushMonitorLine('INFO', `discord_dm_code_sent: ${handle} (resends: ${nextResendCount}/${CLUB_CONFIG.MAX_RESENDS_BEFORE_LOCK})`);
      updateSendCodeButtonState();
    });

    document.getElementById('submit-signin-btn').addEventListener('click', async () => {
      const handle = document.getElementById('auth-handle').value.trim();
      const discordId = document.getElementById('auth-discord-id').value.trim();
      const enteredCode = document.getElementById('auth-proof-input').value.trim();
      const errEl = document.getElementById('auth-error-msg');
      errEl.textContent = '';

      if (!handle) {
        errEl.textContent = 'Enter your Discord username.';
        return;
      }
      if (!codeSentOnceForCurrentTarget || getTargetKey(handle, discordId) !== activeTargetKey) {
        errEl.textContent = 'Click "Send Code" first to receive a Discord DM code.';
        return;
      }
      if (!/^\d{6}$/.test(enteredCode)) {
        errEl.textContent = 'Enter the 6-digit code sent to your Discord DM.';
        return;
      }

      currentDevice = getOrCreateDevice();
      const res = await detailedApiRequest('/api/rochess/auth/verify', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          provider: 'discord',
          handle,
          discordId,
          code: enteredCode,
          device: currentDevice
        })
      });

      if (!res.ok || !res.data?.verified) {
        errEl.textContent = res.errorMessage || res.data?.error || 'Incorrect or expired 6-digit code.';
        return;
      }

      const data = res.data;
      session = {
        provider: 'discord',
        handle: data.session?.handle || handle,
        discordId: data.session?.discordId || discordId,
        userId: data.session?.userId || discordId || `web_${Date.now().toString().slice(-6)}`,
        roles: Array.isArray(data.roles) ? data.roles : (Array.isArray(data.session?.roles) ? data.session.roles : []),
        verified: true,
        verifiedAt: new Date().toISOString()
      };
      codeSentOnceForCurrentTarget = false;
      activeTargetKey = '';
      localStorage.setItem('rochess_web_session', JSON.stringify(session));
      closeAuthModal();
      updateAuthUI();
      renderMemberships();
      updateCheckoutGateUI();
      buildMemberViews();
      await fetchLiveState();
      playChessSound('notify');
      showToast(`Verified & signed in as ${session.handle}`);
      pushMonitorLine('INFO', `discord_signin_verified: ${session.handle}`);
    });

    document.getElementById('signout-btn').addEventListener('click', () => {
      const prevHandle = session?.handle || 'Guest';
      session = null;
      liveState = null;
      codeSentOnceForCurrentTarget = false;
      activeTargetKey = '';
      localStorage.removeItem('rochess_web_session');
      closeAuthModal();
      closeProfileModal();
      setActiveView('lobby');
      updateAuthUI();
      renderMemberships();
      updateCheckoutGateUI();
      showToast('Signed out (Guest Mode)');
      pushMonitorLine('INFO', `signout: ${prevHandle} returned to Guest Mode`);
    });

    function updateAuthUI() {
      const signedIn = isSignedIn();
      document.body.classList.toggle('signed-in', signedIn);

      const dot = document.getElementById('header-dot');
      const chipText = document.getElementById('header-session-text');
      const authBtn = document.getElementById('header-auth-btn');
      const profileBtn = document.getElementById('header-profile-btn');
      const lobbyTitle = document.getElementById('lobby-account-title');
      const lobbyBadge = document.getElementById('lobby-account-badge');
      const lobbyDesc = document.getElementById('lobby-account-desc');
      const lobbyMeta = document.getElementById('lobby-account-meta');
      const lobbyActions = document.getElementById('lobby-account-actions');

      document.getElementById('join-server-btn').href = CLUB_CONFIG.DISCORD_INVITE_URL;
      document.getElementById('lobby-whop-dest').textContent = CLUB_CONFIG.WHOP_DESTINATION_ACCOUNT;
      document.getElementById('lobby-api-url').textContent = sanitizePublicText(API_BASE_URL || 'same-origin');

      document.querySelectorAll('.nav-btn[data-auth-only="true"]').forEach(btn => {
        btn.classList.toggle('locked-tab', !signedIn);
      });

      if (!signedIn) {
        dot.classList.remove('online');
        chipText.textContent = 'Guest Mode';
        authBtn.style.display = '';
        profileBtn.style.display = 'none';
        lobbyTitle.textContent = 'Guest Mode (Unverified)';
        lobbyBadge.textContent = 'Guest';
        lobbyBadge.className = 'badge';
        lobbyDesc.textContent = 'Sign up with your Discord username to check server membership and receive a 6-digit code in Discord DMs.';
        lobbyMeta.innerHTML = '';
        lobbyActions.innerHTML = `<button class="btn btn-primary btn-sm guest-only" id="lobby-card-signin-btn">Sign In with Discord</button>`;
        document.getElementById('lobby-card-signin-btn').addEventListener('click', openAuthModal);
        return;
      }

      const flags = getUserRoleFlags();
      dot.classList.add('online');
      chipText.textContent = `${escapeHtml(session.handle)} · ${flags.isManagement ? 'Management' : (flags.isEntertainment ? 'Entertainment' : 'Verified')}`;
      authBtn.style.display = 'none';
      profileBtn.style.display = '';
      lobbyTitle.textContent = escapeHtml(session.handle);
      lobbyBadge.textContent = flags.isManagement ? 'Management' : (flags.isEntertainment ? 'Entertainment' : 'Verified Discord');
      lobbyBadge.className = 'badge badge-ok';
      lobbyDesc.textContent = `Signed in via Discord as ${escapeHtml(session.handle)} (Guest Mode disabled).`;
      lobbyMeta.innerHTML = `Discord ID: <code>${escapeHtml(session.discordId || session.userId)}</code> · ELO: <strong>${getCurrentUserElo()}</strong>`;
      lobbyActions.innerHTML = `
        <button class="btn btn-secondary btn-sm" id="lobby-profile-btn">View Profile</button>
        <button class="btn btn-ghost btn-sm" id="lobby-signout-btn">Sign Out</button>
      `;
      document.getElementById('lobby-profile-btn').addEventListener('click', openProfileModal);
      document.getElementById('lobby-signout-btn').addEventListener('click', () => document.getElementById('signout-btn').click());
    }

    function updateCheckoutGateUI() {
      const badge = document.getElementById('checkout-auth-badge');
      const banner = document.getElementById('checkout-lock-banner');
      const checkoutBtn = document.getElementById('checkout-btn');
      if (!badge || !banner || !checkoutBtn) return;

      const sub = getSubStatusFromDb();

      if (!isSignedIn()) {
        badge.textContent = 'Discord Sign-In Required';
        badge.className = 'badge';
        banner.style.display = '';
        checkoutBtn.disabled = true;
        checkoutBtn.textContent = 'Sign In First to Submit to Whop';
      } else if (sub.hasActiveSub) {
        badge.textContent = 'Active Subscription';
        badge.className = 'badge badge-ok';
        banner.style.display = 'none';
        checkoutBtn.disabled = true;
        checkoutBtn.textContent = 'Active Subscription — Cannot Buy Another Yet';
      } else {
        badge.textContent = `Member: ${escapeHtml(session.handle)}`;
        badge.className = 'badge badge-ok';
        banner.style.display = 'none';
        checkoutBtn.disabled = false;
        checkoutBtn.textContent = 'Submit Payment & Send to Whop';
      }
    }

    function updatePaymentMethodPanels() {
      const method = document.getElementById('pay-method').value;
      document.getElementById('pay-fields-debit').style.display = method === 'Debit' ? 'block' : 'none';
      document.getElementById('pay-fields-apple').style.display = method === 'Apple' ? 'block' : 'none';
      document.getElementById('pay-fields-play').style.display = method === 'Play Store' ? 'block' : 'none';
      document.getElementById('checkout-error').textContent = '';
    }
    document.getElementById('pay-method').addEventListener('change', updatePaymentMethodPanels);

    function luhnCheck(numStr) {
      const digits = numStr.replace(/\D/g, '');
      if (digits.length < 13 || digits.length > 19) return false;
      let sum = 0;
      let alt = false;
      for (let i = digits.length - 1; i >= 0; i--) {
        let n = Number(digits[i]);
        if (alt) {
          n *= 2;
          if (n > 9) n -= 9;
        }
        sum += n;
        alt = !alt;
      }
      return sum % 10 === 0;
    }

    function validatePaymentMethodFields() {
      const method = document.getElementById('pay-method').value;
      const errEl = document.getElementById('checkout-error');
      errEl.textContent = '';

      if (method === 'Debit') {
        const cardName = document.getElementById('debit-name').value.trim();
        const cardNum = document.getElementById('debit-number').value.replace(/\s+/g, '');
        const exp = document.getElementById('debit-exp').value.trim();
        const cvc = document.getElementById('debit-cvc').value.trim();

        if (!cardName) { errEl.textContent = 'Enter the cardholder name for the debit card.'; return null; }
        if (!/^\d{13,19}$/.test(cardNum) || !luhnCheck(cardNum)) { errEl.textContent = 'Enter a valid debit card number.'; return null; }
        if (!/^(0[1-9]|1[0-2])\/\d{2}$/.test(exp)) { errEl.textContent = 'Enter card expiry in MM/YY format.'; return null; }
        if (!/^\d{3,4}$/.test(cvc)) { errEl.textContent = 'Enter a valid 3- or 4-digit CVC.'; return null; }
        return { method: 'Debit', whopRoute: 'whop_debit_card', cardholderName: cardName, cardLast4: cardNum.slice(-4), expiry: exp };
      }

      if (method === 'Apple') {
        const appleEmail = document.getElementById('apple-email').value.trim();
        const appleTag = document.getElementById('apple-device-tag').value.trim();
        if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(appleEmail)) { errEl.textContent = 'Enter a valid Apple Pay / Apple ID email.'; return null; }
        if (!appleTag) { errEl.textContent = 'Enter your Apple Pay wallet / device label.'; return null; }
        return { method: 'Apple', whopRoute: 'whop_apple_pay', appleEmail, appleDeviceTag: appleTag };
      }

      const playEmail = document.getElementById('play-email').value.trim();
      const playToken = document.getElementById('play-token').value.trim();
      if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(playEmail)) { errEl.textContent = 'Enter a valid Google Play Store email.'; return null; }
      if (!playToken) { errEl.textContent = 'Enter your Play Store account tag or billing reference.'; return null; }
      return { method: 'Play Store', whopRoute: 'whop_play_store', playEmail, playToken };
    }

    function renderPublicSchedule() {
      const all = getMergedTournaments();
      document.getElementById('public-schedule-list').innerHTML = all.slice(0, 4).map(t => `
        <div class="box-item">
          <div class="row-between">
            <strong>${escapeHtml(t.title)}</strong>
            <span class="badge">${escapeHtml(t.format || 'Event')}</span>
          </div>
          <p class="small" style="margin-top: 2px;">${escapeHtml(t.description || 'Club schedule event')}</p>
        </div>
      `).join('');
    }

    function renderMemberships() {
      const sub = getSubStatusFromDb();
      const plans = getActivePlansForUser();
      const modeBadge = document.getElementById('membership-mode-badge');
      const subtitleEl = document.getElementById('membership-subtitle');
      const bannerEl = document.getElementById('membership-status-banner');

      if (modeBadge) {
        if (sub.hasActiveSub) {
          modeBadge.textContent = 'Active Subscription';
          modeBadge.className = 'badge badge-ok';
        } else if (sub.trialEnded) {
          modeBadge.textContent = 'Renewal Plans ($2.49 / $6.49)';
          modeBadge.className = 'badge badge-warn';
        } else {
          modeBadge.textContent = 'Standard Plans';
          modeBadge.className = 'badge';
        }
      }

      if (subtitleEl) {
        subtitleEl.textContent = sub.trialEnded
          ? 'Your free trial has ended — Renewal Plans are now shown in place of standard new-member plans.'
          : 'Browse tiers anytime. Sign in with Discord first before submitting payment details to Whop.';
      }

      if (bannerEl) {
        if (sub.hasActiveSub) {
          bannerEl.style.display = 'block';
          const expText = sub.expiresAt ? ` until <strong>${escapeHtml(new Date(sub.expiresAt).toLocaleString())}</strong>` : '';
          bannerEl.innerHTML = `<strong style="color: var(--emerald);">Active Subscription (${escapeHtml(sub.planLabel)}):</strong> You already have an active subscription${expText}. You cannot purchase another membership until it ends.`;
        } else if (sub.trialEnded) {
          bannerEl.style.display = 'block';
          bannerEl.innerHTML = `<strong style="color: var(--gold);">Free Trial Ended:</strong> Normal plans have been replaced with <strong>Renewal Plans</strong> ($2.49 Monthly / $6.49 Yearly).`;
        } else {
          bannerEl.style.display = 'none';
        }
      }

      document.getElementById('membership-list').innerHTML = plans.map(p => `
        <div class="plan-card">
          <h3>${escapeHtml(p.name)}</h3>
          <div class="price">$${p.price.toFixed(2)}</div>
          <p class="small" style="margin-bottom: 7px;">${escapeHtml(p.note)}</p>
          <button class="btn btn-primary btn-sm" style="width: 100%;" ${sub.hasActiveSub ? 'disabled' : ''} onclick="addMembership('${p.id}')">
            ${sub.hasActiveSub ? 'Subscription Active' : 'Add to Cart'}
          </button>
        </div>
      `).join('');
    }

    window.addMembership = function(id) {
      const sub = getSubStatusFromDb();
      if (sub.hasActiveSub) {
        return showToast('You already have an active subscription until it ends.');
      }
      const pool = getActivePlansForUser();
      const plan = pool.find(p => p.id === id);
      if (!plan) return;
      const existing = cart.find(c => c.id === id);
      if (existing) existing.qty += 1;
      else cart.push({ ...plan, qty: 1 });
      localStorage.setItem('rochess_web_cart', JSON.stringify(cart));
      renderCart();
      showToast(`Added ${plan.name}`);
      pushMonitorLine('INFO', `cart_add: ${plan.name} ($${plan.price.toFixed(2)})`);
    };

    window.removeMembership = function(id) {
      cart = cart.filter(c => c.id !== id);
      localStorage.setItem('rochess_web_cart', JSON.stringify(cart));
      renderCart();
      showToast('Removed from cart');
      pushMonitorLine('INFO', `cart_remove: ${id}`);
    };

    function renderCart() {
      const box = document.getElementById('cart-items');
      if (!cart.length) {
        box.innerHTML = `<p class="small">Your cart is empty.</p>`;
        document.getElementById('cart-total').textContent = '$0.00';
        return;
      }
      let total = 0;
      box.innerHTML = cart.map(c => {
        const lineTotal = c.price * c.qty;
        total += lineTotal;
        return `
          <div class="box-item row-between">
            <div>
              <strong>${escapeHtml(c.name)}</strong> ×${c.qty}
              <div class="small">$${lineTotal.toFixed(2)}</div>
            </div>
            <button class="btn btn-ghost btn-sm" onclick="removeMembership('${c.id}')">Remove</button>
          </div>
        `;
      }).join('');
      document.getElementById('cart-total').textContent = `$${total.toFixed(2)}`;
    }

    function renderOrdersLog() {
      const el = document.getElementById('orders-log');
      if (!localOrders.length) {
        el.innerHTML = 'No Whop orders submitted yet.';
        return;
      }
      el.innerHTML = localOrders.slice(0, 5).map(o => `
        <div class="box-item">
          <div class="row-between">
            <strong>${escapeHtml(o.planName)}</strong>
            <span class="badge ${o.serverConfirmed ? 'badge-ok' : 'badge-info'}">${escapeHtml(o.whopStatus || 'Queued (Needs Backend Whop API)')}</span>
          </div>
          <div style="margin-top: 2px;">
            <span style="color: var(--gold); font-weight: 700;">$${Number(o.price).toFixed(2)}</span> · ${escapeHtml(o.paymentMethod)} · Whop: <code>${escapeHtml(o.whopDestinationAccount || CLUB_CONFIG.WHOP_DESTINATION_ACCOUNT)}</code>
          </div>
          <div class="small" style="margin-top: 2px;">Ref: <code>${escapeHtml(o.whopRef)}</code> · Member: ${escapeHtml(o.handle)}</div>
        </div>
      `).join('');
    }

    document.getElementById('checkout-btn').addEventListener('click', async () => {
      const errEl = document.getElementById('checkout-error');
      errEl.textContent = '';

      if (!isSignedIn()) {
        errEl.textContent = 'Sign in with Discord before submitting payment.';
        openAuthModal();
        return;
      }
      const sub = getSubStatusFromDb();
      if (sub.hasActiveSub) {
        errEl.textContent = 'You already have an active subscription. You cannot buy another membership until it ends.';
        return;
      }
      if (!cart.length) {
        errEl.textContent = 'Add at least one membership plan to your cart.';
        return;
      }

      const paymentDetails = validatePaymentMethodFields();
      if (!paymentDetails) return;

      const proofNote = document.getElementById('pay-proof').value.trim();

      for (const item of cart) {
        const whopRef = `WHOP-${Date.now().toString().slice(-6)}-${Math.floor(100 + Math.random() * 900)}`;
        const payload = {
          userId: session.discordId || session.userId,
          handle: session.handle,
          provider: 'discord',
          planId: item.id,
          planName: `${item.name} (×${item.qty})`,
          price: Number((item.price * item.qty).toFixed(2)),
          paymentMethod: paymentDetails.method,
          paymentDetails,
          whopTarget: 'whop',
          whopDestinationAccount: CLUB_CONFIG.WHOP_DESTINATION_ACCOUNT,
          whopRef,
          proofNote,
          createdAt: new Date().toISOString()
        };

        let whopStatus = 'Queued (Needs Backend Whop API)';
        let serverConfirmed = false;

        const res = await detailedApiRequest('/api/rochess/whop/checkout', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(payload)
        });

        if (res.ok) {
          whopStatus = res.data?.whopStatus || 'Forwarded to Whop';
          serverConfirmed = true;
        } else if (backendReachable && res.status >= 400) {
          errEl.textContent = res.errorMessage;
          return;
        }

        localOrders.unshift({ ...payload, whopStatus, serverConfirmed });
        pushMonitorLine('INFO', `whop_checkout: ${payload.planName} ($${payload.price}) via ${paymentDetails.method} [${whopRef}] status=${whopStatus}`);
      }

      localOrders = localOrders.slice(0, 25);
      localStorage.setItem('rochess_web_orders', JSON.stringify(localOrders));
      cart = [];
      localStorage.setItem('rochess_web_cart', '[]');
      document.getElementById('debit-number').value = '';
      document.getElementById('debit-cvc').value = '';
      document.getElementById('pay-proof').value = '';
      renderCart();
      renderOrdersLog();
      await fetchLiveState();
      showToast('Whop checkout payload recorded');
    });

    async function fetchLiveState() {
      const uid = session?.discordId || session?.userId || '';
      currentDevice = getOrCreateDevice();
      const params = new URLSearchParams();
      if (uid) params.set('discordId', uid);
      if (currentDevice?.deviceId) params.set('deviceId', currentDevice.deviceId);
      const q = params.toString() ? `?${params.toString()}` : '';
      const res = await detailedApiRequest('/api/rochess/state' + q);
      if (res.ok) {
        liveState = res.data;
        backendReachable = true;
        if (session && Array.isArray(res.data?.roleInfo?.roles)) {
          session.roles = res.data.roleInfo.roles;
          localStorage.setItem('rochess_web_session', JSON.stringify(session));
        }
        setBridgeBadge(true);
      } else {
        backendReachable = false;
        setBridgeBadge(false, res.status ? `HTTP ${res.status}` : 'Fetch Failed');
      }
      updateAuthUI();
      renderPublicSchedule();
      renderMemberships();
      updateCheckoutGateUI();
      if (isSignedIn()) renderConnectedViews();
    }

    function renderConnectedViews() {
      if (!isSignedIn()) return;
      renderOpponentAndEloBar();
      render1v1Board();
      updateClockDisplay();
      renderPuzzleBoard();
      renderAnnouncementsFeed();

      const flags = getUserRoleFlags();
      const guildId = (liveState && liveState.guildId) || CLUB_CONFIG.MAIN_GUILD_ID;
      const hostRoleId = (liveState && liveState.hostEventRoleId) || CLUB_CONFIG.HOST_EVENT_ROLE_ID;

      const canHost = flags.canHostEvent;
      const badge = document.getElementById('host-status-badge');
      const gateMsg = document.getElementById('host-gate-msg');
      const submitBtn = document.getElementById('host-submit-btn');

      if (badge && gateMsg && submitBtn) {
        if (canHost) {
          badge.textContent = flags.isManagement ? 'Management Host' : 'Entertainment Host';
          badge.className = 'badge badge-ok';
          gateMsg.innerHTML = `Unlocked for <strong>${escapeHtml(session.handle)}</strong> (Management or Entertainment Team).`;
          submitBtn.disabled = false;
        } else if (!backendReachable) {
          badge.textContent = 'Role Restricted';
          badge.className = 'badge';
          gateMsg.innerHTML = `Requires Management or Entertainment Team role on Discord ID.`;
          submitBtn.disabled = true;
        } else {
          badge.textContent = 'Role Required';
          badge.className = 'badge';
          gateMsg.innerHTML = `Requires Management or Entertainment Team role (<code>${escapeHtml(hostRoleId)}</code>).`;
          submitBtn.disabled = true;
        }
      }

      const tournListEl = document.getElementById('tournaments-list');
      if (tournListEl) {
        const filterVal = document.getElementById('tourn-filter')?.value || 'ALL';
        const combined = getMergedTournaments();
        const filtered = filterVal === 'ALL' ? combined : combined.filter(t => t.format === filterVal);

        tournListEl.innerHTML = filtered.length ? filtered.map(t => {
          const joined = joinedTournamentIds.includes(t.id);
          return `
            <div class="box-item">
              <div class="row-between">
                <strong>${escapeHtml(t.title)}</strong>
                <span class="badge">${escapeHtml(t.format || 'Tournament')}</span>
              </div>
              <div class="small" style="margin: 2px 0;">Host: ${escapeHtml(t.hostName || 'RoChess Management')}</div>
              ${t.description ? `<p class="small" style="margin-bottom: 5px;">${escapeHtml(t.description)}</p>` : ''}
              <div class="row-between">
                <button class="btn ${joined ? 'btn-secondary' : 'btn-primary'} btn-sm" onclick="toggleJoinTournament('${escapeHtml(t.id)}')">
                  ${joined ? 'Registered ✓' : 'Join Tournament'}
                </button>
                ${t.link ? `<a href="${escapeHtml(t.link)}" target="_blank" rel="noopener noreferrer">Bracket Link →</a>` : '<span class="small">Club match</span>'}
              </div>
            </div>
          `;
        }).join('') : `<p class="small">No tournaments match that format.</p>`;
      }

      const dmFeedEl = document.getElementById('dm-feed');
      if (dmFeedEl) {
        const threads = (backendReachable && Array.isArray(liveState?.dmThreads) && liveState.dmThreads.length)
          ? liveState.dmThreads
          : localDmThreads;
        dmFeedEl.innerHTML = threads.length ? threads.map(m => `
          <div class="dm-msg">
            <div class="row-between">
              <strong>${escapeHtml(m.senderHandle || 'Member')}</strong>
              <span class="badge">${escapeHtml(m.requestType || 'Message')}</span>
            </div>
            ${m.requestedValue ? `<div class="small" style="margin-top: 2px;">Target: ${escapeHtml(m.requestedValue)}</div>` : ''}
            <div style="margin-top: 3px;">${escapeHtml(m.text || m.messageText || '')}</div>
          </div>
        `).join('') : `<p class="small">No management messages yet.</p>`;
      }

      const reqLogEl = document.getElementById('requests-log');
      if (reqLogEl) {
        const reqs = (backendReachable && Array.isArray(liveState?.roleRequests) && liveState.roleRequests.length)
          ? liveState.roleRequests
          : localRequests;
        reqLogEl.innerHTML = reqs.length ? reqs.map(r => `
          <div class="box-item">
            <div class="row-between">
              <strong>${escapeHtml(r.id || 'REQ')} · ${escapeHtml(r.type || 'Request')}</strong>
              <span class="badge">${escapeHtml(r.status || 'Open')}</span>
            </div>
            <div class="small" style="margin-top: 2px;">${escapeHtml(r.requestedValue || '')} · ${escapeHtml(r.handle || 'Member')}</div>
          </div>
        `).join('') : `<p class="small">No requests logged yet.</p>`;
      }

      const dbEl = document.getElementById('live-db-summary');
      if (dbEl) {
        if (!backendReachable || !liveState) {
          dbEl.innerHTML = `
            <div class="box-item">
              <div class="row-between">
                <strong>Backend Bridge:</strong>
                <span class="badge">Offline / Check Logs Below</span>
              </div>
              <p class="small" style="margin-top: 3px;">
                <code>${escapeHtml(sanitizePublicText(apiUrl('/api/rochess/state')))}</code> did not return a 200 response. Check the <strong>Server &amp; Error Bridge</strong> log box below for the exact HTTP status or network/CORS error.
              </p>
            </div>
          `;
        } else {
          const s = liveState.dbStats || {};
          const up = liveState.userProfile;
          const sub = getSubStatusFromDb();
          dbEl.innerHTML = `
            <div class="box-item">
              <strong>Bot Status:</strong> ${liveState.botOnline ? 'Online' : 'Offline'} (${escapeHtml(liveState.botTag || 'RoChess Bot')})<br/>
              <strong>Guild ID:</strong> <code>${escapeHtml(guildId)}</code> · <strong>Host Role:</strong> <code>${escapeHtml(hostRoleId)}</code>
            </div>
            <div class="box-item">
              <strong>Database:</strong> ${s.usersCount || 0} economy users · ${s.membersCount || 0} members · ${s.activeTicketsCount || 0} active tickets · ${s.casesCount || 0} cases · ${s.eventLogCount || 0} events
            </div>
            ${up ? `
              <div class="box-item">
                <strong>Player Profile:</strong> ${Number(up.chess_coins || 0).toLocaleString()} Çess · ${Number(up.bank_coins || 0).toLocaleString()} Bank · ${Number(up.tokens || 0)} Tokens · Plan: <strong>${escapeHtml(sub.planLabel)}</strong>
              </div>
            ` : ''}
          `;
        }
      }
    }

    function restoreInitialView() {
      const savedView = localStorage.getItem(ACTIVE_VIEW_STORAGE_KEY) || 'lobby';
      const target = document.getElementById(`view-${savedView}`) ? savedView : 'lobby';
      document.querySelectorAll('.nav-btn').forEach(b => b.classList.toggle('active', b.dataset.view === target));
      document.querySelectorAll('.view').forEach(v => v.classList.toggle('active', v.id === `view-${target}`));
    }

    checkUrlMatchInvite();
    pushMonitorLine('INFO', `portal_boot: endpoint="${sanitizePublicText(API_BASE_URL)}" origin="${window.location.origin}"`);
    updateSoundButtonUI();
    startResendTicker();
    startClockLoop();
    applySiteTheme();
    updateAuthUI();
    restoreInitialView();
    renderMemberships();
    updateCheckoutGateUI();
    updatePaymentMethodPanels();
    renderCart();
    renderOrdersLog();
    renderPublicSchedule();
    buildMemberViews();
    fetchLiveState();
  </script>
</body>
</html>
