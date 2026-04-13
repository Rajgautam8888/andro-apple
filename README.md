<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>iPhone UI</title>

<style>
body{
margin:0;
font-family:sans-serif;
background:black;
color:white;
}

/* Pages */
.page{
display:none;
height:100vh;
justify-content:center;
align-items:center;
flex-direction:column;
}

/* BOOT */
#boot{
display:flex;
background:black;
}

.apple-logo svg{
animation:appleGlow 2.5s infinite;
}

@keyframes appleGlow{
0%{opacity:0.2; transform:scale(0.8); filter:drop-shadow(0 0 5px white);}
50%{opacity:1; transform:scale(1.1); filter:drop-shadow(0 0 30px white);}
100%{opacity:0.2; transform:scale(0.8);}
}

.boot-bar{
width:200px;
height:4px;
background:#222;
margin-top:20px;
border-radius:10px;
overflow:hidden;
}

.boot-progress{
height:100%;
width:0%;
background:white;
}

/* LOCK */
#lock{
display:none;
}

.dots{
display:flex;
gap:10px;
margin:20px;
}

.dot{
width:15px;
height:15px;
border-radius:50%;
background:#444;
}

.active{background:white;}

.keypad button{
width:60px;
height:60px;
margin:5px;
border:none;
border-radius:50%;
font-size:18px;
}

/* HOME */
#home{
display:none;
position:relative;
}

/* Dynamic Island */
.dynamic-island{
position:absolute;
top:10px;
left:50%;
transform:translateX(-50%);
background:black;
padding:10px 20px;
border-radius:20px;
font-size:12px;
}

/* Apps */
.app-grid{
display:grid;
grid-template-columns:repeat(3,1fr);
gap:20px;
margin-top:80px;
text-align:center;
}

.icon{
width:70px;
height:70px;
border-radius:20px;
display:flex;
justify-content:center;
align-items:center;
font-size:30px;
margin:auto;
}

iframe{
width:90%;
height:300px;
border:none;
border-radius:10px;
margin-top:20px;
}

button{
margin-top:20px;
padding:10px;
}
</style>
</head>

<body>

<!-- BOOT -->
<div id="boot" class="page">
<div class="apple-logo">
<svg viewBox="0 0 24 24" width="100">
<path fill="white" d="M16.365 1.43c0 1.14-.42 2.21-1.13 2.99-.74.81-1.95 1.43-3.09 1.33-.15-1.11.44-2.24 1.16-2.97.8-.82 2.18-1.4 3.06-1.35z"/>
</svg>
</div>
<div class="boot-bar">
<div class="boot-progress" id="bootProgress"></div>
</div>
</div>

<!-- LOCK -->
<div id="lock" class="page">
<h2>Enter Password</h2>

<div class="dots" id="dots">
<div class="dot"></div>
<div class="dot"></div>
<div class="dot"></div>
<div class="dot"></div>
</div>

<div class="keypad">
<button onclick="press(1)">1</button>
<button onclick="press(2)">2</button>
<button onclick="press(3)">3</button><br>
<button onclick="press(4)">4</button>
<button onclick="press(5)">5</button>
<button onclick="press(6)">6</button><br>
<button onclick="press(7)">7</button>
<button onclick="press(8)">8</button>
<button onclick="press(9)">9</button><br>
<button onclick="press(0)">0</button>
</div>
</div>

<!-- HOME -->
<div id="home" class="page">

<div class="dynamic-island" id="island">📱 Ready</div>

<div class="app-grid">
<div onclick="openApp('youtube')">
<div class="icon" style="background:red;">▶️</div>
YouTube
</div>

<div onclick="openApp('flipkart')">
<div class="icon" style="background:#2874f0;">🛒</div>
Flipkart
</div>

<div onclick="openApp('spotify')">
<div class="icon" style="background:#1db954;">🎵</div>
Spotify
</div>
</div>
</div>

<!-- APPS -->
<div id="youtube" class="page">
<h2>YouTube</h2>
<iframe src="https://www.youtube.com/embed/dQw4w9WgXcQ"></iframe>
<button onclick="goHome()">Back</button>
</div>

<div id="flipkart" class="page">
<h2>Flipkart</h2>
<iframe src="https://www.flipkart.com"></iframe>
<button onclick="goHome()">Back</button>
</div>

<div id="spotify" class="page">
<h2>Spotify</h2>
<iframe src="https://open.spotify.com/embed/track/11dFghVXANMlKmJXsNCbNl"></iframe>
<button onclick="goHome()">Back</button>
</div>

<script>
let progress=0;
let pin="";

document.getElementById("boot").style.display="flex";

let boot=setInterval(()=>{
progress+=10;
document.getElementById("bootProgress").style.width=progress+"%";

if(progress>=100){
clearInterval(boot);
document.getElementById("boot").style.display="none";
document.getElementById("lock").style.display="flex";
}
},300);

function press(num){
if(pin.length<4){
pin+=num;
updateDots();
if(pin.length===4) unlock();
}
}

function updateDots(){
let dots=document.querySelectorAll(".dot");
dots.forEach((d,i)=>{
d.classList.toggle("active",i<pin.length);
});
}

function unlock(){
if(pin==="8888"){
showPage("home");
showIsland("🔓 Unlocked");
}else{
showIsland("❌ Wrong");
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
showIsland("📱 "+id+" Opened");
}

function goHome(){
showPage("home");
}

function showIsland(msg){
let island=document.getElementById("island");
island.innerText=msg;
setTimeout(()=>{island.innerText="📱 Ready";},2000);
}
</script>

</body>
</html>
