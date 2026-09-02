<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Protótipo · acompanhamento nutricional</title>
<style>
  :root{
    --cream:#FBF6EE; --cream-deep:#F3ECDD; --card:#FFFFFF; --line:#E6DFCD;
    --ink:#3D3A2E; --ink-soft:#8A8370;
    --sage:#5B7A52; --sage-bg:#EAF3E3; --sage-line:#CFE3C2; --pastel:#DCEAD2;
    --terracota:#9C5A3C; --terracota-line:#D8AE96; --terracota-bg:#FBEFE7;
    --orange:#D98A3D; --orange-bg:#FBEBD8; --orange-line:#F0CB9C;
    --blue-bg:#E7F0F6; --blue:#5B84A0; --blue-line:#C8DAE5;
  }
  *{box-sizing:border-box;}
  body{margin:0; font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,sans-serif; background:var(--cream-deep); color:var(--ink); -webkit-font-smoothing:antialiased;}
  #app{max-width:420px; margin:0 auto; min-height:100vh; background:var(--cream); padding-bottom:96px; position:relative;}
  header{padding:20px 20px 8px; display:flex; align-items:center; justify-content:space-between;}
  header .eyebrow{font-size:13px; color:var(--ink-soft); margin:0 0 2px;}
  header h1{font-size:19px; font-weight:600; margin:0;}
  .header-icon{width:38px; height:38px; border-radius:50%; background:var(--pastel); display:flex; align-items:center; justify-content:center; flex-shrink:0;}
  .day-strip{display:flex; gap:6px; padding:10px 20px 14px;}
  .day-pill{flex:1; text-align:center; padding:8px 2px; border-radius:12px; background:var(--card); border:0.5px solid var(--line);}
  .day-pill .dl{font-size:10px; color:var(--ink-soft); display:block;}
  .day-pill .dn{font-size:13px; font-weight:600; color:var(--ink); display:block; margin-top:2px;}
  .day-pill.today{background:var(--sage); border-color:var(--sage);}
  .day-pill.today .dl, .day-pill.today .dn{color:#fff;}
  .screen{padding:0 20px 20px;}
  .card{background:var(--card); border:0.5px solid var(--line); border-radius:16px; padding:16px; margin-bottom:14px;}
  .card h3{margin:0 0 10px; font-size:14px; color:var(--ink-soft); font-weight:600; display:flex; align-items:center; gap:6px;}
  .banner{background:var(--blue-bg); border:0.5px solid var(--blue-line); border-radius:16px; padding:14px 16px; margin-bottom:14px; display:flex; align-items:center; gap:10px; font-size:13px; color:var(--blue); font-weight:500; position:relative;}
  .banner-x{position:absolute; top:8px; right:8px; background:none; border:none; color:inherit; opacity:0.6; padding:4px;}
  .support-btn{width:100%; background:var(--terracota-bg); border:0.5px solid var(--terracota-line); border-radius:999px; padding:13px 16px; font-size:14px; color:var(--terracota); font-weight:600; display:flex; align-items:center; justify-content:center; gap:8px;}
  .registrar-btn{width:100%; background:var(--sage); color:#fff; border:none; border-radius:18px; padding:16px; font-size:15px; font-weight:700; margin-bottom:14px; display:flex; align-items:center; justify-content:center; gap:10px; box-shadow:0 4px 14px rgba(91,122,82,0.3);}
  nav{position:fixed; bottom:16px; left:16px; right:16px; max-width:388px; margin:0 auto; background:var(--card); border-radius:28px; display:flex; box-shadow:0 6px 20px rgba(61,58,46,0.18); padding:6px;}
  nav button{flex:1; background:none; border:none; padding:9px 2px; color:var(--ink-soft); display:flex; align-items:center; justify-content:center; border-radius:20px;}
  nav button.active{color:#fff; background:var(--sage);}
  .opt-btn{display:flex; align-items:center; gap:10px; width:100%; text-align:left; background:var(--cream-deep); border:0.5px solid var(--line); border-radius:12px; padding:12px 14px; margin-bottom:8px; font-size:14px; color:var(--ink);}
  .opt-btn:active{background:var(--sage-bg); border-color:var(--sage-line);}
  textarea, input[type=text], input[type=date], input[type=time], input[type=number], input[type=file]{width:100%; border:0.5px solid var(--line); border-radius:12px; padding:10px 12px; font-size:14px; font-family:inherit; background:var(--card); color:var(--ink); resize:none;}
  select{border:0.5px solid var(--line); border-radius:10px; padding:9px 8px; font-size:13px; font-family:inherit; background:var(--card); color:var(--ink);}
  .primary-btn{width:100%; background:var(--sage); color:#fff; border:none; border-radius:999px; padding:13px; font-size:14px; font-weight:600; margin-top:12px; display:flex; align-items:center; justify-content:center; gap:8px;}
  .ghost-btn{width:100%; background:none; border:0.5px solid var(--line); border-radius:999px; padding:12px; font-size:13px; color:var(--ink-soft); margin-top:8px;}
  .msg{font-size:14px; line-height:1.7; background:var(--sage-bg); border:0.5px solid var(--sage-line); border-radius:16px; padding:16px; display:flex; gap:10px;}
  .small{font-size:12px; color:var(--ink-soft);}
  .hidden{display:none;}
  .avoid-tag{display:inline-block; font-size:12px; background:var(--cream-deep); border:0.5px solid var(--line); border-radius:999px; padding:5px 10px; margin:0 6px 6px 0; color:var(--ink-soft);}
  .seg{display:flex; background:var(--cream-deep); border-radius:12px; padding:3px; margin-bottom:14px;}
  .seg button{flex:1; border:none; background:none; padding:9px 4px; font-size:12px; font-weight:600; color:var(--ink-soft); border-radius:9px;}
  .seg button.active{background:var(--card); color:var(--sage); box-shadow:0 1px 2px rgba(0,0,0,0.06);}
  .estimate-note{font-size:11px; color:var(--orange); background:var(--orange-bg); border-radius:10px; padding:8px 10px; margin-bottom:12px; display:flex; gap:6px;}
  .kcal-row{display:flex; gap:8px; margin-bottom:8px;}
  .kcal-box{flex:1; background:var(--card); border:0.5px solid var(--line); border-radius:14px; padding:12px 8px; text-align:center;}
  .kcal-box.plano{background:var(--sage-bg); border-color:var(--sage-line);}
  .kcal-box .kv{font-size:17px; font-weight:700; color:var(--ink);}
  .kcal-box.plano .kv{color:var(--sage);}
  .kcal-box .kl{font-size:10px; color:var(--ink-soft); margin-top:2px;}
  .macro-summary{display:flex; justify-content:space-around; background:var(--card); border:0.5px solid var(--line); border-radius:14px; padding:10px; margin-bottom:14px;}
  .macro-summary div{text-align:center;}
  .macro-summary .mv{font-size:14px; font-weight:700;}
  .macro-summary .ml{font-size:9px; color:var(--ink-soft); text-transform:uppercase;}
  .macro-bar{display:flex; height:5px; border-radius:99px; overflow:hidden; background:var(--cream-deep); margin-top:8px;}
  .macro-bar span{height:100%;}
  .macro-legend{font-size:10px; color:var(--ink-soft); margin-top:4px; display:flex; gap:8px;}
  .meal-card{background:var(--card); border:0.5px solid var(--line); border-radius:16px; padding:16px; margin-bottom:10px;}
  .meal-card.done{padding:10px 16px;}
  .meal-head{display:flex; align-items:center; gap:10px;}
  .meal-icon{width:36px; height:36px; border-radius:50%; display:flex; align-items:center; justify-content:center; flex-shrink:0;}
  .meal-icon.sm{width:28px; height:28px;}
  .meal-titles{flex:1;}
  .meal-card .mtitle{font-size:15px; font-weight:600; margin:0;}
  .meal-card .mtime{font-size:12px; color:var(--ink-soft); font-weight:400;}
  .kcal-badge{font-size:11px; color:var(--orange); background:var(--orange-bg); border-radius:999px; padding:3px 8px; white-space:nowrap;}
  .supp-tag{font-size:11px; color:var(--terracota); background:var(--terracota-bg); border-radius:10px; padding:6px 10px; margin-top:10px; display:flex; align-items:center; justify-content:space-between; gap:6px;}
  .supp-toggle{background:#fff; border:0.5px solid var(--terracota-line); border-radius:999px; padding:4px 9px; font-size:10px; color:var(--terracota); display:flex; align-items:center; gap:4px;}
  .supp-toggle.done{background:var(--terracota); color:#fff;}
  .desc-toggle{background:none; border:none; padding:4px; color:var(--ink-soft); flex-shrink:0;}
  .mdesc{font-size:13px; color:var(--ink-soft); margin:8px 0 0; line-height:1.5; display:none;}
  .mdesc.open{display:block;}
  .status-row{display:flex; gap:8px; margin-top:12px;}
  .status-btn{flex:1; font-size:12px; padding:9px 4px; border-radius:10px; border:0.5px solid var(--line); background:var(--cream-deep); color:var(--ink); display:flex; flex-direction:column; align-items:center; gap:4px;}
  .done-row{display:flex; align-items:center; gap:10px;}
  .done-check{width:22px; height:22px; border-radius:50%; background:var(--sage-bg); color:var(--sage); display:flex; align-items:center; justify-content:center; flex-shrink:0;}
  .done-check.nao{background:var(--cream-deep); color:var(--ink-soft);}
  .done-check.parcial{background:var(--orange-bg); color:var(--orange);}
  .edit-link{font-size:11px; color:var(--ink-soft); cursor:pointer; flex-shrink:0;}
  .food-row{border-top:0.5px solid #EFE9DA; padding:12px 0;}
  .food-row .fname{font-size:13px; color:var(--sage); font-weight:600; margin-bottom:4px; display:flex; align-items:center; gap:6px;}
  .food-macro{font-size:11px; color:var(--ink-soft); margin-bottom:8px;}
  .food-inline{display:flex; gap:6px; align-items:center;}
  .food-inline input{flex:1; max-width:80px;}
  .mini-btn{font-size:12px; padding:9px 10px; border-radius:10px; border:0.5px solid var(--line); background:var(--cream-deep); color:var(--ink); white-space:nowrap; display:flex; align-items:center; gap:5px;}
  .mini-btn.ok{background:var(--sage-bg); border-color:var(--sage-line); color:var(--sage);}
  .swap-list{margin-top:8px; padding:8px; background:var(--cream-deep); border-radius:10px;}
  .swap-list button{display:flex; align-items:center; justify-content:space-between; gap:8px; width:100%; text-align:left; background:none; border:none; padding:8px 4px; font-size:12px; color:var(--ink); border-bottom:0.5px solid var(--line);}
  .swap-list button:last-child{border-bottom:none;}
  .carry-note{font-size:12px; color:var(--orange); background:var(--orange-bg); border-radius:10px; padding:8px 10px; margin-top:10px; display:flex; gap:8px;}
  .warn-banner{background:var(--orange-bg); border:0.5px solid var(--orange-line); border-radius:16px; padding:14px 16px; margin-bottom:14px; font-size:13px; color:var(--orange); line-height:1.5; display:flex; gap:10px; position:relative;}
  .insight-card{background:linear-gradient(135deg, var(--sage-bg), var(--pastel)); border:0.5px solid var(--sage-line); border-radius:16px; padding:18px; margin-bottom:14px;}
  .insight-card h3{color:var(--sage); margin-bottom:8px;}
  .insight-card p{font-size:13px; line-height:1.6; margin:6px 0; color:var(--ink);}
  .table-wrap{border:0.5px solid var(--line); border-radius:14px; overflow:hidden; margin-bottom:10px;}
  .table-head{background:var(--sage-bg); padding:10px 12px; display:flex; justify-content:space-between; align-items:center;}
  .table-head .tt{font-size:14px; font-weight:600; color:var(--sage);}
  .table-head .tk{font-size:11px; color:var(--sage);}
  .trow{display:flex; align-items:center; padding:10px 12px; border-top:0.5px solid #EFE9DA; font-size:12px; background:var(--card);}
  .trow .tcol-grp{flex:0 0 78px; color:var(--sage); font-size:10.5px; font-weight:600; text-transform:uppercase;}
  .trow .tcol-food{flex:1; font-weight:600; color:var(--ink);}
  .trow .tcol-qtd{flex:0 0 70px; text-align:right; color:var(--ink-soft); font-size:11px;}
  .trow .tcol-btn{flex:0 0 28px; text-align:right;}
  .sub-toggle{background:none; border:none; color:var(--sage); cursor:pointer; padding:2px;}
  .sub-panel{background:var(--cream-deep); padding:8px 12px 8px 90px;}
  .sub-item{font-size:11px; color:var(--ink-soft); padding:4px 0;}
  .supp-row{display:flex; align-items:center; gap:10px; padding:10px 0; border-top:0.5px solid #EFE9DA;}
  .supp-row:first-child{border-top:none;}
  .supp-icon{width:30px; height:30px; border-radius:50%; background:var(--terracota-bg); color:var(--terracota); display:flex; align-items:center; justify-content:center; flex-shrink:0;}
  .grp{margin-bottom:10px;}
  .grp b{font-size:12px; color:var(--sage); display:block; margin-bottom:4px;}
  .opt-line{font-size:13px; color:var(--ink); padding:3px 0;}
  .opt-line .m{font-size:11px; color:var(--ink-soft);}
  .event-item{display:flex; align-items:center; gap:10px; padding:10px 0; border-top:0.5px solid #EFE9DA;}
  .event-item:first-child{border-top:none;}
  .event-date{width:42px; text-align:center; background:var(--orange-bg); border-radius:10px; padding:6px 0; flex-shrink:0;}
  .event-date .dd{font-size:15px; font-weight:700; color:var(--orange); display:block;}
  .event-date .mm{font-size:9px; color:var(--orange); text-transform:uppercase;}
  .event-info{flex:1;}
  .event-info .et{font-size:13px; font-weight:600;}
  .event-info .em{font-size:11px; color:var(--ink-soft);}
  .event-del{background:none; border:none; color:var(--ink-soft); padding:4px;}
  .month-label{font-size:12px; color:var(--ink-soft); font-weight:600; margin:14px 0 4px; text-transform:uppercase;}
  .chip-row{display:flex; flex-wrap:wrap; gap:6px; margin-top:8px;}
  .chip{font-size:11px; padding:6px 10px; border-radius:999px; border:0.5px solid var(--line); background:var(--cream-deep); color:var(--ink); cursor:pointer;}
  .chip.sel{background:var(--sage-bg); border-color:var(--sage-line); color:var(--sage);}
  .week-row{display:flex; gap:6px; margin-bottom:12px;}
  .week-day{flex:1; background:var(--card); border:0.5px solid var(--line); border-radius:12px; padding:8px 4px; text-align:center;}
  .week-day.today{background:var(--sage); border-color:var(--sage);}
  .week-day.today .wl,.week-day.today .wn{color:#fff;}
  .week-day .wl{font-size:9px; color:var(--ink-soft); display:block;}
  .week-day .wn{font-size:13px; font-weight:600; display:block; margin:2px 0;}
  .week-day .we{font-size:8.5px; color:var(--orange); display:block; line-height:1.2; margin-top:2px;}
  .month-grid{display:grid; grid-template-columns:repeat(7,1fr); gap:4px; margin-bottom:6px;}
  .month-cell{aspect-ratio:1; display:flex; flex-direction:column; align-items:center; justify-content:center; border-radius:10px; background:var(--card); border:0.5px solid var(--line); font-size:11px; position:relative;}
  .month-cell.today{background:var(--sage); border-color:var(--sage); color:#fff; font-weight:700;}
  .month-cell.empty{background:none; border:none;}
  .month-cell .evdot{width:5px; height:5px; border-radius:50%; background:var(--orange); position:absolute; bottom:4px;}
  .month-cell.today .evdot{background:#fff;}
  .month-wd{display:grid; grid-template-columns:repeat(7,1fr); gap:4px; margin-bottom:6px;}
  .month-wd span{text-align:center; font-size:9px; color:var(--ink-soft); text-transform:uppercase;}
  .shop-item{display:flex; align-items:center; gap:10px; padding:10px 0; border-top:0.5px solid #EFE9DA;}
  .shop-item:first-child{border-top:none;}
  .shop-check{width:24px; height:24px; border-radius:50%; border:1.5px solid var(--line); display:flex; align-items:center; justify-content:center; flex-shrink:0; color:transparent;}
  .shop-check.done{background:var(--sage); border-color:var(--sage); color:#fff;}
  .shop-name{flex:1; font-size:13px;}
  .shop-name.done{text-decoration:line-through; color:var(--ink-soft);}
  .shop-qtd{font-size:12px; color:var(--ink-soft); white-space:nowrap;}
  .checkin-cta{border-radius:16px; padding:16px; margin-bottom:14px; display:flex; align-items:center; gap:12px; cursor:pointer;}
  .checkin-cta.due{background:var(--sage); color:#fff;}
  .checkin-cta.wait{background:var(--card); border:0.5px solid var(--line); color:var(--ink);}
  .checkin-cta .cc-title{font-size:14px; font-weight:600;}
  .checkin-cta .cc-sub{font-size:11px; opacity:0.85;}
  .action-item{display:flex; align-items:center; gap:10px; padding:9px 0; border-top:0.5px solid #EFE9DA;}
  .action-item:first-child{border-top:none;}
  .status-pill{font-size:11px; padding:4px 10px; border-radius:999px; font-weight:600;}
  .status-pill.confirmada{background:var(--sage-bg); color:var(--sage);}
  .status-pill.pendente{background:var(--orange-bg); color:var(--orange);}
  .choice-btn{display:flex; flex-direction:column; align-items:center; gap:8px; background:var(--card); border:0.5px solid var(--line); border-radius:16px; padding:18px 10px; flex:1;}
  .choice-row{display:flex; gap:10px; margin-bottom:14px;}
  .img-preview{width:100%; border-radius:14px; margin-bottom:10px;}
  svg{display:block;}
</style>
</head>
<body>
<div id="app">
  <header>
    <div><p class="eyebrow" id="dateLabel"></p><h1 id="greeting">Olá</h1></div>
    <div class="header-icon" id="headerIcon"></div>
  </header>
  <div class="day-strip hidden" id="dayStrip"></div>

  <div id="screen-inicio" class="screen"></div>
  <div id="screen-hoje" class="screen hidden"></div>
  <div id="screen-compras" class="screen hidden"></div>
  <div id="screen-planoacao" class="screen hidden"></div>
  <div id="screen-apoio" class="screen hidden"></div>
  <div id="screen-calendario" class="screen hidden"></div>
  <div id="screen-registrar" class="screen hidden"></div>

  <nav>
    <button id="nav-inicio" class="active" onclick="showScreen('inicio')"></button>
    <button id="nav-hoje" onclick="showScreen('hoje')"></button>
    <button id="nav-compras" onclick="showScreen('compras')"></button>
    <button id="nav-planoacao" onclick="showScreen('planoacao')"></button>
    <button id="nav-calendario" onclick="showScreen('calendario')"></button>
    <button id="nav-apoio" onclick="showScreen('apoio')"></button>
  </nav>
</div>

<script>
const ICON = {
  home:'<svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M3 10.5 12 3l9 7.5"/><path d="M5 9.5V21h14V9.5"/></svg>',
  fork:'<svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M7 3v7a2 2 0 0 0 4 0V3M9 10v11M17 3c-1.5 0-2 1.5-2 3v4c0 1 .5 2 2 2s2-1 2-2V6c0-1.5-.5-3-2-3ZM17 12v9"/></svg>',
  cart:'<svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><circle cx="9" cy="20" r="1"/><circle cx="17" cy="20" r="1"/><path d="M3 4h2l2.4 11.2a2 2 0 0 0 2 1.6h7.2a2 2 0 0 0 2-1.6L21 8H6"/></svg>',
  clip:'<svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><rect x="5" y="4" width="14" height="17" rx="2"/><path d="M9 4V3a1 1 0 0 1 1-1h4a1 1 0 0 1 1 1v1"/><path d="m9 13 2 2 4-4"/></svg>',
  leaf:'<svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M5 21c0-9 6-15 15-15 0 9-6 15-15 15Z"/><path d="M5 21c3-5 6-8 11-11"/></svg>',
  cal:'<svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="5" width="18" height="16" rx="2"/><path d="M3 10h18M8 3v4M16 3v4"/><circle cx="12" cy="15" r="1.5"/></svg>',
  check:'<svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round"><path d="m5 13 4 4L19 7"/></svg>',
  x:'<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M6 6l12 12M18 6 6 18"/></svg>',
  swap:'<svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M7 4 3 8l4 4"/><path d="M3 8h13"/><path d="m17 20 4-4-4-4"/><path d="M21 16H8"/></svg>',
  chevronDown:'<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m6 9 6 6 6-6"/></svg>',
  chevronUp:'<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m18 15-6-6-6 6"/></svg>',
  bell:'<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M18 8a6 6 0 0 0-12 0c0 7-3 9-3 9h18s-3-2-3-9"/><path d="M13.7 21a2 2 0 0 1-3.4 0"/></svg>',
  drop:'<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M12 2s7 8 7 13a7 7 0 0 1-14 0c0-5 7-13 7-13Z"/></svg>',
  bowl:'<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M3 12h18a9 6 0 0 1-18 0Z"/><path d="M12 12V5"/><path d="M9 6l3-3 3 3"/></svg>',
  apple:'<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M12 8c-3.5-3-8 0-8 5.5C4 18 7 21 9.5 21c1.2 0 1.8-.6 2.5-.6s1.3.6 2.5.6C17 21 20 18 20 13.5c0-4-2.7-6.5-5.5-6"/><path d="M12 8V4c0-1 1-2 2-2"/></svg>',
  moon:'<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M20 14.5A8 8 0 1 1 9.5 4a6.5 6.5 0 0 0 10.5 10.5Z"/></svg>',
  tea:'<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M3 8h14v5a5 5 0 0 1-5 5H8a5 5 0 0 1-5-5V8Z"/><path d="M17 9h1a3 3 0 0 1 0 6h-1"/><path d="M7 4c0 1-1 1-1 2M11 4c0 1-1 1-1 2"/></svg>',
  flame:'<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M12 2s-6 6-6 12a6 6 0 0 0 12 0c0-2-1-3-2-4 .3 2-1 3-1 3 .5-3-2-4-2-7 0-1.5.5-2.5 1-4 0 0-2 0-2 0Z"/></svg>',
  star:'<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="m12 3 2.6 5.9 6.4.6-4.8 4.3 1.4 6.2L12 16.8 6.4 20l1.4-6.2L3 9.5l6.4-.6L12 3Z"/></svg>',
  trash:'<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M4 7h16M9 7V5a1 1 0 0 1 1-1h4a1 1 0 0 1 1 1v2m-9 0 1 13a1 1 0 0 0 1 1h8a1 1 0 0 0 1-1l1-13"/></svg>',
  plus:'<svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 5v14M5 12h14"/></svg>',
  pill:'<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="8" width="18" height="8" rx="4" transform="rotate(-35 12 12)"/><path d="M9 9l6 6"/></svg>',
  camera:'<svg width="26" height="26" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round"><path d="M4 8a2 2 0 0 1 2-2h1l1.5-2h7L17 6h1a2 2 0 0 1 2 2v10a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2Z"/><circle cx="12" cy="13" r="3.5"/></svg>',
  edit:'<svg width="26" height="26" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round"><path d="M12 20h9"/><path d="M16.5 3.5a2.1 2.1 0 0 1 3 3L7 19l-4 1 1-4Z"/></svg>',
  sparkle:'<svg width="26" height="26" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round"><path d="M12 3v4M12 17v4M3 12h4M17 12h4M5.5 5.5l2.8 2.8M15.7 15.7l2.8 2.8M18.5 5.5l-2.8 2.8M8.3 15.7l-2.8 2.8"/></svg>'
};
function ic(name, size){ let s = ICON[name]||''; if(size){ s = s.replace(/width="\d+"/,'width="'+size+'"').replace(/height="\d+"/,'height="'+size+'"'); } return s; }

const MEAL_ICON = {
  "06:00":{i:'drop', bg:'var(--blue-bg)', c:'var(--blue)'},
  "08:00":{i:'bowl', bg:'var(--sage-bg)', c:'var(--sage)'},
  "12:00":{i:'bowl', bg:'var(--pastel)', c:'var(--sage)'},
  "15:30":{i:'apple', bg:'var(--orange-bg)', c:'var(--orange)'},
  "18:00":{i:'apple', bg:'var(--orange-bg)', c:'var(--orange)'},
  "19:30":{i:'moon', bg:'var(--blue-bg)', c:'var(--blue)'},
  "23:00":{i:'tea', bg:'var(--sage-bg)', c:'var(--sage)'}
};
const OBRIGATORIAS = ["08:00","12:00","15:30","19:30"];
const MACRO_COL = {p:'var(--sage)', c:'var(--orange)', g:'var(--blue)'};
const SUPPLEMENTS = [{nome:"Ômega 3", quando:"Antes do almoço", refeicao:"12:00"}];

const DIET = {
  "06:00": {nome:"Em jejum", desc:"Hidratação logo ao acordar, antes de qualquer outro alimento.", grupos:[
    {r:"Hidratação", itens:[{nome:"Água natural", valor:250, unidade:"ml", tipo:"volume", kcal:0,p:0,c:0,g:0}]}
  ]},
  "08:00": {nome:"Café da manhã", desc:"Une proteína e fibra logo cedo, o que ajuda a segurar a fome até o almoço.", grupos:[
    {r:"Carboidrato", itens:[
      {nome:"Pão de forma integral", valor:25, unidade:"g", tipo:"fixo", kcal:65,p:3,c:12,g:1},
      {nome:"Pão francês sem miolo", valor:30, unidade:"g", tipo:"fixo", kcal:80,p:3,c:16,g:0.5},
      {nome:"Flocos de milho (cuscuz)", valor:20, unidade:"g", tipo:"fixo", kcal:75,p:2,c:16,g:0.5}
    ]},
    {r:"Proteína", itens:[
      {nome:"Ovo inteiro cozido", valor:61, unidade:"g", tipo:"fixo", kcal:90,p:7,c:1,g:6},
      {nome:"Queijo muçarela light", valor:30, unidade:"g", tipo:"fixo", kcal:70,p:7,c:1,g:4},
      {nome:"Requeijão light", valor:30, unidade:"g", tipo:"fixo", kcal:55,p:3,c:2,g:4},
      {nome:"Patê de frango", valor:60, unidade:"g", tipo:"fixo", kcal:95,p:12,c:1,g:5}
    ]},
    {r:"Fruta", itens:[
      {nome:"Mamão papaia", valor:150, unidade:"g", tipo:"fixo", kcal:60,p:1,c:15,g:0},
      {nome:"Banana prata", valor:65, unidade:"g", tipo:"fixo", kcal:60,p:1,c:15,g:0},
      {nome:"Uva", valor:96, unidade:"g", tipo:"fixo", kcal:65,p:0.5,c:16,g:0},
      {nome:"Morango", valor:120, unidade:"g", tipo:"fixo", kcal:40,p:1,c:9,g:0},
      {nome:"Melão", valor:173, unidade:"g", tipo:"fixo", kcal:60,p:1,c:14,g:0},
      {nome:"Ameixa", valor:84, unidade:"g", tipo:"fixo", kcal:45,p:0.5,c:11,g:0},
      {nome:"Manga", valor:83, unidade:"g", tipo:"fixo", kcal:50,p:0.5,c:13,g:0},
      {nome:"Pêssego", valor:150, unidade:"g", tipo:"fixo", kcal:60,p:1,c:14,g:0},
      {nome:"Maçã com casca", valor:130, unidade:"g", tipo:"fixo", kcal:70,p:0.3,c:18,g:0}
    ]},
    {r:"Fibra e proteína", itens:[
      {nome:"Gel de chia", valor:1, unidade:"colher de sopa", tipo:"fixo", kcal:35,p:1,c:3,g:2},
      {nome:"Whey protein", valor:20, unidade:"g", tipo:"fixo", kcal:75,p:18,c:1,g:1},
      {nome:"Leite desnatado", valor:150, unidade:"ml", tipo:"volume", kcal:55,p:5,c:7,g:0.2}
    ]}
  ]},
  "12:00": {nome:"Almoço", desc:"A refeição mais completa do dia, equilibrando proteína, carboidrato e fibra.", grupos:[
    {r:"Fibra", itens:[
      {nome:"Salada crua à vontade + azeite", valor:8, unidade:"g", tipo:"fixo", kcal:70,p:0,c:0,g:8},
      {nome:"Salada + molho de mostarda", valor:65, unidade:"g", tipo:"fixo", kcal:95,p:1,c:4,g:9},
      {nome:"Salada + molho balsâmico", valor:16, unidade:"g", tipo:"fixo", kcal:80,p:0,c:1,g:8}
    ]},
    {r:"Fibra", itens:[
      {nome:"Legumes cozidos", valor:60, unidade:"g", tipo:"fixo", kcal:25,p:1,c:5,g:0},
      {nome:"Legumes ao forno", valor:54, unidade:"g", tipo:"fixo", kcal:20,p:1,c:3,g:1}
    ]},
    {r:"Proteína", itens:[
      {nome:"Frango grelhado", valor:100, unidade:"g", tipo:"fixo", kcal:165,p:31,c:0,g:4},
      {nome:"Carne bovina magra (máx. 2x/sem)", valor:90, unidade:"g", tipo:"fixo", kcal:170,p:28,c:0,g:6},
      {nome:"Filé de peixe", valor:120, unidade:"g", tipo:"fixo", kcal:140,p:26,c:0,g:3},
      {nome:"Lombo suíno assado", valor:90, unidade:"g", tipo:"fixo", kcal:160,p:24,c:0,g:7}
    ]},
    {r:"Carboidrato", itens:[
      {nome:"Arroz cozido", valor:100, unidade:"g", tipo:"fixo", kcal:130,p:2,c:28,g:0.2},
      {nome:"Batata inglesa cozida", valor:225, unidade:"g", tipo:"fixo", kcal:170,p:4,c:39,g:0},
      {nome:"Macarrão cozido", valor:75, unidade:"g", tipo:"fixo", kcal:110,p:4,c:22,g:0.5},
      {nome:"Abóbora cozida", valor:252, unidade:"g", tipo:"fixo", kcal:100,p:2,c:24,g:0},
      {nome:"Mandioquinha cozida", valor:160, unidade:"g", tipo:"fixo", kcal:190,p:2,c:45,g:0.3}
    ]},
    {r:"Proteína vegetal", itens:[{nome:"Feijão preto cozido", valor:70, unidade:"g", tipo:"fixo", kcal:60,p:4,c:11,g:0.3}]},
    {r:"Vitamina C", itens:[
      {nome:"Tangerina", valor:100, unidade:"g", tipo:"fixo", kcal:45,p:1,c:11,g:0},
      {nome:"Laranja", valor:90, unidade:"g", tipo:"fixo", kcal:40,p:1,c:10,g:0},
      {nome:"Morango", valor:42, unidade:"g", tipo:"fixo", kcal:15,p:0.3,c:3,g:0},
      {nome:"Abacaxi", valor:75, unidade:"g", tipo:"fixo", kcal:40,p:0.3,c:10,g:0},
      {nome:"Kiwi", valor:76, unidade:"g", tipo:"fixo", kcal:45,p:1,c:11,g:0},
      {nome:"Mamão", valor:100, unidade:"g", tipo:"fixo", kcal:40,p:1,c:10,g:0},
      {nome:"Suco de laranja", valor:100, unidade:"ml", tipo:"volume", kcal:45,p:1,c:11,g:0}
    ]}
  ]},
  "15:30": {nome:"Lanche da tarde", desc:"Faz a ponte entre o almoço e o jantar, com proteína para evitar chegar com fome excessiva à noite.", grupos:[
    {r:"Carboidrato", itens:[
      {nome:"Pão de forma industrializado", valor:50, unidade:"g", tipo:"fixo", kcal:130,p:4,c:24,g:2},
      {nome:"Rap10 ou pão sírio", valor:1, unidade:"unidade", tipo:"fixo", kcal:90,p:3,c:17,g:1},
      {nome:"Torradas", valor:32, unidade:"g", tipo:"fixo", kcal:130,p:3,c:24,g:2},
      {nome:"Tapioca de goma", valor:30, unidade:"g", tipo:"fixo", kcal:65,p:0,c:16,g:0}
    ]},
    {r:"Proteína", itens:[
      {nome:"Iogurte natural desnatado", valor:140, unidade:"g", tipo:"fixo", kcal:60,p:6,c:8,g:0},
      {nome:"Iogurte grego", valor:90, unidade:"g", tipo:"fixo", kcal:60,p:6,c:4,g:3},
      {nome:"Patê de frango", valor:40, unidade:"g", tipo:"fixo", kcal:65,p:8,c:1,g:3},
      {nome:"Ovo cozido", valor:61, unidade:"g", tipo:"fixo", kcal:90,p:7,c:1,g:6},
      {nome:"Patê de atum light", valor:51, unidade:"g", tipo:"fixo", kcal:70,p:9,c:1,g:3}
    ]},
    {r:"Proteína", itens:[
      {nome:"Whey protein", valor:10, unidade:"g", tipo:"fixo", kcal:38,p:9,c:0.5,g:0.5},
      {nome:"Queijo muçarela light/minas", valor:20, unidade:"g", tipo:"fixo", kcal:45,p:5,c:1,g:2.5}
    ]}
  ]},
  "18:00": {nome:"Lanche (se fome ao chegar)", desc:"Existe só para os dias em que a fome aparecer antes do jantar.", grupos:[
    {r:"Proteína", itens:[
      {nome:"Iogurte grego", valor:90, unidade:"g", tipo:"fixo", kcal:60,p:6,c:4,g:3},
      {nome:"Ovo cozido", valor:61, unidade:"g", tipo:"fixo", kcal:90,p:7,c:1,g:6},
      {nome:"Leite + whey", valor:100, unidade:"ml", tipo:"volume", kcal:75,p:13,c:4,g:0.5}
    ]}
  ]},
  "19:30": {nome:"Jantar", desc:"Mais leve que o almoço, pensado para dar saciedade sem pesar para a noite e para o sono.", grupos:[
    {r:"Fibra", itens:[
      {nome:"Salada crua à vontade + azeite", valor:8, unidade:"g", tipo:"fixo", kcal:70,p:0,c:0,g:8},
      {nome:"Salada + molho de mostarda", valor:65, unidade:"g", tipo:"fixo", kcal:95,p:1,c:4,g:9},
      {nome:"Salada + molho balsâmico", valor:16, unidade:"g", tipo:"fixo", kcal:80,p:0,c:1,g:8}
    ]},
    {r:"Fibra", itens:[
      {nome:"Legumes cozidos", valor:60, unidade:"g", tipo:"fixo", kcal:25,p:1,c:5,g:0},
      {nome:"Legumes ao forno", valor:54, unidade:"g", tipo:"fixo", kcal:20,p:1,c:3,g:1}
    ]},
    {r:"Proteína", itens:[
      {nome:"Frango grelhado", valor:80, unidade:"g", tipo:"fixo", kcal:130,p:25,c:0,g:3},
      {nome:"Carne bovina magra (máx. 2x/sem)", valor:70, unidade:"g", tipo:"fixo", kcal:130,p:22,c:0,g:5},
      {nome:"Peixe grelhado", valor:100, unidade:"g", tipo:"fixo", kcal:115,p:22,c:0,g:2.5},
      {nome:"Lombo suíno assado", valor:70, unidade:"g", tipo:"fixo", kcal:125,p:19,c:0,g:5.5}
    ]},
    {r:"Carboidrato", itens:[
      {nome:"Arroz cozido", valor:75, unidade:"g", tipo:"fixo", kcal:100,p:2,c:21,g:0.2},
      {nome:"Batata inglesa cozida", valor:175, unidade:"g", tipo:"fixo", kcal:130,p:3,c:30,g:0},
      {nome:"Macarrão cozido", valor:75, unidade:"g", tipo:"fixo", kcal:110,p:4,c:22,g:0.5},
      {nome:"Abóbora cozida", valor:216, unidade:"g", tipo:"fixo", kcal:85,p:2,c:20,g:0},
      {nome:"Mandioquinha cozida", valor:120, unidade:"g", tipo:"fixo", kcal:140,p:1,c:34,g:0.2}
    ]},
    {r:"Proteína vegetal", itens:[{nome:"Feijão preto cozido", valor:50, unidade:"g", tipo:"fixo", kcal:45,p:3,c:8,g:0.2}]},
    {r:"Vitamina C", itens:[
      {nome:"Tangerina", valor:100, unidade:"g", tipo:"fixo", kcal:45,p:1,c:11,g:0},
      {nome:"Laranja", valor:90, unidade:"g", tipo:"fixo", kcal:40,p:1,c:10,g:0},
      {nome:"Morango", valor:42, unidade:"g", tipo:"fixo", kcal:15,p:0.3,c:3,g:0},
      {nome:"Kiwi", valor:76, unidade:"g", tipo:"fixo", kcal:45,p:1,c:11,g:0},
      {nome:"Mamão", valor:100, unidade:"g", tipo:"fixo", kcal:40,p:1,c:10,g:0}
    ]}
  ]},
  "23:00": {nome:"Chá (opcional, 1h antes de deitar)", desc:"Apoio para relaxar antes de dormir, sem relação com controle calórico.", grupos:[
    {r:"Relaxamento", itens:[{nome:"Chá de camomila ou similar", valor:150, unidade:"ml", tipo:"volume", kcal:2,p:0,c:0.5,g:0}]}
  ]}
};
const AVOID = ["ultraprocessados em geral","frituras e empanados","embutidos (bacon, salame, salsicha, presunto)","doces e produtos açucarados","refrigerantes e sucos de caixinha","farinhas e massas muito refinadas"];
const VOL_UNITS = {ml:1, "colher de sopa":15, "xícara":240, "copo":200};
function convertVol(valor, de, para){ const ml = valor * VOL_UNITS[de]; return Math.round((ml / VOL_UNITS[para])*10)/10; }
function mealRefKcal(t){ return DIET[t].grupos.reduce((s,g)=>s+g.itens[0].kcal,0); }
function mealRefMacros(t){ return DIET[t].grupos.reduce((s,g)=>{ const it=g.itens[0]; return {p:s.p+it.p, c:s.c+it.c, g:s.g+it.g}; }, {p:0,c:0,g:0}); }
function totalDiaKcal(){ return OBRIGATORIAS.reduce((s,t)=>s+mealRefKcal(t),0); }
function totalGeralKcal(){ return mealTimes().reduce((s,t)=>s+mealRefKcal(t),0); }
function macroBarHTML(macros){
  const pk=macros.p*4, ck=macros.c*4, gk=macros.g*9, tot=pk+ck+gk || 1;
  const pw=(pk/tot*100).toFixed(0), cw=(ck/tot*100).toFixed(0), gw=(gk/tot*100).toFixed(0);
  let html = '<div class="macro-bar"><span style="width:'+pw+'%; background:'+MACRO_COL.p+';"></span><span style="width:'+cw+'%; background:'+MACRO_COL.c+';"></span><span style="width:'+gw+'%; background:'+MACRO_COL.g+';"></span></div>';
  html += '<div class="macro-legend"><span>P '+macros.p.toFixed(0)+'g</span><span>C '+macros.c.toFixed(0)+'g</span><span>G '+macros.g.toFixed(0)+'g</span></div>';
  return html;
}

let profile=null, checkins=[], retomadas=[], registros={}, avisos=[], eventos=[];
let compras={periodo:'7', itensAdicionados:[], comprados:{}};
let consulta={data:'', horario:'', confirmada:false};
let acoes=[];
let suplementosLog={};
let bannerDismiss={};
let descOpen={}, hojeTab='registro', subOpen={};
let novoEventoImpacto=[];
let calView='semana', calMonthOffset=0;
let comprasSubOpen={};
let registrarState={step:'choose', mode:null, imageBase64:null, mediaType:null, texto:'', refeicaoEscolhida:'', resultado:null, loading:false, error:null};
let ciclo={ativo:false, dataUltima:'', duracao:28};
let configNutri={alertaDiasLimite:12};
let alertaFomeHoje=null;
let checkinFlowState='intro';
let checkinDraft={semana:'', comentario:'', fome:'', planoOk:'', sono:'', estresse:'', dificuldade:'', funcionouBem:''};

async function loadData(){
  try{ const r=await window.storage.get('profile'); profile=r?JSON.parse(r.value):null; }catch(e){ profile=null; }
  try{ const r=await window.storage.get('checkins'); checkins=r?JSON.parse(r.value):[]; }catch(e){ checkins=[]; }
  try{ const r=await window.storage.get('retomadas'); retomadas=r?JSON.parse(r.value):[]; }catch(e){ retomadas=[]; }
  try{ const r=await window.storage.get('registros'); registros=r?JSON.parse(r.value):{}; }catch(e){ registros={}; }
  try{ const r=await window.storage.get('avisos'); avisos=r?JSON.parse(r.value):[]; }catch(e){ avisos=[]; }
  try{ const r=await window.storage.get('eventos'); eventos=r?JSON.parse(r.value):[]; }catch(e){ eventos=[]; }
  try{ const r=await window.storage.get('compras'); const loaded=r?JSON.parse(r.value):{}; compras=Object.assign({periodo:'7', itensAdicionados:[], comprados:{}}, loaded||{}); if(!Array.isArray(compras.itensAdicionados)) compras.itensAdicionados=[]; if(!compras.comprados) compras.comprados={}; }catch(e){}
  try{ const r=await window.storage.get('consulta'); consulta=r?JSON.parse(r.value):consulta; }catch(e){}
  try{ const r=await window.storage.get('acoes'); acoes=r?JSON.parse(r.value):[]; }catch(e){ acoes=[]; }
  try{ const r=await window.storage.get('suplementosLog'); suplementosLog=r?JSON.parse(r.value):{}; }catch(e){ suplementosLog={}; }
  try{ const r=await window.storage.get('bannerDismiss'); bannerDismiss=r?JSON.parse(r.value):{}; }catch(e){ bannerDismiss={}; }
  try{ const r=await window.storage.get('ciclo'); ciclo=r?JSON.parse(r.value):ciclo; }catch(e){}
  try{ const r=await window.storage.get('configNutri'); configNutri=r?JSON.parse(r.value):configNutri; }catch(e){}
  try{ const r=await window.storage.get('alertasFome'); const af=r?JSON.parse(r.value):[]; alertaFomeHoje = af.find(a=>a.date===todayKey())||null; window._alertasFome=af; }catch(e){ window._alertasFome=[]; }
  try{ const r=await window.storage.get('checkinDraft'); checkinDraft=r?JSON.parse(r.value):checkinDraft; }catch(e){}
}
async function saveProfile(){ try{ await window.storage.set('profile', JSON.stringify(profile)); }catch(e){} }
async function saveCheckins(){ try{ await window.storage.set('checkins', JSON.stringify(checkins)); }catch(e){} }
async function saveRetomadas(){ try{ await window.storage.set('retomadas', JSON.stringify(retomadas)); }catch(e){} }
async function saveRegistros(){ try{ await window.storage.set('registros', JSON.stringify(registros)); }catch(e){} }
async function saveAvisos(){ try{ await window.storage.set('avisos', JSON.stringify(avisos)); }catch(e){} }
async function saveEventos(){ try{ await window.storage.set('eventos', JSON.stringify(eventos)); }catch(e){} }
async function saveCompras(){ try{ await window.storage.set('compras', JSON.stringify(compras)); }catch(e){} }
async function saveConsulta(){ try{ await window.storage.set('consulta', JSON.stringify(consulta)); }catch(e){} }
async function saveAcoes(){ try{ await window.storage.set('acoes', JSON.stringify(acoes)); }catch(e){} }
async function saveSuplementosLog(){ try{ await window.storage.set('suplementosLog', JSON.stringify(suplementosLog)); }catch(e){} }
async function saveBannerDismiss(){ try{ await window.storage.set('bannerDismiss', JSON.stringify(bannerDismiss)); }catch(e){} }
async function saveCiclo(){ try{ await window.storage.set('ciclo', JSON.stringify(ciclo)); }catch(e){} }
async function saveConfigNutri(){ try{ await window.storage.set('configNutri', JSON.stringify(configNutri)); }catch(e){} }
async function saveAlertasFome(){ try{ await window.storage.set('alertasFome', JSON.stringify(window._alertasFome||[])); }catch(e){} }
async function saveCheckinDraft(){ try{ await window.storage.set('checkinDraft', JSON.stringify(checkinDraft)); }catch(e){} }

function todayKey(){ const d=new Date(); return d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0'); }
function dateKey(d){ return d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0'); }
function todayReg(){ const k=todayKey(); if(!registros[k]) registros[k]={}; return registros[k]; }
function mealTimes(){ return Object.keys(DIET); }
function nextMealTime(fromTime){ const keys=mealTimes(); const i=keys.indexOf(fromTime); return (i>=0 && i<keys.length-1)?keys[i+1]:null; }
function fmtDate(){
  const d=new Date();
  const dias=["domingo","segunda-feira","terça-feira","quarta-feira","quinta-feira","sexta-feira","sábado"];
  const meses=["jan","fev","mar","abr","mai","jun","jul","ago","set","out","nov","dez"];
  return dias[d.getDay()].charAt(0).toUpperCase()+dias[d.getDay()].slice(1)+", "+d.getDate()+" de "+meses[d.getMonth()];
}
function isMonday(){ return new Date().getDay()===1; }
function alreadyCheckedInThisWeek(){
  if(!checkins.length) return false;
  const last=new Date(checkins[checkins.length-1].date);
  return (new Date()-last)/(1000*60*60*24) < 6;
}
function diasAteProximoCheckin(){
  if(isMonday() && !alreadyCheckedInThisWeek()) return 0;
  const day=new Date().getDay();
  let diff=(8-day)%7; if(diff===0) diff=7;
  return diff;
}
function eventosNoDia(dk){ return eventos.filter(e=>e.data===dk); }
function todayBanner(){ const k=todayKey(); if(!bannerDismiss[k]) bannerDismiss[k]={}; return bannerDismiss[k]; }

function faseCiclo(){
  if(!ciclo.ativo || !ciclo.dataUltima) return null;
  const inicio = new Date(ciclo.dataUltima+'T00:00:00');
  const hoje = new Date(todayKey()+'T00:00:00');
  const dur = ciclo.duracao || 28;
  let diasDesde = Math.floor((hoje - inicio)/(1000*60*60*24)) % dur;
  if(diasDesde < 0) diasDesde += dur;
  if(diasDesde < 5) return {fase:'menstrual', dia:diasDesde+1};
  if(diasDesde >= dur-5) return {fase:'pre-menstrual', dia:diasDesde+1};
  if(diasDesde >= Math.floor(dur/2)-2 && diasDesde <= Math.floor(dur/2)+2) return {fase:'ovulacao', dia:diasDesde+1};
  return {fase:'normal', dia:diasDesde+1};
}
const CICLO_DICAS = {
  'menstrual': "Período menstrual: é comum sentir mais cansaço e, em algumas pessoas, mais desejo por alimentos específicos. Manter a hidratação e ficar atenta a sinais de mal-estar intenso ajuda. Cólicas fortes ou sangramento muito intenso merecem avaliação médica.",
  'pre-menstrual': "Fase pré-menstrual: alterações de apetite, inchaço e oscilações de humor são comuns nessa fase, por causa de mudanças hormonais normais do ciclo. Isso não significa falta de força de vontade. Se notar muita dificuldade em seguir o plano nesses dias, vale comentar com sua nutricionista."
};
function diasSemManterDieta(){
  let dias=0;
  for(let i=1;i<=60;i++){
    const d=new Date(); d.setDate(d.getDate()-i);
    const dk=dateKey(d);
    const reg=registros[dk];
    if(!reg){ dias++; continue; }
    const teveFez = OBRIGATORIAS.some(t=> reg[t] && reg[t].status==='fez');
    if(teveFez) break;
    dias++;
  }
  return dias;
}

function renderDayStrip(){
  const labels=['D','S','T','Q','Q','S','S'];
  const d=new Date(); const todayIdx=d.getDay();
  const start=new Date(d); start.setDate(d.getDate()-todayIdx);
  let html='';
  for(let i=0;i<7;i++){
    const day=new Date(start); day.setDate(start.getDate()+i);
    const isToday=i===todayIdx;
    html += '<div class="day-pill'+(isToday?' today':'')+'"><span class="dl">'+labels[i]+'</span><span class="dn">'+day.getDate()+'</span></div>';
  }
  document.getElementById('dayStrip').innerHTML = html;
}

function showScreen(name){
  ['inicio','hoje','compras','apoio','calendario','planoacao','registrar'].forEach(s=>{
    document.getElementById('screen-'+s).classList.toggle('hidden', s!==name);
  });
  ['inicio','hoje','compras','planoacao','calendario','apoio'].forEach(s=>{
    const btn=document.getElementById('nav-'+s); if(btn) btn.classList.toggle('active', s===name);
  });
  document.getElementById('nav-inicio').innerHTML=ic('home');
  document.getElementById('nav-hoje').innerHTML=ic('fork');
  document.getElementById('nav-compras').innerHTML=ic('cart');
  document.getElementById('nav-planoacao').innerHTML=ic('clip');
  document.getElementById('nav-calendario').innerHTML=ic('cal');
  document.getElementById('nav-apoio').innerHTML=ic('leaf');
  document.getElementById('headerIcon').innerHTML='<span style="color:var(--sage)">'+ic('leaf',18)+'</span>';
  document.getElementById('dayStrip').classList.toggle('hidden', name!=='hoje');
  if(name==='inicio') renderInicio();
  if(name==='hoje'){ renderDayStrip(); renderHoje(); }
  if(name==='compras') renderCompras();
  if(name==='planoacao') renderPlanoAcao();
  if(name==='apoio') renderApoio();
  if(name==='calendario') renderCalendario();
}
function switchHojeTab(tab){ hojeTab=tab; renderHoje(); }

function consumedForMeal(t, entry){
  if(!entry || !entry.status) return {kcal:0,p:0,c:0,g:0};
  if(entry.status==='fez'){ const m=mealRefMacros(t); return {kcal:mealRefKcal(t), p:m.p, c:m.c, g:m.g}; }
  if(entry.status==='parcial' && entry.selecoes){
    let kcal=0,p=0,c=0,g=0;
    Object.keys(entry.selecoes).forEach(gi=>{
      const s=entry.selecoes[gi];
      if(s && s.ok){ const item=DIET[t].grupos[gi].itens[s.idx]; kcal+=item.kcal; p+=item.p; c+=item.c; g+=item.g; }
    });
    return {kcal,p,c,g};
  }
  return {kcal:0,p:0,c:0,g:0};
}
function consumedTotals(){
  const reg=todayReg(); let kcal=0,p=0,c=0,g=0;
  mealTimes().forEach(t=>{ const cm=consumedForMeal(t,reg[t]); kcal+=cm.kcal; p+=cm.p; c+=cm.c; g+=cm.g; });
  return {kcal,p,c,g};
}
function allObrigatoriasRegistradas(){
  const reg=todayReg();
  return OBRIGATORIAS.every(t=> reg[t] && ['fez','parcial','nao'].includes(reg[t].status));
}

// ---------- INÍCIO ----------
function renderInicio(){
  const el=document.getElementById('screen-inicio');
  const nome=profile && profile.name ? profile.name : '';
  document.getElementById('greeting').textContent = nome ? ('Olá, '+nome) : 'Olá';
  document.getElementById('dateLabel').textContent = fmtDate();

  let html = '<div style="display:flex; gap:10px; margin-bottom:14px;">'+
    '<button class="registrar-btn" style="margin-bottom:0; flex:1; padding:14px 8px; font-size:13px;" onclick="openRegistrar()">'+ic('sparkle',17)+' Registrar refeição</button>';
  const dias0 = diasAteProximoCheckin(); const due0 = dias0===0;
  html += '<div class="checkin-cta '+(due0?'due':'wait')+'" style="flex:1; margin-bottom:0; flex-direction:column; text-align:center; gap:4px; padding:12px 8px;" onclick="abrirCheckin();">'+ic('clip',18)+
    '<div><div class="cc-title">Check-in semanal</div><div class="cc-sub">'+(due0?'Disponível hoje':'Próximo em '+dias0+' dia'+(dias0>1?'s':''))+'</div></div></div>'+
    '</div>';

  const diasSem = diasSemManterDieta();
  if(diasSem >= (configNutri.alertaDiasLimite||12)){
    html += '<div class="warn-banner" style="background:var(--terracota-bg); border-color:var(--terracota-line); color:var(--terracota);"><span>'+ic('bell')+'</span><span>Já fazem '+diasSem+' dias sem conseguir manter o plano principal. Pode ser um bom momento para um check-in, uma consulta extra, ou chamar sua nutricionista para reajustar juntas.</span></div>';
  }

  const lembreteRefeicao = refeicaoParaLembrar();
  if(lembreteRefeicao){
    html += '<div class="banner" style="background:var(--sage-bg); border-color:var(--sage-line); color:var(--sage); flex-wrap:wrap;">'+
      '<span>'+ic('bell')+'</span><span style="flex:1;">Já é hora de <b>'+DIET[lembreteRefeicao].nome.toLowerCase()+'</b> ('+lembreteRefeicao+'). Quer registrar agora?</span>'+
      '<button class="banner-x" onclick="dismissLembrete(\''+lembreteRefeicao+'\')">'+ic('x')+'</button>'+
      '<button class="mini-btn ok" style="width:100%; margin-top:6px; justify-content:center;" onclick="showScreen(\'hoje\')">'+ic('fork',13)+' Registrar '+DIET[lembreteRefeicao].nome.toLowerCase()+'</button>'+
      '</div>';
  }

  const b = todayBanner();
  const avisosHoje = avisos.filter(a=>a.date===todayKey() && !a.dismissed);
  if(avisosHoje.length && !b.aviso){
    const nomes = avisosHoje.map(a=>DIET[a.meal].nome).join(', ');
    html += '<div class="warn-banner"><span>'+ic('bell')+'</span><span>Hoje ficou sem registrar redistribuição em: <b>'+nomes+'</b>. Todas as refeições foram pensadas com cuidado para você, pular sem repor pode deixar essa energia em aberto.</span><button class="banner-x" onclick="dismissBanner(\'aviso\')">'+ic('x')+'</button></div>';
  }
  const eventoHoje = eventosNoDia(todayKey())[0];
  if(eventoHoje && !b.evento){
    html += '<div class="banner"><span>'+ic('cal')+'</span><span>Hoje: <b>'+eventoHoje.titulo+'</b>'+(eventoHoje.horario?' às '+eventoHoje.horario:'')+(eventoHoje.impacto&&eventoHoje.impacto.length?' · pode afetar '+eventoHoje.impacto.join(', '):'')+'</span><button class="banner-x" onclick="dismissBanner(\'evento\')">'+ic('x')+'</button></div>';
  }
  const faseAtual = faseCiclo();
  if(faseAtual && CICLO_DICAS[faseAtual.fase] && !b.ciclo){
    html += '<div class="banner" style="background:var(--pastel); border-color:var(--sage-line); color:var(--sage);"><span>'+ic('leaf')+'</span><span>'+CICLO_DICAS[faseAtual.fase]+'</span><button class="banner-x" onclick="dismissBanner(\'ciclo\')">'+ic('x')+'</button></div>';
  }

  html += renderStatusSemana();

  html += '<div class="card"><h3>'+ic('bell',14)+' Como você está?</h3>'+
    '<p style="font-size:13px; margin-bottom:10px;">Nos últimos dias, você tem sentido mais fome do que o normal, ou sente que o plano não está encaixando na sua rotina?</p>';
  if(alertaFomeHoje){
    html += '<p class="small" style="color:var(--sage);">'+ic('check',12)+' Já sinalizado para sua nutricionista hoje.</p>';
  } else {
    html += '<div class="status-row"><button class="status-btn" onclick="marcarFome(true)">Sim, tenho sentido</button><button class="status-btn" onclick="marcarFome(false)">Não, está tranquilo</button></div>';
  }
  html += '</div>';

  html += '<div class="card"><h3>'+ic('cal',14)+' Próxima consulta</h3>';
  if(consulta.data){
    const d=new Date(consulta.data+'T00:00:00');
    html += '<p style="font-size:14px; margin:4px 0;">'+d.toLocaleDateString('pt-BR')+(consulta.horario?' às '+consulta.horario:'')+'</p>'+
      '<span class="status-pill '+(consulta.confirmada?'confirmada':'pendente')+'">'+(consulta.confirmada?'Confirmada':'Pendente')+'</span>';
  } else { html += '<p class="small">Nenhuma consulta agendada ainda.</p>'; }
  html += '<button class="ghost-btn" onclick="showScreen(\'planoacao\')">Ver plano de ação</button></div>';

  const pend = acoes.filter(a=>!a.feito).length, feitas = acoes.filter(a=>a.feito).length;
  html += '<div class="card"><h3>'+ic('clip',14)+' Plano de ação da semana</h3>';
  if(acoes.length){
    html += '<p style="font-size:14px; margin:4px 0;">'+feitas+' de '+acoes.length+' ações concluídas</p>';
    acoes.slice(0,3).forEach(a=>{ html += '<p class="small">'+(a.feito?'✓ ':'· ')+a.texto+'</p>'; });
  } else { html += '<p class="small">Nenhuma ação registrada ainda.</p>'; }
  html += '</div>';

  const proximos = [...eventos].filter(e=>e.data>=todayKey()).sort((a,b2)=>a.data.localeCompare(b2.data)).slice(0,3);
  html += '<div class="card"><h3>'+ic('star',14)+' Próximos eventos</h3>';
  if(proximos.length){ proximos.forEach(e=>{ const d=new Date(e.data+'T00:00:00'); html += '<p class="small">'+d.toLocaleDateString('pt-BR')+' · '+e.titulo+'</p>'; }); }
  else { html += '<p class="small">Nenhum evento futuro registrado.</p>'; }
  html += '</div>';

  el.innerHTML = html;
}
function renderStatusSemana(){
  let fez=0, parcial=0, nao=0, total=0;
  for(let i=0;i<7;i++){
    const d=new Date(); d.setDate(d.getDate()-i);
    const reg=registros[dateKey(d)]; if(!reg) continue;
    OBRIGATORIAS.forEach(t=>{ if(reg[t]){ total++; if(reg[t].status==='fez') fez++; else if(reg[t].status==='parcial') parcial++; else if(reg[t].status==='nao') nao++; } });
  }
  const pct = total ? Math.round((fez/total)*100) : null;
  let insight;
  if(total===0){ insight = "Ainda não há registros suficientes essa semana para uma análise."; }
  else if(pct >= 80){ insight = "Semana bem consistente. O que está funcionando vale a pena manter."; }
  else if(pct >= 50){ insight = "Semana com altos e baixos, dentro do esperado. Repare em quais dias foram mais difíceis."; }
  else { insight = "Semana mais desafiadora que o normal. Considere usar o apoio ou conversar no próximo check-in sobre o que está pesando."; }
  let html = '<div class="card"><h3>'+ic('flame',14)+' Status da semana</h3>';
  if(total>0){
    html += '<div style="display:flex; gap:14px; margin-bottom:10px;">'+
      '<div style="text-align:center;"><div style="font-size:18px; font-weight:700; color:var(--sage);">'+fez+'</div><div class="small">feitas</div></div>'+
      '<div style="text-align:center;"><div style="font-size:18px; font-weight:700; color:var(--orange);">'+parcial+'</div><div class="small">parciais</div></div>'+
      '<div style="text-align:center;"><div style="font-size:18px; font-weight:700; color:var(--ink-soft);">'+nao+'</div><div class="small">não feitas</div></div>'+
      '</div>';
  }
  html += '<p class="small">'+insight+'</p></div>';
  return html;
}
async function marcarFome(sim){
  const list = window._alertasFome||[];
  list.push({date:todayKey(), sentiuFome:sim});
  window._alertasFome = list;
  alertaFomeHoje = {date:todayKey(), sentiuFome:sim};
  await saveAlertasFome();
  renderInicio();
}
function horaAtualMinutos(){ const d=new Date(); return d.getHours()*60+d.getMinutes(); }
function paraMinutos(hhmm){ const [h,m]=hhmm.split(':').map(Number); return h*60+m; }
function refeicaoParaLembrar(){
  const reg = todayReg();
  const agora = horaAtualMinutos();
  const b = todayBanner();
  let candidata = null;
  mealTimes().forEach(t=>{
    if(t==='06:00' || t==='23:00') return;
    const jaRegistrada = reg[t] && ['fez','parcial','nao'].includes(reg[t].status);
    if(jaRegistrada) return;
    if(b['lembrete_'+t]) return;
    if(agora >= paraMinutos(t)){
      if(!candidata || paraMinutos(t) > paraMinutos(candidata)) candidata = t;
    }
  });
  return candidata;
}
function dismissLembrete(t){ const b=todayBanner(); b['lembrete_'+t]=true; saveBannerDismiss(); renderInicio(); }
function dismissBanner(tipo){ const b=todayBanner(); b[tipo]=true; saveBannerDismiss(); renderInicio(); }

// ---------- ALIMENTAÇÃO (ex-Hoje) ----------
function renderHoje(){
  const el=document.getElementById('screen-hoje');
  const nome=profile && profile.name ? profile.name : '';
  document.getElementById('greeting').textContent = nome ? ('Olá, '+nome) : 'Olá';
  document.getElementById('dateLabel').textContent = fmtDate();
  let html='<div class="seg">'+
    '<button class="'+(hojeTab==='registro'?'active':'')+'" onclick="switchHojeTab(\'registro\')">Registro do dia</button>'+
    '<button class="'+(hojeTab==='plano'?'active':'')+'" onclick="switchHojeTab(\'plano\')">Orientação da nutricionista</button></div>';
  if(hojeTab==='plano'){ html += renderPlanoFixoContent(); el.innerHTML=html; return; }

  html += '<div class="estimate-note">'+ic('flame')+' Calorias e macros são estimativas de referência, a confirmar quando a tabela de composição for adicionada.</div>';
  const cons = consumedTotals();
  html += '<div class="kcal-row">'+
    '<div class="kcal-box"><div class="kv">~'+Math.round(cons.kcal)+'</div><div class="kl">consumidas</div></div>'+
    '<div class="kcal-box plano"><div class="kv">~'+totalDiaKcal()+'</div><div class="kl">do plano</div></div>'+
    '<div class="kcal-box"><div class="kv">~'+totalGeralKcal()+'</div><div class="kl">total c/ opcionais</div></div></div>';
  html += '<div class="macro-summary">'+
    '<div><div class="mv" style="color:'+MACRO_COL.p+';">'+cons.p.toFixed(0)+'g</div><div class="ml">Proteína</div></div>'+
    '<div><div class="mv" style="color:'+MACRO_COL.c+';">'+cons.c.toFixed(0)+'g</div><div class="ml">Carbo</div></div>'+
    '<div><div class="mv" style="color:'+MACRO_COL.g+';">'+cons.g.toFixed(0)+'g</div><div class="ml">Gordura</div></div></div>';

  if(allObrigatoriasRegistradas()){ html += renderInsightsDia(); }
  const reg = todayReg();
  mealTimes().forEach(t=>{ html += renderMealCard(t, reg[t]); });
  html += '<button class="support-btn" onclick="showScreen(\'apoio\')">'+ic('leaf')+' Precisa de um apoio agora?</button>';
  el.innerHTML = html;
}
function renderInsightsDia(){
  const reg=todayReg();
  let fez=0, parcial=0, nao=0;
  OBRIGATORIAS.forEach(t=>{ const s=reg[t].status; if(s==='fez') fez++; else if(s==='parcial') parcial++; else if(s==='nao') nao++; });
  const cons=consumedTotals(); const plano=totalDiaKcal(); const diff = plano - cons.kcal;
  let tomColor = nao>1 ? 'var(--orange)' : 'var(--sage)';
  let tituloResumo = (nao===0 && parcial===0) ? "Dia completo, do jeito planejado" : (nao>0 ? "Um dia com ajustes, e tudo bem" : "Dia com alguns pontos parciais");
  let msg2 = (Math.abs(diff) < plano*0.1) ? "O total consumido ficou bem próximo do planejado." :
    (diff>0 ? "Ficou cerca de "+Math.round(diff)+" kcal abaixo do planejado. Se isso se repetir, vale ajustar com sua nutricionista." : "Ficou um pouco acima do planejado, sem problema, o que importa é a consistência na semana.");
  let msg3 = "Para amanhã: mantenha os horários que funcionaram melhor hoje, e use o apoio se sentir que vai ser um dia mais difícil.";
  let html = '<div class="insight-card">'+
    '<h3>'+ic('star',16)+' Como foi o seu dia</h3>'+
    '<p style="font-size:14px; font-weight:600; color:'+tomColor+'; margin:0 0 12px;">'+tituloResumo+'</p>'+
    '<div style="display:flex; gap:10px; margin-bottom:14px;">'+
      '<div style="flex:1; background:rgba(255,255,255,0.6); border-radius:12px; padding:10px; text-align:center;">'+ic('check',16)+'<div style="font-size:16px; font-weight:700; color:var(--sage); margin-top:4px;">'+fez+'</div><div class="small">feitas</div></div>'+
      '<div style="flex:1; background:rgba(255,255,255,0.6); border-radius:12px; padding:10px; text-align:center;">'+ic('swap',16)+'<div style="font-size:16px; font-weight:700; color:var(--orange); margin-top:4px;">'+parcial+'</div><div class="small">parciais</div></div>'+
      '<div style="flex:1; background:rgba(255,255,255,0.6); border-radius:12px; padding:10px; text-align:center;">'+ic('x',16)+'<div style="font-size:16px; font-weight:700; color:var(--ink-soft); margin-top:4px;">'+nao+'</div><div class="small">não feitas</div></div>'+
    '</div>'+
    '<div style="display:flex; align-items:center; gap:8px; margin-bottom:8px;">'+ic('flame',15)+'<p style="margin:0; font-size:13px;">'+msg2+'</p></div>'+
    '<div style="display:flex; align-items:center; gap:8px;">'+ic('leaf',15)+'<p style="margin:0; font-size:13px;">'+msg3+'</p></div>'+
  '</div>';
  return html;
}
function renderPlanoFixoContent(){
  let html = '<p class="small" style="margin-bottom:12px;">Esta é a orientação fixa da nutricionista. Ela não muda com o que você registra no dia a dia.</p>';
  html += '<div class="card"><h3>'+ic('pill',15)+' Suplementos</h3>';
  SUPPLEMENTS.forEach(s=>{ html += '<div class="supp-row"><div class="supp-icon">'+ic('pill',15)+'</div><div><div style="font-size:13px; font-weight:600;">'+s.nome+'</div><div class="small">'+s.quando+'</div></div></div>'; });
  html += '</div>';
  mealTimes().forEach(t=>{
    const m=DIET[t];
    html += '<div class="table-wrap"><div class="table-head"><span class="tt">'+m.nome+' · '+t+'</span><span class="tk">~'+mealRefKcal(t)+' kcal</span></div>';
    m.grupos.forEach((g,gi)=>{
      const key = t+'_'+gi; const def = g.itens[0];
      html += '<div class="trow"><span class="tcol-grp">'+g.r+'</span><span class="tcol-food">'+def.nome+'</span><span class="tcol-qtd">'+def.valor+' '+def.unidade+'</span>';
      if(g.itens.length>1){ html += '<span class="tcol-btn"><button class="sub-toggle" onclick="toggleSub(\''+key+'\')">'+ic(subOpen[key]?'chevronUp':'chevronDown',15)+'</button></span>'; }
      else { html += '<span class="tcol-btn"></span>'; }
      html += '</div>';
      if(subOpen[key]){
        html += '<div class="sub-panel">';
        g.itens.slice(1).forEach(it=>{ html += '<div class="sub-item">'+it.nome+' — '+it.valor+' '+it.unidade+' · ~'+it.kcal+'kcal</div>'; });
        html += '</div>';
      }
    });
    html += '</div>';
  });
  html += '<div class="card"><h3>Evitar</h3>';
  AVOID.forEach(a=>{ html += '<span class="avoid-tag">'+a+'</span>'; });
  html += '<p class="small" style="margin-top:10px;">Água: cerca de 35ml por kg de peso ao longo do dia.</p></div>';
  return html;
}
function toggleSub(key){ subOpen[key] = !subOpen[key]; renderHoje(); }
function setName(){ const v=document.getElementById('nameInput').value.trim(); if(!v) return; profile={name:v}; saveProfile(); renderHoje(); }

function toggleSuplemento(nome){
  const k=todayKey(); if(!suplementosLog[k]) suplementosLog[k]={};
  suplementosLog[k][nome] = !suplementosLog[k][nome];
  saveSuplementosLog(); renderHoje();
}
function renderMealCard(t, entry){
  const m=DIET[t]; const mi=MEAL_ICON[t]; const dkey=t.replace(':','');
  const isOpen=!!descOpen[t];
  const finalized = entry && ['fez','parcial','nao'].includes(entry.status);
  const supp = SUPPLEMENTS.find(s=>s.refeicao===t);
  const suppDone = supp && suplementosLog[todayKey()] && suplementosLog[todayKey()][supp.nome];

  if(finalized){
    const iconCls = entry.status==='fez'?'':(entry.status==='parcial'?'parcial':'nao');
    let foodsHtml = '';
    if(entry.status==='fez'){
      const nomes = m.grupos.map(g=>g.itens[0].nome+' ('+g.itens[0].valor+' '+g.itens[0].unidade+')');
      foodsHtml = '<p class="small" style="margin:6px 0 0 46px;">'+nomes.join(' · ')+'</p>';
    } else if(entry.status==='parcial' && entry.selecoes){
      const nomes = [];
      Object.keys(entry.selecoes).forEach(gi=>{
        const s = entry.selecoes[gi];
        if(s && s.ok){ const item=m.grupos[gi].itens[s.idx]; nomes.push(item.nome+' ('+s.valor+' '+s.unidade+')'); }
      });
      foodsHtml = nomes.length ? '<p class="small" style="margin:6px 0 0 46px;">'+nomes.join(' · ')+'</p>' : '';
    } else if(entry.status==='nao'){
      foodsHtml = '<p class="small" style="margin:6px 0 0 46px;">Nenhum alimento registrado nessa refeição.</p>';
    }
    return '<div class="meal-card done"><div class="done-row">'+
      '<div class="meal-icon sm" style="background:'+mi.bg+'; color:'+mi.c+';">'+ic(mi.i,16)+'</div>'+
      '<div class="meal-titles"><p class="mtitle" style="font-size:13px;">'+m.nome+'</p></div>'+
      '<span class="done-check '+iconCls+'">'+ic('check',13)+'</span>'+
      '<span class="edit-link" onclick="resetMeal(\''+t+'\')">alterar</span></div>'+foodsHtml+'</div>';
  }
  let carry='';
  if(entry && entry.carriedFrom){ carry = '<div class="carry-note"><span>'+ic('bell')+'</span><span>Trazido de '+entry.carriedFrom+': considere incluir também as opções dessa refeição aqui.</span></div>'; }
  let body='';
  if(!entry || !entry.status){
    body = '<div class="status-row">'+
      '<button class="status-btn" onclick="markFez(\''+t+'\')">'+ic('check')+' Fiz</button>'+
      '<button class="status-btn" onclick="openParcial(\''+t+'\')">'+ic('swap')+' Parcial</button>'+
      '<button class="status-btn" onclick="openNaoFez(\''+t+'\')">Não fiz</button></div>';
  } else if(entry.status==='parcial_editing'){ body = renderParcialEditor(t, entry); }
  else if(entry.status==='nao_pergunta'){
    body = '<p style="font-size:13px; margin:10px 0 6px;">Quer redistribuir essa refeição nas próximas?</p>'+
      '<div class="status-row"><button class="status-btn" onclick="confirmNaoFez(\''+t+'\', true)">Sim, redistribuir</button><button class="status-btn" onclick="confirmNaoFez(\''+t+'\', false)">Não</button></div>';
  }
  const rm = mealRefMacros(t);
  const suppHtml = supp ? '<div class="supp-tag"><span>'+ic('pill',14)+' '+supp.nome+', '+supp.quando.toLowerCase()+'</span><button class="supp-toggle'+(suppDone?' done':'')+'" onclick="toggleSuplemento(\''+supp.nome+'\')">'+ic('check',11)+' '+(suppDone?'tomado':'marcar')+'</button></div>' : '';
  return '<div class="meal-card"><div class="meal-head">'+
      '<div class="meal-icon" style="background:'+mi.bg+'; color:'+mi.c+';">'+ic(mi.i)+'</div>'+
      '<div class="meal-titles"><p class="mtitle">'+m.nome+'</p><p class="mtime">'+t+'</p></div>'+
      '<span class="kcal-badge">~'+mealRefKcal(t)+' kcal</span>'+
      '<button class="desc-toggle" onclick="toggleDesc(\''+t+'\')">'+ic(isOpen?'chevronUp':'chevronDown')+'</button></div>'+
    macroBarHTML(rm)+suppHtml+
    '<p class="mdesc'+(isOpen?' open':'')+'" id="desc-'+dkey+'">'+m.desc+'</p>'+carry+body+'</div>';
}
function toggleDesc(t){ descOpen[t]=!descOpen[t]; renderHoje(); }
function renderParcialEditor(t, entry){
  const m=DIET[t]; const sel=entry.selecoes || {}; let html='';
  m.grupos.forEach((g,gi)=>{
    const cur = sel[gi] || {idx:0, valor:g.itens[0].valor, unidade:g.itens[0].unidade, ok:false};
    const item=g.itens[cur.idx];
    html += '<div class="food-row"><div class="fname">'+ic('bowl',14)+' '+item.nome+'</div>'+
      '<div class="food-macro">~'+item.kcal+' kcal · P'+item.p+'g C'+item.c+'g G'+item.g+'g</div>'+
      '<div class="food-inline"><input type="text" inputmode="decimal" id="qtd-'+t.replace(':','')+'-'+gi+'" value="'+cur.valor+'"/>';
    if(item.tipo==='volume'){
      html += '<select id="uni-'+t.replace(':','')+'-'+gi+'" onchange="changeUnit(\''+t+'\','+gi+')">';
      Object.keys(VOL_UNITS).forEach(u=>{ html += '<option value="'+u+'"'+(u===cur.unidade?' selected':'')+'>'+u+'</option>'; });
      html += '</select>';
    } else { html += '<span class="small" style="min-width:60px;">'+item.unidade+'</span>'; }
    html += '<button class="mini-btn'+(cur.ok?' ok':'')+'" onclick="confirmFoodItem(\''+t+'\','+gi+')">'+ic('check')+'</button>'+
      '<button class="mini-btn" onclick="toggleSwap(\''+t+'\','+gi+')">'+ic('swap')+'</button></div>'+
      '<div id="swap-'+t.replace(':','')+'-'+gi+'"></div></div>';
  });
  html += '<button class="primary-btn" onclick="finishParcial(\''+t+'\')">'+ic('check')+' Concluir refeição parcial</button>';
  return html;
}
function openParcial(t){
  const reg=todayReg(); const m=DIET[t]; const selecoes={};
  m.grupos.forEach((g,gi)=>{ selecoes[gi]={idx:0, valor:g.itens[0].valor, unidade:g.itens[0].unidade, ok:false}; });
  reg[t]={status:'parcial_editing', selecoes}; saveRegistros(); renderHoje();
}
function toggleSwap(t, gi){
  const id='swap-'+t.replace(':','')+'-'+gi; const el=document.getElementById(id);
  if(el.innerHTML){ el.innerHTML=''; return; }
  const g=DIET[t].grupos[gi]; let html='<div class="swap-list">';
  g.itens.forEach((item,idx)=>{ html += '<button onclick="pickSwap(\''+t+'\','+gi+','+idx+')"><span>'+ic('swap',13)+' '+item.nome+'</span><span class="small">'+item.valor+' '+item.unidade+'</span></button>'; });
  html += '</div>'; el.innerHTML=html;
}
function pickSwap(t, gi, idx){
  const reg=todayReg(); const item=DIET[t].grupos[gi].itens[idx];
  reg[t].selecoes[gi]={idx:idx, valor:item.valor, unidade:item.unidade, ok:false};
  saveRegistros(); renderHoje();
}
function changeUnit(t, gi){
  const reg=todayReg(); const sel=reg[t].selecoes[gi];
  const newUnit=document.getElementById('uni-'+t.replace(':','')+'-'+gi).value;
  const curVal=parseFloat(document.getElementById('qtd-'+t.replace(':','')+'-'+gi).value)||sel.valor;
  sel.valor=convertVol(curVal, sel.unidade, newUnit); sel.unidade=newUnit;
  saveRegistros(); renderHoje();
}
function confirmFoodItem(t, gi){
  const reg=todayReg();
  const val=parseFloat(document.getElementById('qtd-'+t.replace(':','')+'-'+gi).value)||reg[t].selecoes[gi].valor;
  reg[t].selecoes[gi].valor=val; reg[t].selecoes[gi].ok=true;
  saveRegistros(); renderHoje();
}
async function finishParcial(t){ const reg=todayReg(); reg[t].status='parcial'; await saveRegistros(); renderHoje(); }
async function markFez(t){ const reg=todayReg(); reg[t]={status:'fez'}; await saveRegistros(); renderHoje(); }
function resetMeal(t){ const reg=todayReg(); delete reg[t]; saveRegistros(); renderHoje(); }
function openNaoFez(t){ const reg=todayReg(); reg[t]={status:'nao_pergunta'}; saveRegistros(); renderHoje(); }
async function confirmNaoFez(t, redistribuir){
  const reg=todayReg();
  if(redistribuir){
    const next=nextMealTime(t);
    if(next){ reg[next]=reg[next]||{}; reg[next].carriedFrom=DIET[t].nome; }
    reg[t]={status:'nao'};
  } else {
    reg[t]={status:'nao'};
    avisos.push({date:todayKey(), meal:t, dismissed:false});
    await saveAvisos();
  }
  await saveRegistros(); renderHoje();
}

// ---------- CHECK-IN detalhado (acessado via botão no Início) ----------
function abrirCheckin(){
  checkinFlowState='intro';
  document.getElementById('screen-inicio').classList.add('hidden');
  document.getElementById('screen-registrar').classList.remove('hidden');
  renderCheckinFlow();
}
function proximoCheckinData(){
  const dias = diasAteProximoCheckin();
  const d = new Date(); d.setDate(d.getDate()+dias);
  return d.toLocaleDateString('pt-BR');
}
function renderCheckinFlow(){
  const el=document.getElementById('screen-registrar');
  let html = '<button class="ghost-btn" style="margin-bottom:14px;" onclick="showScreen(\'inicio\')">'+ic('x',13)+' Fechar</button>';

  if(checkinFlowState==='intro'){
    const dias = diasAteProximoCheckin(); const due = dias===0;
    html += '<div class="card"><h3>'+ic('clip',15)+' Check-in semanal</h3>'+
      '<p class="small" style="margin-bottom:10px;">O check-in é o momento em que você conta para sua nutricionista como a semana foi de verdade, o que funcionou, o que pesou, e como está se sentindo. É esse retorno que permite ajustar o plano para que ele continue fazendo sentido.</p>'+
      '<p class="small" style="margin-bottom:10px;">Leva poucos minutos, e não existe resposta certa ou errada, quanto mais honesto, melhor o ajuste.</p>'+
      '<p style="font-size:13px; font-weight:600;">Prazo desta semana: '+proximoCheckinData()+(due?' (hoje)':'')+'</p>'+
      '<button class="primary-btn" onclick="iniciarRespostaCheckin()">'+ic('check')+' Responder agora</button></div>';
  } else if(checkinFlowState==='confirmar-antecipar'){
    html += '<div class="card"><h3>Responder antes do prazo?</h3>'+
      '<p class="small" style="margin-bottom:10px;">O prazo desse check-in é '+proximoCheckinData()+'. Você está respondendo antes disso. Quer mesmo antecipar agora?</p>'+
      '<div class="status-row"><button class="status-btn" onclick="checkinFlowState=\'perguntas\'; renderCheckinFlow();">Sim, quero responder agora</button><button class="status-btn" onclick="checkinFlowState=\'intro\'; renderCheckinFlow();">Não, prefiro esperar</button></div></div>';
  } else if(checkinFlowState==='perguntas'){
    html += renderCheckinPerguntas();
  } else if(checkinFlowState==='enviado'){
    html += '<div class="msg"><span>'+ic('leaf')+'</span><span>Check-in enviado. Obrigada por compartilhar com tantos detalhes, isso ajuda bastante a ajustar o plano para fazer mais sentido.</span></div>';
  }
  el.innerHTML = html;
}
function iniciarRespostaCheckin(){
  const dias = diasAteProximoCheckin();
  checkinFlowState = dias>0 ? 'confirmar-antecipar' : 'perguntas';
  renderCheckinFlow();
}
function calcularAderenciaSemana(){
  let fez=0, parcial=0, nao=0, total=0;
  for(let i=0;i<7;i++){
    const d=new Date(); d.setDate(d.getDate()-i);
    const reg=registros[dateKey(d)]; if(!reg) continue;
    OBRIGATORIAS.forEach(t=>{ if(reg[t]){ total++; if(reg[t].status==='fez') fez++; else if(reg[t].status==='parcial') parcial++; else if(reg[t].status==='nao') nao++; } });
  }
  const pct = total ? Math.round((fez/total)*100) : 0;
  const label = total===0 ? 'sem_registro' : (pct>=80 ? 'tranquila' : (pct>=50 ? 'desafios' : 'dificil'));
  return {fez,parcial,nao,total,pct,label};
}
function renderCheckinPerguntas(){
  const d = checkinDraft;
  const ad = calcularAderenciaSemana();
  const opt = (campo, valor, label) => '<button class="opt-btn'+(d[campo]===valor?' selected':'')+'" style="'+(d[campo]===valor?'background:var(--sage-bg); border-color:var(--sage-line);':'')+'" onclick="setDraft(\''+campo+'\',\''+valor+'\')">'+label+'</button>';
  let html = '<div class="card"><h3>'+ic('flame',15)+' Aderência da semana, calculada pelo app</h3>'+
    (ad.total===0 ? '<p class="small">Ainda não há registros suficientes essa semana.</p>' :
    '<div style="display:flex; gap:10px; margin:10px 0;">'+
      '<div style="flex:1; text-align:center;"><div style="font-size:18px; font-weight:700; color:var(--sage);">'+ad.fez+'</div><div class="small">feitas</div></div>'+
      '<div style="flex:1; text-align:center;"><div style="font-size:18px; font-weight:700; color:var(--orange);">'+ad.parcial+'</div><div class="small">parciais</div></div>'+
      '<div style="flex:1; text-align:center;"><div style="font-size:18px; font-weight:700; color:var(--ink-soft);">'+ad.nao+'</div><div class="small">não feitas</div></div></div>'+
    '<p class="small">'+ad.pct+'% das refeições principais registradas foram concluídas essa semana. Isso vai junto com o check-in.</p>')+
    '</div>';
  html += '<div class="card"><h3>Nos últimos dias, sentiu mais fome que o normal?</h3>'+
    opt('fome','sim','Sim')+opt('fome','as_vezes','Às vezes')+opt('fome','nao','Não')+'</div>';
  html += '<div class="card"><h3>O plano está fazendo sentido para sua rotina?</h3>'+
    opt('planoOk','sim','Sim, está encaixando bem')+opt('planoOk','parcial','Parcialmente')+opt('planoOk','nao','Não muito')+'</div>';
  html += '<div class="card"><h3>Como está seu sono essa semana?</h3>'+
    opt('sono','bem','Bem')+opt('sono','regular','Regular')+opt('sono','ruim','Ruim')+'</div>';
  html += '<div class="card"><h3>Como está seu nível de estresse?</h3>'+
    opt('estresse','baixo','Baixo')+opt('estresse','medio','Médio')+opt('estresse','alto','Alto')+'</div>';
  html += '<div class="card"><h3>Algo específico dificultou seguir o plano essa semana?</h3><textarea id="dificuldadeTxt" rows="3" placeholder="Opcional">'+(d.dificuldade||'')+'</textarea></div>';
  html += '<div class="card"><h3>Algo que funcionou bem e vale manter?</h3><textarea id="funcionouTxt" rows="3" placeholder="Opcional">'+(d.funcionouBem||'')+'</textarea></div>';
  html += '<div class="card"><h3>Comentário livre (opcional)</h3><textarea id="comentarioTxt" rows="3" placeholder="Qualquer outra coisa que queira contar">'+(d.comentario||'')+'</textarea></div>';
  html += '<button class="primary-btn" onclick="enviarCheckinDetalhado()">'+ic('check')+' Enviar check-in</button>'+
    '<button class="ghost-btn" onclick="salvarRascunhoCheckin()">Salvar e continuar depois</button>'+
    '<button class="ghost-btn" onclick="cancelarCheckin()">Cancelar</button>';
  return html;
}
function setDraft(campo, valor){ checkinDraft[campo]=valor; renderCheckinFlow(); }
function coletarTextos(){
  const dif=document.getElementById('dificuldadeTxt'); if(dif) checkinDraft.dificuldade=dif.value;
  const fun=document.getElementById('funcionouTxt'); if(fun) checkinDraft.funcionouBem=fun.value;
  const com=document.getElementById('comentarioTxt'); if(com) checkinDraft.comentario=com.value;
}
async function salvarRascunhoCheckin(){
  coletarTextos(); await saveCheckinDraft();
  document.getElementById('screen-registrar').innerHTML = '<div class="msg"><span>'+ic('clip')+'</span><span>Rascunho salvo. Você pode continuar de onde parou quando quiser, tocando em Check-in semanal novamente.</span></div>';
  setTimeout(()=>showScreen('inicio'), 1600);
}
async function cancelarCheckin(){
  checkinDraft={semana:'', comentario:'', fome:'', planoOk:'', sono:'', estresse:'', dificuldade:'', funcionouBem:''};
  await saveCheckinDraft();
  showScreen('inicio');
}
async function enviarCheckinDetalhado(){
  coletarTextos();
  checkinDraft.semana = calcularAderenciaSemana().label;
  checkins.push({date:new Date().toISOString(), ...checkinDraft});
  await saveCheckins();
  if(checkinDraft.fome==='sim'){
    const list = window._alertasFome||[];
    list.push({date:todayKey(), sentiuFome:true, origem:'checkin'});
    window._alertasFome=list; alertaFomeHoje={date:todayKey(), sentiuFome:true};
    await saveAlertasFome();
  }
  checkinDraft={semana:'', comentario:'', fome:'', planoOk:'', sono:'', estresse:'', dificuldade:'', funcionouBem:''};
  await saveCheckinDraft();
  checkinFlowState='enviado'; renderCheckinFlow();
  setTimeout(()=>showScreen('inicio'), 2000);
}

// ---------- PLANO DE AÇÃO ----------
function renderPlanoAcao(){
  const el=document.getElementById('screen-planoacao');
  let html = '<div class="card"><h3>'+ic('cal',14)+' Próxima consulta</h3>'+
    '<input type="date" id="consData" value="'+(consulta.data||'')+'" style="margin-bottom:8px;"/>'+
    '<input type="time" id="consHorario" value="'+(consulta.horario||'')+'" style="margin-bottom:8px;"/>'+
    '<button class="primary-btn" onclick="salvarConsulta()">'+ic('check')+' Salvar data e horário</button>';
  if(consulta.data){
    html += '<div style="margin-top:10px; display:flex; align-items:center; justify-content:space-between;">'+
      '<span class="status-pill '+(consulta.confirmada?'confirmada':'pendente')+'">'+(consulta.confirmada?'Confirmada':'Pendente de confirmação')+'</span>'+
      '<button class="mini-btn" onclick="toggleConfirmaConsulta()">'+(consulta.confirmada?'Desmarcar':'Confirmar presença')+'</button></div>';
  }
  html += '</div>';

  html += '<div class="card"><h3>'+ic('clip',14)+' Ações da semana</h3>'+
    '<div style="display:flex; gap:8px; margin-bottom:10px;"><input type="text" id="novaAcao" placeholder="Nova ação..."/><button class="mini-btn" onclick="addAcao()">'+ic('plus',14)+'</button></div>';
  if(!acoes.length){ html += '<p class="small">Nenhuma ação registrada ainda.</p>'; }
  acoes.forEach(a=>{
    html += '<div class="action-item"><button class="shop-check'+(a.feito?' done':'')+'" onclick="toggleAcao(\''+a.id+'\')">'+ic('check',13)+'</button>'+
      '<span class="shop-name'+(a.feito?' done':'')+'" style="flex:1;">'+a.texto+'</span>'+
      '<button class="event-del" onclick="delAcao(\''+a.id+'\')">'+ic('trash')+'</button></div>';
  });
  html += '</div>';

  html += '<div class="card"><h3>'+ic('bell',14)+' Alerta de adesão</h3>'+
    '<p class="small" style="margin-bottom:8px;">Depois de quantos dias sem manter o plano principal o app deve avisar sobre a necessidade de reajuste?</p>'+
    '<div style="display:flex; gap:8px; align-items:center;"><input type="number" id="limiteAlerta" value="'+configNutri.alertaDiasLimite+'" min="1" style="max-width:90px;"/><button class="mini-btn" onclick="salvarLimiteAlerta()">'+ic('check',13)+' salvar</button></div></div>';

  html += '<div class="card"><h3>'+ic('leaf',14)+' Ciclo menstrual</h3>'+
    '<p class="small" style="margin-bottom:8px;">Opcional. Se ativado, o app mostra observações gerais nos períodos menstrual e pré-menstrual.</p>'+
    '<div class="chip-row" style="margin-bottom:10px;"><span class="chip'+(ciclo.ativo?' sel':'')+'" onclick="toggleCiclo()">'+(ciclo.ativo?'Ativado':'Desativado, toque para ativar')+'</span></div>';
  if(ciclo.ativo){
    html += '<p class="small" style="margin-bottom:4px;">Data de início da última menstruação</p><input type="date" id="cicloData" value="'+(ciclo.dataUltima||'')+'" style="margin-bottom:8px;"/>'+
      '<p class="small" style="margin-bottom:4px;">Duração média do ciclo (dias)</p><input type="number" id="cicloDuracao" value="'+(ciclo.duracao||28)+'" style="margin-bottom:8px;"/>'+
      '<button class="primary-btn" onclick="salvarCiclo()">'+ic('check')+' Salvar ciclo</button>';
  }
  html += '</div>';
  el.innerHTML = html;
}
function salvarLimiteAlerta(){ configNutri.alertaDiasLimite = parseInt(document.getElementById('limiteAlerta').value)||12; saveConfigNutri(); renderPlanoAcao(); }
function toggleCiclo(){ ciclo.ativo = !ciclo.ativo; saveCiclo(); renderPlanoAcao(); }
function salvarCiclo(){
  ciclo.dataUltima = document.getElementById('cicloData').value;
  ciclo.duracao = parseInt(document.getElementById('cicloDuracao').value)||28;
  saveCiclo(); renderPlanoAcao();
}
function salvarConsulta(){
  consulta.data = document.getElementById('consData').value;
  consulta.horario = document.getElementById('consHorario').value;
  consulta.confirmada = false;
  saveConsulta(); renderPlanoAcao();
}
function toggleConfirmaConsulta(){ consulta.confirmada = !consulta.confirmada; saveConsulta(); renderPlanoAcao(); }
function addAcao(){
  const v=document.getElementById('novaAcao').value.trim(); if(!v) return;
  acoes.push({id:Date.now().toString(), texto:v, feito:false});
  saveAcoes(); renderPlanoAcao();
}
function toggleAcao(id){ const a=acoes.find(x=>x.id===id); if(a){ a.feito=!a.feito; saveAcoes(); renderPlanoAcao(); } }
function delAcao(id){ acoes=acoes.filter(x=>x.id!==id); saveAcoes(); renderPlanoAcao(); }

// ---------- APOIO ----------
const RETOMADA_MSGS = {
  "Fim de semana puxado": "Um fim de semana diferente não apaga a semana. A próxima refeição simples já é o próximo passo, não precisa ser nada especial.",
  "Evento social": "Aproveitar um evento faz parte. Quando puder, volte para a próxima refeição planejada, sem regra extra nenhuma.",
  "Correria de trabalho": "Nos dias corridos, o mínimo já ajuda: beber água e fazer a próxima refeição com o que estiver mais à mão do plano.",
  "Viagem": "Viagem tem seu próprio ritmo. Assim que puder, retome pelo café da manhã ou pela refeição mais próxima do horário normal.",
  "Perdi a motivação": "Motivação vai e volta, isso é normal. Não precisa recomeçar do zero, só a próxima escolha já conta."
};
function renderApoio(){
  const el=document.getElementById('screen-apoio');
  let html='<div class="card"><h3>O que está rolando</h3>';
  Object.keys(RETOMADA_MSGS).forEach(k=>{ html += '<button class="opt-btn" onclick="pickApoio(\''+k.replace(/'/g,"\\'")+'\')">'+ic('leaf',16)+' '+k+'</button>'; });
  html += '</div>'; el.innerHTML=html;
}
async function pickApoio(k){
  retomadas.push({date:new Date().toISOString(), situacao:k});
  await saveRetomadas();
  document.getElementById('screen-apoio').innerHTML = '<div class="msg"><span>'+ic('leaf')+'</span><span>'+RETOMADA_MSGS[k]+'</span></div><button class="ghost-btn" onclick="showScreen(\'inicio\')">Voltar para o início</button>';
}

// ---------- CALENDÁRIO ----------
const IMPACTO_OPCOES = ["Café da manhã","Almoço","Lanche da tarde","Jantar","Dia todo"];
function toggleImpacto(op){ const i=novoEventoImpacto.indexOf(op); if(i>=0) novoEventoImpacto.splice(i,1); else novoEventoImpacto.push(op); renderCalendario(); }
function switchCalView(v){ calView=v; calMonthOffset=0; renderCalendario(); }
function shiftMonth(delta){ calMonthOffset += delta; renderCalendario(); }
function renderCalendario(){
  const el=document.getElementById('screen-calendario');
  let html = '<div class="seg"><button class="'+(calView==='semana'?'active':'')+'" onclick="switchCalView(\'semana\')">Semana</button><button class="'+(calView==='mes'?'active':'')+'" onclick="switchCalView(\'mes\')">Mês</button></div>';
  html += (calView==='semana') ? renderCalSemana() : renderCalMes();
  html += '<div class="card"><h3>'+ic('plus',14)+' Novo evento</h3>'+
    '<input type="text" id="evTitulo" placeholder="Título (ex: aniversário, viagem)" style="margin-bottom:8px;"/>'+
    '<input type="date" id="evData" style="margin-bottom:8px;"/><input type="time" id="evHorario" style="margin-bottom:8px;"/>'+
    '<p class="small" style="margin-bottom:4px;">Pode afetar:</p><div class="chip-row">';
  IMPACTO_OPCOES.forEach(op=>{ html += '<span class="chip'+(novoEventoImpacto.includes(op)?' sel':'')+'" onclick="toggleImpacto(\''+op+'\')">'+op+'</span>'; });
  html += '</div><button class="primary-btn" onclick="addEvento()">'+ic('plus')+' Adicionar evento</button></div>';
  html += '<div class="card"><h3>'+ic('star',14)+' Seus eventos</h3>';
  if(!eventos.length){ html += '<p class="small">Nenhum evento registrado ainda.</p>'; }
  else {
    const ordenados=[...eventos].sort((a,b)=>a.data.localeCompare(b.data));
    const meses=["jan","fev","mar","abr","mai","jun","jul","ago","set","out","nov","dez"]; let lastMonth='';
    ordenados.forEach(ev=>{
      const d=new Date(ev.data+'T00:00:00'); const mk=d.getFullYear()+'-'+d.getMonth();
      if(mk!==lastMonth){ html += '<div class="month-label">'+meses[d.getMonth()]+' de '+d.getFullYear()+'</div>'; lastMonth=mk; }
      html += '<div class="event-item"><div class="event-date"><span class="dd">'+d.getDate()+'</span><span class="mm">'+meses[d.getMonth()]+'</span></div>'+
        '<div class="event-info"><div class="et">'+ev.titulo+'</div><div class="em">'+(ev.horario?ev.horario+' · ':'')+(ev.impacto&&ev.impacto.length?ev.impacto.join(', '):'sem impacto definido')+'</div></div>'+
        '<button class="event-del" onclick="delEvento(\''+ev.id+'\')">'+ic('trash')+'</button></div>';
    });
  }
  html += '</div>'; el.innerHTML = html;
}
function renderCalSemana(){
  const labels=['D','S','T','Q','Q','S','S'];
  const d=new Date(); const todayIdx=d.getDay();
  const start=new Date(d); start.setDate(d.getDate()-todayIdx);
  let html='<div class="week-row">';
  for(let i=0;i<7;i++){
    const day=new Date(start); day.setDate(start.getDate()+i);
    const evs=eventosNoDia(dateKey(day));
    html += '<div class="week-day'+(i===todayIdx?' today':'')+'"><span class="wl">'+labels[i]+'</span><span class="wn">'+day.getDate()+'</span>'+(evs.length?'<span class="we">'+evs[0].titulo.slice(0,10)+'</span>':'')+'</div>';
  }
  html += '</div>';
  const semEventos=[];
  for(let i=0;i<7;i++){ const day=new Date(start); day.setDate(start.getDate()+i); eventosNoDia(dateKey(day)).forEach(e=>semEventos.push(e)); }
  if(semEventos.length){
    html += '<div class="card"><h3>Eventos desta semana</h3>';
    semEventos.forEach(e=>{ html += '<p class="small">'+e.titulo+(e.horario?' às '+e.horario:'')+(e.impacto&&e.impacto.length?' — afeta: '+e.impacto.join(', '):'')+'</p>'; });
    html += '</div>';
  }
  return html;
}
function renderCalMes(){
  const base=new Date(); base.setMonth(base.getMonth()+calMonthOffset);
  const year=base.getFullYear(), month=base.getMonth();
  const meses=["Janeiro","Fevereiro","Março","Abril","Maio","Junho","Julho","Agosto","Setembro","Outubro","Novembro","Dezembro"];
  const firstDay=new Date(year,month,1).getDay(); const daysInMonth=new Date(year,month+1,0).getDate(); const today=new Date();
  let html = '<div class="card"><div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:10px;">'+
    '<button class="mini-btn" onclick="shiftMonth(-1)">‹</button><span style="font-size:14px; font-weight:600;">'+meses[month]+' '+year+'</span><button class="mini-btn" onclick="shiftMonth(1)">›</button></div>';
  html += '<div class="month-wd"><span>D</span><span>S</span><span>T</span><span>Q</span><span>Q</span><span>S</span><span>S</span></div><div class="month-grid">';
  for(let i=0;i<firstDay;i++){ html += '<div class="month-cell empty"></div>'; }
  for(let d=1; d<=daysInMonth; d++){
    const dObj=new Date(year,month,d); const dk=dateKey(dObj);
    const isToday = dObj.toDateString()===today.toDateString();
    const evs = eventosNoDia(dk);
    html += '<div class="month-cell'+(isToday?' today':'')+'">'+d+(evs.length?'<span class="evdot"></span>':'')+'</div>';
  }
  html += '</div></div>';
  const eventosDoMes = eventos.filter(e=>{ const d=new Date(e.data+'T00:00:00'); return d.getFullYear()===year && d.getMonth()===month; }).sort((a,b)=>a.data.localeCompare(b.data));
  if(eventosDoMes.length){
    html += '<div class="card"><h3>Eventos de '+meses[month]+'</h3>';
    eventosDoMes.forEach(e=>{ const d=new Date(e.data+'T00:00:00'); html += '<p class="small"><b>'+d.getDate()+'</b> · '+e.titulo+(e.horario?' às '+e.horario:'')+(e.impacto&&e.impacto.length?' — afeta: '+e.impacto.join(', '):'')+'</p>'; });
    html += '</div>';
  }
  return html;
}
async function addEvento(){
  const titulo=document.getElementById('evTitulo').value.trim();
  const data=document.getElementById('evData').value;
  const horario=document.getElementById('evHorario').value;
  if(!titulo || !data) return;
  eventos.push({id:Date.now().toString(), titulo, data, horario, impacto:[...novoEventoImpacto]});
  novoEventoImpacto=[]; await saveEventos(); renderCalendario();
}
async function delEvento(id){ eventos = eventos.filter(e=>e.id!==id); await saveEventos(); renderCalendario(); }

// ---------- COMPRAS ----------
function shoppingBaseItems(){
  const map={};
  mealTimes().forEach(t=>{ DIET[t].grupos.forEach(g=>{ const it=g.itens[0]; const key=it.nome+'|'+it.unidade; if(!map[key]) map[key]={nome:it.nome, unidade:it.unidade, diario:0}; map[key].diario += it.valor; }); });
  return Object.values(map);
}
function shoppingDays(){ if(compras.periodo==='personalizado') return parseInt(compras.diasPersonalizado)||7; return parseInt(compras.periodo)||7; }
function setPeriodo(p){ compras.periodo=p; saveCompras(); renderCompras(); }
function setDiasPersonalizado(){ compras.diasPersonalizado=parseInt(document.getElementById('diasPersInput').value)||7; saveCompras(); renderCompras(); }
function toggleComprado(key){ compras.comprados[key]=!compras.comprados[key]; saveCompras(); renderCompras(); }
function addSubstituicao(t, gi, idx){
  const item = DIET[t].grupos[gi].itens[idx]; const key='add_'+t+'_'+gi+'_'+idx;
  if(compras.itensAdicionados.find(a=>a.key===key)){ renderCompras(); return; }
  compras.itensAdicionados.push({key, nome:item.nome, unidade:item.unidade, diario:item.valor});
  saveCompras(); renderCompras();
}
function removeSubstituicao(key){ compras.itensAdicionados = compras.itensAdicionados.filter(a=>a.key!==key); delete compras.comprados[key]; saveCompras(); renderCompras(); }
function toggleComprasSub(t){ comprasSubOpen[t]=!comprasSubOpen[t]; renderCompras(); }
function renderCompras(){
  const el=document.getElementById('screen-compras');
  const days = shoppingDays();
  let html = '<div class="card"><h3>'+ic('cart',15)+' Período de compra</h3><div class="chip-row">';
  [['7','7 dias'],['15','15 dias'],['30','30 dias'],['personalizado','Personalizado']].forEach(([v,l])=>{ html += '<span class="chip'+(compras.periodo===v?' sel':'')+'" onclick="setPeriodo(\''+v+'\')">'+l+'</span>'; });
  html += '</div>';
  if(compras.periodo==='personalizado'){ html += '<div style="margin-top:10px; display:flex; gap:8px; align-items:center;"><input type="number" id="diasPersInput" value="'+(compras.diasPersonalizado||7)+'" min="1" style="max-width:90px;"/><button class="mini-btn" onclick="setDiasPersonalizado()">'+ic('check',13)+' aplicar</button></div>'; }
  html += '<p class="small" style="margin-top:8px;">Calculando para '+days+' dias.</p></div>';
  html += '<div class="card"><h3>Itens do plano</h3>';
  shoppingBaseItems().forEach(item=>{
    const key='base_'+item.nome; const total=Math.round(item.diario*days*10)/10; const done=!!compras.comprados[key];
    html += '<div class="shop-item"><button class="shop-check'+(done?' done':'')+'" onclick="toggleComprado(\''+key+'\')">'+ic('check',13)+'</button>'+
      '<span class="shop-name'+(done?' done':'')+'">'+item.nome+'</span><span class="shop-qtd">'+total+' '+item.unidade+'</span></div>';
  });
  html += '</div>';
  if(compras.itensAdicionados.length){
    html += '<div class="card"><h3>Substituições adicionadas</h3>';
    compras.itensAdicionados.forEach(item=>{
      const total=Math.round(item.diario*days*10)/10; const done=!!compras.comprados[item.key];
      html += '<div class="shop-item"><button class="shop-check'+(done?' done':'')+'" onclick="toggleComprado(\''+item.key+'\')">'+ic('check',13)+'</button>'+
        '<span class="shop-name'+(done?' done':'')+'">'+item.nome+'</span><span class="shop-qtd">'+total+' '+item.unidade+'</span>'+
        '<button class="event-del" onclick="removeSubstituicao(\''+item.key+'\')">'+ic('trash')+'</button></div>';
    });
    html += '</div>';
  }
  html += '<div class="card"><h3>'+ic('plus',14)+' Adicionar substituições à lista</h3><p class="small" style="margin-bottom:6px;">Inclua opções alternativas do plano, caso queira variar as compras.</p>';
  mealTimes().forEach(t=>{
    html += '<div style="margin-bottom:6px;"><button class="mini-btn" style="width:100%; justify-content:space-between;" onclick="toggleComprasSub(\''+t+'\')"><span>'+DIET[t].nome+'</span>'+ic(comprasSubOpen[t]?'chevronUp':'chevronDown',14)+'</button>';
    if(comprasSubOpen[t]){
      DIET[t].grupos.forEach((g,gi)=>{
        g.itens.slice(1).forEach((it,idxRel)=>{
          const idx=idxRel+1; const key='add_'+t+'_'+gi+'_'+idx; const already=compras.itensAdicionados.find(a=>a.key===key);
          html += '<div class="shop-item" style="padding:6px 0;"><span class="shop-name" style="font-size:12px;">'+it.nome+' <span class="small">('+it.valor+' '+it.unidade+'/dia)</span></span>'+
            '<button class="mini-btn'+(already?' ok':'')+'" onclick="addSubstituicao(\''+t+'\','+gi+','+idx+')">'+ic(already?'check':'plus',13)+'</button></div>';
        });
      });
    }
    html += '</div>';
  });
  html += '</div>'; el.innerHTML = html;
}

// ---------- REGISTRAR REFEIÇÃO (manual / foto / descrição com IA) ----------
function openRegistrar(){
  registrarState = {step:'choose', mode:null, imageBase64:null, mediaType:null, texto:'', refeicaoEscolhida:'', resultado:null, loading:false, error:null};
  document.getElementById('screen-inicio').classList.add('hidden');
  document.getElementById('screen-registrar').classList.remove('hidden');
  renderRegistrar();
}
function closeRegistrar(){ showScreen('inicio'); }
function renderRegistrar(){
  const el=document.getElementById('screen-registrar');
  let html = '<button class="ghost-btn" style="margin-bottom:14px;" onclick="closeRegistrar()">'+ic('x',13)+' Fechar</button>';

  if(registrarState.step==='choose'){
    html += '<div class="card"><h3>Como você quer registrar?</h3><div class="choice-row">'+
      '<button class="choice-btn" onclick="chooseMode(\'manual\')">'+ic('clip')+'<span class="small">Manual</span></button>'+
      '<button class="choice-btn" onclick="chooseMode(\'foto\')">'+ic('camera')+'<span class="small">Foto</span></button>'+
      '<button class="choice-btn" onclick="chooseMode(\'descricao\')">'+ic('edit')+'<span class="small">Descrição</span></button>'+
      '</div></div>';
  } else if(registrarState.step==='foto-input'){
    html += '<div class="card"><h3>Foto da refeição</h3>'+
      '<p class="small" style="margin-bottom:4px;">Qual refeição é essa?</p>'+
      renderSeletorRefeicao()+
      (registrarState.imageBase64 ? '<img class="img-preview" src="data:'+registrarState.mediaType+';base64,'+registrarState.imageBase64+'"/>' : '')+
      '<input type="file" accept="image/*" onchange="handleFotoInput(event)"/>'+
      (registrarState.imageBase64 ? '<button class="primary-btn" onclick="analisar()">'+ic('sparkle',15)+' Analisar foto</button>' : '')+
      '</div>';
  } else if(registrarState.step==='descricao-input'){
    html += '<div class="card"><h3>Descreva a refeição</h3>'+
      '<p class="small" style="margin-bottom:4px;">Qual refeição é essa?</p>'+
      renderSeletorRefeicao()+
      '<textarea id="descTexto" rows="4" placeholder="Ex: comi 2 ovos, uma fatia de pão integral e um pouco de mamão">'+registrarState.texto+'</textarea>'+
      '<button class="primary-btn" onclick="analisarDescricao()">'+ic('sparkle',15)+' Analisar descrição</button></div>';
  } else if(registrarState.step==='loading'){
    html += '<div class="card"><p style="text-align:center; font-size:14px;">'+ic('sparkle',18)+' Analisando...</p></div>';
  } else if(registrarState.step==='resultado'){
    html += renderResultadoIA();
  } else if(registrarState.step==='erro'){
    html += '<div class="card"><h3>Não consegui analisar</h3><p class="small">'+registrarState.error+'</p><button class="ghost-btn" onclick="chooseMode(registrarState.mode)">Tentar novamente</button><button class="ghost-btn" onclick="closeRegistrar(); showScreen(\'hoje\');">Registrar manualmente</button></div>';
  }
  el.innerHTML = html;
}
function chooseMode(mode){
  registrarState.mode = mode;
  if(mode==='manual'){ closeRegistrar(); showScreen('hoje'); hojeTab='registro'; return; }
  registrarState.step = mode==='foto' ? 'foto-input' : 'descricao-input';
  renderRegistrar();
}
function handleFotoInput(evt){
  const file = evt.target.files[0]; if(!file) return;
  const reader = new FileReader();
  reader.onload = function(){
    const result = reader.result;
    registrarState.mediaType = file.type;
    registrarState.imageBase64 = result.split(',')[1];
    renderRegistrar();
  };
  reader.readAsDataURL(file);
}
function renderSeletorRefeicao(){
  let html = '<select id="refeicaoHint" onchange="registrarState.refeicaoEscolhida=this.value" style="margin-bottom:10px; width:100%;">'+
    '<option value="">Deixar a IA identificar</option>';
  mealTimes().forEach(t=>{ html += '<option value="'+t+'"'+(registrarState.refeicaoEscolhida===t?' selected':'')+'>'+DIET[t].nome+' ('+t+')</option>'; });
  html += '</select>';
  return html;
}
function dietContextJSON(){
  return JSON.stringify(mealTimes().map(t=>({
    horario:t, nome:DIET[t].nome,
    grupos:DIET[t].grupos.map((g,gi)=>({grupoIndex:gi, categoria:g.r, opcoes:g.itens.map((it,ii)=>({itemIndex:ii, nome:it.nome, valorPadrao:it.valor, unidade:it.unidade}))}))
  })));
}
async function chamarIA(contentArr){
  let instructions = "Você identifica qual refeição do plano alimentar abaixo a pessoa provavelmente registrou. Plano em JSON: "+dietContextJSON()+
    ". Responda APENAS com um JSON válido, sem texto antes ou depois, sem markdown, no formato exato: "+
    '{"refeicao":"08:00","selecoes":[{"grupoIndex":0,"itemIndex":0,"valorEstimado":25}],"confianca":"alta","observacao":"texto curto"}. '+
    "Use grupoIndex e itemIndex exatamente como no plano fornecido, escolhendo o item mais parecido em cada grupo relevante à refeição identificada. Se não conseguir identificar com confiança, use confianca:\"baixa\".";
  if(registrarState.refeicaoEscolhida){
    instructions += ' A pessoa já indicou que esta refeição é "'+DIET[registrarState.refeicaoEscolhida].nome+'" ('+registrarState.refeicaoEscolhida+'). Use esse horário no campo "refeicao" da resposta.';
  }
  contentArr.push({type:"text", text:instructions});
  const response = await fetch("https://api.anthropic.com/v1/messages", {
    method:"POST", headers:{"Content-Type":"application/json"},
    body: JSON.stringify({ model:"claude-sonnet-4-6", max_tokens:1000, messages:[{role:"user", content:contentArr}] })
  });
  const data = await response.json();
  const textBlocks = (data.content||[]).filter(b=>b.type==='text').map(b=>b.text).join('\n');
  const clean = textBlocks.replace(/```json|```/g,'').trim();
  return JSON.parse(clean);
}
async function analisar(){
  registrarState.step='loading'; renderRegistrar();
  try{
    const contentArr = [{type:"image", source:{type:"base64", media_type:registrarState.mediaType, data:registrarState.imageBase64}}];
    const resultado = await chamarIA(contentArr);
    registrarState.resultado = resultado; registrarState.step='resultado'; renderRegistrar();
  } catch(e){
    registrarState.step='erro'; registrarState.error='Não foi possível interpretar a imagem agora. Você pode tentar de novo ou registrar manualmente.'; renderRegistrar();
  }
}
async function analisarDescricao(){
  registrarState.texto = document.getElementById('descTexto').value.trim();
  if(!registrarState.texto) return;
  registrarState.step='loading'; renderRegistrar();
  try{
    const contentArr = [{type:"text", text:"Descrição da pessoa: "+registrarState.texto}];
    const resultado = await chamarIA(contentArr);
    registrarState.resultado = resultado; registrarState.step='resultado'; renderRegistrar();
  } catch(e){
    registrarState.step='erro'; registrarState.error='Não foi possível interpretar a descrição agora. Você pode tentar de novo ou registrar manualmente.'; renderRegistrar();
  }
}
function renderResultadoIA(){
  const r = registrarState.resultado;
  if(!r || !r.refeicao || !DIET[r.refeicao]){
    return '<div class="card"><h3>Não ficou claro</h3><p class="small">Não consegui identificar a refeição com segurança. Prefere registrar manualmente?</p><button class="ghost-btn" onclick="closeRegistrar(); showScreen(\'hoje\');">Registrar manualmente</button></div>';
  }
  const m = DIET[r.refeicao];
  let html = '<div class="card"><h3>'+ic('sparkle',15)+' Sugestão da IA</h3>'+
    '<p class="small" style="margin-bottom:10px;">Confiança: '+(r.confianca||'média')+(r.observacao?' · '+r.observacao:'')+'</p>'+
    '<p class="small" style="margin-bottom:4px;">Refeição identificada (você pode corrigir):</p>'+
    '<select id="refeicaoCorrecao" onchange="corrigirRefeicaoIA(this.value)" style="margin-bottom:10px; width:100%;">';
  mealTimes().forEach(t=>{ html += '<option value="'+t+'"'+(t===r.refeicao?' selected':'')+'>'+DIET[t].nome+' ('+t+')</option>'; });
  html += '</select>';
  (r.selecoes||[]).forEach((s,i)=>{
    const g = m.grupos[s.grupoIndex]; if(!g) return;
    const item = g.itens[s.itemIndex]; if(!item) return;
    html += '<div class="food-row"><div class="fname">'+ic('bowl',14)+' '+item.nome+'</div>'+
      '<div class="food-inline"><input type="text" id="ia-qtd-'+i+'" value="'+(s.valorEstimado||item.valor)+'"/><span class="small">'+item.unidade+'</span></div></div>';
  });
  html += '<button class="primary-btn" onclick="confirmarResultadoIA()">'+ic('check')+' Confirmar registro</button>'+
    '<button class="ghost-btn" onclick="closeRegistrar(); showScreen(\'hoje\');">Prefiro ajustar manualmente</button></div>';
  return html;
}
function corrigirRefeicaoIA(novaRefeicao){
  const r = registrarState.resultado;
  r.refeicao = novaRefeicao;
  r.selecoes = DIET[novaRefeicao].grupos.map((g,gi)=>({grupoIndex:gi, itemIndex:0, valorEstimado:g.itens[0].valor}));
  renderRegistrar();
}
async function confirmarResultadoIA(){
  const r = registrarState.resultado; const t = r.refeicao;
  const reg = todayReg(); const selecoes = {};
  (r.selecoes||[]).forEach((s,i)=>{
    const val = parseFloat(document.getElementById('ia-qtd-'+i).value) || s.valorEstimado;
    selecoes[s.grupoIndex] = {idx:s.itemIndex, valor:val, unidade:DIET[t].grupos[s.grupoIndex].itens[s.itemIndex].unidade, ok:true};
  });
  reg[t] = {status:'parcial', selecoes};
  await saveRegistros();
  closeRegistrar();
  showScreen('hoje');
}

(async function init(){
  await loadData();
  if(!profile){ profile = {name:"Nathália"}; await saveProfile(); }
  showScreen('inicio');
})();
</script>
</body>
</html>
