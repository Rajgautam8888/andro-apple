<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">


<style>
*{margin:0;padding:0;box-sizing:border-box;}

body{
font-family:-apple-system, BlinkMacSystemFont, sans-serif;
background:#000;
color:#fff;
overflow:hidden;
}

/* Pages */
.page{
display:none;
height:100vh;
width:100%;
justify-content:center;
align-items:center;
flex-direction:column;
}

/* BOOT */
#boot{display:flex;background:#000;}

.apple-logo svg{
animation:glow 2.5s infinite ease-in-out;
}

@keyframes glow{
0%{opacity:0.2;transform:scale(0.8);filter:drop-shadow(0 0 5px #fff);}
50%{opacity:1;transform:scale(1.1);filter:drop-shadow(0 0 40px #fff);}
100%{opacity:0.2;transform:scale(0.8);}
}

.boot-bar{
width:220px;height:4px;background:#222;
margin-top:30px;border-radius:10px;overflow:hidden;
}

.boot-progress{
height:100%;width:0%;
background:#fff;
}

/* LOCK SCREEN */
#lock{
display:none;
background:url('https://images.unsplash.com/photo-1506744038136-46273834b3fb') center/cover;
backdrop-filter:blur(10px);
}

.lock-box{
background:rgba(0,0,0,0.4);
padding:25px;
border-radius:20px;
backdrop-filter:blur(15px);
}

.dots{display:flex;gap:10px;margin:20px;justify-content:center;}
.dot{
width:12px;height:12px;border-radius:50%;
background:#555;
}
.dot.active{background:#fff;}

.keypad button{
width:65px;height:65px;
margin:6px;
border-radius:50%;
border:none;
background:rgba(255,255,255,0.1);
color:#fff;
font-size:18px;
backdrop-filter:blur(10px);
}

/* HOME */
#home{
display:none;
background:url('https://images.unsplash.com/photo-1492724441997-5dc865305da7') center/cover;
position:relative;
}

/* Dynamic Island */
.dynamic-island{
position:absolute;
top:12px;
left:50%;
transform:translateX(-50%);
background:rgba(0,0,0,0.7);
padding:8px 20px;
border-radius:30px;
font-size:13px;
backdrop-filter:blur(10px);
transition:0.4s;
}

/* App Grid */
.app-grid{
display:grid;
grid-template-columns:repeat(4,1fr);
gap:25px;
margin-top:120px;
padding:20px;
text-align:center;
}

.app{
cursor:pointer;
transition:0.3s;
}

.app:hover{
transform:scale(1.1);
}

.icon{
width:65px;height:65px;
border-radius:18px;
display:flex;
justify-content:center;
align-items:center;
font-size:26px;
margin:auto;
box-shadow:0 8px 20px rgba(0,0,0,0.5);
}

.label{
font-size:12px;
margin-top:6px;
}

/* Apps Page */
iframe{
width:92%;
height:320px;
border:none;
border-radius:15px;
margin-top:20px;
}

button{
padding:10px 20px;
border:none;
border-radius:10px;
background:#fff;
color:#000;
margin-top:20px;
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
<div class="lock-box">
<h3 align="center">Enter Password</h3>

<div class="dots">
<div class="dot"></div><div class="dot"></div>
<div class="dot"></div><div class="dot"></div>
</div>

<div class="keypad" align="center">
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
</div>

<!-- HOME -->
<div id="home" class="page">
<div class="dynamic-island" id="island">📱 Ready</div>

<div class="app-grid">

<div class="app" onclick="openApp('youtube')">
<div class="icon" style="background:red;">▶️</div>
<div class="label">YouTube</div>
</div>

<div class="app" onclick="openApp('flipkart')">
<div class="icon" style="background:#2874f0;">🛒</div>
<div class="label">Flipkart</div>
</div>

<div class="app" onclick="openApp('spotify')">
<div class="icon" style="background:#1db954;">🎵</div>
<div class="label">Spotify</div>
</div>

<div class="app" onclick="openApp('camera')">
<div class="icon" style="background:#555;">📷</div>
<div class="label">Camera</div>
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

<div id="camera" class="page">
<h2>Camera</h2>
<p>📸 Camera UI Coming Soon</p>
<button onclick="goHome()">Back</button>
</div>

<script>
let progress=0, pin="";

document.getElementById("boot").style.display="flex";

let boot=setInterval(()=>{
progress+=8;
bootProgress.style.width=progress+"%";

if(progress>=100){
clearInterval(boot);
boot.style.opacity="0";
setTimeout(()=>{
boot.style.display="none";
lock.style.display="flex";
},500);
}
},250);

function press(n){
if(pin.length<4){
pin+=n;updateDots();
if(pin.length===4) unlock();
}
}

function updateDots(){
document.querySelectorAll(".dot").forEach((d,i)=>{
d.classList.toggle("active",i<pin.length);
});
}

function unlock(){
if(pin==="8888"){
showPage("home");
showIsland("🔓 Unlocked");
}else{
showIsland("❌ Wrong");
pin="";updateDots();
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

function goHome(){showPage("home");}

function showIsland(msg){
let i=document.getElementById("island");
i.innerText=msg;
setTimeout(()=>i.innerText="📱 Ready",2000);
}
</script>

</body>
</html>
