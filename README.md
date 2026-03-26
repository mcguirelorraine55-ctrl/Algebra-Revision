[Angle_Explorer_Game.html](https://github.com/user-attachments/files/26274846/Angle_Explorer_Game.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Angle Explorer 📐</title>
<link href="https://fonts.googleapis.com/css2?family=Baloo+2:wght@400;600;700;800&family=Nunito:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#f0f4ff;
  --card:#ffffff;
  --card2:#f7f9ff;
  --border:#dde3f5;
  --navy:#1a2e5a;
  --blue:#3a6fd8;
  --teal:#00b4a6;
  --yellow:#ffcc00;
  --orange:#ff8c42;
  --pink:#ff5fa0;
  --green:#22c55e;
  --red:#ef4444;
  --text:#1a2e5a;
  --muted:#6b7db3;
  --light:#eef1fc;
}
body{font-family:'Nunito',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;display:flex;flex-direction:column;align-items:center;padding:20px 16px 60px;background-image:radial-gradient(circle at 20% 20%,#dce8ff 0%,transparent 50%),radial-gradient(circle at 80% 80%,#ffe8f5 0%,transparent 50%);}
h1{font-family:'Baloo 2',cursive;font-size:2.6rem;font-weight:800;color:var(--navy);text-align:center;line-height:1.1;margin-bottom:4px;}
h1 span{color:var(--blue);}
.tagline{color:var(--muted);font-size:1rem;text-align:center;margin-bottom:28px;font-weight:600;}

/* SCREENS */
.screen{width:100%;max-width:660px;display:none;flex-direction:column;align-items:center;gap:20px;}
.screen.active{display:flex;}

/* CARDS */
.card{background:var(--card);border:2px solid var(--border);border-radius:20px;padding:28px 30px;width:100%;box-shadow:0 4px 24px rgba(58,111,216,.07);}
.card h2{font-family:'Baloo 2',cursive;font-size:1.7rem;font-weight:800;color:var(--navy);margin-bottom:10px;}

/* BUTTONS */
.btn{font-family:'Baloo 2',cursive;font-size:1.1rem;font-weight:700;border:none;border-radius:14px;padding:13px 28px;cursor:pointer;transition:transform .12s,box-shadow .12s;letter-spacing:.3px;}
.btn:active{transform:scale(.97);}
.btn-primary{background:var(--blue);color:#fff;box-shadow:0 4px 14px rgba(58,111,216,.3);}
.btn-primary:hover{box-shadow:0 6px 20px rgba(58,111,216,.4);}
.btn-teal{background:var(--teal);color:#fff;box-shadow:0 4px 14px rgba(0,180,166,.3);}
.btn-orange{background:var(--orange);color:#fff;box-shadow:0 4px 14px rgba(255,140,66,.3);}
.btn-outline{background:transparent;border:2px solid var(--border);color:var(--muted);font-family:'Baloo 2',cursive;font-size:1rem;font-weight:700;border-radius:14px;padding:11px 22px;cursor:pointer;transition:all .2s;}
.btn-outline:hover{border-color:var(--blue);color:var(--blue);}

/* NAME INPUT */
.name-wrap{display:flex;gap:10px;flex-wrap:wrap;justify-content:center;margin-top:16px;}
.name-input{font-family:'Nunito',sans-serif;font-size:1.1rem;font-weight:700;background:var(--light);border:2px solid var(--border);border-radius:12px;color:var(--text);padding:12px 18px;outline:none;width:260px;transition:border-color .2s;}
.name-input:focus{border-color:var(--blue);}

/* LEVEL GRID */
.levels-grid{display:grid;grid-template-columns:1fr 1fr;gap:14px;width:100%;}
.lcard{background:var(--card);border:2.5px solid var(--border);border-radius:18px;padding:20px 16px;text-align:center;cursor:pointer;transition:border-color .2s,transform .15s,box-shadow .15s;box-shadow:0 2px 12px rgba(58,111,216,.06);}
.lcard:hover:not(.locked){border-color:var(--blue);transform:translateY(-3px);box-shadow:0 6px 20px rgba(58,111,216,.13);}
.lcard.locked{opacity:.45;cursor:not-allowed;filter:grayscale(.4);}
.lcard.done{border-color:var(--green);}
.lcard .lnum{font-family:'Baloo 2',cursive;font-size:2.2rem;font-weight:800;color:var(--blue);}
.lcard.done .lnum{color:var(--green);}
.lcard.locked .lnum{color:var(--muted);}
.lcard .ltitle{font-size:.95rem;font-weight:800;color:var(--navy);margin:4px 0 6px;}
.lcard .lbadge{font-size:.75rem;font-weight:700;background:var(--light);border-radius:8px;padding:3px 10px;color:var(--muted);display:inline-block;}
.lcard.done .lbadge{background:#dcfce7;color:#166534;}
.lcard.locked .lbadge{background:#f1f1f1;}
.done-tick{font-size:1rem;margin-left:4px;}
.export-row{width:100%;display:flex;justify-content:center;margin-top:4px;}

/* CONFIDENCE */
.conf-card{background:var(--card);border:2px solid var(--border);border-radius:20px;padding:24px 28px;width:100%;text-align:center;box-shadow:0 4px 24px rgba(58,111,216,.07);}
.conf-card h2{font-family:'Baloo 2',cursive;font-size:1.5rem;font-weight:800;color:var(--navy);margin-bottom:8px;}
.conf-card p{color:var(--muted);font-size:.95rem;font-weight:600;margin-bottom:18px;}
.face-row{display:flex;justify-content:center;gap:10px;flex-wrap:wrap;margin-bottom:20px;}
.fface{background:var(--light);border:3px solid var(--border);border-radius:16px;padding:10px 12px;cursor:pointer;transition:all .18s;text-align:center;min-width:72px;}
.fface:hover{border-color:var(--yellow);transform:scale(1.08);}
.fface.sel{border-color:var(--blue);background:#eef3ff;box-shadow:0 0 0 3px rgba(58,111,216,.15);}
.fface .face-emoji{font-size:2rem;display:block;}
.fface .face-lbl{font-size:.68rem;font-weight:800;color:var(--muted);margin-top:3px;line-height:1.2;}

/* PROGRESS */
.prog-header{width:100%;display:flex;justify-content:space-between;align-items:center;font-size:.85rem;font-weight:700;color:var(--muted);}
.prog-wrap{width:100%;background:var(--card);border:2px solid var(--border);border-radius:10px;height:14px;overflow:hidden;}
.prog-fill{height:100%;border-radius:8px;transition:width .4s ease;}
.prog-fill.l1{background:linear-gradient(90deg,#3a6fd8,#00b4a6);}
.prog-fill.l2{background:linear-gradient(90deg,#ff8c42,#ffcc00);}
.prog-fill.l3{background:linear-gradient(90deg,#ff5fa0,#ff8c42);}
.prog-fill.l4{background:linear-gradient(90deg,#7c3aed,#3a6fd8);}

/* QUESTION CARD */
.qcard{background:var(--card);border:2px solid var(--border);border-radius:20px;padding:24px 26px;width:100%;box-shadow:0 4px 24px rgba(58,111,216,.07);}
.qcard-top{display:flex;justify-content:space-between;align-items:center;margin-bottom:14px;}
.q-label{font-size:.8rem;font-weight:800;color:var(--muted);text-transform:uppercase;letter-spacing:1px;}
.score-pill{background:var(--light);border-radius:20px;padding:4px 14px;font-weight:800;color:var(--blue);font-size:.9rem;}
.q-text{font-size:1.1rem;font-weight:700;color:var(--navy);margin-bottom:16px;line-height:1.5;}

/* SVG diagram */
.svg-area{display:flex;justify-content:center;margin-bottom:16px;}
.svg-area svg{border-radius:14px;background:var(--light);border:1.5px solid var(--border);}

/* MC */
.mc-wrap{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
.mc-opt{background:var(--light);border:2.5px solid var(--border);border-radius:13px;color:var(--navy);font-family:'Nunito',sans-serif;font-size:1rem;font-weight:800;padding:13px 10px;cursor:pointer;transition:all .18s;text-align:center;}
.mc-opt:hover:not(:disabled){border-color:var(--blue);background:#eef3ff;}
.mc-opt.correct{border-color:var(--green);background:#dcfce7;color:#166534;}
.mc-opt.wrong{border-color:var(--red);background:#fee2e2;color:#991b1b;}
.mc-opt:disabled{cursor:not-allowed;}

/* TEXT INPUT */
.text-row{display:flex;gap:10px;flex-wrap:wrap;align-items:center;}
.ans-input{font-family:'Nunito',sans-serif;font-size:1.2rem;font-weight:800;background:var(--light);border:2.5px solid var(--border);border-radius:12px;color:var(--text);padding:12px 16px;outline:none;flex:1;min-width:150px;transition:border-color .2s;text-transform:uppercase;}
.ans-input:focus{border-color:var(--blue);}
.check-btn{font-family:'Baloo 2',cursive;font-size:1rem;font-weight:700;background:var(--teal);color:#fff;border:none;border-radius:12px;padding:12px 20px;cursor:pointer;white-space:nowrap;}
.check-btn:disabled{opacity:.5;cursor:not-allowed;}

/* FEEDBACK */
.feedback{border-radius:12px;padding:12px 16px;font-weight:700;font-size:.95rem;margin-top:12px;display:none;line-height:1.5;}
.feedback.ok{background:#dcfce7;border:2px solid #86efac;color:#166534;display:block;}
.feedback.bad{background:#fee2e2;border:2px solid #fca5a5;color:#991b1b;display:block;}
.next-btn{display:none;align-self:flex-end;margin-top:10px;}
.next-btn.show{display:block;}

/* RESULTS */
.results-card{background:var(--card);border:2px solid var(--border);border-radius:20px;padding:28px;width:100%;text-align:center;box-shadow:0 4px 24px rgba(58,111,216,.07);}
.results-card h2{font-family:'Baloo 2',cursive;font-size:2rem;font-weight:800;color:var(--navy);margin-bottom:6px;}
.big-score{font-family:'Baloo 2',cursive;font-size:4.5rem;font-weight:800;line-height:1;margin:8px 0 4px;}
.score-msg{font-size:1rem;font-weight:700;color:var(--muted);margin-bottom:18px;}
.breakdown-grid{display:grid;grid-template-columns:repeat(5,1fr);gap:6px;margin:14px 0 20px;}
.bg-hdr{background:var(--light);border-radius:8px;padding:6px 4px;font-size:.72rem;font-weight:800;color:var(--muted);text-align:center;}
.bg-cell{border-radius:8px;padding:8px 4px;font-size:.9rem;font-weight:800;text-align:center;}
.bg-cell.ok{background:#dcfce7;color:#166534;}
.bg-cell.no{background:#fee2e2;color:#991b1b;}
.bg-cell.q{background:var(--light);color:var(--navy);font-size:.8rem;}

/* RESPONSIVE */
@media(max-width:480px){
  h1{font-size:2rem;}
  .levels-grid{grid-template-columns:1fr;}
  .mc-wrap{grid-template-columns:1fr;}
  .breakdown-grid{grid-template-columns:repeat(3,1fr);}
  .card,.qcard,.conf-card,.results-card{padding:18px 16px;}
}
</style>
</head>
<body>

<h1>📐 <span>Angle</span> Explorer</h1>
<p class="tagline">Master angles — one level at a time!</p>

<!-- ══════════ WELCOME ══════════ -->
<div class="screen active" id="s-welcome">
  <div class="card" style="text-align:center;">
    <h2>Welcome! 👋</h2>
    <p style="color:var(--muted);font-weight:600;line-height:1.6;margin-bottom:6px;">
      This game has <strong style="color:var(--blue)">4 levels</strong> all about angles.<br>
      Complete each level to unlock the next one!
    </p>
    <div class="name-wrap">
      <input class="name-input" id="name-input" type="text" placeholder="What's your name?" maxlength="40" />
      <button class="btn btn-primary" onclick="goConfPre()">Let's go! 🚀</button>
    </div>
  </div>
</div>

<!-- ══════════ PRE-CONFIDENCE ══════════ -->
<div class="screen" id="s-conf-pre">
  <div class="conf-card">
    <h2>Before we start… 🤔</h2>
    <p id="pre-conf-msg">How confident are you with <strong style="color:var(--blue)">angles</strong> right now?</p>
    <div class="face-row">
      <div class="fface" onclick="pickFace('pre',1)"><span class="face-emoji">😟</span><span class="face-lbl">Not<br>sure</span></div>
      <div class="fface" onclick="pickFace('pre',2)"><span class="face-emoji">😕</span><span class="face-lbl">A<br>little</span></div>
      <div class="fface" onclick="pickFace('pre',3)"><span class="face-emoji">🙂</span><span class="face-lbl">OK-<br>ish</span></div>
      <div class="fface" onclick="pickFace('pre',4)"><span class="face-emoji">😊</span><span class="face-lbl">Pretty<br>good</span></div>
      <div class="fface" onclick="pickFace('pre',5)"><span class="face-emoji">🤩</span><span class="face-lbl">Very<br>confident</span></div>
    </div>
    <button class="btn btn-primary" id="pre-next-btn" onclick="goLevels()" style="opacity:.35;pointer-events:none;">Continue →</button>
  </div>
</div>

<!-- ══════════ LEVEL SELECT ══════════ -->
<div class="screen" id="s-levels">
  <div style="width:100%;text-align:center;">
    <span style="font-weight:800;color:var(--muted);font-size:.95rem;">Playing as: </span>
    <span id="name-tag" style="font-weight:800;color:var(--blue);font-size:1rem;">—</span>
  </div>
  <div class="levels-grid">
    <div class="lcard" id="lc1" onclick="startLevel(1)">
      <div class="lnum">1</div>
      <div class="ltitle">Name That Angle</div>
      <div class="lbadge">Multiple choice</div>
    </div>
    <div class="lcard locked" id="lc2" onclick="startLevel(2)">
      <div class="lnum">2</div>
      <div class="ltitle">Real-Life Angles</div>
      <div class="lbadge">Multiple choice</div>
    </div>
    <div class="lcard locked" id="lc3" onclick="startLevel(3)">
      <div class="lnum">3</div>
      <div class="ltitle">Letter Names</div>
      <div class="lbadge">Type your answer</div>
    </div>
    <div class="lcard locked" id="lc4" onclick="startLevel(4)">
      <div class="lnum">4</div>
      <div class="ltitle">Mixed Challenge</div>
      <div class="lbadge">All types</div>
    </div>
  </div>
  <div class="export-row">
    <button class="btn btn-orange" onclick="exportCSV()">📊 Download My Results (CSV)</button>
  </div>
</div>

<!-- ══════════ GAME ══════════ -->
<div class="screen" id="s-game">
  <div class="prog-header">
    <span id="g-prog-txt">Question 1 of 10</span>
    <span id="g-score-txt">Score: 0 / 10</span>
  </div>
  <div class="prog-wrap"><div class="prog-fill" id="g-prog-bar" style="width:0%"></div></div>

  <div class="qcard">
    <div class="qcard-top">
      <span class="q-label" id="g-qlabel">Level 1 · Q1</span>
      <span class="score-pill">⭐ <span id="g-score">0</span></span>
    </div>
    <div class="q-text" id="g-qtext">Question text here</div>
    <div class="svg-area" id="g-svg" style="display:none;"></div>
    <div class="mc-wrap" id="g-mc"></div>
    <div class="text-row" id="g-textrow" style="display:none;">
      <input class="ans-input" id="g-input" type="text" placeholder="e.g.  ABC" maxlength="20" />
      <button class="check-btn" id="g-check" onclick="checkText()">Check ✓</button>
    </div>
    <div class="feedback" id="g-feedback"></div>
    <button class="btn btn-teal next-btn" id="g-next" onclick="nextQ()">Next →</button>
  </div>
</div>

<!-- ══════════ RESULTS + POST-CONFIDENCE ══════════ -->
<div class="screen" id="s-results">
  <div class="results-card">
    <h2 id="r-title">Level 1 Complete! 🎉</h2>
    <div class="big-score" id="r-score" style="color:var(--blue);">8 / 10</div>
    <div class="score-msg" id="r-msg">Great work!</div>
    <div class="breakdown-grid" id="r-breakdown"></div>
  </div>
  <div class="conf-card">
    <h2>How do you feel now? 😊</h2>
    <p id="post-conf-msg">After completing this level — how confident are you with <strong style="color:var(--blue)">angles</strong>?</p>
    <div class="face-row">
      <div class="fface" onclick="pickFace('post',1)"><span class="face-emoji">😟</span><span class="face-lbl">Still<br>unsure</span></div>
      <div class="fface" onclick="pickFace('post',2)"><span class="face-emoji">😕</span><span class="face-lbl">A<br>little</span></div>
      <div class="fface" onclick="pickFace('post',3)"><span class="face-emoji">🙂</span><span class="face-lbl">Getting<br>there</span></div>
      <div class="fface" onclick="pickFace('post',4)"><span class="face-emoji">😊</span><span class="face-lbl">Pretty<br>good</span></div>
      <div class="fface" onclick="pickFace('post',5)"><span class="face-emoji">🤩</span><span class="face-lbl">Got<br>it!</span></div>
    </div>
    <button class="btn btn-primary" id="post-next-btn" onclick="afterLevel()" style="opacity:.35;pointer-events:none;">Back to Levels →</button>
  </div>
</div>

<!-- ══════════ JAVASCRIPT ══════════ -->
<script>
// ─── STATE ───────────────────────────────────────────────
let studentName = '';
let confPre = 0, confPost = {};
let curLevel = 0, curQs = [], curIdx = 0, curScore = 0;
let answered = false;
let selConfPre = 0, selConfPost = 0;
let allResults = {}; // {1:[{q,qtext,correct,given,mark},...], ...}
let levelsUnlocked = [1]; // starts with only level 1

// ─── SVG HELPERS ─────────────────────────────────────────
function pt(cx,cy,r,deg){
  const rad=deg*Math.PI/180;
  return {x:cx+r*Math.cos(rad), y:cy-r*Math.sin(rad)};
}

function angleSVG(type, size=200){
  const cx=size/2, cy=size/2+12, r=68;
  const cols={acute:'#3a6fd8',right:'#00b4a6',obtuse:'#ff8c42',straight:'#ff5fa0',reflex:'#7c3aed',full:'#22c55e'};
  const col=cols[type]||'#3a6fd8';
  let lines='', arc='', lbl='';
  function arcSVG(a1,a2,ar,sweep=1){
    const p1=pt(cx,cy,ar,a1),p2=pt(cx,cy,ar,a2);
    const large=Math.abs(a2-a1)>180?1:0;
    return `<path d="M${p1.x},${p1.y} A${ar},${ar} 0 ${large} ${sweep} ${p2.x},${p2.y}" fill="none" stroke="${col}" stroke-width="2.5" stroke-linecap="round"/>`;
  }
  if(type==='acute'){
    const p1=pt(cx,cy,r,0),p2=pt(cx,cy,r,50);
    lines=`<line x1="${cx}" y1="${cy}" x2="${p1.x}" y2="${p1.y}" stroke="${col}" stroke-width="3" stroke-linecap="round"/>
           <line x1="${cx}" y1="${cy}" x2="${p2.x}" y2="${p2.y}" stroke="${col}" stroke-width="3" stroke-linecap="round"/>`;
    arc=arcSVG(0,50,30);
    const lp=pt(cx,cy,46,25);
    lbl=`<text x="${lp.x}" y="${lp.y}" text-anchor="middle" fill="${col}" font-size="12" font-family="Nunito" font-weight="700">50°</text>`;
  } else if(type==='right'){
    const p1=pt(cx,cy,r,0),p2=pt(cx,cy,r,90);
    lines=`<line x1="${cx}" y1="${cy}" x2="${p1.x}" y2="${p1.y}" stroke="${col}" stroke-width="3" stroke-linecap="round"/>
           <line x1="${cx}" y1="${cy}" x2="${p2.x}" y2="${p2.y}" stroke="${col}" stroke-width="3" stroke-linecap="round"/>`;
    const sq=12;
    lines+=`<polyline points="${cx+sq},${cy} ${cx+sq},${cy-sq} ${cx},${cy-sq}" fill="none" stroke="${col}" stroke-width="2.2"/>`;
    lbl=`<text x="${cx+28}" y="${cy-22}" fill="${col}" font-size="12" font-family="Nunito" font-weight="700">90°</text>`;
  } else if(type==='obtuse'){
    const p1=pt(cx,cy,r,0),p2=pt(cx,cy,r,130);
    lines=`<line x1="${cx}" y1="${cy}" x2="${p1.x}" y2="${p1.y}" stroke="${col}" stroke-width="3" stroke-linecap="round"/>
           <line x1="${cx}" y1="${cy}" x2="${p2.x}" y2="${p2.y}" stroke="${col}" stroke-width="3" stroke-linecap="round"/>`;
    arc=arcSVG(0,130,32);
    const lp=pt(cx,cy,50,65);
    lbl=`<text x="${lp.x}" y="${lp.y}" text-anchor="middle" fill="${col}" font-size="12" font-family="Nunito" font-weight="700">130°</text>`;
  } else if(type==='straight'){
    lines=`<line x1="${cx-r}" y1="${cy}" x2="${cx+r}" y2="${cy}" stroke="${col}" stroke-width="3" stroke-linecap="round"/>
           <line x1="${cx}" y1="${cy}" x2="${cx}" y2="${cy}" stroke="${col}" stroke-width="3"/>`;
    arc=arcSVG(0,180,30);
    lbl=`<text x="${cx}" y="${cy-38}" text-anchor="middle" fill="${col}" font-size="12" font-family="Nunito" font-weight="700">180°</text>`;
  } else if(type==='reflex'){
    const p1=pt(cx,cy,r,0),p2=pt(cx,cy,r,290);
    lines=`<line x1="${cx}" y1="${cy}" x2="${p1.x}" y2="${p1.y}" stroke="${col}" stroke-width="3" stroke-linecap="round"/>
           <line x1="${cx}" y1="${cy}" x2="${p2.x}" y2="${p2.y}" stroke="${col}" stroke-width="3" stroke-linecap="round"/>`;
    arc=arcSVG(0,290,34,0);
    const lp=pt(cx,cy,52,145);
    lbl=`<text x="${lp.x}" y="${lp.y}" text-anchor="middle" fill="${col}" font-size="12" font-family="Nunito" font-weight="700">290°</text>`;
  } else if(type==='full'){
    lines=`<circle cx="${cx}" cy="${cy}" r="${r}" fill="none" stroke="${col}" stroke-width="3"/>`;
    lbl=`<text x="${cx}" y="${cy+5}" text-anchor="middle" fill="${col}" font-size="13" font-family="Nunito" font-weight="700">360°</text>`;
  }
  return `<svg width="${size}" height="${size}" viewBox="0 0 ${size} ${size}">${arc}${lines}<circle cx="${cx}" cy="${cy}" r="5" fill="${col}"/>${lbl}</svg>`;
}

function letterSVG(A,B,C,deg,size=200){
  const ox=size/2, oy=size*0.62, r=72;
  const p1=pt(ox,oy,r,180);
  const p2=pt(ox,oy,r,180-deg);
  const labOff=18;
  const lx1=p1.x-labOff, lx2=(p2.x<ox)?p2.x-labOff:p2.x+4;
  const ly2=(p2.y<oy-5)?p2.y-10:p2.y+16;
  return `<svg width="${size}" height="${size}" viewBox="0 0 ${size} ${size}">
    <line x1="${p1.x}" y1="${p1.y}" x2="${ox}" y2="${oy}" stroke="#3a6fd8" stroke-width="3" stroke-linecap="round"/>
    <line x1="${ox}" y1="${oy}" x2="${p2.x}" y2="${p2.y}" stroke="#3a6fd8" stroke-width="3" stroke-linecap="round"/>
    <circle cx="${ox}" cy="${oy}" r="5" fill="#3a6fd8"/>
    <text x="${lx1}" y="${p1.y+5}" fill="#1a2e5a" font-size="16" font-family="Nunito" font-weight="800">${A}</text>
    <text x="${ox+7}" y="${oy+18}" fill="#1a2e5a" font-size="16" font-family="Nunito" font-weight="800">${B}</text>
    <text x="${lx2}" y="${ly2}" fill="#1a2e5a" font-size="16" font-family="Nunito" font-weight="800">${C}</text>
  </svg>`;
}

// ─── QUESTION BANKS ──────────────────────────────────────
const NAMES = ['Acute','Right','Obtuse','Straight','Reflex','Full revolution'];
const TYPES = ['acute','right','obtuse','straight','reflex','full'];
const DESCS = {
  acute:'Less than 90°',right:'Exactly 90°',obtuse:'Between 90° and 180°',
  straight:'Exactly 180°',reflex:'Between 180° and 360°',full:'Exactly 360°'
};

function shuffle(a){return [...a].sort(()=>Math.random()-.5);}
function pick(a,n){return shuffle(a).slice(0,n);}
function mcOpts(correct,pool){
  const wrong=pick(pool.filter(x=>x!==correct),3);
  return shuffle([correct,...wrong]);
}

function genL1(){
  // ensure all 6 types appear, then pad to 10 with random
  const base=shuffle(TYPES);
  const pool=[...base,...shuffle(TYPES)].slice(0,10);
  return pool.map(type=>{
    const correct=NAMES[TYPES.indexOf(type)];
    return{kind:'mc',svg:angleSVG(type),
      text:'What type of angle is shown in the diagram?',
      correct, opts:mcOpts(correct,NAMES), type};
  });
}

const L2_ITEMS=[
  {text:'The corner of a square piece of paper',type:'right',icon:'📄'},
  {text:"The hands of a clock showing 3 o'clock",type:'right',icon:'🕒'},
  {text:'The sharp tip of a freshly sharpened pencil',type:'acute',icon:'✏️'},
  {text:'A small slice of pizza with a narrow pointy end',type:'acute',icon:'🍕'},
  {text:'A book lying completely flat and open on a desk',type:'straight',icon:'📖'},
  {text:'A door pushed almost all the way back against a wall',type:'reflex',icon:'🚪'},
  {text:'The angle of a skateboard ramp (gentle slope)',type:'acute',icon:'🛹'},
  {text:"A clock showing 6 o'clock — the hands point straight up and down",type:'straight',icon:'🕕'},
  {text:'An elbow bent at more than a right angle but not flat',type:'obtuse',icon:'💪'},
  {text:'A spinning top completing one full rotation',type:'full',icon:'🌀'},
  {text:'A pair of scissors opened very wide',type:'obtuse',icon:'✂️'},
  {text:'The pointed corner of a triangle with a very sharp tip',type:'acute',icon:'🔺'},
  {text:'The corner of a rectangular door frame',type:'right',icon:'🚪'},
  {text:'A fan blade that has spun all the way back to the start',type:'full',icon:'🌪️'},
];

function genL2(){
  return pick(L2_ITEMS,10).map(item=>{
    const correct=NAMES[TYPES.indexOf(item.type)];
    return{kind:'mc',svg:'',
      text:`${item.icon}  ${item.text}\n\nWhat type of angle best describes this?`,
      correct, opts:mcOpts(correct,NAMES)};
  });
}

const L3_SETS=[
  {A:'A',B:'B',C:'C',deg:55},{A:'P',B:'Q',C:'R',deg:90},{A:'X',B:'Y',C:'Z',deg:125},
  {A:'D',B:'E',C:'F',deg:160},{A:'M',B:'N',C:'O',deg:35},{A:'J',B:'K',C:'L',deg:270},
  {A:'G',B:'H',C:'I',deg:180},{A:'S',B:'T',C:'U',deg:75},{A:'V',B:'W',C:'X',deg:110},
  {A:'E',B:'F',C:'G',deg:45},{A:'L',B:'M',C:'N',deg:95},{A:'R',B:'S',C:'T',deg:200},
];

function genL3(){
  return pick(L3_SETS,10).map(s=>{
    const correct=`${s.A}${s.B}${s.C}`;
    return{kind:'text',svg:letterSVG(s.A,s.B,s.C,s.deg),
      text:`The diagram shows an angle with three labelled points.\nUsing the letters, write the name of this angle.\n✏️ Hint: the middle letter is always the vertex (the corner).`,
      correct, accept:[correct,`ANGLE ${correct}`,`∠${correct}`],
      A:s.A,B:s.B,C:s.C};
  });
}

function genL4(){
  const pool=[];
  // value-based MC (4 questions)
  const valueQs=[
    {text:'An angle measures 47°. What type of angle is it?',correct:'Acute',opts:['Acute','Right','Obtuse','Reflex']},
    {text:'An angle measures 156°. What type of angle is it?',correct:'Obtuse',opts:['Obtuse','Acute','Straight','Reflex']},
    {text:'An angle measures 233°. What type of angle is it?',correct:'Reflex',opts:['Reflex','Obtuse','Straight','Full revolution']},
    {text:'An angle measures 90°. What type of angle is it?',correct:'Right',opts:['Right','Acute','Obtuse','Straight']},
    {text:'Which angle type is always greater than 180°?',correct:'Reflex',opts:['Reflex','Obtuse','Straight','Full revolution']},
    {text:'Which of these is NOT an acute angle?',correct:'95°',opts:['95°','45°','72°','13°']},
  ];
  shuffle(valueQs).slice(0,4).forEach(q=>{
    pool.push({kind:'mc',svg:'',text:q.text,correct:q.correct,opts:shuffle(q.opts)});
  });
  // diagram MC (3 questions — harder angles)
  ['reflex','obtuse','straight'].forEach(t=>{
    const correct=NAMES[TYPES.indexOf(t)];
    pool.push({kind:'mc',svg:angleSVG(t),text:'Name the type of angle shown:',correct,opts:mcOpts(correct,NAMES)});
  });
  // letter naming (3 questions)
  pick(L3_SETS,3).forEach(s=>{
    const correct=`${s.A}${s.B}${s.C}`;
    pool.push({kind:'text',svg:letterSVG(s.A,s.B,s.C,s.deg),
      text:`Name the angle below using the three letters shown (vertex in the middle):`,
      correct,accept:[correct,`ANGLE ${correct}`,`∠${correct}`]});
  });
  return shuffle(pool).slice(0,10);
}

// ─── NAV ─────────────────────────────────────────────────
function show(id){
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  window.scrollTo(0,0);
}

function goConfPre(){
  const n=document.getElementById('name-input').value.trim();
  if(!n){document.getElementById('name-input').focus();return;}
  studentName=n;
  document.getElementById('name-tag').textContent=n;
  document.getElementById('pre-conf-msg').innerHTML=`Hey <strong style="color:var(--blue)">${n}</strong>! How confident are you with <strong style="color:var(--blue)">angles</strong> right now?`;
  selConfPre=0;
  document.querySelectorAll('#s-conf-pre .fface').forEach(f=>f.classList.remove('sel'));
  lockBtn('pre-next-btn');
  show('s-conf-pre');
}

function goLevels(){
  confPre=selConfPre;
  refreshLevelCards();
  show('s-levels');
}

document.getElementById('name-input').addEventListener('keydown',e=>{if(e.key==='Enter')goConfPre();});

function pickFace(phase,val){
  const parent=phase==='pre'?'#s-conf-pre':'#s-results';
  document.querySelectorAll(`${parent} .fface`).forEach(f=>f.classList.remove('sel'));
  document.querySelectorAll(`${parent} .fface`)[val-1].classList.add('sel');
  if(phase==='pre'){selConfPre=val;unlockBtn('pre-next-btn');}
  else{selConfPost=val;unlockBtn('post-next-btn');}
}

function lockBtn(id){const b=document.getElementById(id);b.style.opacity='.35';b.style.pointerEvents='none';}
function unlockBtn(id){const b=document.getElementById(id);b.style.opacity='1';b.style.pointerEvents='auto';}

// ─── LEVEL START ─────────────────────────────────────────
function startLevel(lvl){
  if(!levelsUnlocked.includes(lvl))return;
  curLevel=lvl;curScore=0;curIdx=0;answered=false;selConfPost=0;
  if(lvl===1)curQs=genL1();
  else if(lvl===2)curQs=genL2();
  else if(lvl===3)curQs=genL3();
  else curQs=genL4();
  allResults[lvl]=[];
  const bar=document.getElementById('g-prog-bar');
  bar.className='prog-fill l'+lvl;
  loadQ();
  show('s-game');
}

function refreshLevelCards(){
  for(let i=1;i<=4;i++){
    const c=document.getElementById('lc'+i);
    c.classList.remove('locked','done');
    if(!levelsUnlocked.includes(i))c.classList.add('locked');
    if(allResults[i]&&allResults[i].length===10){
      c.classList.add('done');
      c.querySelector('.lbadge').textContent='✓ Done — '+allResults[i].reduce((a,r)=>a+r.mark,0)+'/10';
    }
  }
}

// ─── QUESTION RENDER ─────────────────────────────────────
function loadQ(){
  answered=false;
  const q=curQs[curIdx], total=curQs.length;
  document.getElementById('g-prog-txt').textContent=`Question ${curIdx+1} of ${total}`;
  document.getElementById('g-score-txt').textContent=`Score: ${curScore} / ${total}`;
  document.getElementById('g-score').textContent=curScore;
  document.getElementById('g-qlabel').textContent=`Level ${curLevel} · Q${curIdx+1}`;
  document.getElementById('g-prog-bar').style.width=`${(curIdx/total)*100}%`;
  document.getElementById('g-qtext').innerHTML=q.text.replace(/\n/g,'<br>');

  // SVG
  const svgEl=document.getElementById('g-svg');
  svgEl.innerHTML=q.svg||'';
  svgEl.style.display=q.svg?'flex':'none';

  // reset feedback / next
  const fb=document.getElementById('g-feedback');
  fb.className='feedback';fb.textContent='';
  document.getElementById('g-next').classList.remove('show');

  // MC vs text
  const mc=document.getElementById('g-mc');
  const tr=document.getElementById('g-textrow');
  mc.innerHTML='';

  if(q.kind==='mc'){
    mc.style.display='grid';tr.style.display='none';
    q.opts.forEach(opt=>{
      const b=document.createElement('button');
      b.className='mc-opt';b.textContent=opt;
      b.onclick=()=>checkMC(opt,q,b);
      mc.appendChild(b);
    });
  } else {
    mc.style.display='none';tr.style.display='flex';
    const inp=document.getElementById('g-input');
    inp.value='';inp.disabled=false;inp.style.borderColor='';
    document.getElementById('g-check').disabled=false;
    setTimeout(()=>inp.focus(),80);
  }
}

function checkMC(chosen,q,btn){
  if(answered)return;
  answered=true;
  const ok=chosen===q.correct;
  if(ok)curScore++;
  allResults[curLevel].push({q:curIdx+1,qtext:(q.text||'').replace(/<[^>]+>/g,'').replace(/\n/g,' ').substring(0,70),correct:q.correct,given:chosen,mark:ok?1:0});
  btn.classList.add(ok?'correct':'wrong');
  if(!ok){
    document.querySelectorAll('.mc-opt').forEach(b=>{
      if(b.textContent===q.correct)b.classList.add('correct');
    });
  }
  document.querySelectorAll('.mc-opt').forEach(b=>b.disabled=true);
  showFeedback(ok, ok?`✅ Correct! ${q.type?'"'+NAMES[TYPES.indexOf(q.type)]+'" — '+DESCS[q.type]:'Well done!'}`:`❌ Not quite — the answer was "${q.correct}"`);
  update();
}

function checkText(){
  if(answered)return;
  const raw=document.getElementById('g-input').value.trim().toUpperCase().replace(/\s+/g,' ');
  if(!raw){document.getElementById('g-input').focus();return;}
  answered=true;
  const q=curQs[curIdx];
  const accept=(q.accept||[q.correct]).map(a=>a.toUpperCase());
  const ok=accept.includes(raw)||accept.includes(raw.replace(/\s/g,''));
  if(ok)curScore++;
  allResults[curLevel].push({q:curIdx+1,qtext:q.text.replace(/\n/g,' ').substring(0,70),correct:q.correct,given:raw,mark:ok?1:0});
  const inp=document.getElementById('g-input');
  inp.disabled=true;inp.style.borderColor=ok?'var(--green)':'var(--red)';
  document.getElementById('g-check').disabled=true;
  showFeedback(ok,ok?`✅ Correct! The angle is named ${q.correct}. Always put the vertex letter in the middle.`:`❌ Not quite — the answer was ${q.correct}. The middle letter is always the vertex (corner) point.`);
  update();
}

document.getElementById('g-input').addEventListener('keydown',e=>{if(e.key==='Enter')checkText();});

function showFeedback(ok,msg){
  const fb=document.getElementById('g-feedback');
  fb.className='feedback '+(ok?'ok':'bad');
  fb.textContent=msg;
}

function update(){
  document.getElementById('g-score').textContent=curScore;
  document.getElementById('g-score-txt').textContent=`Score: ${curScore} / ${curQs.length}`;
  document.getElementById('g-next').classList.add('show');
}

function nextQ(){
  curIdx++;
  if(curIdx>=curQs.length)showResults();
  else loadQ();
}

// ─── RESULTS ─────────────────────────────────────────────
function showResults(){
  document.getElementById('g-prog-bar').style.width='100%';
  const res=allResults[curLevel]||[];
  const total=res.length, score=res.reduce((a,r)=>a+r.mark,0);
  document.getElementById('r-title').textContent=`Level ${curLevel} Complete! 🎉`;
  const scoreEl=document.getElementById('r-score');
  scoreEl.textContent=`${score} / ${total}`;
  const pct=score/total;
  scoreEl.style.color=pct>=.8?'var(--green)':pct>=.5?'var(--orange)':'var(--red)';

  const msgs=['Keep going — practice makes perfect! 💪','Good effort — you\'re getting there! 🙂','Solid work — well done! 👏','Great job — you really know your angles! 🌟','Outstanding — absolutely brilliant! 🏆'];
  document.getElementById('r-msg').textContent=msgs[Math.min(Math.floor(pct*5),4)];

  // breakdown
  const bd=document.getElementById('r-breakdown');
  bd.innerHTML='<div class="bg-hdr">Q</div><div class="bg-hdr">Mark</div><div class="bg-hdr">Q</div><div class="bg-hdr">Mark</div><div class="bg-hdr">Total</div>';
  for(let i=0;i<10;i+=2){
    const a=res[i]||{q:i+1,mark:'-'};
    const b=res[i+1]||{q:i+2,mark:null};
    bd.innerHTML+=`<div class="bg-cell q">Q${a.q}</div><div class="bg-cell ${a.mark===1?'ok':'no'}">${a.mark===1?'✓':'✗'}</div>`;
    if(b.mark!==null) bd.innerHTML+=`<div class="bg-cell q">Q${b.q}</div><div class="bg-cell ${b.mark===1?'ok':'no'}">${b.mark===1?'✓':'✗'}</div>`;
    else bd.innerHTML+=`<div class="bg-cell"></div><div class="bg-cell"></div>`;
    if(i===8) bd.innerHTML+=`<div class="bg-cell ok" style="font-weight:800;color:var(--blue)">${score}/10</div>`;
  }

  document.getElementById('post-conf-msg').innerHTML=`After completing <strong style="color:var(--blue)">Level ${curLevel}</strong> — how confident are you with angles?`;
  selConfPost=0;
  document.querySelectorAll('#s-results .fface').forEach(f=>f.classList.remove('sel'));
  lockBtn('post-next-btn');
  show('s-results');
}

function afterLevel(){
  confPost[curLevel]=selConfPost;
  // unlock next
  const next=curLevel+1;
  if(next<=4&&!levelsUnlocked.includes(next))levelsUnlocked.push(next);
  refreshLevelCards();
  show('s-levels');
}

// ─── CSV EXPORT ───────────────────────────────────────────
function exportCSV(){
  let csv='Student Name,Level,Question No,Question Summary,Correct Answer,Student Answer,Mark (1=Correct 0=Wrong)\n';
  let hasData=false;
  for(let lvl=1;lvl<=4;lvl++){
    const res=allResults[lvl]||[];
    if(res.length===0){
      csv+=`"${studentName}","Level ${lvl}",—,"No data recorded","—","—","—"\n`;
    } else {
      hasData=true;
      res.forEach(r=>{
        const qt=(r.qtext||'').replace(/"/g,"'");
        const co=(r.correct||'').replace(/"/g,"'");
        const gi=(r.given||'').replace(/"/g,"'");
        csv+=`"${studentName}","Level ${lvl}","${r.q}","${qt}","${co}","${gi}","${r.mark}"\n`;
      });
      const tot=res.reduce((a,x)=>a+x.mark,0);
      csv+=`"${studentName}","Level ${lvl} TOTAL","","","","","${tot}/10"\n`;
      const pre=confPre||'—';
      const post=confPost[lvl]||'—';
      csv+=`"${studentName}","Level ${lvl} Confidence Before","","","","","${pre}/5"\n`;
      csv+=`"${studentName}","Level ${lvl} Confidence After","","","","","${post}/5"\n`;
      csv+=`"","","","","","",""\n`;
    }
  }
  if(!hasData){alert('Complete at least one level before downloading results!');return;}
  const blob=new Blob([csv],{type:'text/csv;charset=utf-8;'});
  const url=URL.createObjectURL(blob);
  const a=document.createElement('a');
  a.href=url;
  a.download=`Angle_Results_${studentName.replace(/[^a-z0-9]/gi,'_')}.csv`;
  a.click();
  URL.revokeObjectURL(url);
}
</script>
</body>
</html>
