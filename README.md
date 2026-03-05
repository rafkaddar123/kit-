<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Raafaa | Cyber Portal</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">

<style>
/* ====== أساسي ====== */
body{
margin:0;
font-family:'Orbitron',sans-serif;
background:black;
color:white;
overflow:hidden;
}

/* ====== شاشة التحميل ====== */
#loader{
position:fixed;
width:100%;
height:100%;
background:black;
display:flex;
justify-content:center;
align-items:center;
flex-direction:column;
z-index:100;
color:#00ff99;
font-size:18px;
}
.bar{
width:200px;
height:4px;
background:#111;
margin-top:15px;
overflow:hidden;
}
.bar span{
display:block;
height:100%;
width:0;
background:#00ff99;
animation:load 3s linear forwards;
}
@keyframes load{to{width:100%;}}

/* ====== Matrix Rain ====== */
canvas{
position:fixed;
top:0;
left:0;
z-index:-1;
}

/* ====== المحتوى ====== */
.container{
position:absolute;
top:50%;
left:50%;
transform:translate(-50%,-50%);
text-align:center;
transition:transform 0.2s ease;
}

.card{
background:rgba(0,0,0,0.75);
padding:40px;
border-radius:20px;
box-shadow:0 0 25px #00ff99;
}

/* ====== صورة شخصية مع Neon + Glitch + Blur + Scan ====== */
.profile-wrapper{
position:relative;
width:180px;
height:180px;
margin:0 auto 25px auto;
display:flex;
justify-content:center;
align-items:center;
perspective:1000px;
}
.profile-pic{
width:150px;
height:150px;
object-fit:cover;
border-radius:50%;
backdrop-filter:blur(8px);
background:rgba(0,255,153,0.05);
border:2px solid rgba(0,255,153,0.4);
box-shadow:0 0 20px #00ff99;
animation:glitchIntro 0.6s ease;
}
.neon-ring{
position:absolute;
width:170px;
height:170px;
border-radius:50%;
border:3px solid transparent;
border-top:3px solid #00ff99;
border-right:3px solid #00ffff;
animation:spin 4s linear infinite;
box-shadow:0 0 20px #00ff99;
}
@keyframes spin{from{transform:rotate(0deg);} to{transform:rotate(360deg);}}
@keyframes glitchIntro{0%{transform:translate(0);}20%{transform:translate(-3px,2px);}40%{transform:translate(3px,-2px);}60%{transform:translate(-2px,1px);}80%{transform:translate(2px,-1px);}100%{transform:translate(0);}}
.scanlines{
position:absolute;
width:150px;
height:150px;
border-radius:50%;
pointer-events:none;
background:repeating-linear-gradient(
to bottom,
rgba(255,255,255,0.08) 0px,
rgba(255,255,255,0.08) 1px,
transparent 2px,
transparent 4px
);
mix-blend-mode:overlay;
animation:scanMove 3s linear infinite;
}
@keyframes scanMove{from{background-position:0 0;}to{background-position:0 20px;}}

/* ====== عنوان وTypewriter ====== */
h1{
color:#00ff99;
margin:10px 0 5px 0;
font-size:30px;
}
.typewriter{
margin-top:10px;
font-size:14px;
opacity:0.8;
border-right:2px solid #00ff99;
white-space:nowrap;
overflow:hidden;
width:0;
animation:typing 4s steps(40,end) forwards, blink 0.7s infinite;
}
@keyframes typing{from{width:0}to{width:100%;}}
@keyframes blink{50%{border-color:transparent}}

/* ====== أزرار تفاعلية ====== */
.btn{
display:block;
margin:15px 0;
padding:12px;
border-radius:10px;
text-decoration:none;
color:white;
background:linear-gradient(90deg,#00ff99,#00ffff);
transition:0.3s;
position:relative;
overflow:hidden;
}
.btn:hover{transform:scale(1.08); box-shadow:0 0 15px #00ff99;}
.btn:active{animation:pulse 0.4s ease;}
@keyframes pulse{0%{box-shadow:0 0 0px #00ff99;}50%{box-shadow:0 0 30px #00ff99;}100%{box-shadow:0 0 0px #00ff99;}}
</style>
</head>
<body>

<!-- شاشة التحميل -->
<div id="loader">
<span>Initializing Cyber System...</span>
<div class="bar"><span></span></div>
</div>

<!-- Matrix Rain -->
<canvas id="matrix"></canvas>

<!-- المحتوى -->
<div class="container" id="parallax">
<div class="card">

<!-- الصورة الشخصية -->
<div class="profile-wrapper">
  <div class="neon-ring"></div>
  <div class="scanlines"></div>
  <img src="your-image.jpg" class="profile-pic">
</div>

<!-- العنوان والنص -->
<h1>RAAFAA</h1>
<div class="typewriter">Cyber Developer | Creative Hacker | Digital Architect</div>

<!-- الأزرار -->
<a href="https://tiktok.com/@studio0906" class="btn cyber-link" target="_blank"><i class="fab fa-tiktok"></i> TikTok</a>
<a href="https://www.instagram.com/stu_dior1?igsh=OGh0ZGpsb2hnZXFx" class="btn cyber-link" target="_blank"><i class="fab fa-instagram"></i> Instagram</a>
<a href="https://youtube.com/@Studio-q6i" class="btn cyber-link" target="_blank"><i class="fab fa-youtube"></i> YouTube</a>

</div>
</div>

<script>
// ====== إخفاء شاشة التحميل ======
setTimeout(()=>{document.getElementById("loader").style.display="none";},3000);

// ====== Matrix Rain ======
const canvas=document.getElementById("matrix");
const ctx=canvas.getContext("2d");
canvas.width=window.innerWidth;
canvas.height=window.innerHeight;
const letters="アァカサタナハマヤャラワ0123456789";
const fontSize=16;
const columns=canvas.width/fontSize;
const drops=[];
for(let x=0;x<columns;x++) drops[x]=1;
function draw(){
ctx.fillStyle="rgba(0,0,0,0.05)";
ctx.fillRect(0,0,canvas.width,canvas.height);
ctx.fillStyle="#00ff99";
ctx.font=fontSize+"px monospace";
for(let i=0;i<drops.length;i++){
const text=letters[Math.floor(Math.random()*letters.length)];
ctx.fillText(text,i*fontSize,drops[i]*fontSize);
if(drops[i]*fontSize>canvas.height && Math.random()>0.975) drops[i]=0;
drops[i]++;
}}
setInterval(draw,35);

// ====== 3D Parallax ======
const container=document.getElementById("parallax");
const pic=document.querySelector(".profile-pic");
if(window.DeviceOrientationEvent){
window.addEventListener("deviceorientation",(e)=>{
let x=e.gamma/15; let y=e.beta/20;
container.style.transform=`translate(-50%,-50%) rotateY(${x}deg) rotateX(${-y}deg)`;
pic.style.transform=`rotateY(${x}deg) rotateX(${-y}deg)`;
});
}

// ====== أزرار تفاعلية Neon + اهتزاز + صوت ======
const links=document.querySelectorAll(".cyber-link");
const clickSound=new Audio("https://assets.mixkit.co/sfx/preview/mixkit-arcade-game-jump-coin-216.wav");
links.forEach(link=>{
link.addEventListener("click",function(e){
e.preventDefault();
clickSound.play();
if(navigator.vibrate) navigator.vibrate(100);
let url=this.href;
setTimeout(()=>{window.open(url,"_blank");},400);
});
});
</script>
</body>
</html>
