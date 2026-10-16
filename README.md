# IntroductiontoCells
Today, we learn about cells
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Cell City Patrol</title>
<meta name="claude:viewport-fit-sides" content="cover">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Fredoka:wght@500;600;700&family=Nunito:wght@600;700;800;900&display=swap">
<style>
/* Layout: a microscope-lab game. A level track across the top, one big "slide" card for the current level,
   and a lab notebook strip of earned badges. */
:root{
  --bg:#EAF7F4;        /* lab mint */
  --ink:#16324A;       /* deep lab-coat navy */
  --muted:#4F6B80;
  --card:#FFFFFF;
  --cyto:#FFE1EA;      /* animal cell pink */
  --nuc:#8C6BFF;       /* nucleus violet */
  --leaf:#3DBE72;      /* plant green */
  --sun:#FFC83D;       /* reward gold */
  --rogue:#FF5C8A;     /* rule-breaker cell */
  --ok:#22A06B; --no:#D9485F;
  --display:"Fredoka","Trebuchet MS",Verdana,sans-serif;
  --body:"Nunito","Trebuchet MS",Verdana,sans-serif;
}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#0F2230;--ink:#E8F4FF;--muted:#A8C1D4;--card:#17324A;color-scheme:dark}}
:root[data-theme="dark"]{--bg:#0F2230;--ink:#E8F4FF;--muted:#A8C1D4;--card:#17324A;color-scheme:dark}
*{box-sizing:border-box}
[hidden]{display:none!important}
body{margin:0;background:var(--bg);color:var(--ink);font-family:var(--body);
  background-image:radial-gradient(circle at 15% 20%,rgba(140,107,255,.10) 0 120px,transparent 121px),radial-gradient(circle at 85% 80%,rgba(61,190,114,.12) 0 160px,transparent 161px)}
button{font-family:var(--body);font-weight:900;cursor:pointer;color:inherit}
button:focus-visible,[tabindex]:focus-visible{outline:3px solid var(--nuc);outline-offset:3px}
.wrap{max-width:980px;margin:0 auto;padding-left:max(16px,env(safe-area-inset-left,0px));padding-right:max(16px,env(safe-area-inset-right,0px));padding-block:16px 32px;display:flex;flex-direction:column;gap:14px}
header{display:flex;align-items:center;gap:14px;flex-wrap:wrap}
h1{font-family:var(--display);font-weight:700;font-size:clamp(30px,5vw,46px);margin:0;line-height:1}
h1 span{color:var(--rogue)}
.sub{color:var(--muted);font-weight:800;margin-top:4px}
.score{margin-left:auto;display:flex;gap:8px;flex-wrap:wrap}
.chip{background:var(--card);border:2px solid var(--ink);border-radius:999px;padding:6px 14px;font-weight:900;font-variant-numeric:tabular-nums}
.track{display:grid;grid-template-columns:repeat(5,minmax(0,1fr));gap:8px}
.lvl{border:2px solid var(--ink);background:var(--card);border-radius:14px;padding:8px 10px;font-weight:900;font-size:14px;text-align:left;line-height:1.2;min-width:0}
.lvl small{display:block;color:var(--muted);font-size:12px;letter-spacing:1px;text-transform:uppercase}
.lvl.on{background:var(--sun);color:#16324A}
.lvl.on small{color:#16324A}
.lvl.done{background:#D7F5E5;color:#16324A}
.lvl.done small{color:#16324A}
.lvl:disabled{opacity:.45;cursor:not-allowed}
.stage{background:var(--card);border:3px solid var(--ink);border-radius:24px;padding:20px 22px;box-shadow:0 8px 0 rgba(22,50,74,.18);min-height:420px}
.stage h2{font-family:var(--display);font-size:clamp(24px,3.6vw,34px);margin:0 0 6px;line-height:1.1}
.tell{font-size:18px;line-height:1.55;max-width:68ch;margin:6px 0 12px}
.callout{background:rgba(140,107,255,.12);border-left:6px solid var(--nuc);border-radius:12px;padding:10px 14px;font-size:17px;line-height:1.5;max-width:70ch}
.two{display:grid;grid-template-columns:minmax(0,1.1fr) minmax(0,1fr);gap:18px;align-items:start}
.cellview svg{width:100%;height:auto;display:block}
.part{cursor:pointer}
.info{background:rgba(255,200,61,.18);border:2px solid var(--sun);border-radius:14px;padding:12px 14px;font-size:17px;line-height:1.5;min-height:120px}
.info b{font-family:var(--display);font-size:22px;display:block;margin-bottom:4px}
.found{display:flex;gap:6px;flex-wrap:wrap;margin-top:10px}
.tag{border:2px solid var(--ink);border-radius:999px;padding:4px 10px;font-weight:800;font-size:14px;opacity:.35}
.tag.got{opacity:1;background:#D7F5E5;color:#16324A}
.toggle{display:flex;gap:8px;margin-bottom:10px}
.toggle button{border:2px solid var(--ink);background:var(--card);border-radius:12px;padding:8px 14px;font-size:15px}
.toggle button.on{background:var(--ink);color:var(--card)}
.big{background:var(--sun);color:#16324A;font-family:var(--display);font-weight:700;font-size:20px;border:3px solid #16324A;border-radius:14px;padding:10px 22px;box-shadow:0 4px 0 #C98E00}
.big:disabled{opacity:.45;cursor:not-allowed}
.big:not(:disabled):active{transform:translateY(3px);box-shadow:0 1px 0 #C98E00}
.ghost{background:var(--card);border:3px solid var(--ink);border-radius:14px;padding:9px 16px;font-size:16px}
.row{display:flex;gap:10px;flex-wrap:wrap;align-items:center;margin-top:14px}
.q{font-size:19px;font-weight:800;margin:12px 0 8px}
.opts{display:grid;gap:8px}
.opt{text-align:left;background:var(--card);border:3px solid var(--ink);border-radius:14px;padding:10px 14px;font-size:17px}
.opt.right{background:#D7F5E5;border-color:var(--ok);color:#16324A}
.opt.wrong{background:#FADDE2;border-color:var(--no);color:#16324A}
.fb{border-radius:12px;padding:10px 14px;font-size:16px;line-height:1.5;margin-top:10px}
.fb.ok{background:#D7F5E5;border:2px solid var(--ok);color:#16324A}
.fb.bad{background:#FADDE2;border:2px solid var(--no);color:#16324A}
.bank{display:flex;gap:8px;flex-wrap:wrap;margin:8px 0}
.pill{border:3px solid var(--ink);background:var(--card);border-radius:999px;padding:8px 14px;font-size:16px}
.pill.sel{background:var(--sun);color:#16324A}
.pill.used{opacity:.3;pointer-events:none}
.chain{display:grid;gap:8px;grid-template-columns:repeat(var(--n),minmax(0,1fr))}
.slot{border:3px dashed var(--muted);border-radius:14px;min-height:96px;padding:8px;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:6px;text-align:center;background:var(--card);font-size:14px}
.slot .ic{font-size:30px;line-height:1}
.slot .nm{font-weight:900;font-size:15px}
.slot.right{border-style:solid;border-color:var(--ok);background:#D7F5E5;color:#16324A}
.slot.wrong{border-style:solid;border-color:var(--no);background:#FADDE2;color:#16324A}
.dna{display:flex;gap:6px;flex-wrap:wrap}
.word{border:2px solid var(--ink);border-radius:10px;padding:6px 10px;font-weight:900;font-size:16px;background:var(--card)}
.word.click{cursor:pointer}
.word.click:hover{background:var(--sun);color:#16324A}
.word.bad{background:#FADDE2;border-color:var(--no);color:#16324A}
.word.good{background:#D7F5E5;border-color:var(--ok);color:#16324A}
.copybox{display:grid;gap:10px}
.copybox .lab{font-weight:900;color:var(--muted);font-size:14px;text-transform:uppercase;letter-spacing:1px}
canvas{display:block;width:100%;max-width:640px;height:auto;border:3px solid var(--ink);border-radius:18px;background:#FFF5F8;touch-action:manipulation}
.meter{height:18px;border:2px solid var(--ink);border-radius:999px;overflow:hidden;background:var(--card);max-width:640px}
.meter i{display:block;height:100%;background:linear-gradient(90deg,var(--rogue),#B04CFF);width:0}
.hud{display:flex;gap:10px;flex-wrap:wrap;font-weight:900;margin:8px 0}
.badges{display:flex;gap:8px;flex-wrap:wrap}
.badge{border:2px solid var(--ink);border-radius:12px;padding:6px 10px;font-weight:900;background:var(--card);font-size:14px;opacity:.35}
.badge.got{opacity:1;background:var(--sun);color:#16324A}
.code{font-family:var(--display);font-size:clamp(30px,6vw,48px);background:#16324A;color:var(--sun);border-radius:14px;padding:10px 22px;display:inline-block;letter-spacing:2px}
@media (max-width:700px){.two{grid-template-columns:minmax(0,1fr)}.track{grid-template-columns:repeat(5,minmax(0,1fr))}.lvl{font-size:12px;padding:6px}.lvl small{font-size:10px}.chain{grid-template-columns:repeat(2,minmax(0,1fr))}}
@media (prefers-reduced-motion:reduce){*{transition:none!important;animation:none!important}}
</style>
</head>
<body>
<div class="wrap">
  <header>
    <div><h1>Cell City <span>Patrol</span></h1><div class="sub">Cells, bodies, plants, and what happens when cells break the rules</div></div>
    <div class="score"><div class="chip">Points <span id="pts">0</span></div></div>
  </header>
  <nav class="track" id="track" aria-label="Levels"></nav>
  <main class="stage" id="stage" aria-live="polite"></main>
  <div class="badges" id="badges"></div>
</div>

<script>
(()=>{
const END_CODE="ilovecells";
const LEVELS=[
 {k:"meet",name:"Meet the Cell",badge:"Cell Explorer"},
 {k:"build",name:"Build It!",badge:"Master Builder"},
 {k:"copy",name:"Copy Machine",badge:"Copy Checker"},
 {k:"rogue",name:"Rule Breakers",badge:"Immune Patrol"},
 {k:"help",name:"Helpers & Habits",badge:"Health Hero"}];
let pts=0, done={}, cur=0;
try{const s=JSON.parse(localStorage.getItem('ccp')||'{}');pts=s.pts||0;done=s.done||{}}catch(e){}
const save=()=>{try{localStorage.setItem('ccp',JSON.stringify({pts,done}))}catch(e){}};
const $=id=>document.getElementById(id);
const stage=$('stage');
const shuffle=a=>a.map(v=>[Math.random(),v]).sort((x,y)=>x[0]-y[0]).map(v=>v[1]);
let timer=null;

function chrome(){
  $('pts').textContent=pts;
  $('track').innerHTML=LEVELS.map((l,i)=>{const unlocked=i===0||done[LEVELS[i-1].k];return `<button type="button" class="lvl ${i===cur?'on':''} ${done[l.k]?'done':''}" data-i="${i}" ${unlocked?'':'disabled'}><small>Level ${i+1}${done[l.k]?' ✓':''}</small>${l.name}</button>`}).join('');
  $('track').querySelectorAll('.lvl').forEach(b=>b.onclick=()=>go(+b.dataset.i));
  $('badges').innerHTML=LEVELS.map(l=>`<span class="badge ${done[l.k]?'got':''}">${done[l.k]?'★':'☆'} ${l.badge}</span>`).join('');
}
function go(i){cur=i;if(timer){cancelAnimationFrame(timer);timer=null}chrome();[meet,build,copy,rogue,help][i]();stage.scrollIntoView({block:'nearest'})}
function win(k,extra){
  const fresh=!done[k];done[k]=true;save();chrome();
  const i=LEVELS.findIndex(l=>l.k===k);
  const last=Object.keys(done).length===LEVELS.length;
  stage.insertAdjacentHTML('beforeend',`<div class="fb ok" style="margin-top:16px"><b>Level complete! You earned the “${LEVELS[i].badge}” badge.</b> ${extra||''}</div>
  <div class="row">${i<LEVELS.length-1?`<button class="big" type="button" id="nextLvl">Next level: ${LEVELS[i+1].name}</button>`:''}${last?`<button class="big" type="button" id="final">Get your secret code</button>`:''}</div>`);
  if($('nextLvl')){$('nextLvl').onclick=()=>go(i+1);$('nextLvl').focus()}
  if($('final')){$('final').onclick=finale;if(!$('nextLvl'))$('final').focus()}
}
function add(n){pts+=n;$('pts').textContent=pts;save()}
// generic quiz
function quiz(qs,then){
  let i=0;
  const box=document.createElement('div');stage.appendChild(box);
  const ask=()=>{
    if(i>=qs.length){box.remove();return then()}
    const Q=qs[i];const ord=shuffle(Q.o.map((_,k)=>k));let tries=0;
    box.innerHTML=`<p class="q">${Q.q}</p><div class="opts">${ord.map(k=>`<button class="opt" type="button" data-k="${k}">${Q.o[k]}</button>`).join('')}</div><div class="fbx"></div>`;
    box.querySelectorAll('.opt').forEach(b=>b.onclick=()=>{tries++;const k=+b.dataset.k;
      if(k===0){b.classList.add('right');box.querySelectorAll('.opt').forEach(x=>x.disabled=true);const g=tries===1?10:5;add(g);
        box.querySelector('.fbx').innerHTML=`<div class="fb ok"><b>Yes! +${g}.</b> ${Q.e}</div><div class="row"><button class="big" type="button" id="qn">Next</button></div>`;
        const n=box.querySelector('#qn');n.onclick=()=>{i++;ask()};n.focus()}
      else{b.classList.add('wrong');b.disabled=true;box.querySelector('.fbx').innerHTML=`<div class="fb bad"><b>Not quite.</b> Try another answer.</div>`}})
  };ask();
}

// ---------------------------------------------------------------- Level 1: Meet the Cell
const PARTS={
 animal:[
  ["membrane","Cell membrane","The cell’s skin. It controls what goes in and out, like a security guard at a door."],
  ["nucleus","Nucleus","The control center. It holds DNA, the instructions that tell the cell how to grow, work, and copy itself."],
  ["cyto","Cytoplasm","The jelly that fills the cell. All the other parts float in it."],
  ["mito","Mitochondria","The power plants. They turn food into energy the cell can use."]],
 plant:[
  ["wall","Cell wall","A stiff outer layer only plant cells have. It helps plants stand tall."],
  ["nucleus","Nucleus","The control center with DNA instructions, just like in animal cells."],
  ["chloro","Chloroplasts","Green parts that use sunlight to make food. Animal cells don’t have these!"],
  ["vacuole","Vacuole","A big water storage bag. When it’s full, the plant stays firm instead of wilting."]]};
function cellSVG(kind){
  if(kind==='animal')return `<svg viewBox="0 0 400 320" role="img" aria-label="An animal cell. Tap each part to learn about it.">
   <path class="part" data-p="cyto" d="M200 20 C300 15 380 80 375 165 C370 255 290 305 195 300 C95 296 25 240 28 160 C30 80 100 25 200 20Z" fill="#FFE1EA"/>
   <path class="part" data-p="membrane" d="M200 20 C300 15 380 80 375 165 C370 255 290 305 195 300 C95 296 25 240 28 160 C30 80 100 25 200 20Z" fill="none" stroke="#E2557F" stroke-width="22" pointer-events="stroke"/>
   <g class="part" data-p="nucleus"><circle cx="190" cy="160" r="52" fill="#8C6BFF" stroke="#4B2DB8" stroke-width="5"/><circle cx="178" cy="150" r="16" fill="#4B2DB8"/></g>
   <g class="part" data-p="mito"><g transform="translate(292 110) rotate(25)"><ellipse rx="32" ry="15" fill="#FF8C42" stroke="#B34F12" stroke-width="4"/><path d="M-22 0 l7 -9 l7 9 l7 -9 l7 9 l7 -9" stroke="#FFE0C2" stroke-width="3" fill="none"/></g>
   <g transform="translate(110 230) rotate(-20)"><ellipse rx="30" ry="14" fill="#FF8C42" stroke="#B34F12" stroke-width="4"/><path d="M-20 0 l7 -8 l7 8 l7 -8 l7 8 l7 -8" stroke="#FFE0C2" stroke-width="3" fill="none"/></g>
   <g transform="translate(290 225) rotate(-60)"><ellipse rx="26" ry="12" fill="#FF8C42" stroke="#B34F12" stroke-width="4"/></g></g></svg>`;
  return `<svg viewBox="0 0 400 320" role="img" aria-label="A plant cell. Tap each part to learn about it.">
   <rect class="part" data-p="wall" x="20" y="20" width="360" height="280" rx="18" fill="#BDE9C9" stroke="#1E7A44" stroke-width="12"/>
   <rect x="38" y="38" width="324" height="244" rx="12" fill="#E6F8EA" stroke="#5BBE7F" stroke-width="3" pointer-events="none"/>
   <rect class="part" data-p="vacuole" x="150" y="70" width="180" height="170" rx="40" fill="#A9DDF7" stroke="#3B9FD6" stroke-width="4"/>
   <g class="part" data-p="nucleus"><circle cx="90" cy="95" r="38" fill="#8C6BFF" stroke="#4B2DB8" stroke-width="5"/><circle cx="82" cy="88" r="11" fill="#4B2DB8"/></g>
   <g class="part" data-p="chloro">${[[80,200],[110,250],[70,150],[340,265],[260,265],[350,55]].map(([x,y])=>`<g transform="translate(${x} ${y})"><ellipse rx="24" ry="13" fill="#2FB565" stroke="#156B36" stroke-width="3"/><path d="M-12 -6 v12 M-4 -7 v14 M4 -7 v14 M12 -6 v12" stroke="#156B36" stroke-width="3"/></g>`).join('')}</g></svg>`;
}
function meet(){
  let kind='animal';const got={animal:new Set(),plant:new Set()};
  const render=()=>{
    const P=PARTS[kind];
    stage.innerHTML=`<h2>Level 1: Meet the Cell</h2>
    <p class="tell"><b>Cells are the tiny building blocks of every living thing.</b> You have about 30 trillion of them! Most are too small to see without a microscope. Tap every part of the animal cell AND the plant cell to unlock the quiz.</p>
    <div class="toggle"><button type="button" class="${kind==='animal'?'on':''}" id="tA">Animal cell</button><button type="button" class="${kind==='plant'?'on':''}" id="tP">Plant cell</button></div>
    <div class="two"><div class="cellview" id="cv">${cellSVG(kind)}</div>
    <div><div class="info" id="info"><b>Tap a part!</b>Each part has a job, like workers in a city.</div>
    <div class="found">${P.map(p=>`<span class="tag ${got[kind].has(p[0])?'got':''}">${p[1]}</span>`).join('')}</div>
    <div class="row"><button class="big" type="button" id="toQuiz" ${(got.animal.size===4&&got.plant.size===4)?'':'disabled'}>Take the quiz</button></div></div></div>`;
    $('tA').onclick=()=>{kind='animal';render()};$('tP').onclick=()=>{kind='plant';render()};
    stage.querySelectorAll('.part').forEach(el=>{el.setAttribute('tabindex','0');el.setAttribute('role','button');
      const act=()=>{const p=P.find(x=>x[0]===el.dataset.p);got[kind].add(p[0]);render();$('info').innerHTML=`<b>${p[1]}</b>${p[2]}`};
      el.onclick=act;el.onkeydown=e=>{if(e.key==='Enter'||e.key===' '){e.preventDefault();act()}}});
    $('toQuiz').onclick=()=>{stage.innerHTML=`<h2>Level 1 Quiz</h2>`;quiz([
      {q:"Which part is the cell’s control center that holds DNA?",o:["Nucleus","Cell wall","Vacuole","Cytoplasm"],e:"The nucleus holds DNA, the cell’s instruction book."},
      {q:"Which parts do plant cells have that animal cells do NOT?",o:["Cell wall and chloroplasts","Nucleus and membrane","Mitochondria and cytoplasm","Bones and skin"],e:"Plant cells have a stiff cell wall and chloroplasts that make food from sunlight."},
      {q:"What do mitochondria do?",o:["Turn food into energy","Make the cell green","Store water","Hold the cell’s instructions"],e:"Mitochondria are power plants that turn food into energy."}],()=>{add(20);win('meet','Every living thing, from an oak tree to you, is built from cells.')})};
  };render();
}

// ---------------------------------------------------------------- Level 2: Build it
function build(){
  const sets=[
   {name:"Build a BODY",steps:[["Cell","🔴","a muscle cell"],["Tissue","🧵","muscle tissue"],["Organ","❤️","the heart"],["Organ system","🩸","circulatory system"],["Organism","🧒","you!"]]},
   {name:"Build a PLANT",steps:[["Cell","🟢","a leaf cell"],["Tissue","🍃","leaf tissue"],["Organ","🌿","a leaf"],["Organ system","🌱","the shoot system"],["Organism","🌳","a whole plant"]]}];
  let si=0;
  const run=()=>{
    const S=sets[si];const bank=shuffle(S.steps.map(s=>s[0]));const placed=Array(5).fill(null);let sel=null,tries=0;
    const render=(msg)=>{
      stage.innerHTML=`<h2>Level 2: Build It! (${si+1} of 2)</h2>
      <p class="tell">Cells team up! Similar cells make a <b>tissue</b>. Tissues make an <b>organ</b>. Organs work together in an <b>organ system</b>. Systems make a whole living thing, an <b>organism</b>. Plants are built the same way!</p>
      <p class="q">${S.name}: tap a word, then tap the box where it goes, from smallest to biggest.</p>
      <div class="bank">${bank.map(w=>`<button type="button" class="pill ${sel===w?'sel':''} ${placed.includes(w)?'used':''}" data-w="${w}">${w}</button>`).join('')}</div>
      <div class="chain" style="--n:5">${S.steps.map((s,i)=>`<button type="button" class="slot" data-i="${i}"><span class="ic" aria-hidden="true">${s[1]}</span><span>${s[2]}</span><span class="nm">${placed[i]||'?'}</span></button>`).join('')}</div>
      <div class="row"><button class="big" type="button" id="chk" ${placed.includes(null)?'disabled':''}>Check</button></div><div>${msg||''}</div>`;
      stage.querySelectorAll('.pill').forEach(b=>b.onclick=()=>{sel=b.dataset.w;render()});
      stage.querySelectorAll('.slot').forEach(b=>b.onclick=()=>{const i=+b.dataset.i;if(sel){const o=placed.indexOf(sel);if(o>-1)placed[o]=null;placed[i]=sel;sel=null}else placed[i]=null;render()});
      $('chk').onclick=()=>{tries++;let ok=0;S.steps.forEach((s,i)=>{if(placed[i]===s[0])ok++});
        if(ok===5){add(tries===1?50:25);render(`<div class="fb ok"><b>Perfect build!</b> ${si===0?'A muscle cell → muscle tissue → heart → circulatory system → you!':'A leaf cell → leaf tissue → leaf → shoot system → a whole plant!'}</div><div class="row"><button class="big" type="button" id="nx">${si===0?'Now build a plant':'Finish level'}</button></div>`);
          stage.querySelectorAll('.slot').forEach(b=>b.classList.add('right'));$('chk').disabled=true;
          $('nx').onclick=()=>{if(si===0){si=1;run()}else{stage.innerHTML='<h2>Level 2: Build It!</h2><p class="tell">Bodies and plants are both built from cells, step by step.</p>';win('build','Cells build tissues, organs, organ systems, and whole organisms.')}};$('nx').focus()}
        else{S.steps.forEach((s,i)=>{if(placed[i]!==s[0])placed[i]=null});render(`<div class="fb bad"><b>${ok} of 5 are right.</b> Those stayed in place. Fill in the rest and check again.</div>`)}};
    };render();
  };run();
}

// ---------------------------------------------------------------- Level 3: Copy machine
function copy(){
  const rounds=[
   {orig:["GROW","WORK","STOP when crowded","REPAIR","REST"],copy:["GROW","WORK","STOP when crowded","REPAIR","REST"],bad:-1},
   {orig:["GROW","WORK","STOP when crowded","REPAIR","REST"],copy:["GROW","WORK","GO when crowded","REPAIR","REST"],bad:2},
   {orig:["MAKE energy","GROW","STOP when crowded","FIX mistakes","REST"],copy:["MAKE energy","GROW","STOP when crowded","SKIP mistakes","REST"],bad:3},
   {orig:["GROW","STOP when crowded","WORK","REPAIR","LISTEN to signals"],copy:["GROW","STOP when crowded","WORK","REPAIR","IGNORE signals"],bad:4}];
  let r=0;
  const render=(msg)=>{
    const R=rounds[r];
    stage.innerHTML=`<h2>Level 3: Copy Machine</h2>
    <p class="tell">Your body makes new cells by <b>copying</b> old ones. A cell splits into two, and each new cell needs a copy of the DNA instructions. Cells have “spell-checkers” that catch mistakes. Healthy cells also <b>stop</b> dividing when they get crowded.</p>
    <div class="callout">You are the spell-checker! Compare the copy to the original. Tap the word that changed, or tap “No mistakes” if the copy is perfect.</div>
    <p class="q">Copy ${r+1} of ${rounds.length}</p>
    <div class="copybox"><div><div class="lab">Original instructions</div><div class="dna">${R.orig.map(w=>`<span class="word">${w}</span>`).join('')}</div></div>
    <div><div class="lab">New copy</div><div class="dna">${R.copy.map((w,i)=>`<button type="button" class="word click" data-i="${i}">${w}</button>`).join('')}</div></div></div>
    <div class="row"><button class="ghost" type="button" id="none">No mistakes</button></div><div id="fbx">${msg||''}</div>`;
    const done3=(ok,why)=>{if(ok)add(15);$('fbx').innerHTML=`<div class="fb ${ok?'ok':'bad'}">${why}</div><div class="row"><button class="big" type="button" id="nx">${r+1<rounds.length?'Next copy':'Finish level'}</button></div>`;
      stage.querySelectorAll('.word.click,#none').forEach(b=>b.disabled=true);
      $('nx').onclick=()=>{r++;if(r<rounds.length)render();else{stage.innerHTML='<h2>Level 3: Copy Machine</h2><p class="tell">Cells copy their instructions every time they divide. Most of the time, the copy is perfect or the mistake gets fixed.</p>';win('copy','When a mistake is NOT fixed, a cell might stop following the rules. That’s next!')}};$('nx').focus()};
    stage.querySelectorAll('.word.click').forEach(b=>b.onclick=()=>{const i=+b.dataset.i;
      if(i===R.bad){b.classList.add('bad');done3(true,`<b>Caught it! +15.</b> “${R.orig[i]}” was copied as “${R.copy[i]}”. A mistake like this could make a cell break the rules, so cells try hard to fix them.`)}
      else if(R.bad===-1){done3(false,`<b>Look again!</b> This copy was perfect. Every word matched the original.`)}
      else{b.classList.add('good');$('fbx').innerHTML=`<div class="fb bad">“${R.copy[i]}” matches the original. Keep looking!</div>`}});
    $('none').onclick=()=>{if(R.bad===-1)done3(true,'<b>Correct! +15.</b> This copy matched perfectly. Most cell copies are just right.');else $('fbx').innerHTML=`<div class="fb bad">Look closely. One word is different!</div>`};
  };render();
}

// ---------------------------------------------------------------- Level 4: Rule breakers (cancer)
function rogue(){
  stage.innerHTML=`<h2>Level 4: Rule Breakers</h2>
  <p class="tell"><b>Cancer</b> starts when a cell’s instructions get mixed up and the mistake isn’t fixed. That cell stops following the rules. It ignores the “STOP when crowded” signal and keeps copying itself again and again. The extra cells can pile up into a lump called a <b>tumor</b>.</p>
  <div class="callout">Good news: your <b>immune system</b> has patrol cells that look for rule breakers and remove them. Cancer is <b>not contagious</b>. You can’t catch it from a friend!</div>
  <p class="q">Be the Immune Patrol! Tap the pink, wobbly rule-breaker cells before they crowd out the healthy blue cells. Keep the rule-breaker meter under 100% for 30 seconds.</p>
  <div class="hud"><span>Time: <span id="tm">30</span>s</span><span>Tagged: <span id="tg">0</span></span></div>
  <div class="meter" aria-label="Rule-breaker meter"><i id="mt"></i></div>
  <div class="row" style="margin-top:8px"><canvas id="cv" width="640" height="400" aria-label="Tissue made of cells. Tap the pink rule-breaker cells."></canvas></div>
  <div class="row"><button class="big" type="button" id="startG">Start patrol</button></div><div id="fbx"></div>`;
  const cv=$('cv'),ctx=cv.getContext('2d');const COLS=16,ROWS=10,S=40;
  let grid,tagged,timeLeft,running=false,last=0,acc=0,sparks=[];
  const reset=()=>{grid=[];for(let y=0;y<ROWS;y++){grid.push([]);for(let x=0;x<COLS;x++)grid[y].push(Math.random()<.78?{t:'h',ph:Math.random()*6}:null)}
    for(let k=0;k<2;k++){const x=Math.floor(Math.random()*COLS),y=Math.floor(Math.random()*ROWS);grid[y][x]={t:'r',ph:0}}tagged=0;timeLeft=30;sparks=[]};
  const count=()=>{let r=0;for(const row of grid)for(const c of row)if(c&&c.t==='r')r++;return r};
  const draw=(t)=>{ctx.fillStyle='#FFF5F8';ctx.fillRect(0,0,640,400);
    for(let y=0;y<ROWS;y++)for(let x=0;x<COLS;x++){const c=grid[y][x];if(!c)continue;const cx=x*S+20,cy=y*S+20;
      if(c.t==='h'){ctx.fillStyle='#BFE3FF';ctx.strokeStyle='#3B8FD6';ctx.lineWidth=2.5;ctx.beginPath();ctx.arc(cx,cy,16,0,7);ctx.fill();ctx.stroke();ctx.fillStyle='#8C6BFF';ctx.beginPath();ctx.arc(cx,cy,6,0,7);ctx.fill()}
      else{const w=Math.sin(t/120+x+y)*2.5;ctx.fillStyle='#FF5C8A';ctx.strokeStyle='#A3124A';ctx.lineWidth=3;ctx.beginPath();
        for(let k=0;k<=12;k++){const a=k/12*6.283,rr=17+Math.sin(a*3+t/150)*w;k?ctx.lineTo(cx+Math.cos(a)*rr,cy+Math.sin(a)*rr):ctx.moveTo(cx+Math.cos(a)*rr,cy+Math.sin(a)*rr)}ctx.fill();ctx.stroke();
        ctx.fillStyle='#5B1340';ctx.beginPath();ctx.arc(cx-3,cy-2,5,0,7);ctx.arc(cx+4,cy+3,4,0,7);ctx.fill()}}
    for(const s of sparks){ctx.globalAlpha=Math.max(0,s.l);ctx.fillStyle=s.c;ctx.fillRect(s.x,s.y,5,5);ctx.globalAlpha=1}
    $('mt').style.width=Math.min(100,count()/ (COLS*ROWS*.35)*100)+'%';};
  const step=()=>{ // rule breakers divide into neighbors, even if crowded
    const list=[];for(let y=0;y<ROWS;y++)for(let x=0;x<COLS;x++)if(grid[y][x]&&grid[y][x].t==='r')list.push([x,y]);
    for(const[x,y]of list){if(Math.random()<.42){const d=[[1,0],[-1,0],[0,1],[0,-1]][Math.floor(Math.random()*4)];const nx=x+d[0],ny=y+d[1];if(nx>=0&&ny>=0&&nx<COLS&&ny<ROWS)grid[ny][nx]={t:'r',ph:0}}}
    if(Math.random()<.18){const x=Math.floor(Math.random()*COLS),y=Math.floor(Math.random()*ROWS);if(grid[y][x]&&grid[y][x].t==='h')grid[y][x]={t:'r',ph:0}}
    // healthy cells refill empty space but stop when crowded
    for(let y=0;y<ROWS;y++)for(let x=0;x<COLS;x++)if(!grid[y][x]&&Math.random()<.08)grid[y][x]={t:'h',ph:0};};
  const loop=(t)=>{if(!running)return;const dt=Math.min(.05,(t-last)/1000||0);last=t;acc+=dt;timeLeft-=dt;
    for(const s of sparks){s.x+=s.vx*dt;s.y+=s.vy*dt;s.l-=dt*1.5}sparks=sparks.filter(s=>s.l>0);
    if(acc>1.1){acc=0;step()}draw(t);$('tm').textContent=Math.max(0,Math.ceil(timeLeft));
    const full=count()>=COLS*ROWS*.35;
    if(full||timeLeft<=0){running=false;end(!full);return}
    timer=requestAnimationFrame(loop)};
  const end=(ok)=>{
    if(ok){add(40+tagged*2);$('fbx').innerHTML=`<div class="fb ok"><b>Patrol successful! You tagged ${tagged} rule breakers.</b> That’s what your immune system does every day. It finds most rule-breaking cells and removes them before they cause trouble.</div>`;$('startG').hidden=true;win('rogue','Sometimes a few rule breakers get past the patrol. That’s when doctors can help. Find out how in the last level!')}
    else{$('fbx').innerHTML=`<div class="fb bad"><b>The rule breakers made a lump (a tumor).</b> In real life, this is when doctors step in to help. Try again: tap the pink cells quickly!</div>`;$('startG').textContent='Try again';$('startG').hidden=false}};
  const tap=(e)=>{if(!running)return;const r=cv.getBoundingClientRect();const x=Math.floor((e.clientX-r.left)/r.width*640/S),y=Math.floor((e.clientY-r.top)/r.height*400/S);
    // forgiving: check the tapped cell and its neighbors
    for(const[dx,dy]of[[0,0],[1,0],[-1,0],[0,1],[0,-1]]){const X=x+dx,Y=y+dy;if(X>=0&&Y>=0&&X<COLS&&Y<ROWS&&grid[Y][X]&&grid[Y][X].t==='r'){grid[Y][X]=null;tagged++;$('tg').textContent=tagged;
      for(let k=0;k<12;k++){const a=Math.random()*6.28;sparks.push({x:X*S+20,y:Y*S+20,vx:Math.cos(a)*120,vy:Math.sin(a)*120,l:1,c:['#FFC83D','#3DBE72','#8C6BFF'][k%3]})}break}}};
  cv.addEventListener('pointerdown',tap);
  reset();draw(0);
  $('startG').onclick=()=>{reset();running=true;last=performance.now();acc=0;$('startG').hidden=true;$('fbx').innerHTML='';$('tg').textContent=0;timer=requestAnimationFrame(loop)};
}

// ---------------------------------------------------------------- Level 5: Helpers & habits
function help(){
  stage.innerHTML=`<h2>Level 5: Helpers &amp; Healthy Habits</h2>
  <p class="tell">When rule-breaking cells grow into a tumor, doctors have powerful tools. <b>Surgery</b> can remove a lump. <b>Chemotherapy</b> (medicine) and <b>radiation</b> (special energy beams) target cells that divide too fast. <b>Immunotherapy</b> trains the immune system to find rule breakers. Many people get better, and scientists discover new treatments every year.</p>
  <div class="callout">Plants can get lumps too! Some bacteria cause a plant disease called <b>crown gall</b>, where plant cells grow into a big bumpy lump on the stem. Cells everywhere follow rules, and when the rules break, cells can grow out of control.</div>`;
  quiz([
   {q:"What is cancer?",o:["Cells that stop following the rules and keep dividing","A cold you catch from a friend","Cells that work too slowly","A broken bone"],e:"Cancer is when cells ignore the STOP signal and keep copying themselves."},
   {q:"Can you catch cancer from a friend?",o:["No, cancer is not contagious","Yes, by sharing snacks","Yes, by giving a hug","Only on Tuesdays"],e:"Cancer is not contagious. You can’t catch it like a cold."},
   {q:"Which tool helps the body find and remove rule-breaking cells?",o:["The immune system","The cell wall","Chloroplasts","The vacuole"],e:"Immune cells patrol the body, and immunotherapy can make them even better at it."},
   {q:"Sunburns can mix up the instructions in skin cells. Which habit protects them?",o:["Wearing sunscreen and a hat","Skipping breakfast","Staying up late","Eating extra candy"],e:"Sunscreen blocks UV rays that can damage skin cells’ DNA."},
   {q:"Which choice helps keep your cells healthy?",o:["Eating fruits and veggies, exercising, and never smoking","Eating only chips","Breathing smoke","Never going outside"],e:"Healthy habits help cells copy their instructions correctly."}],
   ()=>{add(30);win('help','You learned how cells build living things, how they copy themselves, and how doctors and healthy habits help when cells break the rules.')});
}
function finale(){
  stage.innerHTML=`<h2>Mission complete, Cell Patrol Agent!</h2>
  <p class="tell">You scored <b>${pts} points</b> and earned all 5 badges. You know what cells are, how they build bodies and plants, how they copy themselves, and what happens when they break the rules.</p>
  <p>Your secret code is:</p><p class="code">${END_CODE}</p><p>Write it down and turn it in to your teacher.</p>
  <div class="row"><button class="ghost" type="button" id="again">Play again from the start</button></div>`;
  $('again').onclick=()=>{pts=0;done={};save();go(0)};
}
go(Math.min(Object.keys(done).length,LEVELS.length-1));
})();
</script>
</body>
</html>
