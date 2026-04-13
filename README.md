<!DOCTYPE html>
<html>
<head>
<title>iPhone 16 UI Final</title>

<style>
body{
margin:0;
background:#000;
display:flex;
justify-content:center;
align-items:center;
height:100vh;
font-family:-apple-system,BlinkMacSystemFont,sans-serif;
}

.phone{
width:360px;
height:700px;
background:black;
border-radius:40px;
overflow:hidden;
position:relative;
}

.page{
display:none;
width:100%;
height:100%;
position:absolute;
top:0;
left:0;
transition:0.5s;
}

/* 🍎 BOOT */
#boot{
background:#000;
display:flex;
justify-content:center;
align-items:center;
}

.boot-content{
display:flex;
flex-direction:column;
align-items:center;
}

.apple-logo svg{
animation:appleGlow 2.5s ease-in-out infinite;
}

@keyframes appleGlow{
0%{opacity:0.2; transform:scale(0.85); filter:drop-shadow(0 0 5px white);}
40%{opacity:1; transform:scale(1); filter:drop-shadow(0 0 25px white);}
70%{opacity:0.9; transform:scale(1.05); filter:drop-shadow(0 0 35px white);}
100%{opacity:0.2; transform:scale(0.9); filter:drop-shadow(0 0 5px white);}
}

.boot-bar{
width:200px;
height:4px;
background:#222;
border-radius:10px;
margin-top:30px;
overflow:hidden;
}

.boot-progress{
width:0%;
height:100%;
background:white;
transition:0.3s;
}

/* 📱 Dynamic Island */
.dynamic-island{
position:absolute;
top:10px;
left:50%;
transform:translateX(-50%);
width:120px;
height:35px;
background:black;
border-radius:25px;
display:flex;
justify-content:center;
align-items:center;
color:white;
font-size:12px;
transition:0.4s;
z-index:10;
}

.dynamic-island.active{
width:220px;
height:45px;
}

/* 🔒 LOCK */
#lock{
background:linear-gradient(to bottom,#000,#111);
color:white;
display:flex;
flex-direction:column;
align-items:center;
padding-top:60px;
}

.big-time{
font-size:60px;
margin-top:20px;
}

.date{
font-size:14px;
opacity:0.7;
margin-bottom:40px;
}

.dots{
font-size:20px;
letter-spacing:8px;
}

.keypad{
display:grid;
grid-template-columns:repeat(3,80px);
gap:15px;
margin-top:20px;
}

.key{
width:80px;
height:80px;
border-radius:50%;
background:rgba(255,255,255,0.1);
display:flex;
justify-content:center;
align-items:center;
font-size:22px;
}

.enter{
margin-top:20px;
padding:10px 30px;
background:#0a84ff;
border-radius:30px;
}

/* HOME */
#home{
background:url("https://images.unsplash.com/photo-1500530855697-b586d89ba3ee");
background-size:cover;
color:white;
display:flex;
justify-content:center;
align-items:center;
font-size:22px;
}
</style>
</head>

<body>

<div class="phone">

<!-- 🍎 BOOT -->
<div id="boot" class="page">
<div class="boot-content">
<div class="apple-logo">
<svg viewBox="0 0 24 24" width="90" height="90">
<path fill="white" d="M16.365 1.43c0 1.14-.42 2.21-1.13 2.99-.74.81-1.95 1.43-3.09 1.33-.15-1.11.44-2.24 1.16-2.97.8-.82 2.18-1.4 3.06-1.35zM21.54 17.52c-.58 1.3-.86 1.88-1.6 3.04-1.04 1.66-2.51 3.74-4.34 3.75-1.62.02-2.04-1.06-4.24-1.05-2.2.01-2.66 1.07-4.28 1.05-1.83-.01-3.22-1.9-4.26-3.56C.83 18.34-.8 13.97 1.18 10.7c1.1-1.82 3.06-2.97 5.19-3 1.64-.03 3.18 1.1 4.24 1.1 1.06 0 3.05-1.36 5.15-1.16.88.04 3.35.36 4.94 2.68-.13.08-2.95 1.73-2.92 5.17.03 4.11 3.62 5.48 3.76 5.53z"/>
</svg>
</div>

<div class="boot-bar">
<div class="boot-progress" id="bootProgress"></div>
</div>
</div>
</div>

<!-- 🔒 LOCK -->
<div id="lock" class="page">

<div class="dynamic-island" id="island">🔕 Silent</div>

<div class="big-time" id="time"></div>
<div class="date" id="date"></div>

<div class="dots" id="dots">○ ○ ○ ○</div>

<div class="keypad">
<div class="key" onclick="press(1)">1</div>
<div class="key" onclick="press(2)">2</div>
<div class="key" onclick="press(3)">3</div>
<div class="key" onclick="press(4)">4</div>
<div class="key" onclick="press(5)">5</div>
<div class="key" onclick="press(6)">6</div>
<div class="key" onclick="press(7)">7</div>
<div class="key" onclick="press(8)">8</div>
<div class="key" onclick="press(9)">9</div>
<div></div>
<div class="key" onclick="press(0)">0</div>
<div class="key" onclick="clearPin()">⌫</div>
</div>

<div class="enter" onclick="unlock()">Unlock</div>
</div>

<!-- HOME -->
<div id="home" class="page">
iPhone 16 UI 🔥
</div>

</div>

<script>

/* BOOT */
let p=0;
document.getElementById("boot").style.display="flex";

let boot=setInterval(()=>{
p+=Math.random()*15;

if(p>=100){
p=100;
clearInterval(boot);

document.getElementById("boot").style.opacity="0";

setTimeout(()=>{
document.getElementById("boot").style.display="none";
document.getElementById("lock").style.display="flex";
},600);
}

document.getElementById("bootProgress").style.width=p+"%";
},300);

/* TIME */
setInterval(()=>{
let d=new Date();
document.getElementById("time").innerText=d.getHours()+":"+String(d.getMinutes()).padStart(2,'0');
document.getElementById("date").innerText=d.toDateString();
},1000);

/* PIN */
let pin="";
function press(n){ if(pin.length<4){pin+=n;update();} }
function update(){
let d="";
for(let i=0;i<pin.length;i++) d+="● ";
for(let i=pin.length;i<4;i++) d+="○ ";
document.getElementById("dots").innerText=d;
}
function clearPin(){pin=pin.slice(0,-1);update();}

/* Dynamic Island */
function showIsland(msg){
let island=document.getElementById("island");
island.innerText=msg;
island.classList.add("active");
setTimeout(()=>island.classList.remove("active"),2000);
}

/* Unlock */
function unlock(){
if(pin==="6664"){
document.querySelectorAll(".page").forEach(p=>p.style.display="none");
document.getElementById("home").style.display="flex";
showIsland("🔓 Unlocked");
}else{
alert("Wrong PIN");
pin="";update();
}
}

</script>

</body>
</html>
