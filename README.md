# CSO-Gyms
[index.html](https://github.com/user-attachments/files/28428945/index.html)
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<meta name="apple-mobile-web-app-capable" content="yes">
<title>ホームジム トレーニング管理</title>
<style>
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
body{font-family:-apple-system,'Hiragino Sans','Yu Gothic UI',sans-serif;background:#1a1a1a;color:#f0ede6;min-height:100vh}
:root{
  --green:#2dbd8c;--green-light:#1a3d30;--green-dark:#a8f0d8;
  --amber:#f0a030;--amber-light:#3d2e0a;--amber-dark:#ffd080;
  --blue:#5090e0;--blue-light:#0e2040;--blue-dark:#a0c8ff;
  --coral:#e06050;--coral-light:#3d1510;--coral-dark:#ffb0a0;
  --purple:#8878e8;--purple-light:#1e1840;--purple-dark:#c8b8ff;
  --bg:#1a1a1a;--surface:#252525;--surface2:#2e2e2e;
  --border:#3a3a3a;--border2:#4a4a4a;
  --text:#f0ede6;--text2:#b0ada6;--text3:#787570;
  --radius:12px;--radius-lg:16px;
}
.app{display:flex;flex-direction:column;min-height:100vh;max-width:1024px;margin:0 auto}

/* HEADER */
.header{background:#202020;border-bottom:1px solid var(--border);padding:16px 20px;display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;z-index:100}
.header h1{font-size:20px;font-weight:700;color:var(--text)}
.header .sub{font-size:13px;color:var(--text3);margin-top:3px}
.header-right{font-size:13px;color:var(--text2);text-align:right;line-height:1.6}

/* TABS */
.tabs{display:flex;background:#202020;border-bottom:1px solid var(--border)}
.tab{flex:1;padding:14px 6px;border:none;background:transparent;font-size:14px;font-weight:600;color:var(--text3);cursor:pointer;display:flex;flex-direction:column;align-items:center;gap:4px;border-bottom:3px solid transparent;transition:all 0.15s}
.tab .tab-icon{font-size:22px}
.tab.active{color:var(--green);border-bottom-color:var(--green)}

/* CONTENT */
.content{padding:16px;flex:1}
.panel{display:none}
.panel.active{display:block}

/* CARDS */
.card{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius-lg);padding:16px 18px;margin-bottom:14px}
.card-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:12px}
.card-title{font-size:16px;font-weight:700;color:var(--text)}
.badge{font-size:12px;padding:4px 10px;border-radius:8px;font-weight:600}
.badge-green{background:var(--green-light);color:var(--green-dark)}
.badge-blue{background:var(--blue-light);color:var(--blue-dark)}
.badge-amber{background:var(--amber-light);color:var(--amber-dark)}
.badge-coral{background:var(--coral-light);color:var(--coral-dark)}
.badge-purple{background:var(--purple-light);color:var(--purple-dark)}

/* SECTION TITLE */
.sec-title{font-size:15px;font-weight:700;color:var(--text2);margin:18px 0 10px;display:flex;align-items:center;gap:8px}
.sec-dot{width:10px;height:10px;border-radius:50%;flex-shrink:0}

/* STAT */
.stat-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:16px}
.stat-card{background:var(--surface2);border-radius:var(--radius);padding:14px;text-align:center;border:1px solid var(--border)}
.stat-label{font-size:13px;color:var(--text3);margin-bottom:6px}
.stat-value{font-size:32px;font-weight:700;color:var(--text);line-height:1}
.stat-unit{font-size:13px;color:var(--text3);margin-top:4px}
.week-dots{display:flex;gap:8px;margin-top:8px;justify-content:center}
.week-dot{width:14px;height:14px;border-radius:50%;background:var(--border);border:1px solid var(--border2)}
.week-dot.done{background:var(--green);border-color:var(--green)}

/* DURATION */
.dur-toggle{display:flex;gap:8px;margin-bottom:14px;align-items:center}
.dur-label{font-size:14px;color:var(--text2);font-weight:600}
.dur-btn{padding:10px 24px;border-radius:24px;border:1.5px solid var(--border2);background:transparent;font-size:14px;font-weight:700;cursor:pointer;color:var(--text2);transition:all 0.15s}
.dur-btn.sel{background:var(--blue);color:#fff;border-color:var(--blue)}

/* EXERCISE */
.ex-row{display:flex;align-items:center;gap:12px;padding:10px 0;border-top:1px solid var(--border)}
.ex-row:first-child{border-top:none}
.ex-check{width:28px;height:28px;border-radius:50%;border:2px solid var(--border2);cursor:pointer;display:flex;align-items:center;justify-content:center;flex-shrink:0;transition:all 0.2s;font-size:15px;font-weight:700}
.ex-check.done{background:var(--green);border-color:var(--green);color:#fff}
.ex-main{flex:1;min-width:0}
.ex-name{font-size:15px;color:var(--text);line-height:1.4;font-weight:500}
.ex-name.done{text-decoration:line-through;color:var(--text3)}
.ex-detail{font-size:13px;color:var(--text3);margin-top:3px}
.ex-caution{font-size:12px;color:var(--coral-dark);background:var(--coral-light);padding:3px 8px;border-radius:6px;white-space:nowrap;flex-shrink:0;font-weight:600}

/* WALK */
.walk-meta{font-size:14px;color:var(--text2);margin-bottom:12px;line-height:1.6}
.walk-controls{display:flex;align-items:center;gap:14px;margin-bottom:12px;flex-wrap:wrap}
.walk-timer{font-size:40px;font-weight:700;color:var(--text);min-width:110px;font-variant-numeric:tabular-nums}
.walk-btn{padding:12px 24px;border-radius:var(--radius);border:none;font-size:15px;font-weight:700;cursor:pointer}
.walk-start{background:var(--green);color:#fff}
.walk-stop{background:var(--coral);color:#fff}
.walk-reset{background:var(--surface2);color:var(--text2);border:1px solid var(--border2)}
.progress-wrap{background:var(--surface2);border-radius:6px;height:10px;overflow:hidden;margin-bottom:8px}
.progress-bar{height:100%;background:var(--green);border-radius:6px;transition:width 0.5s}
.walk-note{font-size:13px;color:var(--text3);line-height:1.5}

/* NOTES */
.notes-area{width:100%;border:1px solid var(--border);border-radius:var(--radius);padding:12px 14px;font-size:15px;font-family:inherit;color:var(--text);background:var(--surface2);resize:vertical;min-height:90px;margin-top:8px}
.notes-area:focus{outline:none;border-color:var(--green)}
.notes-area::placeholder{color:var(--text3)}

/* COMPLETE BTN */
.complete-btn{width:100%;padding:16px;background:var(--green);color:#fff;border:none;border-radius:var(--radius);font-size:16px;font-weight:700;cursor:pointer;margin-top:14px;display:flex;align-items:center;justify-content:center;gap:10px}
.complete-btn:active{opacity:0.85}

/* ADD EXERCISE */
.add-section{background:var(--surface2);border:1.5px dashed var(--border2);border-radius:var(--radius-lg);padding:16px;margin-bottom:14px}
.add-title{font-size:15px;font-weight:700;color:var(--text2);margin-bottom:12px}
.add-form{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.add-input{padding:10px 12px;border:1px solid var(--border2);border-radius:var(--radius);background:var(--surface);color:var(--text);font-size:14px;font-family:inherit}
.add-input:focus{outline:none;border-color:var(--green)}
.add-input::placeholder{color:var(--text3)}
.add-select{padding:10px 12px;border:1px solid var(--border2);border-radius:var(--radius);background:var(--surface);color:var(--text);font-size:14px;font-family:inherit}
.add-btn{grid-column:1/-1;padding:12px;background:var(--blue);color:#fff;border:none;border-radius:var(--radius);font-size:15px;font-weight:700;cursor:pointer}
.add-btn:active{opacity:0.85}
.custom-badge{font-size:11px;padding:2px 7px;border-radius:5px;background:#3a2a50;color:#c8b8ff;font-weight:600;margin-left:6px}

/* SCHEDULE */
.week-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:6px;margin-bottom:18px}
.day-cell{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:10px 4px;text-align:center}
.day-cell.today{border:2px solid var(--green);background:var(--green-light)}
.day-cell.rest{background:var(--surface2)}
.day-name{font-size:12px;color:var(--text3);margin-bottom:4px;font-weight:600}
.day-num{font-size:18px;font-weight:700;color:var(--text)}
.day-type{font-size:10px;margin-top:4px;padding:3px 4px;border-radius:4px;line-height:1.2;font-weight:600}
.day-cell.today .day-type{background:var(--green);color:#fff}
.day-cell.rest .day-type{background:var(--border);color:var(--text3)}
.day-type-normal{background:var(--blue-light);color:var(--blue-dark)}

.program-row{display:flex;align-items:flex-start;gap:14px;padding:12px 0;border-top:1px solid var(--border)}
.program-row:first-child{border-top:none}
.prog-icon{width:44px;height:44px;border-radius:var(--radius);display:flex;align-items:center;justify-content:center;font-size:22px;flex-shrink:0}
.prog-upper{background:var(--blue-light)}
.prog-lower{background:var(--green-light)}
.prog-core{background:var(--amber-light)}
.prog-walk{background:var(--purple-light)}
.prog-rest{background:var(--surface2)}
.prog-content{flex:1}
.prog-day{font-size:12px;color:var(--text3);font-weight:600}
.prog-name{font-size:15px;font-weight:700;color:var(--text);margin:2px 0 4px}
.prog-desc{font-size:13px;color:var(--text2);line-height:1.5}
.prog-time{font-size:12px;color:var(--text3);margin-top:4px;font-weight:600}

.injury-box{background:var(--coral-light);border:1px solid #5a2010;border-radius:var(--radius-lg);padding:16px 18px}
.injury-item{font-size:14px;color:var(--coral-dark);padding:5px 0;line-height:1.6}

/* LIBRARY */
.filter-row{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:14px}
.filter-btn{padding:9px 16px;border-radius:24px;border:1.5px solid var(--border2);background:transparent;font-size:13px;font-weight:600;cursor:pointer;color:var(--text2);transition:all 0.15s}
.filter-btn.sel{background:var(--text);color:#1a1a1a;border-color:var(--text)}
.lib-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius-lg);padding:16px 18px;margin-bottom:12px}
.lib-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:8px}
.lib-name{font-size:15px;font-weight:700;color:var(--text)}
.lib-tags{display:flex;gap:5px;flex-wrap:wrap;margin-bottom:8px}
.tag{font-size:11px;padding:3px 8px;border-radius:5px;font-weight:600}
.tag-upper{background:var(--blue-light);color:var(--blue-dark)}
.tag-lower{background:var(--green-light);color:var(--green-dark)}
.tag-core{background:var(--amber-light);color:var(--amber-dark)}
.tag-walk{background:var(--purple-light);color:var(--purple-dark)}
.tag-ball{background:#1a3020;color:#80e8a0}
.tag-mball{background:#2a1a30;color:#d0a0ff}
.tag-dips{background:#0e2a3a;color:#80d0ff}
.tag-roller{background:#1a2a10;color:#a0e060}
.tag-band{background:#2a1040;color:#e0a0ff}
.tag-stretch{background:#0a2a2a;color:#60e0d0}
.lib-desc{font-size:13px;color:var(--text2);line-height:1.6}
.lib-sets{font-size:13px;color:var(--text);font-weight:700;margin-top:8px}

/* HISTORY */
.hist-entry{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius-lg);padding:16px 18px;margin-bottom:12px}
.hist-date{font-size:12px;color:var(--text3);font-weight:600}
.hist-title{font-size:16px;font-weight:700;color:var(--text);margin:4px 0 8px}
.hist-stats{display:flex;gap:16px;flex-wrap:wrap}
.hist-stat{font-size:13px;color:var(--text2);font-weight:500}
.stars{display:flex;gap:4px;margin-top:10px;align-items:center}
.star{font-size:26px;cursor:pointer;color:var(--border2);transition:color 0.1s}
.star.filled{color:#f0a030}
.star-label{font-size:12px;color:var(--text3);margin-left:6px;font-weight:600}
.hist-note{font-size:13px;color:var(--text2);margin-top:10px;padding:10px 12px;background:var(--surface2);border-radius:var(--radius);line-height:1.6}
.empty{text-align:center;padding:60px 16px;color:var(--text3)}
.empty-icon{font-size:56px;margin-bottom:14px}
.empty-text{font-size:15px;line-height:1.6}
</style>
</head>
<body>
<div class="app">

<div class="header">
  <div>
    <h1>🏋️ ホームジム トレーニング</h1>
    <div class="sub">怪我に配慮した自宅プログラム</div>
  </div>
  <div class="header-right" id="dateDisplay"></div>
</div>

<div class="tabs">
  <button class="tab active" onclick="switchTab('today','tab0')" id="tab0"><span class="tab-icon">📅</span>今日</button>
  <button class="tab" onclick="switchTab('schedule','tab1')" id="tab1"><span class="tab-icon">🗓️</span>週間</button>
  <button class="tab" onclick="switchTab('library','tab2')" id="tab2"><span class="tab-icon">📋</span>種目</button>
  <button class="tab" onclick="switchTab('history','tab3')" id="tab3"><span class="tab-icon">🕐</span>記録</button>
</div>

<div class="content">

<!-- TODAY -->
<div class="panel active" id="panel-today">
  <div class="stat-grid">
    <div class="stat-card">
      <div class="stat-label">今週のトレーニング</div>
      <div class="stat-value" id="weekCount">0</div>
      <div class="stat-unit">/ 5 回</div>
      <div class="week-dots" id="weekDots"></div>
    </div>
    <div class="stat-card">
      <div class="stat-label">今日の完了種目</div>
      <div class="stat-value" id="doneCount">0</div>
      <div class="stat-unit">種目完了</div>
    </div>
  </div>

  <div class="dur-toggle">
    <span class="dur-label">今日の時間：</span>
    <button class="dur-btn sel" id="dur60" onclick="setDuration(60)">60分</button>
    <button class="dur-btn" id="dur30" onclick="setDuration(30)">30分</button>
  </div>

  <div class="sec-title"><span class="sec-dot" style="background:var(--amber)"></span>ウォームアップ（5分）</div>
  <div class="card" id="card-warmup"></div>

  <div class="sec-title"><span class="sec-dot" style="background:var(--blue)"></span>上半身トレーニング <span class="badge badge-blue" style="margin-left:auto;font-size:11px">猫背改善対応</span></div>
  <div class="card" id="card-upper"></div>

  <div class="sec-title"><span class="sec-dot" style="background:var(--green)"></span>下半身トレーニング <span class="badge badge-green" style="margin-left:auto;font-size:11px">膝・足首配慮</span></div>
  <div class="card" id="card-lower"></div>

  <div class="sec-title"><span class="sec-dot" style="background:var(--amber)"></span>体幹・バランスボール <span class="badge badge-amber" style="margin-left:auto;font-size:11px">腰痛配慮</span></div>
  <div class="card" id="card-core"></div>

  <div class="sec-title"><span class="sec-dot" style="background:var(--purple)"></span>ウォーキング（別メニュー）</div>
  <div class="card">
    <div class="card-header">
      <div class="card-title">ルームランナー ウォーキング</div>
      <span class="badge badge-purple">低衝撃</span>
    </div>
    <div class="walk-meta">目標：<span id="walkTarget">30</span>分 ｜ 傾斜1〜3° ｜ 速度4〜5km/h</div>
    <div class="walk-controls">
      <div class="walk-timer" id="walkTimer">00:00</div>
      <button class="walk-btn walk-start" id="walkBtn" onclick="toggleWalk()">開始</button>
      <button class="walk-btn walk-reset" onclick="resetWalk()">リセット</button>
    </div>
    <div class="progress-wrap"><div class="progress-bar" id="walkBar" style="width:0%"></div></div>
    <div class="walk-note">※ ウォーキングはトレーニング後、または別日に実施推奨。走らないこと。</div>
  </div>

  <div class="sec-title"><span class="sec-dot" style="background:#20a090"></span>ストレッチ・リカバリー（トレーニング後）</div>
  <div class="card">
    <div class="card-header">
      <div class="card-title">フォームローラー ＆ ストレッチポール</div>
      <span class="badge badge-green">毎日推奨</span>
    </div>
    <div class="ex-row"><div class="ex-check" onclick="toggleEx('s0',this)"></div><div class="ex-main"><div class="ex-name">ストレッチポール 背骨リセット</div><div class="ex-detail">5〜10分 仰向けに乗るだけ</div></div><div class="ex-caution">猫背改善</div></div>
    <div class="ex-row"><div class="ex-check" onclick="toggleEx('s1',this)"></div><div class="ex-main"><div class="ex-name">フォームローラー 大腿四頭筋ほぐし</div><div class="ex-detail">左右各60秒</div></div><div class="ex-caution">膝ケア</div></div>
    <div class="ex-row"><div class="ex-check" onclick="toggleEx('s2',this)"></div><div class="ex-main"><div class="ex-name">フォームローラー 背中・胸椎ほぐし</div><div class="ex-detail">60秒 × 2セット</div></div><div class="ex-caution">猫背改善</div></div>
    <div class="ex-row"><div class="ex-check" onclick="toggleEx('s3',this)"></div><div class="ex-main"><div class="ex-name">フォームローラー 臀部ほぐし</div><div class="ex-detail">左右各60秒</div></div><div class="ex-caution">腰痛ケア</div></div>
  </div>

  <div class="sec-title"><span class="sec-dot" style="background:var(--text3)"></span>今日のメモ</div>
  <textarea class="notes-area" id="todayNotes" placeholder="体調・痛みの具合・使用重量など..."></textarea>
  <button class="complete-btn" onclick="completeWorkout()">✓ トレーニング完了として記録する</button>
</div>

<!-- SCHEDULE -->
<div class="panel" id="panel-schedule">
  <div class="sec-title" style="margin-top:0"><span class="sec-dot" style="background:var(--green)"></span>今週のカレンダー</div>
  <div class="week-grid" id="weekGrid"></div>
  <div class="sec-title"><span class="sec-dot" style="background:var(--blue)"></span>週間プログラム</div>
  <div class="card" id="weeklyProg"></div>
  <div class="sec-title"><span class="sec-dot" style="background:var(--coral)"></span>怪我への対応メモ</div>
  <div class="injury-box" id="injuryBox"></div>
</div>

<!-- LIBRARY -->
<div class="panel" id="panel-library">
  <div class="filter-row">
    <button class="filter-btn sel" onclick="filterLib('all',this)">すべて</button>
    <button class="filter-btn" onclick="filterLib('upper',this)">上半身</button>
    <button class="filter-btn" onclick="filterLib('lower',this)">下半身</button>
    <button class="filter-btn" onclick="filterLib('core',this)">体幹</button>
    <button class="filter-btn" onclick="filterLib('ball',this)">バランスボール</button>
    <button class="filter-btn" onclick="filterLib('mball',this)">ウエイトボール</button>
    <button class="filter-btn" onclick="filterLib('dips',this)">ディップス</button>
    <button class="filter-btn" onclick="filterLib('roller',this)">腹筋ローラー</button>
    <button class="filter-btn" onclick="filterLib('band',this)">ヒップバンド</button>
    <button class="filter-btn" onclick="filterLib('stretch',this)">ストレッチ</button>
    <button class="filter-btn" onclick="filterLib('walk',this)">ウォーキング</button>
  </div>
  <div id="libList"></div>
</div>

<!-- HISTORY -->
<div class="panel" id="panel-history">
  <div id="histList"></div>
</div>

</div>
</div>

<script>
const DAYS_JP=['日','月','火','水','木','金','土'];

const warmupData=[
  {name:'肩回し・首ストレッチ',detail:'前後各10回',caution:null},
  {name:'キャットカウ（四つん這い・背中丸め反らし）',detail:'10回ゆっくり',caution:'腰に注意'},
  {name:'足首回し・ふくらはぎストレッチ',detail:'各方向10秒',caution:'手術後は様子見'},
];
const upperFull=[
  {name:'ダンベル チェストプレス（ベンチ仰向け）',detail:'10kg × 3セット × 10回',caution:null},
  {name:'ダンベル ロウ（片手・ベンチ支持）',detail:'15kg × 3セット × 10回',caution:null},
  {name:'ダンベル ショルダープレス',detail:'7kg × 3セット × 12回',caution:'肩痛時は軽量'},
  {name:'ダンベル カール',detail:'10kg × 3セット × 12回',caution:null},
  {name:'フェイスプル（BARWINGマシン）',detail:'3セット × 15回',caution:'猫背改善'},
  {name:'ケトルベルスイング（低強度）',detail:'12kg × 3セット × 15回',caution:'腰に注意'},
  {name:'ディップス',detail:'自重 × 3セット × 5〜8回',caution:'肩痛時は浅く'},
  {name:'ネガティブ懸垂',detail:'3セット × 5回（5秒下ろす）',caution:'補助つきでもOK'},
];
const upperShort=[
  {name:'ダンベル チェストプレス',detail:'10kg × 2セット × 12回',caution:null},
  {name:'ダンベル ロウ',detail:'15kg × 2セット × 12回',caution:null},
  {name:'フェイスプル（BARWINGマシン）',detail:'2セット × 15回',caution:'猫背改善'},
];
const lowerFull=[
  {name:'ハーフスクワット（ダンベル持ち）',detail:'10kg × 3セット × 12回',caution:'痛みは浅めに'},
  {name:'ヒップスラスト（ベンチ使用）',detail:'17kg × 3セット × 12回',caution:'臀部強化'},
  {name:'ヒップヒンジ / RDL',detail:'15kg × 3セット × 10回',caution:'背中まっすぐ'},
  {name:'レッグエクステンション（BARWINGマシン）',detail:'3セット × 15回',caution:'大腿四頭筋'},
  {name:'カーフレイズ（ゆっくり）',detail:'自重 × 3セット × 20回',caution:'足首ゆっくり'},
  {name:'バンド グルートブリッジ',detail:'中強度 × 3セット × 15回',caution:'臀部に効かせる'},
  {name:'バンド クラムシェル',detail:'軽〜中強度 × 3セット × 左右15回',caution:'膝安定'},
];
const lowerShort=[
  {name:'ハーフスクワット（ダンベル）',detail:'10kg × 2セット × 12回',caution:'痛みは浅めに'},
  {name:'ヒップスラスト（ベンチ）',detail:'自重 × 2セット × 15回',caution:'臀部強化'},
  {name:'カーフレイズ',detail:'自重 × 2セット × 20回',caution:'足首ゆっくり'},
  {name:'バンド クラムシェル',detail:'軽強度 × 2セット × 左右15回',caution:'膝安定'},
];
const coreFull=[
  {name:'プランク',detail:'30秒 × 3セット',caution:'腰が下がらないよう'},
  {name:'バードドッグ（対角手足伸ばし）',detail:'左右10回 × 3セット',caution:'腰痛改善'},
  {name:'グルートブリッジ',detail:'3セット × 15回',caution:'腰・臀部強化'},
  {name:'バランスボール 腹筋ロール',detail:'3セット × 10回',caution:'腰注意・ゆっくり'},
  {name:'バランスボール 体幹キープ（座位）',detail:'30秒 × 3セット',caution:'姿勢改善'},
  {name:'ウエイトボール ロシアンツイスト',detail:'10kg × 2セット × 左右10回',caution:'腰注意'},
  {name:'膝つき腹筋ローラー',detail:'3セット × 8回',caution:'腰が反らないよう'},
];
const coreShort=[
  {name:'プランク',detail:'30秒 × 2セット',caution:'腰に注意'},
  {name:'グルートブリッジ',detail:'2セット × 15回',caution:'腰・臀部強化'},
  {name:'バランスボール 体幹キープ（座位）',detail:'30秒 × 2セット',caution:'姿勢改善'},
];

const weeklyData=[
  {day:'月曜日',label:'上半身A + 体幹',dur:'60分',type:'upper',icon:'💪',desc:'胸・背中中心。ダンベル＋BARWINGマシン'},
  {day:'火曜日',label:'下半身A + ウォーキング',dur:'60分',type:'lower',icon:'🦵',desc:'大腿四頭筋・臀部。低衝撃スクワット'},
  {day:'水曜日',label:'体幹 + バランスボール',dur:'30分',type:'core',icon:'🔥',desc:'軽め。姿勢改善・腰痛予防・バランスボール'},
  {day:'木曜日',label:'上半身B + ディップス',dur:'60分',type:'upper',icon:'💪',desc:'肩・腕・背中。ディップス・ネガティブ懸垂も'},
  {day:'金曜日',label:'下半身B + ウォーキング',dur:'60分',type:'lower',icon:'🦵',desc:'ふくらはぎ・臀部・体幹の複合'},
  {day:'土曜日',label:'完全休養',dur:'休み',type:'rest',icon:'😴',desc:'畑仕事もOK！軽いストレッチ推奨'},
  {day:'日曜日',label:'ウォーキングのみ（任意）',dur:'30分',type:'walk',icon:'🚶',desc:'ルームランナーでリカバリー歩行'},
];
const injuryItems=[
  '🦵 膝靭帯：スクワットは浅め・ゆっくり。痛みが出たら即中止',
  '🦶 足首：カーフレイズはゆっくり丁寧に。跳ぶ・走る系は禁止',
  '🔙 腰痛：ヒップヒンジ時は背中まっすぐを徹底。重量より形重視',
  '🏃 ランニング禁止：ルームランナーは速歩き（4〜5km/h）のみ',
  '🤸 懸垂：補助つきで週1〜2回まで。無理は禁物',
  '💪 肩・首：ショルダープレスは痛みが出たら軽量に変更',
  '🪑 猫背対策：フェイスプル・バードドッグを毎回必ず実施',
  '⚽ バランスボール：座位から始めて無理なく体幹を鍛える',
  '🩷 ヒップバンド：膝の安定性向上にも効果的。強度は軽→中→強の順で慣らす',
  '🧘 ストレッチポール：毎日乗るだけで猫背・腰痛改善。トレーニング後に必ず実施',
  '🫀 フォームローラー：痛い部分はゆっくり圧をかける。強く転がしすぎない',
];

const libraryData=[
  {name:'ダンベル チェストプレス',cat:'upper',tags:['上半身','胸'],desc:'ベンチに仰向けになりダンベルを押し上げる。大胸筋を鍛える基本種目。',sets:'10〜15kg × 3セット × 10〜12回'},
  {name:'ダンベル ロウ（片手）',cat:'upper',tags:['上半身','背中','猫背改善'],desc:'片手でベンチを支えにダンベルを引き上げる。広背筋・菱形筋を強化し猫背改善に有効。',sets:'15〜17kg × 3セット × 10回'},
  {name:'ダンベル ショルダープレス',cat:'upper',tags:['上半身','肩'],desc:'肩より上にダンベルを押し上げる。肩が痛む場合は7kg以下で行う。',sets:'7〜10kg × 3セット × 12回'},
  {name:'フェイスプル',cat:'upper',tags:['上半身','猫背改善','肩'],desc:'BARWINGマシンでケーブルを顔に向けて引く。巻き肩・猫背の改善に最重要種目。毎回必ず実施。',sets:'3セット × 15回（軽重量・丁寧に）'},
  {name:'ダンベル カール',cat:'upper',tags:['上半身','腕'],desc:'肘を固定してダンベルを曲げる。上腕二頭筋強化。ゆっくり下ろすことで効果アップ。',sets:'10kg × 3セット × 12回'},
  {name:'ケトルベルスイング',cat:'upper',tags:['上半身','全身','有酸素'],desc:'ケトルベルを股間から肩の高さまで振り上げる。全身有酸素＋臀部強化。腰の状態を確認しながら実施。',sets:'12〜16kg × 3セット × 15回'},
  {name:'ハーフスクワット（浅め）',cat:'lower',tags:['下半身','大腿四頭筋','膝配慮'],desc:'膝が痛む場合は浅めのスクワット。椅子から立ち上がる動作からスタートしてもOK。',sets:'ダンベル10kg × 3セット × 12回'},
  {name:'レッグエクステンション',cat:'lower',tags:['下半身','大腿四頭筋'],desc:'BARWINGマシンで脚を伸ばして大腿四頭筋を集中強化。スクワットが辛い場合の代替種目。',sets:'3セット × 15回'},
  {name:'ヒップスラスト',cat:'lower',tags:['下半身','臀部'],desc:'ベンチに肩を乗せ、ダンベルを腰に置いて腰を持ち上げる。臀部強化の最重要種目。膝・腰への負担が少ない。',sets:'自重 → 17〜20kg × 3セット × 12回'},
  {name:'ヒップヒンジ（RDL）',cat:'lower',tags:['下半身','臀部','ハムストリング'],desc:'腰をまっすぐ保ったまま上体を前傾。ハムストリング・臀部・姿勢改善に効果的。背中が丸まらないよう注意。',sets:'15kg × 3セット × 10回'},
  {name:'カーフレイズ',cat:'lower',tags:['下半身','ふくらはぎ','足首配慮'],desc:'つま先立ちをゆっくり繰り返す。ふくらはぎ強化。足首の状態に合わせてゆっくり行う。',sets:'自重 × 3セット × 20回（ゆっくり）'},
  {name:'プランク',cat:'core',tags:['体幹','腰痛予防'],desc:'うつ伏せで肘とつま先で体を支える。腰が下がらないよう注意。腰痛改善の基本種目。',sets:'30秒 × 3セット'},
  {name:'バードドッグ',cat:'core',tags:['体幹','腰痛予防','猫背改善'],desc:'四つん這いで対角線の手足をゆっくり伸ばす。体幹安定・腰痛予防の最重要種目。',sets:'左右各10回 × 3セット'},
  {name:'グルートブリッジ',cat:'core',tags:['体幹','臀部','腰痛予防'],desc:'仰向けで膝を曲げ腰を持ち上げる。臀部と体幹を同時強化。腰痛がある人でも安全に行える。',sets:'3セット × 15回'},
  {name:'バランスボール 体幹キープ（座位）',cat:'ball',tags:['バランスボール','体幹','姿勢改善'],desc:'バランスボールに座って体幹を安定させる。猫背・姿勢改善に効果的。PC作業の合間にもおすすめ。',sets:'30秒 × 3セット'},
  {name:'バランスボール 腹筋ロール',cat:'ball',tags:['バランスボール','体幹','腹筋'],desc:'ボールに前腕を乗せて前後に転がす。腹筋・体幹強化。腰が反らないよう注意。',sets:'3セット × 10回'},
  {name:'バランスボール ヒップリフト',cat:'ball',tags:['バランスボール','臀部','体幹'],desc:'仰向けでボールに足を乗せて腰を持ち上げる。臀部・ハムストリング強化。バランス感覚も鍛えられる。',sets:'3セット × 12回'},
  {name:'バランスボール 背中伸ばし',cat:'ball',tags:['バランスボール','姿勢改善','腰痛予防'],desc:'ボールに背中をあてて後ろに反る。背中・腰のストレッチ。PC業務後の疲労回復に。',sets:'30秒 × 2セット'},
  {name:'メディシンボール スクワット',cat:'mball',tags:['ウエイトボール','下半身','大腿四頭筋'],desc:'10kgボールを胸に抱えてスクワット。膝が痛む場合は浅めに。上半身が安定しやすい。',sets:'10kg × 3セット × 12回'},
  {name:'メディシンボール ロシアンツイスト',cat:'mball',tags:['ウエイトボール','体幹','腹斜筋'],desc:'座位でボールを持ち左右に体をひねる。腹斜筋・体幹強化。腰痛がある場合は軽く回転させる程度でOK。',sets:'10kg × 3セット × 左右10回'},
  {name:'メディシンボール チェストパス（壁）',cat:'mball',tags:['ウエイトボール','上半身','胸'],desc:'壁に向かってボールを押し出す。大胸筋・三頭筋強化。軽い爆発的な動きで筋力・瞬発力向上。',sets:'3セット × 10回'},
  {name:'メディシンボール デッドリフト',cat:'mball',tags:['ウエイトボール','下半身','臀部'],desc:'ボールを床から持ち上げる。臀部・ハムストリング・背中の強化。背中まっすぐを徹底すること。',sets:'10kg × 3セット × 10回'},
  {name:'メディシンボール スラム（低強度）',cat:'mball',tags:['ウエイトボール','全身','有酸素'],desc:'ボールを頭上から床に叩きつける。全身を使う有酸素種目。腰・膝に注意してゆっくり行う。',sets:'3セット × 10回'},
  {name:'ディップス（自重）',cat:'dips',tags:['ディップス','上半身','胸・三頭筋'],desc:'ディップススタンドで体を上下させる。大胸筋下部・上腕三頭筋・肩前部を強化。肘を曲げる角度は90度まで。肩に痛みがある場合は可動域を狭めて行う。',sets:'自重 × 3セット × 5〜8回（できる回数から）'},
  {name:'アシスト懸垂（チューブ補助）',cat:'dips',tags:['ディップス','上半身','背中'],desc:'懸垂マシンで補助を使いながら懸垂。広背筋・上腕二頭筋強化。現在補助つきで5回できるので、少しずつ補助を減らしていく。',sets:'補助つき × 3セット × 5回'},
  {name:'ネガティブ懸垂（ゆっくり下ろす）',cat:'dips',tags:['ディップス','上半身','背中'],desc:'台に乗って懸垂の上の位置からスタートし、ゆっくり5秒かけて下ろす。筋力強化に効果的。懸垂が1回しかできない場合の最適な練習法。',sets:'3セット × 3〜5回（5秒かけて下ろす）'},
  {name:'ハンギングニーレイズ',cat:'dips',tags:['ディップス','体幹','腹筋'],desc:'懸垂マシンにぶら下がり膝を胸に引き寄せる。腹筋・体幹強化。肩・腕への負荷も軽くかかる。腰への負担が少ない。',sets:'3セット × 10〜15回'},
  {name:'L字ハング（キープ）',cat:'dips',tags:['ディップス','体幹','腹筋'],desc:'懸垂マシンにぶら下がり脚を水平に保つ。体幹・腸腰筋の強化。難しければ膝を曲げた状態でもOK。',sets:'15〜30秒 × 3セット'},
  {name:'膝つき腹筋ローラー（初級）',cat:'roller',tags:['腹筋ローラー','体幹','腹筋'],desc:'膝をついた状態でローラーを前に転がして戻す。初心者向け。腰が反らないよう腹に力を入れて行う。腰痛がある場合はまずこちらから。',sets:'3セット × 8〜10回'},
  {name:'腹筋ローラー 壁あてロール',cat:'roller',tags:['腹筋ローラー','体幹','腹筋'],desc:'壁から30〜50cm離れてローラーを転がし壁に当てて戻す。可動域を制限した安全なやり方。腰への負担を最小限に抑えられる。',sets:'3セット × 10回'},
  {name:'腹筋ローラー 立ちロール（上級）',cat:'roller',tags:['腹筋ローラー','体幹','腹筋'],desc:'立った状態からローラーを前に転がす。非常に強度が高い。まずは膝つきで十分な筋力をつけてから挑戦。腰痛時は禁止。',sets:'できる回数 × 3セット（目標5回）'},
  {name:'腹筋ローラー サイドロール',cat:'roller',tags:['腹筋ローラー','体幹','腹斜筋'],desc:'斜め方向にローラーを転がす。腹斜筋・脇腹を強化。まず膝つき正面ができてから追加する。',sets:'左右各5回 × 3セット'},
  {name:'バンド ヒップアブダクション（横歩き）',cat:'band',tags:['ヒップバンド','臀部','太もも'],desc:'バンドを膝上に巻いてカニ歩き。中臀筋・外転筋を強化。膝の安定性向上にも効果的。膝の靭帯ケアにもおすすめ。',sets:'強度：軽〜中 × 3セット × 左右15歩'},
  {name:'バンド グルートブリッジ',cat:'band',tags:['ヒップバンド','臀部','体幹'],desc:'バンドを膝上に巻いてヒップリフト。通常より臀部への負荷が大幅アップ。腰痛予防・美尻づくりに最適。',sets:'強度：中 × 3セット × 15回'},
  {name:'バンド スクワット',cat:'band',tags:['ヒップバンド','下半身','大腿四頭筋'],desc:'バンドを膝上に巻いてスクワット。膝が内側に入るのを防ぐ。膝の安定性向上と臀部の活性化が同時にできる。',sets:'強度：軽〜中 × 3セット × 12回'},
  {name:'バンド クラムシェル',cat:'band',tags:['ヒップバンド','臀部','中臀筋'],desc:'横向きに寝てバンドを膝上に巻き、膝を貝のように開閉する。中臀筋・外旋筋の強化。膝・腰の安定性向上に最適。',sets:'強度：軽〜中 × 3セット × 左右15回'},
  {name:'バンド キックバック（四つん這い）',cat:'band',tags:['ヒップバンド','臀部','ハムストリング'],desc:'四つん這いでバンドを足首に巻き後ろに蹴り上げる。大臀筋・ハムストリング強化。美尻・桃尻づくりの定番種目。',sets:'強度：中〜強 × 3セット × 左右12回'},
  {name:'バンド サイドライイングアブダクション',cat:'band',tags:['ヒップバンド','臀部','太もも'],desc:'横向きに寝てバンドを膝上に巻き、上の脚を持ち上げる。外転筋・中臀筋の集中強化。美脚づくりに効果的。',sets:'強度：中 × 3セット × 左右15回'},
  {name:'フォームローラー 大腿四頭筋ほぐし',cat:'stretch',tags:['フォームローラー','リカバリー','膝ケア'],desc:'うつ伏せで太ももの前面をローラーでほぐす。膝への負担を軽減する効果あり。膝の靭帯が痛む場合のケアに最適。痛い部分は圧を弱めてゆっくり。',sets:'左右各60秒 × 2セット'},
  {name:'フォームローラー 腸脛靭帯ほぐし',cat:'stretch',tags:['フォームローラー','リカバリー','膝ケア'],desc:'横向きで太ももの外側（腸脛靭帯）をほぐす。膝の外側の痛みに効果的。ゆっくり転がして痛い部分で止めて圧をかける。',sets:'左右各60秒 × 2セット'},
  {name:'フォームローラー 背中・胸椎ほぐし',cat:'stretch',tags:['フォームローラー','リカバリー','猫背改善'],desc:'仰向けでローラーを背中の下に置き前後に転がす。胸椎の可動域改善・猫背改善に効果的。PC業務後のケアに最適。',sets:'60秒 × 2セット'},
  {name:'フォームローラー 臀部・梨状筋ほぐし',cat:'stretch',tags:['フォームローラー','リカバリー','腰痛ケア'],desc:'座位でローラーに臀部を乗せてほぐす。梨状筋・臀部の張りをほぐして腰痛改善に効果的。片側ずつ体重をかける。',sets:'左右各60秒 × 2セット'},
  {name:'フォームローラー ふくらはぎほぐし',cat:'stretch',tags:['フォームローラー','リカバリー','足首ケア'],desc:'床に座りふくらはぎの下にローラーを置いてほぐす。足首の柔軟性向上・ふくらはぎの疲労回復に効果的。',sets:'左右各60秒 × 2セット'},
  {name:'ストレッチポール 背骨リセット',cat:'stretch',tags:['ストレッチポール','リカバリー','猫背改善'],desc:'ポールを背骨に沿って縦に置き仰向けに乗る。重力で背骨・胸椎が自然に伸びる。猫背・巻き肩改善の基本。5〜10分乗るだけでOK。',sets:'5〜10分 × 毎日推奨'},
  {name:'ストレッチポール 肩甲骨ほぐし',cat:'stretch',tags:['ストレッチポール','リカバリー','肩こり'],desc:'ポールに仰向けに乗り腕を左右に広げてゆっくり動かす。肩甲骨まわりをほぐす。肩・首の痛みケアに効果的。',sets:'左右各30秒 × 3セット'},
  {name:'ストレッチポール 腰椎ストレッチ',cat:'stretch',tags:['ストレッチポール','リカバリー','腰痛ケア'],desc:'ポールを腰の下に横置きして仰向けに乗る。腰椎のアーチを整える。腰痛持ちに特に効果的。痛みが出たら中止。',sets:'60秒 × 2セット'},
  {name:'ストレッチポール 股関節ストレッチ',cat:'stretch',tags:['ストレッチポール','リカバリー','下半身'],desc:'ポールに仰向けに乗り膝を曲げて左右にゆっくり倒す。股関節・内転筋のストレッチ。下半身トレーニング後のケアに最適。',sets:'左右各30秒 × 3セット'},
  {name:'ルームランナー ウォーキング',cat:'walk',tags:['ウォーキング','有酸素','低衝撃'],desc:'傾斜1〜3°、速度4〜5km/hで速歩き。膝・足首への衝撃を最小限に。脂肪燃焼・体力向上に。走らないこと。',sets:'30〜60分 ｜ 週3〜5回'},
];

let duration=60;
let checked={};
let customExercises=JSON.parse(localStorage.getItem('hgCustomEx')||'[]');
let walkOn=false,walkSec=0,walkIv=null;
let hist=JSON.parse(localStorage.getItem('hgHist')||'[]');
let wkCnt=parseInt(localStorage.getItem('hgWk')||'0');
let wkMon=localStorage.getItem('hgMon')||'';

function checkNewWeek(){
  const now=new Date();
  const mon=getMondayStr(now);
  if(mon!==wkMon){wkCnt=0;wkMon=mon;localStorage.setItem('hgMon',mon);localStorage.setItem('hgWk','0');}
}
function getMondayStr(d){
  const dt=new Date(d);const day=dt.getDay();
  dt.setDate(dt.getDate()-day+(day===0?-6:1));
  return dt.toDateString();
}

function setDuration(d){
  duration=d;
  document.getElementById('dur60').classList.toggle('sel',d===60);
  document.getElementById('dur30').classList.toggle('sel',d===30);
  renderToday();
}

function getCustomByCategory(cat){
  return customExercises.filter(e=>e.cat===cat);
}

function renderToday(){
  const up=duration===60?upperFull:upperShort;
  const lo=duration===60?lowerFull:lowerShort;
  const co=duration===60?coreFull:coreShort;
  renderExList('card-warmup',warmupData,'w',[]);
  renderExList('card-upper',up,'u',getCustomByCategory('upper'));
  renderExList('card-lower',lo,'l',getCustomByCategory('lower'));
  renderExList('card-core',[...co,...getCustomByCategory('ball')],'c',getCustomByCategory('core'));
  updateCounts();
  updateWeekDots();
}

function renderExList(id,data,prefix,extra){
  const all=[...data,...extra];
  let html=all.map((e,i)=>{
    const k=prefix+i;
    const done=checked[k];
    const isCustom=i>=data.length;
    return `<div class="ex-row">
      <div class="ex-check${done?' done':''}" onclick="toggleEx('${k}',this)">${done?'✓':''}</div>
      <div class="ex-main">
        <div class="ex-name${done?' done':''}">${e.name}${isCustom?'<span class="custom-badge">追加</span>':''}</div>
        <div class="ex-detail">${e.detail}</div>
      </div>
      ${e.caution?`<div class="ex-caution">${e.caution}</div>`:''}
    </div>`;
  }).join('');
  document.getElementById(id).innerHTML=html;
}

function toggleEx(k,el){
  checked[k]=!checked[k];
  el.classList.toggle('done',checked[k]);
  el.textContent=checked[k]?'✓':'';
  const row=el.parentElement;
  const nm=row.querySelector('.ex-name');
  if(nm)nm.classList.toggle('done',checked[k]);
  updateCounts();
}

function updateCounts(){
  const cnt=Object.values(checked).filter(Boolean).length;
  document.getElementById('doneCount').textContent=cnt;
}

function updateWeekDots(){
  let h='';
  for(let i=0;i<5;i++) h+=`<div class="week-dot${i<wkCnt?' done':''}"></div>`;
  document.getElementById('weekDots').innerHTML=h;
  document.getElementById('weekCount').textContent=wkCnt;
}

function toggleWalk(){
  if(!walkOn){
    walkOn=true;
    document.getElementById('walkBtn').textContent='停止';
    document.getElementById('walkBtn').className='walk-btn walk-stop';
    walkIv=setInterval(()=>{walkSec++;updWalk();},1000);
  } else {
    walkOn=false;
    document.getElementById('walkBtn').textContent='再開';
    document.getElementById('walkBtn').className='walk-btn walk-start';
    clearInterval(walkIv);
  }
}
function resetWalk(){
  walkOn=false;clearInterval(walkIv);walkSec=0;
  document.getElementById('walkBtn').textContent='開始';
  document.getElementById('walkBtn').className='walk-btn walk-start';
  updWalk();
}
function updWalk(){
  const m=Math.floor(walkSec/60),s=walkSec%60;
  document.getElementById('walkTimer').textContent=pad(m)+':'+pad(s);
  const pct=Math.min(100,Math.round((walkSec/1800)*100));
  document.getElementById('walkBar').style.width=pct+'%';
}
function pad(n){return String(n).padStart(2,'0');}

function completeWorkout(){
  const done=Object.values(checked).filter(Boolean).length;
  const all=warmupData.length+(duration===60?upperFull.length+lowerFull.length+coreFull.length:upperShort.length+lowerShort.length+coreShort.length);
  const note=document.getElementById('todayNotes').value;
  hist.unshift({date:new Date().toLocaleDateString('ja-JP'),dur:duration,done:done,total:all,walk:Math.floor(walkSec/60),note:note,stars:0});
  if(hist.length>50)hist.pop();
  localStorage.setItem('hgHist',JSON.stringify(hist));
  wkCnt=Math.min(5,wkCnt+1);
  localStorage.setItem('hgWk',String(wkCnt));
  checked={};renderToday();resetWalk();
  document.getElementById('todayNotes').value='';
  alert('✅ トレーニングを記録しました！\nお疲れ様でした！');
  switchTab('history','tab3');renderHistory();
}

function renderWeekGrid(){
  const today=new Date();const dow=today.getDay();
  const labels=['休養','上半身','下半身','体幹','上半身','下半身','歩行'];
  let h='';
  DAYS_JP.forEach((d,i)=>{
    const dt=new Date(today);dt.setDate(today.getDate()+(i-dow));
    const cls=i===dow?'today':(i===0||i===6?'rest':'');
    h+=`<div class="day-cell ${cls}"><div class="day-name">${d}</div><div class="day-num">${dt.getDate()}</div><div class="day-type">${labels[i]}</div></div>`;
  });
  document.getElementById('weekGrid').innerHTML=h;
}

function renderWeeklyProg(){
  const colors={upper:'prog-upper',lower:'prog-lower',core:'prog-core',walk:'prog-walk',rest:'prog-rest'};
  document.getElementById('weeklyProg').innerHTML=weeklyData.map(p=>`
    <div class="program-row">
      <div class="prog-icon ${colors[p.type]}">${p.icon}</div>
      <div class="prog-content">
        <div class="prog-day">${p.day}</div>
        <div class="prog-name">${p.label}</div>
        <div class="prog-desc">${p.desc}</div>
        <div class="prog-time">⏱ ${p.dur}</div>
      </div>
    </div>`).join('');
  document.getElementById('injuryBox').innerHTML=injuryItems.map(t=>`<div class="injury-item">${t}</div>`).join('');
}

function renderLibrary(cat){
  const allData=[...libraryData,...customExercises.map(e=>({...e,tags:[e.cat==='upper'?'上半身':e.cat==='lower'?'下半身':e.cat==='ball'?'バランスボール':'体幹','追加種目']}))];
  const data=cat==='all'?allData:allData.filter(e=>e.cat===cat);
  const tc={upper:'tag-upper',lower:'tag-lower',core:'tag-core',walk:'tag-walk',ball:'tag-ball',mball:'tag-mball',dips:'tag-dips',roller:'tag-roller',band:'tag-band',stretch:'tag-stretch'};
  const bc={upper:'badge-blue',lower:'badge-green',core:'badge-amber',walk:'badge-purple',ball:'badge-green',mball:'badge-amber',dips:'badge-blue',roller:'badge-amber',band:'badge-purple',stretch:'badge-green'};
  const bl={upper:'上半身',lower:'下半身',core:'体幹',walk:'歩行',ball:'ボール',mball:'ウエイトB',dips:'ディップス',roller:'腹筋ローラー',band:'ヒップバンド',stretch:'ストレッチ'};
  let html=`<div class="add-section">
    <div class="add-title">➕ 種目を追加する</div>
    <div class="add-form">
      <input class="add-input" id="newName" placeholder="種目名（例：ダンベルフライ）" style="grid-column:1/-1">
      <input class="add-input" id="newDetail" placeholder="セット数・回数（例：3セット×12回）">
      <input class="add-input" id="newCaution" placeholder="注意点（任意）">
      <select class="add-select" id="newCat">
        <option value="upper">上半身</option>
        <option value="lower">下半身</option>
        <option value="core">体幹</option>
        <option value="ball">バランスボール</option>
        <option value="mball">ウエイトボール</option>
        <option value="dips">ディップス・懸垂</option>
        <option value="roller">腹筋ローラー</option>
        <option value="band">ヒップバンド</option>
        <option value="stretch">ストレッチ・リカバリー</option>
      </select>
      <button class="add-btn" onclick="addExercise()">追加する</button>
    </div>
  </div>`;
  html+=data.map((e,idx)=>{
    const isCustom=idx>=libraryData.length||(e.tags&&e.tags.includes('追加種目'));
    return `<div class="lib-card">
      <div class="lib-header">
        <div class="lib-name">${e.name}${isCustom?'<span class="custom-badge">追加</span>':''}</div>
        <span class="badge ${bc[e.cat]||'badge-blue'}">${bl[e.cat]||e.cat}</span>
      </div>
      <div class="lib-tags">${(e.tags||[]).map(t=>`<span class="tag ${tc[e.cat]||'tag-upper'}">${t}</span>`).join('')}</div>
      <div class="lib-desc">${e.desc||''}</div>
      <div class="lib-sets">📋 ${e.sets||e.detail||''}</div>
      ${isCustom?`<button onclick="removeCustomEx(${customExercises.indexOf(e)})" style="margin-top:8px;padding:6px 12px;background:var(--coral-light);color:var(--coral-dark);border:none;border-radius:6px;font-size:12px;font-weight:700;cursor:pointer">削除</button>`:''}
    </div>`;
  }).join('');
  document.getElementById('libList').innerHTML=html;
}

function addExercise(){
  const name=document.getElementById('newName').value.trim();
  const detail=document.getElementById('newDetail').value.trim();
  const caution=document.getElementById('newCaution').value.trim();
  const cat=document.getElementById('newCat').value;
  if(!name){alert('種目名を入力してください');return;}
  customExercises.push({name,detail:detail||'記録なし',caution:caution||null,cat,sets:detail||'記録なし',desc:'追加した種目です',tags:[cat==='upper'?'上半身':cat==='lower'?'下半身':cat==='ball'?'バランスボール':'体幹','追加種目']});
  localStorage.setItem('hgCustomEx',JSON.stringify(customExercises));
  renderLibrary('all');
  renderToday();
  alert('✅ 種目を追加しました！');
}

function removeCustomEx(idx){
  if(!confirm('この種目を削除しますか？'))return;
  customExercises.splice(idx,1);
  localStorage.setItem('hgCustomEx',JSON.stringify(customExercises));
  renderLibrary('all');renderToday();
}

function filterLib(cat,btn){
  document.querySelectorAll('.filter-btn').forEach(b=>b.classList.remove('sel'));
  btn.classList.add('sel');
  renderLibrary(cat);
}

function renderHistory(){
  const el=document.getElementById('histList');
  if(!hist.length){
    el.innerHTML='<div class="empty"><div class="empty-icon">🏆</div><div class="empty-text">まだ記録がありません。<br>最初のトレーニングを完了しましょう！</div></div>';
    return;
  }
  el.innerHTML=hist.map((h,idx)=>`
    <div class="hist-entry">
      <div class="hist-date">${h.date}</div>
      <div class="hist-title">${h.dur}分トレーニング — ${h.done}/${h.total}種目完了</div>
      <div class="hist-stats">
        <span class="hist-stat">⏱ ${h.dur}分</span>
        <span class="hist-stat">🚶 ウォーキング${h.walk}分</span>
        ${h.note?'<span class="hist-stat">📝 メモあり</span>':''}
      </div>
      <div class="stars">
        ${[1,2,3,4,5].map(s=>`<span class="star${h.stars>=s?' filled':''}" onclick="rateStar(${idx},${s})">★</span>`).join('')}
        <span class="star-label">達成度</span>
      </div>
      ${h.note?`<div class="hist-note">${h.note}</div>`:''}
    </div>`).join('');
}

function rateStar(idx,s){
  hist[idx].stars=s;
  localStorage.setItem('hgHist',JSON.stringify(hist));
  renderHistory();
}

function switchTab(name,tabId){
  document.querySelectorAll('.panel').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
  document.getElementById('panel-'+name).classList.add('active');
  document.getElementById(tabId).classList.add('active');
  if(name==='schedule'){renderWeekGrid();renderWeeklyProg();}
  if(name==='history')renderHistory();
  if(name==='library')renderLibrary('all');
}

function init(){
  checkNewWeek();
  const now=new Date();
  document.getElementById('dateDisplay').innerHTML=
    `${now.getFullYear()}年${now.getMonth()+1}月${now.getDate()}日（${DAYS_JP[now.getDay()]}）`;
  updateWeekDots();renderToday();
}
init();
</script>
</body>
</html>
