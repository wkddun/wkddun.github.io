# wkddun.github.io
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<title>CogPhys — 인지·신체 평가</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700;900&family=JetBrains+Mono:wght@400;600;700&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
<style>
:root{
  --bg:#060b14;--s1:#0d1524;--s2:#121e32;--s3:#19283f;
  --b1:#1e2e47;--b2:#243552;
  --a1:#3ecfff;--a2:#8b5cf6;--a3:#10d98c;--a4:#f59e0b;--a5:#f43f5e;
  --t1:#f0f6ff;--t2:#94a3b8;--t3:#4a6080;
  --r:14px;--rm:10px;--rs:8px;
  --ff:'Noto Sans KR',sans-serif;--fm:'JetBrains Mono',monospace;
  --safe-bottom:env(safe-area-inset-bottom,0px);
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent;}
html,body{height:100%;background:var(--bg);color:var(--t1);font-family:var(--ff);overscroll-behavior:none;}
body{display:flex;flex-direction:column;}

/* ── SCROLLBAR ── */
::-webkit-scrollbar{width:4px;height:4px;}
::-webkit-scrollbar-track{background:transparent;}
::-webkit-scrollbar-thumb{background:var(--b2);border-radius:2px;}

/* ══════════════════════════════════
   BOTTOM NAV (mobile-first)
══════════════════════════════════ */
.bottom-nav{
  position:fixed;bottom:0;left:0;right:0;z-index:200;
  background:rgba(6,11,20,.95);backdrop-filter:blur(20px);
  border-top:1px solid var(--b1);
  display:flex;padding-bottom:var(--safe-bottom);
}
.bn-item{
  flex:1;display:flex;flex-direction:column;align-items:center;
  gap:3px;padding:10px 4px;cursor:pointer;transition:all .2s;
  border:none;background:none;color:var(--t3);font-family:var(--ff);
}
.bn-item.active{color:var(--a1);}
.bn-icon{font-size:22px;line-height:1;}
.bn-label{font-size:10px;font-weight:600;letter-spacing:.3px;}

/* ── MAIN ── */
main{flex:1;overflow-y:auto;padding-bottom:calc(70px + var(--safe-bottom));}

/* ── PAGES ── */
.page{display:none;padding:16px 16px 8px;max-width:720px;margin:0 auto;}
.page.active{display:block;}

/* ── HEADER BLOCK ── */
.page-header{padding:20px 0 16px;border-bottom:1px solid var(--b1);margin-bottom:20px;}
.page-header h1{font-size:22px;font-weight:900;letter-spacing:-.5px;}
.page-header p{font-size:13px;color:var(--t2);margin-top:4px;line-height:1.6;}

/* ── CARDS ── */
.card{background:var(--s1);border:1px solid var(--b1);border-radius:var(--r);padding:18px;margin-bottom:14px;}
.card-label{font-size:10px;font-family:var(--fm);text-transform:uppercase;letter-spacing:.8px;color:var(--t3);margin-bottom:14px;}

/* ── FORM ── */
.fg{display:flex;flex-direction:column;gap:6px;margin-bottom:12px;}
.fg label{font-size:11px;font-weight:700;color:var(--t2);text-transform:uppercase;letter-spacing:.5px;}
.fg input,.fg select{
  background:var(--s2);border:1.5px solid var(--b1);border-radius:var(--rs);
  padding:12px 14px;color:var(--t1);font-size:15px;font-family:var(--ff);
  transition:border .2s;outline:none;width:100%;
  -webkit-appearance:none;appearance:none;
}
.fg input:focus,.fg select:focus{border-color:var(--a1);box-shadow:0 0 0 3px rgba(62,207,255,.1);}
.fg select{background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath d='M1 1l5 5 5-5' stroke='%2394a3b8' stroke-width='1.5' fill='none' stroke-linecap='round'/%3E%3C/svg%3E");background-repeat:no-repeat;background-position:right 14px center;padding-right:36px;}
.form-row{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
.form-row3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px;}

/* ── BMI GRID ── */
.bmi-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:8px;}
.bmi-tile{background:var(--s2);border:1px solid var(--b1);border-radius:var(--rs);padding:12px 14px;}
.bmi-tile .tl{font-size:10px;font-family:var(--fm);color:var(--t3);text-transform:uppercase;letter-spacing:.5px;margin-bottom:4px;}
.bmi-tile .tv{font-size:20px;font-weight:700;font-family:var(--fm);}
.bmi-tile .ts{font-size:11px;color:var(--t2);margin-top:2px;}
.tv.ok{color:var(--a3)}.tv.warn{color:var(--a4)}.tv.bad{color:var(--a5)}

/* ── BUTTONS ── */
.btn{display:inline-flex;align-items:center;justify-content:center;gap:8px;padding:13px 20px;border-radius:var(--rs);font-size:14px;font-weight:700;cursor:pointer;transition:all .18s;border:none;font-family:var(--ff);width:100%;margin-top:4px;}
.btn+.btn{margin-top:8px;}
.btn-row{display:flex;gap:8px;}
.btn-row .btn{width:auto;flex:1;}
.btn-p{background:var(--a1);color:#06070d;}
.btn-p:hover,.btn-p:active{filter:brightness(1.08);}
.btn-s{background:var(--s2);color:var(--t1);border:1.5px solid var(--b2);}
.btn-s:hover,.btn-s:active{border-color:var(--a1);color:var(--a1);}
.btn-d{background:rgba(244,63,94,.12);color:var(--a5);border:1.5px solid rgba(244,63,94,.25);}
.btn-g{background:rgba(16,217,140,.12);color:var(--a3);border:1.5px solid rgba(16,217,140,.25);}
.btn-v{background:rgba(139,92,246,.12);color:var(--a2);border:1.5px solid rgba(139,92,246,.25);}
.btn-y{background:rgba(245,158,11,.12);color:var(--a4);border:1.5px solid rgba(245,158,11,.25);}
.btn-sm{padding:8px 14px;font-size:12px;width:auto;}

/* ── SUBJECT LIST ── */
.subj-card{background:var(--s1);border:1.5px solid var(--b1);border-radius:var(--r);padding:14px 16px;margin-bottom:10px;cursor:pointer;transition:all .2s;}
.subj-card.sel{border-color:var(--a1);background:rgba(62,207,255,.05);}
.subj-card:active{transform:scale(.99);}
.subj-top{display:flex;align-items:center;gap:10px;margin-bottom:8px;}
.subj-id{font-family:var(--fm);font-size:12px;color:var(--a1);font-weight:700;background:rgba(62,207,255,.1);padding:3px 8px;border-radius:4px;}
.subj-name{font-size:15px;font-weight:700;}
.subj-age{font-size:12px;color:var(--t2);margin-left:auto;}
.subj-chips{display:flex;gap:6px;flex-wrap:wrap;}
.chip{font-size:11px;font-family:var(--fm);padding:3px 8px;border-radius:4px;}
.ch-1{background:rgba(62,207,255,.12);color:var(--a1);}
.ch-2{background:rgba(139,92,246,.12);color:var(--a2);}
.ch-3{background:rgba(16,217,140,.12);color:var(--a3);}
.ch-n{background:var(--s2);color:var(--t3);}

/* ── TEST SELECTOR ── */
.test-btn{background:var(--s1);border:1.5px solid var(--b1);border-radius:var(--r);padding:18px;cursor:pointer;transition:all .2s;text-align:left;margin-bottom:10px;width:100%;font-family:var(--ff);}
.test-btn:active{transform:scale(.98);}
.test-btn.tb-1:hover,.test-btn.tb-1:focus{border-color:var(--a1);}
.test-btn.tb-2:hover,.test-btn.tb-2:focus{border-color:var(--a2);}
.test-btn.tb-3:hover,.test-btn.tb-3:focus{border-color:var(--a3);}
.tb-icon{font-size:28px;margin-bottom:8px;}
.tb-title{font-size:16px;font-weight:800;color:var(--t1);margin-bottom:4px;}
.tb-sub{font-size:12px;color:var(--t2);}
.tb-badge{display:inline-block;margin-top:8px;font-size:10px;font-family:var(--fm);padding:3px 8px;border-radius:4px;}

/* ── TEST CONTAINER ── */
.test-wrap{background:var(--s1);border:1px solid var(--b1);border-radius:var(--r);padding:18px;}
.test-head{margin-bottom:20px;}
.test-head h2{font-size:19px;font-weight:900;}
.test-head p{font-size:12px;color:var(--t2);margin-top:4px;}
.test-subj-info{background:var(--s2);border-radius:var(--rs);padding:10px 14px;font-size:12px;color:var(--t2);margin-bottom:18px;display:flex;align-items:center;gap:8px;}
.test-subj-info b{color:var(--a1);}

/* MoCA */
.moca-sec{border:1px solid var(--b1);border-radius:var(--rs);padding:14px;margin-bottom:10px;}
.moca-sec-title{font-size:11px;font-family:var(--fm);color:var(--a1);text-transform:uppercase;letter-spacing:.6px;display:flex;justify-content:space-between;margin-bottom:12px;}
.moca-item{display:flex;align-items:center;gap:8px;padding:8px 0;border-bottom:1px solid var(--b1);}
.moca-item:last-child{border-bottom:none;padding-bottom:0;}
.moca-q{flex:1;font-size:13px;line-height:1.5;color:var(--t1);}
.moca-btns{display:flex;gap:4px;}
.sb{width:36px;height:36px;border-radius:6px;border:1.5px solid var(--b1);background:var(--s2);color:var(--t2);font-size:13px;font-weight:700;cursor:pointer;transition:all .15s;font-family:var(--fm);}
.sb.on{background:var(--a1);color:#06070d;border-color:var(--a1);}
.sb:active{transform:scale(.93);}
.moca-total-row{display:flex;align-items:center;justify-content:space-between;padding-top:14px;border-top:1px solid var(--b1);margin-top:4px;}
.moca-total-label{font-size:13px;color:var(--t2);}
.moca-total-val{font-size:28px;font-weight:900;font-family:var(--fm);color:var(--a1);}

/* TUG */
.timer-big{text-align:center;padding:20px 0;}
.timer-num{font-size:72px;font-weight:900;font-family:var(--fm);color:var(--a2);letter-spacing:-2px;line-height:1;}
.timer-num.run{animation:tp 1s infinite;}
@keyframes tp{0%,100%{opacity:1}50%{opacity:.5}}
.timer-label{font-size:13px;color:var(--t2);margin-top:8px;}
.tug-ref-table{width:100%;border-collapse:collapse;font-size:12px;margin-top:10px;}
.tug-ref-table th,.tug-ref-table td{padding:8px 10px;border-bottom:1px solid var(--b1);text-align:center;font-family:var(--fm);}
.tug-ref-table th{color:var(--t3);font-size:10px;text-transform:uppercase;letter-spacing:.4px;}
.tug-ref-table td:first-child{text-align:left;color:var(--t2);font-family:var(--ff);}

/* N-back */
.nb-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;max-width:280px;margin:0 auto 18px;}
.nb-cell{aspect-ratio:1;border-radius:10px;background:var(--s2);border:2px solid var(--b1);transition:all .12s;}
.nb-cell.lit{background:var(--a2);border-color:var(--a2);box-shadow:0 0 20px rgba(139,92,246,.5);}
.nb-cell.hit{background:var(--a3);border-color:var(--a3);box-shadow:0 0 20px rgba(16,217,140,.5);}
.nb-stat-row{display:flex;justify-content:space-around;background:var(--s2);border-radius:var(--rs);padding:12px;margin-bottom:16px;font-size:12px;}
.nb-stat-row span{text-align:center;}
.nb-stat-row .sv{font-size:18px;font-weight:700;font-family:var(--fm);display:block;}
.nb-stat-row .sk{font-size:10px;color:var(--t3);text-transform:uppercase;letter-spacing:.4px;}
.nb-level-row{display:flex;gap:8px;margin-bottom:16px;}
.nb-level-row .btn{font-size:12px;padding:10px;}
.nb-match-btn{font-size:18px;padding:18px;border-radius:14px;background:var(--s2);border:2px solid var(--b2);color:var(--t1);width:100%;cursor:pointer;font-family:var(--ff);font-weight:700;transition:all .15s;}
.nb-match-btn:active{transform:scale(.97);background:rgba(16,217,140,.2);border-color:var(--a3);}
.nb-match-btn:disabled{opacity:.35;}
.nb-feedback{text-align:center;min-height:24px;font-size:14px;font-weight:700;margin:8px 0;}

/* ── HISTORY ── */
.hist-session{background:var(--s1);border:1px solid var(--b1);border-radius:var(--r);margin-bottom:10px;overflow:hidden;}
.hist-session-head{padding:14px 16px;cursor:pointer;display:flex;align-items:center;gap:10px;}
.hist-session-head:active{background:var(--s2);}
.hs-date{font-family:var(--fm);font-size:12px;color:var(--a1);}
.hs-round{font-size:10px;font-family:var(--fm);background:rgba(62,207,255,.1);color:var(--a1);padding:2px 7px;border-radius:4px;}
.hs-arrow{margin-left:auto;color:var(--t3);transition:transform .2s;}
.hs-arrow.open{transform:rotate(180deg);}
.hist-session-body{display:none;border-top:1px solid var(--b1);}
.hist-session-body.open{display:block;}
.hist-row{display:flex;align-items:center;padding:10px 16px;border-bottom:1px solid var(--b1);font-size:13px;}
.hist-row:last-child{border-bottom:none;}
.hist-row-key{color:var(--t2);flex:1;}
.hist-row-val{font-family:var(--fm);font-weight:700;color:var(--t1);}
.hist-row-interp{font-size:11px;margin-left:8px;padding:2px 6px;border-radius:4px;}

/* ── COMPARE TABLE ── */
.compare-wrap{overflow-x:auto;-webkit-overflow-scrolling:touch;}
.compare-table{width:100%;border-collapse:collapse;font-size:12px;min-width:500px;}
.compare-table th{padding:10px 12px;font-size:10px;font-family:var(--fm);color:var(--t3);text-transform:uppercase;letter-spacing:.4px;border-bottom:1px solid var(--b1);text-align:center;white-space:nowrap;}
.compare-table th:first-child{text-align:left;}
.compare-table td{padding:10px 12px;border-bottom:1px solid var(--b1);text-align:center;font-family:var(--fm);}
.compare-table td:first-child{text-align:left;font-family:var(--ff);color:var(--t2);}
.compare-table tr:last-child td{border-bottom:none;}
.diff-up{color:var(--a3);}
.diff-down{color:var(--a5);}
.diff-same{color:var(--t3);}

/* ── RESULTS ── */
.score-trio{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-bottom:16px;}
.score-tile{background:var(--s1);border:1px solid var(--b1);border-radius:var(--rm);padding:14px 10px;text-align:center;}
.st-label{font-size:9px;font-family:var(--fm);text-transform:uppercase;letter-spacing:.6px;color:var(--t3);margin-bottom:6px;}
.st-val{font-size:28px;font-weight:900;font-family:var(--fm);line-height:1;}
.st-unit{font-size:10px;color:var(--t3);margin-top:2px;}
.st-badge{font-size:10px;font-weight:700;padding:3px 8px;border-radius:10px;margin-top:6px;display:inline-block;}

/* ── EMPTY ── */
.empty{text-align:center;padding:40px 20px;color:var(--t3);}
.empty .ei{font-size:40px;margin-bottom:10px;}
.empty p{font-size:13px;}

/* ── TOAST ── */
.toast{position:fixed;bottom:calc(76px + var(--safe-bottom) + 10px);left:50%;transform:translateX(-50%) translateY(20px);background:var(--s1);border:1px solid var(--b1);border-radius:10px;padding:11px 18px;font-size:13px;font-weight:600;z-index:999;opacity:0;transition:all .25s;white-space:nowrap;box-shadow:0 8px 30px rgba(0,0,0,.5);pointer-events:none;}
.toast.show{opacity:1;transform:translateX(-50%) translateY(0);}

/* ── MODAL ── */
.modal-bg{position:fixed;inset:0;background:rgba(0,0,0,.7);backdrop-filter:blur(6px);z-index:300;display:none;align-items:flex-end;justify-content:center;}
.modal-bg.open{display:flex;}
.modal{background:var(--s1);border:1px solid var(--b1);border-radius:20px 20px 0 0;padding:20px 16px calc(20px + var(--safe-bottom));width:100%;max-height:90vh;overflow-y:auto;animation:slideUp .25s ease;}
@keyframes slideUp{from{transform:translateY(100%)}to{transform:translateY(0)}}
.modal h3{font-size:17px;font-weight:800;margin-bottom:16px;}
.modal-handle{width:40px;height:4px;background:var(--b2);border-radius:2px;margin:0 auto 16px;}

/* ── DESKTOP TWEAKS ── */
@media(min-width:600px){
  .page{padding:24px 24px 8px;}
  .bmi-grid{grid-template-columns:repeat(4,1fr);}
  .form-row3{grid-template-columns:repeat(4,1fr);}
  .score-trio{gap:12px;}
  .st-val{font-size:36px;}
  .bottom-nav{max-width:720px;left:50%;transform:translateX(-50%);border-radius:16px 16px 0 0;border-left:1px solid var(--b1);border-right:1px solid var(--b1);}
  .modal-bg{align-items:center;}
  .modal{border-radius:20px;max-width:600px;padding-bottom:20px;}
  @keyframes slideUp{from{opacity:0;transform:translateY(20px)}to{opacity:1;transform:translateY(0)}}
  .timer-num{font-size:96px;}
}
@media(min-width:900px){.bmi-grid{grid-template-columns:repeat(4,1fr);}}
</style>
</head>
<body>

<main>

<!-- ══ HOME ══ -->
<div class="page active" id="p-home">
  <div style="text-align:center;padding:32px 0 24px;">
    <div style="font-size:44px;margin-bottom:12px;">🧠</div>
    <h1 style="font-size:26px;font-weight:900;letter-spacing:-.5px;">CogPhys</h1>
    <p style="font-size:13px;color:var(--t2);margin-top:6px;line-height:1.8;">인지·신체 기능 통합 평가 시스템<br>MoCA · TUG · N-back</p>
    <div id="selBadge" style="display:inline-block;margin-top:12px;font-size:12px;font-family:var(--fm);background:var(--s2);border:1px solid var(--b1);padding:5px 14px;border-radius:20px;color:var(--t2);">피험자 미선택</div>
  </div>
  <div class="card" style="margin-bottom:12px;">
    <div class="card-label">빠른 시작</div>
    <button class="test-btn tb-1" onclick="goPage('register')">
      <div class="tb-icon">👤</div>
      <div class="tb-title">피험자 등록</div>
      <div class="tb-sub">기본 정보 · BMI · 신체 계측</div>
      <span class="tb-badge" style="background:rgba(62,207,255,.1);color:var(--a1)">먼저 등록</span>
    </button>
    <button class="test-btn tb-1" onclick="goPage('tests')">
      <div class="tb-icon">📋</div>
      <div class="tb-title">검사 실시</div>
      <div class="tb-sub">MoCA · TUG · N-back</div>
      <span class="tb-badge" style="background:rgba(62,207,255,.1);color:var(--a1)">3종 검사</span>
    </button>
    <button class="test-btn tb-2" onclick="goPage('history')">
      <div class="tb-icon">📈</div>
      <div class="tb-title">검사 기록 · 전후 비교</div>
      <div class="tb-sub">회차별 기록 · 변화 추이</div>
      <span class="tb-badge" style="background:rgba(139,92,246,.1);color:var(--a2)">히스토리</span>
    </button>
    <button class="test-btn tb-3" onclick="exportExcel()">
      <div class="tb-icon">📊</div>
      <div class="tb-title">엑셀 내보내기</div>
      <div class="tb-sub">전체 데이터 .xlsx 다운로드</div>
      <span class="tb-badge" style="background:rgba(16,217,140,.1);color:var(--a3)">Excel</span>
    </button>
  </div>
  <div style="text-align:center;font-size:11px;color:var(--t3);padding-bottom:12px;">데이터는 이 기기에만 저장됩니다.</div>
</div>

<!-- ══ REGISTER ══ -->
<div class="page" id="p-register">
  <div class="page-header">
    <h1>피험자 등록</h1>
    <p>기본 정보를 입력하면 신체 지수가 자동 계산됩니다.</p>
  </div>

  <div class="card">
    <div class="card-label">기본 정보</div>
    <div class="form-row">
      <div class="fg"><label>ID</label><input id="fi-id" type="text" placeholder="PT-001"></div>
      <div class="fg"><label>이름</label><input id="fi-name" type="text" placeholder="홍길동"></div>
    </div>
    <div class="form-row">
      <div class="fg"><label>나이 (세)</label><input id="fi-age" type="number" placeholder="65" min="1" max="120" inputmode="numeric"></div>
      <div class="fg"><label>성별</label>
        <select id="fi-gender"><option value="">선택</option><option value="M">남성</option><option value="F">여성</option></select>
      </div>
    </div>
    <div class="form-row">
      <div class="fg"><label>키 (cm)</label><input id="fi-h" type="number" placeholder="168" oninput="calcBMI()" inputmode="decimal"></div>
      <div class="fg"><label>체중 (kg)</label><input id="fi-w" type="number" placeholder="65" oninput="calcBMI()" inputmode="decimal"></div>
    </div>
    <div class="form-row">
      <div class="fg"><label>교육연수 (년)</label><input id="fi-edu" type="number" placeholder="12" inputmode="numeric"></div>
      <div class="fg"><label>검사일</label><input id="fi-date" type="date"></div>
    </div>
  </div>

  <div class="card">
    <div class="card-label">📊 신체 계측 지수 (자동)</div>
    <div class="bmi-grid" id="bmiGrid">
      <div class="bmi-tile"><div class="tl">BMI</div><div class="tv" id="bv-bmi">—</div><div class="ts">체질량지수</div></div>
      <div class="bmi-tile"><div class="tl">분류</div><div class="tv" id="bv-cls" style="font-size:15px;margin-top:2px">—</div><div class="ts">WHO 기준</div></div>
      <div class="bmi-tile"><div class="tl">표준체중</div><div class="tv" id="bv-ideal" style="font-size:16px">—</div><div class="ts">Broca 변법</div></div>
      <div class="bmi-tile"><div class="tl">비만도</div><div class="tv" id="bv-ob" style="font-size:16px">—</div><div class="ts">실제/표준 %</div></div>
      <div class="bmi-tile"><div class="tl">체표면적</div><div class="tv" id="bv-bsa" style="font-size:16px">—</div><div class="ts">BSA (m²)</div></div>
      <div class="bmi-tile"><div class="tl">연령군</div><div class="tv" id="bv-ag" style="font-size:14px;margin-top:2px">—</div><div class="ts">기능평가 기준</div></div>
    </div>
  </div>

  <div class="btn-row">
    <button class="btn btn-p" onclick="saveSubject()">✅ 등록 완료</button>
    <button class="btn btn-s" onclick="clearReg()">↺</button>
  </div>

  <div style="height:14px"></div>
  <div class="card">
    <div class="card-label" style="margin-bottom:12px">등록된 피험자</div>
    <div id="subjList"><div class="empty"><div class="ei">👤</div><p>등록된 피험자 없음</p></div></div>
  </div>
</div>

<!-- ══ TESTS ══ -->
<div class="page" id="p-tests">
  <div class="page-header">
    <h1>검사 실시</h1>
    <p>피험자 선택 후 검사를 시작하세요.</p>
  </div>
  <div id="testSubjPicker" style="margin-bottom:14px"></div>
  <div id="testSelector"></div>
  <div id="testArea"></div>
</div>

<!-- ══ HISTORY ══ -->
<div class="page" id="p-history">
  <div class="page-header">
    <h1>검사 기록</h1>
    <p>피험자별 회차 기록과 전후 비교</p>
  </div>
  <div id="histSubjPicker" style="margin-bottom:14px"></div>
  <div id="histArea"></div>
</div>

<!-- ══ RESULTS ══ -->
<div class="page" id="p-results">
  <div class="page-header">
    <h1>결과 조회</h1>
    <p>최신 검사 결과 및 종합 해석</p>
  </div>
  <div id="resSubjPicker" style="margin-bottom:14px"></div>
  <div id="resArea"></div>
</div>

</main>

<!-- BOTTOM NAV -->
<nav class="bottom-nav">
  <button class="bn-item active" id="bn-home" onclick="goPage('home')"><span class="bn-icon">🏠</span><span class="bn-label">홈</span></button>
  <button class="bn-item" id="bn-register" onclick="goPage('register')"><span class="bn-icon">👤</span><span class="bn-label">등록</span></button>
  <button class="bn-item" id="bn-tests" onclick="goPage('tests')"><span class="bn-icon">📋</span><span class="bn-label">검사</span></button>
  <button class="bn-item" id="bn-history" onclick="goPage('history')"><span class="bn-icon">📈</span><span class="bn-label">기록</span></button>
  <button class="bn-item" id="bn-results" onclick="goPage('results')"><span class="bn-icon">📊</span><span class="bn-label">결과</span></button>
</nav>

<div class="toast" id="toast"></div>

<script>
// ═══════════════════════════════════
//  STORE  — subjects + sessions
// ═══════════════════════════════════
let DB = JSON.parse(localStorage.getItem('cogphys_v2') || 'null') || { subjects: [], sessions: [] };
let selId = null; // selected subject id

function saveDB(){ localStorage.setItem('cogphys_v2', JSON.stringify(DB)); }
function getSub(id){ return DB.subjects.find(s=>s.id===id); }
function getSessions(id){ return DB.sessions.filter(s=>s.subjectId===id).sort((a,b)=>new Date(b.date)-new Date(a.date)); }
function getLatestSession(id){ const arr=getSessions(id); return arr[0]||null; }

// ═══════════════════════════════════
//  NAV
// ═══════════════════════════════════
function goPage(name){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.bn-item').forEach(b=>b.classList.remove('active'));
  document.getElementById('p-'+name).classList.add('active');
  document.getElementById('bn-'+name).classList.add('active');
  if(name==='register') renderSubjList();
  if(name==='tests'){ renderTestSubjPicker(); renderTestSelector(); document.getElementById('testArea').innerHTML=''; }
  if(name==='history'){ renderHistSubjPicker(); renderHist(); }
  if(name==='results'){ renderResSubjPicker(); renderRes(); }
  window.scrollTo(0,0);
}

// ═══════════════════════════════════
//  BMI
// ═══════════════════════════════════
document.getElementById('fi-date').value = new Date().toISOString().split('T')[0];

function calcBMI(){
  const h=parseFloat(document.getElementById('fi-h').value);
  const w=parseFloat(document.getElementById('fi-w').value);
  const age=parseInt(document.getElementById('fi-age').value)||0;
  if(!h||!w) return;
  const bmi=(w/((h/100)**2)).toFixed(1);
  let cls='',c='';
  if(bmi<18.5){cls='저체중';c='warn';}else if(bmi<23){cls='정상';c='ok';}else if(bmi<25){cls='과체중';c='warn';}else if(bmi<30){cls='비만1';c='bad';}else{cls='비만2+';c='bad';}
  const ideal=(h-100)*0.9;
  const ob=((w/ideal)*100).toFixed(1);
  const bsa=(0.007184*Math.pow(h,0.725)*Math.pow(w,0.425)).toFixed(2);
  const ag=age<40?'성인':age<65?'중장년':age<75?'초기 노인':'후기 노인';
  set('bv-bmi',bmi,c); set('bv-cls',cls,c);
  document.getElementById('bv-ideal').textContent=ideal.toFixed(1)+' kg';
  document.getElementById('bv-ob').textContent=ob+'%';
  document.getElementById('bv-bsa').textContent=bsa+' m²';
  document.getElementById('bv-ag').textContent=ag;
}
function set(id,v,c){ const el=document.getElementById(id); el.textContent=v; el.className='tv '+(c||''); }

// ═══════════════════════════════════
//  REGISTER
// ═══════════════════════════════════
function saveSubject(){
  const id=v('fi-id'),name=v('fi-name'),age=parseInt(v('fi-age')),gender=v('fi-gender');
  const h=parseFloat(v('fi-h')),w=parseFloat(v('fi-w'));
  const edu=parseInt(v('fi-edu'))||0,date=v('fi-date');
  if(!id||!name||!age||!h||!w){ toast('⚠️ 필수 정보를 입력하세요'); return; }
  if(DB.subjects.find(s=>s.id===id)){ toast('⚠️ 이미 존재하는 ID'); return; }
  const bmi=(w/((h/100)**2)).toFixed(1);
  DB.subjects.push({id,name,age,gender,height:h,weight:w,edu,date,bmi});
  saveDB(); renderSubjList(); clearReg();
  toast('✅ '+name+' 등록 완료');
}
function v(id){ return document.getElementById(id).value.trim(); }
function clearReg(){
  ['fi-id','fi-name','fi-age','fi-h','fi-w','fi-edu'].forEach(i=>document.getElementById(i).value='');
  document.getElementById('fi-gender').value='';
  document.getElementById('fi-date').value=new Date().toISOString().split('T')[0];
  ['bv-bmi','bv-cls','bv-ideal','bv-ob','bv-bsa','bv-ag'].forEach(id=>{ document.getElementById(id).textContent='—'; document.getElementById(id).className='tv'; });
}
function delSubject(id,e){
  e.stopPropagation();
  if(!confirm('삭제하시겠습니까?')) return;
  DB.subjects=DB.subjects.filter(s=>s.id!==id);
  DB.sessions=DB.sessions.filter(s=>s.subjectId!==id);
  if(selId===id){ selId=null; updateBadge(); }
  saveDB(); renderSubjList(); toast('🗑 삭제 완료');
}
function selectSubj(id){
  selId=id; updateBadge();
  renderSubjList();
  renderTestSubjPicker();
  renderHistSubjPicker();
  renderResSubjPicker();
  toast('👤 '+getSub(id).name+' 선택');
}
function updateBadge(){
  const s=selId?getSub(selId):null;
  document.getElementById('selBadge').textContent=s?s.name+' ('+s.id+')':'피험자 미선택';
}
function renderSubjList(){
  const el=document.getElementById('subjList');
  if(!DB.subjects.length){ el.innerHTML='<div class="empty"><div class="ei">👤</div><p>없음</p></div>'; return; }
  el.innerHTML=DB.subjects.map(s=>{
    const ls=getLatestSession(s.id);
    const moca=ls?.moca!=null?`<span class="chip ch-1">MoCA ${ls.moca}</span>`:'<span class="chip ch-n">MoCA —</span>';
    const tug=ls?.tug!=null?`<span class="chip ch-2">TUG ${ls.tug}s</span>`:'<span class="chip ch-n">TUG —</span>';
    const nb=ls?.nback!=null?`<span class="chip ch-3">N-back ${ls.nback}%</span>`:'<span class="chip ch-n">N-back —</span>';
    return `<div class="subj-card ${selId===s.id?'sel':''}" onclick="selectSubj('${s.id}')">
      <div class="subj-top"><span class="subj-id">${s.id}</span><span class="subj-name">${s.name}</span><span class="subj-age">${s.age}세·${s.gender==='M'?'남':'여'}·BMI ${s.bmi}</span></div>
      <div class="subj-chips">${moca}${tug}${nb}
        <button class="btn btn-d btn-sm" style="margin-top:0;padding:4px 10px;font-size:11px" onclick="delSubject('${s.id}',event)">삭제</button>
      </div></div>`;
  }).join('');
}

// ═══════════════════════════════════
//  TEST SUBJECT PICKER
// ═══════════════════════════════════
function renderTestSubjPicker(){
  const el=document.getElementById('testSubjPicker');
  if(!DB.subjects.length){ el.innerHTML='<div class="card" style="padding:12px;font-size:13px;color:var(--t2)">⚠️ 먼저 피험자를 등록하세요.</div>'; return; }
  el.innerHTML=`<div class="card" style="padding:12px"><div class="card-label" style="margin-bottom:8px">피험자 선택</div><div style="display:flex;gap:6px;flex-wrap:wrap">${DB.subjects.map(s=>`<button class="btn btn-sm ${selId===s.id?'btn-p':'btn-s'}" onclick="selectSubj('${s.id}');renderTestSubjPicker()">${s.name}</button>`).join('')}</div></div>`;
}
function renderHistSubjPicker(){
  const el=document.getElementById('histSubjPicker');
  if(!DB.subjects.length){ el.innerHTML=''; return; }
  el.innerHTML=`<div class="card" style="padding:12px"><div class="card-label" style="margin-bottom:8px">피험자 선택</div><div style="display:flex;gap:6px;flex-wrap:wrap">${DB.subjects.map(s=>`<button class="btn btn-sm ${selId===s.id?'btn-p':'btn-s'}" onclick="selectSubj('${s.id}');renderHist()">${s.name}</button>`).join('')}</div></div>`;
}
function renderResSubjPicker(){
  const el=document.getElementById('resSubjPicker');
  if(!DB.subjects.length){ el.innerHTML=''; return; }
  el.innerHTML=`<div class="card" style="padding:12px"><div class="card-label" style="margin-bottom:8px">피험자 선택</div><div style="display:flex;gap:6px;flex-wrap:wrap">${DB.subjects.map(s=>`<button class="btn btn-sm ${selId===s.id?'btn-p':'btn-s'}" onclick="selectSubj('${s.id}');renderRes()">${s.name}</button>`).join('')}</div></div>`;
}

// ═══════════════════════════════════
//  TEST SELECTOR
// ═══════════════════════════════════
function renderTestSelector(){
  document.getElementById('testSelector').innerHTML=`
  <button class="test-btn tb-1" onclick="startTest('moca')">
    <div class="tb-icon">📋</div><div class="tb-title">MoCA — 몬트리올 인지검사</div>
    <div class="tb-sub">30점 만점 · 약 10분</div>
    <span class="tb-badge" style="background:rgba(62,207,255,.1);color:var(--a1)">인지기능</span>
  </button>
  <button class="test-btn tb-2" onclick="startTest('tug')">
    <div class="tb-icon">⏱️</div><div class="tb-title">TUG — 일어나 걷기 검사</div>
    <div class="tb-sub">낙상 위험도 · 이동 능력</div>
    <span class="tb-badge" style="background:rgba(139,92,246,.1);color:var(--a2)">신체기능</span>
  </button>
  <button class="test-btn tb-3" onclick="startTest('nback')">
    <div class="tb-icon">🔢</div><div class="tb-title">N-back — 작업기억 검사</div>
    <div class="tb-sub">1-back / 2-back · 약 5분</div>
    <span class="tb-badge" style="background:rgba(16,217,140,.1);color:var(--a3)">작업기억</span>
  </button>`;
}

function startTest(type){
  if(!selId){ toast('⚠️ 피험자를 먼저 선택하세요'); return; }
  document.getElementById('testSelector').style.display='none';
  const area=document.getElementById('testArea');
  if(type==='moca') area.innerHTML=buildMoCA();
  if(type==='tug') area.innerHTML=buildTUG();
  if(type==='nback'){ area.innerHTML=buildNback(); initNback(); }
}
function cancelTest(){ document.getElementById('testArea').innerHTML=''; document.getElementById('testSelector').style.display=''; }

// ═══════════════════════════════════
//  SESSION SAVE
// ═══════════════════════════════════
function saveSession(data){
  const sub=getSub(selId);
  DB.sessions.push({
    id: Date.now().toString(),
    subjectId: selId,
    date: new Date().toISOString().split('T')[0],
    ...data
  });
  saveDB(); renderSubjList();
}

// ═══════════════════════════════════
//  MoCA
// ═══════════════════════════════════
const MOCA_SECS=[
  {t:'시공간·실행',max:5,items:[{q:'시계 윤곽',m:1},{q:'시계 숫자',m:1},{q:'시계 바늘',m:1},{q:'입체도형 모사',m:1},{q:'선로잇기 (TMT-B)',m:1}]},
  {t:'이름대기',max:3,items:[{q:'사자',m:1},{q:'코뿔소',m:1},{q:'낙타',m:1}]},
  {t:'즉각회상 (점수없음)',max:0,items:[{q:'5단어 1회차 학습',m:0},{q:'5단어 2회차 학습',m:0}]},
  {t:'주의집중',max:6,items:[{q:'숫자 바로 (5자리)',m:1},{q:'숫자 거꾸로 (3자리)',m:1},{q:'경계 과제 (A)',m:1},{q:'100-7 연속 (3~4개)',m:2},{q:'100-7 연속 (5개)',m:1}]},
  {t:'언어',max:3,items:[{q:'문장 따라 말하기 ①',m:1},{q:'문장 따라 말하기 ②',m:1},{q:'ㄱ 유창성 (≥11개)',m:1}]},
  {t:'추상적 사고',max:2,items:[{q:'기차-자전거 유사성',m:1},{q:'시계-자 유사성',m:1}]},
  {t:'지연 회상',max:5,items:[{q:'단어 1',m:1},{q:'단어 2',m:1},{q:'단어 3',m:1},{q:'단어 4',m:1},{q:'단어 5',m:1}]},
  {t:'지남력',max:6,items:[{q:'날짜',m:1},{q:'월',m:1},{q:'연도',m:1},{q:'요일',m:1},{q:'장소',m:1},{q:'도시',m:1}]}
];

let MS={};
function buildMoCA(){
  MS={};
  const sub=getSub(selId);
  let html=`<div class="test-wrap">
  <div class="test-head"><h2>📋 MoCA 검사</h2><p>Montreal Cognitive Assessment · 30점 만점</p></div>
  <div class="test-subj-info">👤 <b>${sub.name}</b> (${sub.id}) · ${sub.age}세 · 교육 ${sub.edu}년</div>`;
  MOCA_SECS.forEach((sec,si)=>{
    html+=`<div class="moca-sec"><div class="moca-sec-title"><span>${sec.t}</span><span>${sec.max}점</span></div>`;
    sec.items.forEach((item,ii)=>{
      const key=`${si}_${ii}`;
      if(item.m===0){ html+=`<div class="moca-item"><div class="moca-q" style="color:var(--t3)">${item.q}</div></div>`; }
      else {
        const btns=[...Array(item.m+1)].map((_,v)=>`<button class="sb" data-k="${key}" data-v="${v}" onclick="setMS('${key}',${v})">${v}</button>`).join('');
        html+=`<div class="moca-item"><div class="moca-q">${item.q}</div><div class="moca-btns">${btns}</div></div>`;
      }
    });
    html+=`</div>`;
  });
  html+=`<div class="moca-sec"><div class="moca-sec-title">교육 보정</div>
  <div class="moca-item"><div class="moca-q">12년 미만 교육 +1점</div>
  <div class="moca-btns"><button class="sb" data-k="edu" data-v="0" onclick="setMS('edu',0)">0</button><button class="sb" data-k="edu" data-v="1" onclick="setMS('edu',1)">+1</button></div></div></div>`;
  html+=`<div class="moca-total-row"><span class="moca-total-label">합계</span><span class="moca-total-val"><span id="mTotal">0</span> / 30</span></div>`;
  html+=`<div class="btn-row" style="margin-top:14px">
    <button class="btn btn-p" onclick="saveMoCA()">✅ 저장</button>
    <button class="btn btn-s" onclick="cancelTest()">취소</button>
  </div></div>`;
  return html;
}
function setMS(k,v){ MS[k]=v; document.querySelectorAll(`.sb[data-k="${k}"]`).forEach(b=>b.classList.toggle('on',parseInt(b.dataset.v)===v)); document.getElementById('mTotal').textContent=Object.values(MS).reduce((a,b)=>a+b,0); }
function saveMoCA(){ const t=Object.values(MS).reduce((a,b)=>a+b,0); saveSession({type:'moca',moca:t}); toast('✅ MoCA 저장: '+t+'점'); cancelTest(); goPage('results'); }

// ═══════════════════════════════════
//  TUG
// ═══════════════════════════════════
let TT=null,TS=null,TM=0,TR=false;
function buildTUG(){
  const sub=getSub(selId);
  return `<div class="test-wrap">
  <div class="test-head"><h2>⏱️ TUG 테스트</h2><p>Timed Up and Go · 낙상 위험도</p></div>
  <div class="test-subj-info">👤 <b>${sub.name}</b> · ${sub.age}세</div>
  <div style="background:var(--s2);border-radius:var(--rs);padding:12px 14px;font-size:12px;color:var(--t2);margin-bottom:16px;line-height:1.8">
    <b style="color:var(--t1)">방법:</b> 팔걸이 의자에서 일어남 → 3m 표시 → 돌아서 → 착석<br>
    출발 신호에 시작, 완전 착석 시 정지
  </div>
  <div class="timer-big">
    <div class="timer-num" id="tugNum">00.00</div>
    <div class="timer-label" id="tugLabel">준비 — 시작 버튼을 누르세요</div>
  </div>
  <div class="btn-row" style="margin-bottom:12px">
    <button class="btn btn-v" id="tugGo" onclick="tugToggle()" style="font-size:18px;padding:18px;">▶ 시작</button>
    <button class="btn btn-s" onclick="tugReset()">↺</button>
  </div>
  <div style="font-size:13px;color:var(--t2);text-align:center;margin-bottom:16px">결과: <b id="tugRes" style="font-family:var(--fm);color:var(--a2)">—</b></div>
  <div class="card" style="padding:14px">
    <div class="card-label">연령별 기준치</div>
    <table class="tug-ref-table">
      <tr><th>연령</th><th>정상</th><th>주의</th><th>고위험</th></tr>
      <tr><td>60–69세</td><td>≤8.1초</td><td>~13.5</td><td>>13.5</td></tr>
      <tr><td>70–79세</td><td>≤9.2초</td><td>~16.0</td><td>>16.0</td></tr>
      <tr><td>80+세</td><td>≤11.3초</td><td>~20.0</td><td>>20.0</td></tr>
      <tr><td id="tugRefLabel">${sub.name} (${sub.age}세)</td><td colspan="3" id="tugRefResult" style="color:var(--a2)">—</td></tr>
    </table>
  </div>
  <div class="btn-row" style="margin-top:8px">
    <button class="btn btn-g" onclick="saveTUG()">✅ 저장</button>
    <button class="btn btn-s" onclick="cancelTest()">취소</button>
  </div></div>`;
}
function tugToggle(){
  if(!TR){
    TR=true;TS=Date.now()-TM;
    document.getElementById('tugGo').textContent='⏹ 정지';
    document.getElementById('tugGo').className='btn btn-d';
    document.getElementById('tugLabel').textContent='측정 중...';
    document.getElementById('tugNum').classList.add('run');
    TT=setInterval(()=>{ TM=Date.now()-TS; document.getElementById('tugNum').textContent=(TM/1000).toFixed(2).padStart(5,'0'); },50);
  } else {
    clearInterval(TT);TR=false;
    const s=(TM/1000).toFixed(2);
    document.getElementById('tugGo').textContent='▶ 시작';
    document.getElementById('tugGo').className='btn btn-v';
    document.getElementById('tugLabel').textContent='측정 완료';
    document.getElementById('tugNum').classList.remove('run');
    document.getElementById('tugRes').textContent=s+'초';
    const age=getSub(selId)?.age||70;
    const n=age<70?8.1:age<80?9.2:11.3, w=age<70?13.5:age<80?16.0:20.0;
    const sv=parseFloat(s);
    const interp=sv<=n?'✅ 정상':sv<=w?'⚠️ 주의':'🚨 고위험';
    const col=sv<=n?'var(--a3)':sv<=w?'var(--a4)':'var(--a5)';
    const r=document.getElementById('tugRefResult');
    if(r){ r.textContent=s+'초 → '+interp; r.style.color=col; }
  }
}
function tugReset(){ clearInterval(TT);TR=false;TM=0; document.getElementById('tugNum').textContent='00.00'; document.getElementById('tugLabel').textContent='준비 — 시작 버튼을 누르세요'; document.getElementById('tugNum').classList.remove('run'); document.getElementById('tugGo').textContent='▶ 시작'; document.getElementById('tugGo').className='btn btn-v'; document.getElementById('tugRes').textContent='—'; if(document.getElementById('tugRefResult')) document.getElementById('tugRefResult').textContent='—'; }
function saveTUG(){ if(!TM){ toast('⚠️ 측정값 없음'); return; } const s=parseFloat((TM/1000).toFixed(2)); saveSession({type:'tug',tug:s}); toast('✅ TUG 저장: '+s+'초'); cancelTest(); goPage('results'); }

// ═══════════════════════════════════
//  N-BACK
// ═══════════════════════════════════
let NB={};
function buildNback(){
  return `<div class="test-wrap">
  <div class="test-head"><h2>🔢 N-back 검사</h2><p>작업기억 평가 · 1-back / 2-back</p></div>
  <div class="nb-level-row">
    <button class="btn btn-s" id="nb1" onclick="setNBLevel(1)" style="border-color:var(--a1);color:var(--a1)">1-back</button>
    <button class="btn btn-s" id="nb2" onclick="setNBLevel(2)">2-back</button>
  </div>
  <div style="background:var(--s2);border-radius:var(--rs);padding:12px;font-size:12px;color:var(--t2);margin-bottom:14px;line-height:1.8">
    <b style="color:var(--a3)">1-back</b> — 직전과 같은 위치면 반응<br>
    <b style="color:var(--a3)">2-back</b> — 2번 전과 같은 위치면 반응<br>
    연습 5회 → 본시행 20회 · 자극 2.5초
  </div>
  <div class="nb-stat-row">
    <span><span class="sv" id="nbTrial">0/0</span><span class="sk">시행</span></span>
    <span><span class="sv" id="nbHit" style="color:var(--a3)">0</span><span class="sk">정반응</span></span>
    <span><span class="sv" id="nbFA" style="color:var(--a5)">0</span><span class="sk">오경보</span></span>
    <span><span class="sv" id="nbAcc" style="color:var(--a1)">0%</span><span class="sk">정확도</span></span>
  </div>
  <div class="nb-grid">${[...Array(9)].map((_,i)=>`<div class="nb-cell" id="nbc${i}"></div>`).join('')}</div>
  <div class="nb-feedback" id="nbFb"></div>
  <button class="nb-match-btn" id="nbMatchBtn" onclick="nbMatch()" disabled>👆 일치 (Space)</button>
  <div class="btn-row" style="margin-top:12px">
    <button class="btn btn-g" id="nbStart" onclick="nbStart()">▶ 시작</button>
    <button class="btn btn-s" onclick="nbStop()">⏹ 중지</button>
  </div>
  <div class="btn-row" style="margin-top:8px">
    <button class="btn btn-g" onclick="saveNback()">✅ 저장</button>
    <button class="btn btn-s" onclick="cancelTest()">취소</button>
  </div></div>`;
}
function initNback(){ NB={level:1,seq:[],idx:0,hits:0,fa:0,tgts:0,running:false,resp:false,timer:null,prac:5,total:20,acc:null}; document.addEventListener('keydown',nbKey); }
function setNBLevel(n){ nbStop(); NB.level=n; document.getElementById('nb1').style.cssText=n===1?'border-color:var(--a1);color:var(--a1)':''; document.getElementById('nb2').style.cssText=n===2?'border-color:var(--a1);color:var(--a1)':''; }
function nbKey(e){ if(e.code==='Space'){ e.preventDefault(); nbMatch(); } }
function nbStart(){
  NB.seq=[];NB.idx=0;NB.hits=0;NB.fa=0;NB.tgts=0;NB.running=true;NB.resp=false;NB.acc=null;
  const total=NB.prac+NB.total;
  for(let i=0;i<total;i++){ let p=Math.floor(Math.random()*9); if(i>=NB.level&&Math.random()<0.35) p=NB.seq[i-NB.level]; NB.seq.push(p); }
  document.getElementById('nbStart').disabled=true;
  document.getElementById('nbMatchBtn').disabled=false;
  nbTick();
}
function nbTick(){
  if(!NB.running) return;
  const total=NB.prac+NB.total;
  if(NB.idx>=total){ nbEnd(); return; }
  const pos=NB.seq[NB.idx], isPrac=NB.idx<NB.prac, isTgt=NB.idx>=NB.level&&NB.seq[NB.idx-NB.level]===pos;
  if(!isPrac&&isTgt) NB.tgts++;
  NB.resp=false;
  document.querySelectorAll('.nb-cell').forEach(c=>c.classList.remove('lit','hit'));
  document.getElementById('nbc'+pos).classList.add('lit');
  document.getElementById('nbTrial').textContent=isPrac?'연습'+(NB.idx+1):(NB.idx-NB.prac+1)+'/'+NB.total;
  document.getElementById('nbFb').textContent='';
  NB.timer=setTimeout(()=>{ document.getElementById('nbc'+pos)?.classList.remove('lit','hit'); NB.idx++; nbTick(); },2500);
}
function nbMatch(){
  if(!NB.running||NB.resp) return; NB.resp=true;
  const pos=NB.seq[NB.idx], isPrac=NB.idx<NB.prac, isTgt=NB.idx>=NB.level&&NB.seq[NB.idx-NB.level]===pos;
  if(isTgt){ if(!isPrac)NB.hits++; document.getElementById('nbc'+pos)?.classList.add('hit'); document.getElementById('nbFb').innerHTML='<span style="color:var(--a3)">✅ 정답!</span>'; }
  else { if(!isPrac)NB.fa++; document.getElementById('nbFb').innerHTML='<span style="color:var(--a5)">❌ 오경보</span>'; }
  nbStats();
}
function nbStats(){
  document.getElementById('nbHit').textContent=NB.hits;
  document.getElementById('nbFA').textContent=NB.fa;
  const acc=NB.tgts>0?Math.round(NB.hits/NB.tgts*100):0;
  document.getElementById('nbAcc').textContent=acc+'%';
}
function nbEnd(){
  NB.running=false; const acc=NB.tgts>0?Math.round(NB.hits/NB.tgts*100):0; NB.acc=acc;
  document.getElementById('nbStart').disabled=false;
  document.getElementById('nbMatchBtn').disabled=true;
  document.getElementById('nbFb').innerHTML=`<b style="color:var(--a3)">완료! 정확도 ${acc}% (${NB.hits}/${NB.tgts})</b>`;
  toast('N-back 완료: '+acc+'%');
}
function nbStop(){ NB.running=false; if(NB.timer) clearTimeout(NB.timer); document.querySelectorAll('.nb-cell').forEach(c=>c.classList.remove('lit','hit')); if(document.getElementById('nbStart')) document.getElementById('nbStart').disabled=false; if(document.getElementById('nbMatchBtn')) document.getElementById('nbMatchBtn').disabled=true; }
function saveNback(){ if(NB.acc==null){ toast('⚠️ 완료된 결과 없음'); return; } saveSession({type:'nback',nback:NB.acc,nbackLevel:NB.level}); document.removeEventListener('keydown',nbKey); toast('✅ N-back 저장: '+NB.acc+'%'); cancelTest(); goPage('results'); }

// ═══════════════════════════════════
//  HISTORY — 회차 기록 + 전후 비교
// ═══════════════════════════════════
function renderHist(){
  const el=document.getElementById('histArea');
  if(!selId){ el.innerHTML='<div class="empty"><div class="ei">👈</div><p>피험자를 선택하세요</p></div>'; return; }
  const sub=getSub(selId); const sessions=getSessions(selId);
  if(!sessions.length){ el.innerHTML='<div class="empty"><div class="ei">📋</div><p>검사 기록이 없습니다.<br>검사를 실시해 주세요.</p></div>'; return; }

  // 회차별 합산 (날짜 기준 그룹)
  const byDate={};
  sessions.forEach(s=>{ if(!byDate[s.date]) byDate[s.date]=[]; byDate[s.date].push(s); });
  const dates=Object.keys(byDate).sort((a,b)=>new Date(b)-new Date(a));

  // 전후 비교 섹션
  let compareHtml='';
  if(dates.length>=2){
    const rounds=dates.map((d,i)=>({ round:dates.length-i, date:d, sessions:byDate[d] }));
    // 최신 vs 이전
    const latest=rounds[0], prev=rounds[1];
    const getVal=(r,type)=>{ const s=r.sessions.find(x=>x[type]!=null); return s?s[type]:null; };
    const mL=getVal(latest,'moca'),mP=getVal(prev,'moca');
    const tL=getVal(latest,'tug'),tP=getVal(prev,'tug');
    const nL=getVal(latest,'nback'),nP=getVal(prev,'nback');

    function diffBadge(curr,prev,higher='better'){
      if(curr==null||prev==null) return '<span style="color:var(--t3)">—</span>';
      const d=curr-prev;
      if(d===0) return `<span class="diff-same">±0</span>`;
      const isGood=(higher==='better'&&d>0)||(higher==='lower'&&d<0);
      return `<span class="${isGood?'diff-up':'diff-down'}">${d>0?'+':''}${typeof curr==='number'&&!Number.isInteger(curr)?d.toFixed(2):d}</span>`;
    }

    compareHtml=`<div class="card" style="margin-bottom:14px">
      <div class="card-label">📊 전후 비교 (최신 vs 이전)</div>
      <div class="compare-wrap"><table class="compare-table">
        <tr><th>검사</th><th>회차 ${rounds.length-1} (${prev.date})</th><th>최신 (${latest.date})</th><th>변화</th></tr>
        <tr><td>MoCA (/30)</td><td>${mP??'—'}</td><td style="color:var(--a1);font-weight:700">${mL??'—'}</td><td>${diffBadge(mL,mP,'higher')}</td></tr>
        <tr><td>TUG (초)</td><td>${tP??'—'}</td><td style="color:var(--a2);font-weight:700">${tL??'—'}</td><td>${diffBadge(tL,tP,'lower')}</td></tr>
        <tr><td>N-back (%)</td><td>${nP!=null?nP+'%':'—'}</td><td style="color:var(--a3);font-weight:700">${nL!=null?nL+'%':'—'}</td><td>${diffBadge(nL,nP,'higher')}</td></tr>
      </table></div>
    </div>`;

    // 전체 추이 테이블
    if(dates.length>=3){
      compareHtml+=`<div class="card" style="margin-bottom:14px">
        <div class="card-label">📈 전체 추이</div>
        <div class="compare-wrap"><table class="compare-table">
          <tr><th>회차</th><th>날짜</th><th>MoCA</th><th>TUG</th><th>N-back</th></tr>
          ${rounds.map(r=>`<tr>
            <td>회차 ${r.round}</td>
            <td>${r.date}</td>
            <td style="color:var(--a1)">${getVal(r,'moca')??'—'}</td>
            <td style="color:var(--a2)">${getVal(r,'tug')??'—'}</td>
            <td style="color:var(--a3)">${getVal(r,'nback')!=null?getVal(r,'nback')+'%':'—'}</td>
          </tr>`).join('')}
        </table></div>
      </div>`;
    }
  }

  let sessHtml=dates.map((date,di)=>{
    const round=dates.length-di;
    const sArr=byDate[date];
    const rows=sArr.map(s=>{
      if(s.moca!=null){
        const st=s.moca>=26?'정상':s.moca>=18?'경도 의심':'중증 의심';
        const sc=s.moca>=26?'var(--a3)':s.moca>=18?'var(--a4)':'var(--a5)';
        return `<div class="hist-row"><span class="hist-row-key">MoCA</span><span class="hist-row-val" style="color:var(--a1)">${s.moca} / 30점</span><span class="hist-row-interp" style="background:rgba(62,207,255,.1);color:var(--a1)">${st}</span></div>`;
      }
      if(s.tug!=null){
        const age=sub.age; const n=age<70?8.1:age<80?9.2:11.3, w2=age<70?13.5:age<80?16.0:20.0;
        const st=s.tug<=n?'정상':s.tug<=w2?'주의':'고위험';
        return `<div class="hist-row"><span class="hist-row-key">TUG</span><span class="hist-row-val" style="color:var(--a2)">${s.tug} 초</span><span class="hist-row-interp" style="background:rgba(139,92,246,.1);color:var(--a2)">${st}</span></div>`;
      }
      if(s.nback!=null){
        const st=s.nback>=70?'양호':s.nback>=50?'경계':'저하';
        return `<div class="hist-row"><span class="hist-row-key">N-back (${s.nbackLevel??'?'}-back)</span><span class="hist-row-val" style="color:var(--a3)">${s.nback}%</span><span class="hist-row-interp" style="background:rgba(16,217,140,.1);color:var(--a3)">${st}</span></div>`;
      }
      return '';
    }).join('');
    return `<div class="hist-session">
      <div class="hist-session-head" onclick="toggleHist('hs${di}')">
        <span class="hs-date">${date}</span>
        <span class="hs-round">회차 ${round}</span>
        <span class="hs-arrow" id="hsa${di}">▼</span>
      </div>
      <div class="hist-session-body open" id="hs${di}">${rows}</div>
    </div>`;
  }).join('');

  el.innerHTML=compareHtml+sessHtml;
}
function toggleHist(id){ const b=document.getElementById(id), arrow=document.getElementById('hsa'+id.replace('hs','')); b.classList.toggle('open'); if(arrow) arrow.classList.toggle('open'); }

// ═══════════════════════════════════
//  RESULTS
// ═══════════════════════════════════
function renderRes(){
  const el=document.getElementById('resArea');
  if(!selId){ el.innerHTML='<div class="empty"><div class="ei">👈</div><p>피험자를 선택하세요</p></div>'; return; }
  const sub=getSub(selId);
  const ls=getLatestSession(selId);
  const allSess=getSessions(selId);
  const lastMoca=allSess.find(s=>s.moca!=null);
  const lastTug=allSess.find(s=>s.tug!=null);
  const lastNback=allSess.find(s=>s.nback!=null);

  const hm=sub.height/100;
  const bmi=(sub.weight/(hm*hm)).toFixed(1);
  const ideal=(sub.height-100)*0.9;
  const ob=((sub.weight/ideal)*100).toFixed(1);
  const bsa=(0.007184*Math.pow(sub.height,0.725)*Math.pow(sub.weight,0.425)).toFixed(2);

  // scores
  const mS=lastMoca?.moca, tS=lastTug?.tug, nS=lastNback?.nback;
  const age=sub.age;
  const tn=age<70?8.1:age<80?9.2:11.3, tw=age<70?13.5:age<80?16.0:20.0;
  const mSt=mS!=null?(mS>=26?['정상','var(--a3)']:mS>=18?['경도 의심','var(--a4)']:['중증 의심','var(--a5)']):null;
  const tSt=tS!=null?(tS<=tn?['정상','var(--a3)']:tS<=tw?['주의','var(--a4)']:['고위험','var(--a5)']):null;
  const nSt=nS!=null?(nS>=70?['양호','var(--a3)']:nS>=50?['경계','var(--a4)']:['저하','var(--a5)']):null;

  let html=`<div class="card">
    <div class="card-label">👤 ${sub.name} (${sub.id})</div>
    <div class="bmi-grid">
      <div class="bmi-tile"><div class="tl">나이·성별</div><div class="tv" style="font-size:16px">${sub.age}세 ${sub.gender==='M'?'남':'여'}</div></div>
      <div class="bmi-tile"><div class="tl">신장/체중</div><div class="tv" style="font-size:14px">${sub.height}cm/${sub.weight}kg</div></div>
      <div class="bmi-tile"><div class="tl">BMI</div><div class="tv ${bmi<18.5||bmi>=25?'bad':bmi>=23?'warn':'ok'}">${bmi}</div><div class="ts">${bmi<18.5?'저체중':bmi<23?'정상':bmi<25?'과체중':'비만'}</div></div>
      <div class="bmi-tile"><div class="tl">비만도</div><div class="tv" style="font-size:16px">${ob}%</div><div class="ts">표준 ${ideal.toFixed(1)}kg</div></div>
      <div class="bmi-tile"><div class="tl">체표면적</div><div class="tv" style="font-size:15px">${bsa} m²</div></div>
      <div class="bmi-tile"><div class="tl">교육</div><div class="tv" style="font-size:16px">${sub.edu}년</div></div>
    </div>
  </div>
  <div class="score-trio">
    <div class="score-tile">
      <div class="st-label">MoCA</div>
      <div class="st-val" style="color:var(--a1)">${mS??'—'}</div>
      <div class="st-unit">/ 30점</div>
      ${mSt?`<div class="st-badge" style="background:rgba(62,207,255,.1);color:${mSt[1]}">${mSt[0]}</div>`:'<div class="st-badge" style="background:var(--s2);color:var(--t3)">미실시</div>'}
      <div style="font-size:10px;color:var(--t3);margin-top:4px">${lastMoca?.date||''}</div>
    </div>
    <div class="score-tile">
      <div class="st-label">TUG</div>
      <div class="st-val" style="color:var(--a2)">${tS??'—'}</div>
      <div class="st-unit">초</div>
      ${tSt?`<div class="st-badge" style="background:rgba(139,92,246,.1);color:${tSt[1]}">${tSt[0]}</div>`:'<div class="st-badge" style="background:var(--s2);color:var(--t3)">미실시</div>'}
      <div style="font-size:10px;color:var(--t3);margin-top:4px">${lastTug?.date||''}</div>
    </div>
    <div class="score-tile">
      <div class="st-label">N-back</div>
      <div class="st-val" style="color:var(--a3)">${nS!=null?nS+'%':'—'}</div>
      <div class="st-unit">${lastNback?.nbackLevel?lastNback.nbackLevel+'-back':''}</div>
      ${nSt?`<div class="st-badge" style="background:rgba(16,217,140,.1);color:${nSt[1]}">${nSt[0]}</div>`:'<div class="st-badge" style="background:var(--s2);color:var(--t3)">미실시</div>'}
      <div style="font-size:10px;color:var(--t3);margin-top:4px">${lastNback?.date||''}</div>
    </div>
  </div>
  <div class="card">
    <div class="card-label">📋 종합 해석 및 권고</div>
    <table style="width:100%;border-collapse:collapse;font-size:12px">
      <tr><th style="text-align:left;padding:8px 0;color:var(--t3);font-size:10px;text-transform:uppercase;letter-spacing:.4px;border-bottom:1px solid var(--b1)">검사</th><th style="padding:8px;color:var(--t3);font-size:10px;border-bottom:1px solid var(--b1)">결과</th><th style="text-align:left;padding:8px;color:var(--t3);font-size:10px;border-bottom:1px solid var(--b1)">권고사항</th></tr>
      <tr><td style="padding:10px 0;color:var(--t2);border-bottom:1px solid var(--b1)">MoCA</td>
        <td style="text-align:center;padding:10px;font-family:var(--fm);font-weight:700;border-bottom:1px solid var(--b1);color:var(--a1)">${mS!=null?mS+'/30':'—'}</td>
        <td style="padding:10px;font-size:11px;color:var(--t2);border-bottom:1px solid var(--b1)">${mS!=null?(mS>=26?'정기 모니터링':mS>=18?'신경과 상담 권고, 인지 중재 고려':'전문의 의뢰 필수'):'검사 시행 필요'}</td></tr>
      <tr><td style="padding:10px 0;color:var(--t2);border-bottom:1px solid var(--b1)">TUG</td>
        <td style="text-align:center;padding:10px;font-family:var(--fm);font-weight:700;border-bottom:1px solid var(--b1);color:var(--a2)">${tS!=null?tS+'초':'—'}</td>
        <td style="padding:10px;font-size:11px;color:var(--t2);border-bottom:1px solid var(--b1)">${tS!=null?(tS<=tn?'정기 평가 유지':tS<=tw?'균형·보행 운동 권고':'낙상 예방 중재, 보조기 검토'):'검사 시행 필요'}</td></tr>
      <tr><td style="padding:10px 0;color:var(--t2)">N-back</td>
        <td style="text-align:center;padding:10px;font-family:var(--fm);font-weight:700;color:var(--a3)">${nS!=null?nS+'%':'—'}</td>
        <td style="padding:10px;font-size:11px;color:var(--t2)">${nS!=null?(nS>=70?'유지':nS>=50?'인지 훈련 고려':'집중적 인지 재활 필요'):'검사 시행 필요'}</td></tr>
    </table>
  </div>
  <div class="card">
    <div class="card-label">전체 피험자 요약</div>
    <div class="compare-wrap"><table class="compare-table">
      <tr><th>이름</th><th>나이</th><th>BMI</th><th>MoCA</th><th>TUG</th><th>N-back</th></tr>
      ${DB.subjects.map(s=>{
        const ls2=getLatestSession(s.id);
        const lm=DB.sessions.find(x=>x.subjectId===s.id&&x.moca!=null);
        const lt=DB.sessions.find(x=>x.subjectId===s.id&&x.tug!=null);
        const ln=DB.sessions.find(x=>x.subjectId===s.id&&x.nback!=null);
        return `<tr style="${s.id===selId?'background:rgba(62,207,255,.05)':''}">
          <td style="font-family:var(--ff)">${s.name}</td>
          <td>${s.age}</td>
          <td>${(s.weight/((s.height/100)**2)).toFixed(1)}</td>
          <td style="color:var(--a1)">${lm?.moca??'—'}</td>
          <td style="color:var(--a2)">${lt?.tug??'—'}</td>
          <td style="color:var(--a3)">${ln?.nback!=null?ln.nback+'%':'—'}</td>
        </tr>`;
      }).join('')}
    </table></div>
  </div>
  <button class="btn btn-y" onclick="exportExcel()" style="margin-top:4px">📊 엑셀로 내보내기</button>`;

  el.innerHTML=html;
}

// ═══════════════════════════════════
//  EXCEL EXPORT
// ═══════════════════════════════════
function exportExcel(){
  if(!DB.subjects.length){ toast('⚠️ 데이터가 없습니다'); return; }
  const wb=XLSX.utils.book_new();

  // Sheet 1: 피험자 정보
  const subData=[['ID','이름','나이','성별','키(cm)','체중(kg)','BMI','표준체중(kg)','비만도(%)','체표면적(m²)','교육연수(년)','등록일']];
  DB.subjects.forEach(s=>{
    const hm=s.height/100;
    const bmi=(s.weight/(hm*hm)).toFixed(1);
    const ideal=(s.height-100)*0.9;
    const ob=((s.weight/ideal)*100).toFixed(1);
    const bsa=(0.007184*Math.pow(s.height,0.725)*Math.pow(s.weight,0.425)).toFixed(2);
    subData.push([s.id,s.name,s.age,s.gender==='M'?'남':'여',s.height,s.weight,bmi,ideal.toFixed(1),ob,bsa,s.edu||'',s.date||'']);
  });
  XLSX.utils.book_append_sheet(wb, XLSX.utils.aoa_to_sheet(subData), '피험자정보');

  // Sheet 2: 전체 검사 기록
  const sessData=[['피험자ID','이름','검사일','검사종류','MoCA점수(/30)','MoCA해석','TUG(초)','TUG해석','N-back정확도(%)','N-back레벨','N-back해석']];
  DB.sessions.forEach(s=>{
    const sub=getSub(s.subjectId);
    const age=sub?.age||70;
    const tn=age<70?8.1:age<80?9.2:11.3, tw=age<70?13.5:age<80?16.0:20.0;
    const mInterp=s.moca!=null?(s.moca>=26?'정상':s.moca>=18?'경도인지장애의심':'중증인지장애의심'):'';
    const tInterp=s.tug!=null?(s.tug<=tn?'정상':s.tug<=tw?'주의':'낙상고위험'):'';
    const nInterp=s.nback!=null?(s.nback>=70?'양호':s.nback>=50?'경계':'저하'):'';
    sessData.push([s.subjectId,sub?.name||'',s.date,s.type==='moca'?'MoCA':s.type==='tug'?'TUG':'N-back',s.moca??'',mInterp,s.tug??'',tInterp,s.nback??'',s.nbackLevel??'',nInterp]);
  });
  XLSX.utils.book_append_sheet(wb, XLSX.utils.aoa_to_sheet(sessData), '검사기록');

  // Sheet 3: 피험자별 최신 요약
  const sumData=[['ID','이름','나이','성별','BMI','최신MoCA','MoCA일','최신TUG','TUG일','최신N-back','N-back일','회차수']];
  DB.subjects.forEach(s=>{
    const bmi=(s.weight/((s.height/100)**2)).toFixed(1);
    const lm=DB.sessions.find(x=>x.subjectId===s.id&&x.moca!=null);
    const lt=DB.sessions.find(x=>x.subjectId===s.id&&x.tug!=null);
    const ln=DB.sessions.find(x=>x.subjectId===s.id&&x.nback!=null);
    const rounds=getSessions(s.id);
    sumData.push([s.id,s.name,s.age,s.gender==='M'?'남':'여',bmi,lm?.moca??'',lm?.date??'',lt?.tug??'',lt?.date??'',ln?.nback!=null?ln.nback+'%':'',ln?.date??'',rounds.length]);
  });
  XLSX.utils.book_append_sheet(wb, XLSX.utils.aoa_to_sheet(sumData), '최신요약');

  // Sheet 4: 전후비교
  const compData=[['ID','이름','검사','이전값','이전날짜','최신값','최신날짜','변화량','방향']];
  DB.subjects.forEach(s=>{
    const sArr=getSessions(s.id);
    ['moca','tug','nback'].forEach(type=>{
      const typed=sArr.filter(x=>x[type]!=null).sort((a,b)=>new Date(a.date)-new Date(b.date));
      if(typed.length>=2){
        const prev=typed[typed.length-2], latest=typed[typed.length-1];
        const diff=latest[type]-prev[type];
        const better=(type==='tug'&&diff<0)||(type!=='tug'&&diff>0);
        compData.push([s.id,s.name,type==='moca'?'MoCA':type==='tug'?'TUG':'N-back',prev[type],prev.date,latest[type],latest.date,diff>0?'+'+diff:diff,better?'개선':'저하']);
      }
    });
  });
  XLSX.utils.book_append_sheet(wb, XLSX.utils.aoa_to_sheet(compData), '전후비교');

  XLSX.writeFile(wb, `CogPhys_${new Date().toISOString().split('T')[0]}.xlsx`);
  toast('📊 엑셀 다운로드 완료');
}

// ═══════════════════════════════════
//  TOAST
// ═══════════════════════════════════
let TI;
function toast(msg){ const el=document.getElementById('toast'); el.textContent=msg; el.classList.add('show'); clearTimeout(TI); TI=setTimeout(()=>el.classList.remove('show'),2600); }

// INIT
renderSubjList();
document.getElementById('fi-date').value = new Date().toISOString().split('T')[0];
</script>
</body>
</html>
