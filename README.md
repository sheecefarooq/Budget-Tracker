<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Budget Tracker</title>
<link rel="icon" href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22>💰</text></svg>">
<style>
:root{--bg:#f6f7f9;--card:#fff;--text:#1a1d23;--muted:#6b7280;--line:#e5e7eb;--accent:#2563eb;--inc:#16a34a;--exp:#dc2626;--warn:#d97706;
box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#0f1115;--card:#1a1d23;--text:#f3f4f6;--muted:#9ca3af;--line:#2a2e37;--accent:#60a5fa;--inc:#4ade80;--exp:#f87171;--warn:#fbbf24}}
:root[data-theme="dark"]{--bg:#0f1115;--card:#1a1d23;--text:#f3f4f6;--muted:#9ca3af;--line:#2a2e37;--accent:#60a5fa;--inc:#4ade80;--exp:#f87171;--warn:#fbbf24}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--text);font:16px/1.4 system-ui,-apple-system,"Segoe UI",Roboto,sans-serif}
main{max-width:640px;margin:0 auto;padding:16px}
h1{font-size:22px;margin:4px 0 14px}
h2{font-size:15px;margin:0 0 10px;color:var(--muted);font-weight:600}
.card{background:var(--card);border:1px solid var(--line);border-radius:14px;padding:14px;margin-bottom:14px}
.grid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px}
.stat{text-align:center}.stat small{color:var(--muted);display:block;font-size:12px}.stat b{font-size:17px}
.inc{color:var(--inc)}.exp{color:var(--exp)}
.bar{height:10px;background:var(--line);border-radius:6px;overflow:hidden;margin:8px 0 4px}
.bar>i{display:block;height:100%;background:var(--accent);border-radius:6px;transition:width .3s}
.row{display:flex;gap:8px;margin-bottom:8px}
input,select,button{font:inherit;color:var(--text);background:var(--bg);border:1px solid var(--line);border-radius:10px;padding:10px;min-width:0}
input,select{flex:1;width:100%}
button{cursor:pointer}
.primary{background:var(--accent);color:#fff;border:0;font-weight:600;width:100%}
.seg{display:flex;border:1px solid var(--line);border-radius:10px;overflow:hidden;margin-bottom:8px}
.seg button{flex:1;border:0;border-radius:0;background:transparent}
.seg button.on{background:var(--accent);color:#fff}
.tx{display:flex;align-items:center;gap:10px;padding:10px 0;border-top:1px solid var(--line)}
.tx:first-of-type{border-top:0}
.tx div{flex:1;min-width:0}.tx small{color:var(--muted);display:block}
.tx button{border:0;background:none;color:var(--muted);padding:4px 8px}
.cat{margin-bottom:10px;font-size:14px}.cat span{float:right;color:var(--muted)}
.empty{color:var(--muted);text-align:center;padding:10px}
.head{display:flex;justify-content:space-between;align-items:center}
.head input{width:auto;flex:none}
.card{box-shadow:0 1px 3px rgba(0,0,0,.06)}.donut{width:150px;height:150px;border-radius:50%;margin:4px auto 16px;position:relative}.donut::after{content:"";position:absolute;inset:30px;background:var(--card);border-radius:50%}.donut b{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;z-index:1;font-size:15px}.dot{display:inline-block;width:10px;height:10px;border-radius:50%;margin-right:6px}
#cat{display:none}.pick{flex:1;width:100%;display:flex;align-items:center;gap:8px;text-align:left}.pick span:last-child{margin-left:auto;color:var(--muted)}
.ov{position:fixed;inset:0;background:rgba(0,0,0,.55);display:none;align-items:flex-end;justify-content:center;z-index:50}.ov.on{display:flex}
.sheet{background:var(--card);color:var(--text);width:100%;max-width:640px;max-height:80%;border-radius:22px 22px 0 0;padding:14px 16px calc(16px + env(safe-area-inset-bottom,0px));display:flex;flex-direction:column;box-shadow:0 -8px 30px rgba(0,0,0,.25)}
.grab{width:40px;height:4px;border-radius:2px;background:var(--line);margin:0 auto 12px}
.sheet .list{overflow-y:auto;margin-top:6px}.sheet h3{font-size:12px;color:var(--muted);margin:16px 0 8px;text-transform:uppercase;letter-spacing:.06em}
.chips{display:flex;flex-wrap:wrap;gap:8px}.chip{display:flex;align-items:center;gap:6px;padding:9px 14px;border-radius:999px;font-size:15px}
.chip.on{background:var(--accent);color:#fff;border-color:var(--accent);font-weight:600}
body{background-attachment:fixed}
body{background:var(--page,var(--bg));background-attachment:fixed}
.sheet{background:var(--sheet,var(--card))}.donut::after{background:var(--sheet,var(--card))}
.sw{display:flex;gap:10px;margin-bottom:14px;overflow-x:auto;padding:4px 2px}.sw button{flex:none;width:38px;height:38px;border-radius:50%;border:2px solid var(--line);padding:0}.sw button.on{outline:3px solid var(--accent);outline-offset:2px}
:root[data-theme="light"]{--page:#fff;--bg:#f3f4f6;--card:#fff;--text:#111827;--muted:#6b7280;--line:#e5e7eb;--accent:#2563eb;--inc:#16a34a;--exp:#dc2626;--warn:#d97706;color-scheme:light}
:root[data-theme="dark"]{--page:#000;--bg:#141414;--card:#0d0d0d;--text:#f5f5f5;--muted:#9ca3af;--line:#262626;--accent:#60a5fa;--inc:#4ade80;--exp:#f87171;--warn:#fbbf24;color-scheme:dark}
:root[data-theme="sky"]{--page:linear-gradient(160deg,#e0f2fe,#fce7f3);--bg:rgba(255,255,255,.7);--card:rgba(255,255,255,.72);--sheet:#fff;--text:#0f172a;--muted:#64748b;--line:rgba(15,23,42,.1);--accent:#2563eb;--inc:#16a34a;--exp:#dc2626;--warn:#d97706;color-scheme:light}
:root[data-theme="ocean"]{--page:linear-gradient(160deg,#0f2027,#203a43,#2c5364);--bg:rgba(255,255,255,.08);--card:rgba(255,255,255,.1);--sheet:#16313c;--text:#f1f5f9;--muted:#b6c2cf;--line:rgba(255,255,255,.16);--accent:#0ea5e9;--inc:#4ade80;--exp:#fb7185;--warn:#fbbf24;color-scheme:dark}
:root[data-theme="sunset"]{--page:linear-gradient(160deg,#f97316,#db2777);--bg:rgba(0,0,0,.18);--card:rgba(0,0,0,.24);--sheet:#7a1f3d;--text:#fff;--muted:rgba(255,255,255,.78);--line:rgba(255,255,255,.22);--accent:#e11d48;--inc:#bbf7d0;--exp:#ffe4e6;--warn:#fde68a;color-scheme:dark}
:root[data-theme="forest"]{--page:linear-gradient(160deg,#134e5e,#71b280);--bg:rgba(0,0,0,.16);--card:rgba(0,0,0,.24);--sheet:#1b4d3e;--text:#fff;--muted:rgba(255,255,255,.78);--line:rgba(255,255,255,.2);--accent:#15803d;--inc:#bbf7d0;--exp:#fecaca;--warn:#fde68a;color-scheme:dark}
:root[data-theme="aurora"]{--page:linear-gradient(160deg,#4338ca,#9333ea,#db2777);--bg:rgba(0,0,0,.16);--card:rgba(0,0,0,.24);--sheet:#3b2a82;--text:#fff;--muted:rgba(255,255,255,.78);--line:rgba(255,255,255,.22);--accent:#7c3aed;--inc:#bbf7d0;--exp:#fecdd3;--warn:#fde68a;color-scheme:dark}
.srow{display:flex;justify-content:space-between;align-items:center;gap:10px;padding:10px 0;border-top:1px solid var(--line)}.about{font-size:13px;color:var(--muted);line-height:1.6}
textarea{width:100%;font:inherit;color:var(--text);background:var(--bg);border:1px solid var(--line);border-radius:10px;padding:10px;margin:8px 0}.danger{width:100%;color:var(--exp);border-color:var(--exp)}#hi{font-size:15px;color:var(--muted);margin:-6px 0 12px}.head span{display:flex;gap:8px}
#trend{display:flex;gap:6px}.tc{flex:1;text-align:center}.tb{height:90px;display:flex;align-items:flex-end;justify-content:center;gap:3px}.tb i{width:40%;border-radius:3px 3px 0 0;min-height:1px}.tc small{color:var(--muted);font-size:11px}
</style>
</head>
<body>
<main>
  <div class="head"><h1>💰 Budget Tracker</h1><span><input type="month" id="month" aria-label="Month"><button type="button" id="gear" aria-label="Settings">⚙️</button></span></div>

  
  <div id="hi"></div>
  
  <div class="card"><div class="grid">
    <div class="stat"><small>Income</small><b class="inc" id="sInc">0</b></div>
    <div class="stat"><small>Spent</small><b class="exp" id="sExp">0</b></div>
    <div class="stat"><small>Balance</small><b id="sBal">0</b></div>
  </div></div>

  <div class="card">
    <h2>Monthly spending limit</h2>
    <div class="row"><input type="number" id="limit" inputmode="decimal" placeholder="Set a limit (e.g. 1500)" min="0"></div>
    <div class="bar"><i id="limBar" style="width:0"></i></div>
    <small id="limTxt" style="color:var(--muted)">No limit set</small>
  </div>

  <div class="card">
    <h2>Add transaction</h2>
    <div class="seg"><button id="tExp" class="on">Expense</button><button id="tInc">Income</button></div>
    <div class="row"><input type="number" id="amt" inputmode="decimal" placeholder="Amount" min="0" step="0.01"><input type="date" id="date"></div>
    <div class="row"><select id="cat"></select><button type="button" class="pick" id="catBtn"></button><input id="note" list="items" placeholder="Item or note (search…)"><datalist id="items"></datalist></div>
    <button class="primary" id="add">Add</button>
  </div>

  <div class="card">
    <h2>Savings goal</h2>
    <div class="row"><input type="number" id="goal" inputmode="decimal" placeholder="Target amount (e.g. 5000)" min="0"></div>
    <div class="bar"><i id="goalBar" style="width:0;background:var(--inc)"></i></div>
    <small id="goalTxt" style="color:var(--muted)">No goal set</small>
  </div>

  <div class="card"><h2>Insights this month</h2><div id="ins"></div></div>

  <div class="card"><h2>Last 6 months · green income, red spending</h2><div id="trend"></div></div>

  <div class="card"><h2>Spending by category</h2><div id="cats"></div></div>

  <div class="card"><h2>Transactions</h2><div class="row"><input id="q" placeholder="Search by note or category"></div><div id="list"></div></div>
</main>
<div class="ov" id="sov"><div class="sheet" style="max-height:92%"><div class="grab"></div><div class="head"><span style="font-size:18px;font-weight:700">Settings</span><button type="button" id="sx">Done</button></div><div class="list">
<h3>Appearance</h3><div class="sw" id="sw" aria-label="Theme"></div>
<h3>Language</h3><div class="row"><select id="lang" aria-label="Language"></select></div>
<h3>Currency</h3><div class="row"><input id="cur" list="curs" placeholder="Currency (search…)" aria-label="Currency"><datalist id="curs"></datalist></div>
<h3>Profile</h3><input id="uname" placeholder="Your name (optional)">
<h3>Budget</h3>
<div class="srow"><span>Warn me when spending reaches</span><select id="thr" style="flex:none;width:auto"><option value="70">70%</option><option value="80">80%</option><option value="90">90%</option></select></div>
<div class="srow"><span>Round amounts to whole numbers</span><input type="checkbox" id="rnd" style="flex:none;width:22px;height:22px"></div>
<h3>Security</h3>
<div class="srow"><span id="pinTxt"></span></div>
<div class="row"><input id="pin" type="password" inputmode="numeric" maxlength="6" placeholder="New PIN (4 to 6 digits)"><button type="button" id="pinSet">Set</button><button type="button" id="pinOff">Remove</button></div>
<h3>Your data</h3>
<div class="row"><button type="button" id="bkExp" style="flex:1">Export backup</button><button type="button" id="bkImp" style="flex:1">Import backup</button></div>
<textarea id="bk" rows="3" placeholder="Backup text appears here. To restore, paste it here and tap Import."></textarea>
<small id="bkMsg" style="color:var(--muted)"></small>
<button type="button" id="bkRst" class="danger" style="margin-top:10px">Reset all data</button>
<h3>About</h3>
<div class="about"><b>Budget Tracker</b> · Version 1.0.0<br>Privacy: your data stays on this device. No account, no ads, no tracking, and nothing is sent to a server.<br>Terms: this app offers general budgeting tools, not financial advice.</div>
</div></div></div>
<div class="ov" id="lock" style="z-index:100;align-items:center;background:var(--page,var(--bg))"><div class="card" style="width:min(320px,90%);text-align:center"><h2 style="color:var(--text);font-size:20px">🔒 Enter PIN</h2><input id="pin2" type="password" inputmode="numeric" maxlength="6" placeholder="PIN" style="text-align:center;margin-bottom:8px"><button type="button" class="primary" id="unl">Unlock</button><small id="pinErr" style="color:var(--exp)"></small></div></div>
<div class="ov" id="ov"><div class="sheet"><div class="grab"></div><input id="cq" placeholder="Search categories…"><div class="list" id="cl"></div></div></div>
<script>
(function(){
var KEY="budget-tracker-v1",COMMON=["Food","Housing","Transport","Bills","Health","Study","Shopping","Fun","Savings"],PL={single:"Single",couple:"Couple",family:"Family"},PROF={single:["Gym & fitness","Subscriptions","Personal care","Travel","Courses & books","Hobbies"],couple:["Date nights","Gifts","Joint savings","Travel","Home & furniture","Wedding & events"],family:["Groceries","Childcare","School fees","Kids' activities","Family outings","Insurance","Elder care","Home & repairs"]},INC=["Salary","Freelance","Gift","Other"];
var S={tx:[],limit:0},type="exp";
try{var raw=localStorage.getItem(KEY);if(raw){var p=JSON.parse(raw);if(p&&Array.isArray(p.tx))S=p}}catch(e){}
function save(){try{localStorage.setItem(KEY,JSON.stringify(S))}catch(e){}}
var $=function(id){return document.getElementById(id)};
var PAL=["#2563eb","#f59e0b","#10b981","#ef4444","#8b5cf6","#ec4899","#14b8a6","#f97316","#64748b"];
var IC={Food:"🍽️",Housing:"🏠",Transport:"🚌",Bills:"💡",Health:"🩺",Study:"📚",Shopping:"🛍️",Fun:"🎉",Savings:"🐷","Gym & fitness":"🏋️",Subscriptions:"📺","Personal care":"💆",Travel:"✈️","Courses & books":"🎓",Hobbies:"🎨","Date nights":"🍷",Gifts:"🎁",Gift:"🎁","Joint savings":"💞","Home & furniture":"🛋️","Wedding & events":"💍",Groceries:"🛒",Childcare:"🧸","School fees":"🏫","Kids' activities":"⚽","Family outings":"🎡",Insurance:"🛡️","Elder care":"🧓","Home & repairs":"🔧",Salary:"💼",Freelance:"💻"};
var ic=function(c){return IC[c]||"📦"};
var CODES=[],DN=null;try{CODES=Intl.supportedValuesOf("currency")}catch(e){CODES="USD,EUR,GBP,JPY,INR,CNY,AUD,CAD,CHF,AED,SAR,BRL,MXN,ZAR,NGN,KES,PKR,BDT,IDR,KRW,TRY,RUB,EGP,THB,VND,PHP,MYR,SGD,NZD,SEK,NOK,DKK,PLN,ILS".split(",")}
var fc=function(a){var o={minimumFractionDigits:0,maximumFractionDigits:S.round?0:2};try{if(/^[A-Z]{3}$/.test(S.cur||"")){o.style="currency";o.currency=S.cur}return a.toLocaleString(S.lang||undefined,o)}catch(e){return String(a)}};
var MN=["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"];
var fmt=function(n){return (n<0?"−":"")+fc(Math.abs(n))};
function today(){var d=new Date();return d.getFullYear()+"-"+String(d.getMonth()+1).padStart(2,"0")+"-"+String(d.getDate()).padStart(2,"0")}
$("date").value=today();$("month").value=today().slice(0,7);$("limit").value=S.limit||"";$("goal").value=S.goal||"";if(!/^[A-Z]{3}$/.test(S.cur||""))S.cur="";$("cur").value=S.cur;
function cats(){
  var o=function(a){return a.map(function(c){return "<option>"+c+"</option>"}).join("")};
  if(type==="exp"){$("cat").innerHTML='<optgroup label="Everyday">'+o(COMMON)+'</optgroup><optgroup label="Single">'+o(PROF.single)+'</optgroup><optgroup label="Couple">'+o(PROF.couple)+'</optgroup><optgroup label="Family">'+o(PROF.family)+'</optgroup><option>Other</option>'}
  else $("cat").innerHTML=o(INC);
  sheet();
}
function setType(t){type=t;$("tExp").classList.toggle("on",t==="exp");$("tInc").classList.toggle("on",t==="inc");cats()}
$("tExp").onclick=function(){setType("exp")};$("tInc").onclick=function(){setType("inc")};
function esc(s){return String(s).replace(/[&<>"]/g,function(c){return{"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;"}[c]})}
function extras(m,inc,exp,by,tx){
  var y=+m.slice(0,4),mo=+m.slice(5,7),dim=new Date(y,mo,0).getDate(),t=today(),cm=t.slice(0,7),el=cm===m?+t.slice(8):(m<cm?dim:0),h="";
  if(exp>0){
    var big=tx.filter(function(x){return x.type==="exp"}).sort(function(a,b){return b.amt-a.amt})[0];
    if(el>0){var avg=exp/el;h+='<div class="cat">Daily average<span>'+fmt(avg)+'</span></div>';if(cm===m)h+='<div class="cat">Projected month total<span>'+fmt(avg*dim)+'</span></div>'}
    h+='<div class="cat">Biggest expense<span>'+esc(big.note||big.cat)+' · '+fmt(big.amt)+'</span></div>';
  }
  if(inc>0)h+='<div class="cat">Savings rate<span>'+Math.round((inc-exp)/inc*100)+'%</span></div>';
  $("ins").innerHTML=h||'<div class="empty">Add transactions to see insights</div>';
  var net=S.tx.reduce(function(s,x){return s+(x.type==="inc"?x.amt:-x.amt)},0),G=S.goal||0;
  if(G>0){var gp=Math.max(0,Math.min(100,net/G*100));$("goalBar").style.width=gp+"%";$("goalTxt").textContent=fmt(Math.max(0,net))+" of "+fmt(G)+" ("+Math.round(gp)+"%), based on your all-time balance"}
  else{$("goalBar").style.width="0";$("goalTxt").textContent="No goal set"}
  var ms=[],i;for(i=5;i>=0;i--){var d=new Date(y,mo-1-i,1);ms.push(d.getFullYear()+"-"+String(d.getMonth()+1).padStart(2,"0"))}
  var data=ms.map(function(k){var a=0,b=0;S.tx.forEach(function(x){if(x.date.slice(0,7)===k){if(x.type==="inc")a+=x.amt;else b+=x.amt}});return[k,a,b]});
  var mx=Math.max.apply(null,data.map(function(d){return Math.max(d[1],d[2])}).concat([1]));
  $("trend").innerHTML=data.map(function(d){return '<div class="tc"><div class="tb"><i style="height:'+d[1]/mx*100+'%;background:var(--inc)"></i><i style="height:'+d[2]/mx*100+'%;background:var(--exp)"></i></div><small>'+MN[+d[0].slice(5)-1]+'</small></div>'}).join("");
}
function render(){
  var m=$("month").value,tx=S.tx.filter(function(t){return t.date.slice(0,7)===m}).sort(function(a,b){return b.date.localeCompare(a.date)||b.id-a.id});
  var inc=0,exp=0,by={};
  tx.forEach(function(t){if(t.type==="inc")inc+=t.amt;else{exp+=t.amt;by[t.cat]=(by[t.cat]||0)+t.amt}});
  $("sInc").textContent=fmt(inc);$("sExp").textContent=fmt(exp);
  var bal=inc-exp,b=$("sBal");b.textContent=fmt(bal);b.className=bal>=0?"inc":"exp";
  var L=S.limit||0,bar=$("limBar");
  if(L>0){var pct=Math.min(100,exp/L*100);bar.style.width=pct+"%";bar.style.background=exp>L?"var(--exp)":pct>(S.thr||80)?"var(--warn)":"var(--accent)";
    $("limTxt").textContent=exp>L?"Over limit by "+fmt(exp-L):fmt(L-exp)+" left of "+fmt(L)}
  else{bar.style.width="0";$("limTxt").textContent="No limit set"}
  var keys=Object.keys(by).sort(function(a,b){return by[b]-by[a]});
  var acc=0,seg=keys.map(function(k,i){var s=acc/exp*100;acc+=by[k];return PAL[i%PAL.length]+" "+s+"% "+(acc/exp*100)+"%"}).join(",");
  var dn=keys.length?'<div class="donut" style="background:conic-gradient('+seg+')"><b>'+fmt(exp)+'</b></div>':"";
  $("cats").innerHTML=keys.length?dn+keys.map(function(k,i){var w=exp?by[k]/exp*100:0;return '<div class="cat"><i class="dot" style="background:'+PAL[i%PAL.length]+'"></i>'+ic(k)+' '+esc(k)+'<span>'+fmt(by[k])+' · '+Math.round(w)+'%</span><div class="bar"><i style="width:'+w+'%"></i></div></div>'}).join(""):'<div class="empty">No spending yet this month</div>';
  extras(m,inc,exp,by,tx);var q=($("q").value||"").toLowerCase();tx=tx.filter(function(t){return !q||(t.note+" "+t.cat).toLowerCase().indexOf(q)>-1});
  $("list").innerHTML=tx.length?tx.map(function(t){return '<div class="tx"><span style="font-size:22px">'+ic(t.cat)+'</span><div>'+esc(t.note||t.cat)+'<small>'+esc(t.cat)+' · '+t.date+'</small></div><b class="'+t.type+'">'+(t.type==="inc"?"+":"−")+fmt(t.amt)+'</b><button data-id="'+t.id+'" aria-label="Delete">✕</button></div>'}).join(""):'<div class="empty">No transactions yet</div>';
}
$("add").onclick=function(){
  var a=parseFloat($("amt").value);
  if(!(a>0)){$("amt").focus();return}
  S.tx.push({id:Date.now(),type:type,amt:a,cat:$("cat").value,note:$("note").value.trim(),date:$("date").value||today()});
  $("amt").value="";$("note").value="";save();
  $("month").value=($("date").value||today()).slice(0,7);render();
};
$("list").onclick=function(e){var id=e.target.getAttribute&&e.target.getAttribute("data-id");if(id){S.tx=S.tx.filter(function(t){return String(t.id)!==id});save();render()}};
$("limit").oninput=function(){S.limit=parseFloat(this.value)||0;save();render()};
$("month").onchange=render;$("q").oninput=render;
$("goal").oninput=function(){S.goal=parseFloat(this.value)||0;save();render()};
$("cur").onchange=function(){var v=this.value.trim().toUpperCase(),c=v.slice(0,3),q=this.value.trim().toLowerCase();if(CODES.
