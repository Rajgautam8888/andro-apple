<!DOCTYPE html>
<html>
<head>
<title>iPhone UI Perfect Fix</title>

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
}

/* 🍎 iPhone 16 BOOT */
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

.apple-logo{
font-size:90px;
animation:fadeApple 2s ease-in-out infinite;
text-shadow:0 0 20px white, 0 0 40px rgba(255,255,255,0.5);
}

@keyframes fadeApple{
0%{opacity:0.3; transform:scale(0.9);}
50%{opacity:1; transform:scale(1);}
100%{opacity:0.3; transform:scale(0.9);}
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
transition:width 0.3s;
}

/* 🔒 LOCK SCREEN */
#lock{
background:linear-gradient(to bottom,#000,#111);
color:white;
display:flex;
flex-direction:column;
align-items:center;
justify-content:flex-start;
padding-top:50px;
}

.top-time{
position:absolute;
top:10px;
font-size:14px;
opacity:0.8;
}

.big-time{
font-size:65px;
font-weight:300;
margin-top:40px;
}

.date{
font-size:14px;
opacity:0.7;
margin-bottom:40px;
}

.dots{
font-size:20px;
letter-spacing:8px;
margin-bottom:15px;
}

.keypad{
display:grid;
grid-template-columns:repeat(3,80px);
gap:15px;
margin-top:10px;
}

.key{
width:80px;
height:80px;
border-radius:50%;
background:rgba(255,255,255,0.08);
display:flex;
justify-content:center;
align-items:center;
font-size:22px;
cursor:pointer;
}

.enter{
margin-top:20px;
padding:14px 35px;
background:#0a84ff;
border-radius:30px;
}

/* HOME */
#home{
background:url("https://images.unsplash.com/photo-1500530855697-b586d89ba3ee");
background-size:cover;
background-position:center;
color:white;
}

.app-grid{
display:grid;
grid-template-columns:repeat(3,1fr);
gap:20px;
padding:30px;
justify-items:center;
margin-top:60px;
}

.icon{
width:70px;
height:70px;
border-radius:20px;
display:flex;
justify-content:center;
align-items:center;
font-size:30px;
}

/* APPS */
#table,#gallery,#aditya,#barkha{
background:#000;
color:white;
text-align:center;
padding:10px;
height:100%;
}

input{
width:85%;
padding:12px;
border-radius:12px;
border:none;
text-align:center;
margin:10px;
}

button{
padding:10px 15px;
border-radius:20px;
border:none;
background:#0a84ff;
color:white;
margin:5px;
}

#photos img{
width:85px;
height:85px;
border-radius:12px;
object-fit:cover;
}
</style>
</head>

<body>

<div class="phone">

<!-- 🍎 BOOT -->
<div id="boot" class="page">
<div class="boot-content">
<div class="apple-logo">🍎</div>
<div class="boot-bar">
<div class="boot-progress" id="bootProgress"></div>
</div>
</div>
</div>

<!-- 🔒 LOCK -->
<div id="lock" class="page">
<div class="top-time" id="topTime"></div>
<div class="big-time" id="bigTime"></div>
<div class="date">Loading...</div>

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
<div class="app-grid">
<div onclick="openApp('table')"><div class="icon" style="background:orange;">📊</div></div>
<div onclick="openApp('gallery')"><div class="icon" style="background:#4cd964;">📸</div></div>
</div>
</div>

</div>

<script>

/* 🍎 BOOT SYSTEM */
let progress = 0;

document.getElementById("boot").style.display="flex";

let bootInterval = setInterval(()=>{
progress += Math.random()*15;

if(progress >= 100){
progress = 100;
clearInterval(bootInterval);

setTimeout(()=>{
document.getElementById("boot").style.display="none";
document.getElementById("lock").style.display="flex";
},500);
}

document.getElementById("bootProgress").style.width = progress + "%";

},300);

/* TIME + DATE */
setInterval(()=>{
let d=new Date();
let t=d.getHours()+":"+String(d.getMinutes()).padStart(2,'0');

document.getElementById("topTime").innerText=t;
document.getElementById("bigTime").innerText=t;

let days=["Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"];
let months=["January","February","March","April","May","June","July","August","September","October","November","December"];

document.querySelector(".date").innerText =
days[d.getDay()]+" • "+months[d.getMonth()]+" "+d.getDate();

},1000);

/* PIN */
let pin="";
function press(n){
if(pin.length<4){
pin+=n;
updateDots();
}
}

function updateDots(){
let d="";
for(let i=0;i<pin.length;i++) d+="● ";
for(let i=pin.length;i<4;i++) d+="○ ";
document.getElementById("dots").innerText=d;
}

function clearPin(){
pin=pin.slice(0,-1);
updateDots();
}

function unlock(){
if(pin==="6664"){
showPage("home");
}else{
alert("Wrong PIN");
pin="";
updateDots();
}
}

function showPage(id){
document.querySelectorAll(".page").forEach(p=>p.style.display="none");
document.getElementById(id).style.display="flex";
}

function openApp(id){
showPage(id);
}

</script>

</body>
</html>
