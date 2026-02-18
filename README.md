<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>Daily Routine</title>

<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=IBM+Plex+Mono:wght@300;400;500&family=IBM+Plex+Sans+KR:wght@300;400;500;600&display=swap" rel="stylesheet">

<style>
:root{
  --bg:#f5f4f0;
  --ink:#0f0f0f;
  --red:#e63022;
  --muted:#999;
  --border:#d8d6d0;
  --surface:#ffffff;
  --light:#f0ede8;
}

*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}

body{
  font-family:'IBM Plex Sans KR',sans-serif;
  background:var(--bg);
  color:var(--ink);
  max-width:430px;
  margin:0 auto;
  min-height:100vh;
  padding-bottom:90px;
}

/* LOCK */
#lockScreen{
position:fixed;inset:0;background:#0f0f0f;
display:flex;flex-direction:column;
align-items:center;justify-content:center;
z-index:9999;width:100vw;height:100vh;
padding:40px 24px;
}
#lockScreen.hidden{display:none;}

.lock-title{
font-family:'Bebas Neue',sans-serif;
font-size:56px;letter-spacing:2px;
color:var(--bg);line-height:.9;
text-align:center;margin-bottom:8px;
}
.lock-title span{color:var(--red);}
.lock-sub{
font-family:'IBM Plex Mono',monospace;
font-size:10px;letter-spacing:2px;
color:var(--muted);text-transform:uppercase;
margin-bottom:52px;
}
.lock-dots{display:flex;gap:14px;margin-bottom:40px;}
.lock-dot{
width:14px;height:14px;border-radius:50%;
border:2px solid #3a3a3a;
transition:.15s;
}
.lock-dot.filled{background:var(--bg);border-color:var(--bg);}
.lock-dot.error{background:var(--red);border-color:var(--red);}
.lock-error{
font-family:'IBM Plex Mono',monospace;
font-size:10px;letter-spacing:2px;
color:var(--red);text-transform:uppercase;
height:16px;margin-bottom:32px;text-align:center;
}

.keypad{
display:grid;
grid-template-columns:repeat(3,1fr);
gap:12px;width:100%;max-width:280px;
}
.key{
aspect-ratio:1;background:#1a1a1a;
border:none;border-radius:50%;
color:var(--bg);
font-family:'Bebas Neue',sans-serif;
font-size:28px;cursor:pointer;
display:flex;align-items:center;justify-content:center;
transition:.1s;
}
.key:active{background:#333;transform:scale(.94);}
.key.del{font-family:'IBM Plex Mono',monospace;font-size:16px;color:var(--muted);}
.key.empty{background:transparent;pointer-events:none;}

/* HEADER */
.header{padding:52px 24px 20px;border-bottom:2px solid var(--ink);}
.header-eyebrow{
font-family:'IBM Plex Mono',monospace;
font-size:10px;letter-spacing:3px;
color:var(--muted);text-transform:uppercase;margin-bottom:6px;
}
.header-title{
font-family:'Bebas Neue',sans-serif;
font-size:68px;line-height:.88;letter-spacing:2px;
}
.header-title span{color:var(--red);}
.header-quote{
font-family:'IBM Plex Mono',monospace;
font-size:11px;color:var(--muted);
margin-top:16px;padding-left:12px;
border-left:2px solid var(--red);
line-height:1.6;
}

/* PROGRESS */
.progress-wrap{padding:20px 24px 16px;border-bottom:1px solid var(--border);}
.progress-top{display:flex;justify-content:space-between;margin-bottom:10px;}
.progress-pct{font-family:'Bebas Neue',sans-serif;font-size:52px;}
.progress-msg{
font-family:'IBM Plex Mono',monospace;
font-size:10px;color:var(--muted);
text-align:right;line-height:1.5;max-width:180px;
}
.progress-track{height:2px;background:var(--border);position:relative;}
.progress-fill{
position:absolute;left:0;top:0;height:100%;
background:#0f0f0f;width:0%;
transition:.5s cubic-bezier(.4,0,.2,1);
}
.progress-bottom{display:flex;justify-content:space-between;margin-top:6px;}
.progress-label{
font-family:'IBM Plex Mono',monospace;
font-size:9px;letter-spacing:1.5px;
color:var(--muted);text-transform:uppercase;
}

/* NAV */
.nav{display:flex;border-bottom:2px solid var(--ink);}
.nav-btn{
flex:1;padding:12px 8px;
border:none;border-right:1px solid var(--border);
background:transparent;color:var(--muted);
font-family:'IBM Plex Mono',monospace;
font-size:10px;letter-spacing:2px;
text-transform:uppercase;cursor:pointer;
}
.nav-btn:last-child{border-right:none;}
.nav-btn.active{background:#0f0f0f;color:var(--bg);}

.view{display:none;}
.view.active{display:block;}

/* ITEMS */
.category{border-bottom:1px solid var(--border);}
.cat-label{
padding:14px 24px 6px;
font-family:'IBM Plex Mono',monospace;
font-size:9px;letter-spacing:3px;
text-transform:uppercase;color:var(--muted);
}
.item{
display:flex;align-items:center;
padding:12px 24px;border-top:1px solid var(--border);
cursor:pointer;gap:14px;
}
.item:active{background:var(--light);}
.item.checked{background:var(--light);}
.item-index{
font-family:'IBM Plex Mono',monospace;
font-size:10px;color:var(--border);
width:18px;flex-shrink:0;
}
.item.checked .item-index{color:var(--red);}
.item-name{flex:1;font-size:15px;}
.item.checked .item-name{text-decoration:line-through;color:var(--muted);}
.item-sub{font-family:'IBM Plex Mono',monospace;font-size:10px;color:var(--muted);}
.item-box{
width:18px;height:18px;border:1.5px solid var(--border);
display:flex;align-items:center;justify-content:center;
font-size:10px;font-family:'IBM Plex Mono',monospace;
}
.item.checked .item-box{
background:#0f0f0f;border-color:var(--ink);color:var(--bg);
}

/* BOTTOM */
.bottom-bar{
position:fixed;bottom:0;left:50%;
transform:translateX(-50%);
width:100%;max-width:430px;
background:#0f0f0f;color:var(--bg);
padding:14px 24px;
display:flex;justify-content:space-between;align-items:center;
}
.bottom-msg{
font-family:'IBM Plex Mono',monospace;
font-size:10px;letter-spacing:1.5px;text-transform:uppercase;
}
.bottom-count{
font-family:'Bebas Neue',sans-serif;
font-size:24px;color:var(--red);
}

.toast{
position:fixed;bottom:72px;left:50%;
transform:translateX(-50%);
background:#0f0f0f;color:var(--bg);
font-family:'IBM Plex Mono',monospace;
font-size:10px;padding:10px 20px;
opacity:0;transition:.25s;
}
.toast.show{opacity:1;}
.toast.error{background:var(--red);}
</style>
</head>

<body>

<div id="lockScreen">
<div class="lock-title">DAILY<br><span>ROUTINE</span></div>
<div class="lock-sub">Enter passcode</div>
<div class="lock-dots">
<div class="lock-dot" id="d0"></div>
<div class="lock-dot" id="d1"></div>
<div class="lock-dot" id="d2"></div>
<div class="lock-dot" id="d3"></div>
</div>
<div class="lock-error" id="lockError"></div>
<div class="keypad">
<button class="key" onclick="keyPress('1')">1</button>
<button class="key" onclick="keyPress('2')">2</button>
<button class="key" onclick="keyPress('3')">3</button>
<button class="key" onclick="keyPress('4')">4</button>
<button class="key" onclick="keyPress('5')">5</button>
<button class="key" onclick="keyPress('6')">6</button>
<button class="key" onclick="keyPress('7')">7</button>
<button class="key" onclick="keyPress('8')">8</button>
<button class="key" onclick="keyPress('9')">9</button>
<button class="key empty"></button>
<button class="key" onclick="keyPress('0')">0</button>
<button class="key del" onclick="keyDel()">DEL</button>
</div>
</div>

<div class="bottom-bar">
<div class="bottom-msg" id="bottomMsg">Start your day</div>
<div class="bottom-count" id="bottomCount">0/9</div>
</div>

<div class="toast" id="toast"></div>

<script>
const PASSCODE='4320';
let input='';

function keyPress(n){
if(input.length>=4)return;
input+=n;
updateDots();
if(input.length===4){
setTimeout(()=>{
if(input===PASSCODE){
document.getElementById('lockScreen').classList.add('hidden');
}else{
document.querySelectorAll('.lock-dot').forEach(d=>d.classList.add('error'));
document.getElementById('lockError').textContent='Incorrect passcode';
setTimeout(()=>{
input='';
updateDots();
document.querySelectorAll('.lock-dot').forEach(d=>d.classList.remove('filled','error'));
document.getElementById('lockError').textContent='';
},800);
}
},120);
}
}

function keyDel(){input=input.slice(0,-1);updateDots();}
function updateDots(){
for(let i=0;i<4;i++){
document.getElementById('d'+i).classList.toggle('filled',i<input.length);
}
}

function showToast(msg,isError=false){
const t=document.getElementById('toast');
t.textContent=msg;
t.className='toast show'+(isError?' error':'');
setTimeout(()=>t.classList.remove('show'),1800);
}
</script>

</body>
</html>
