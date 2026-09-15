<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>HAU HADOMI O DOBEN 🌌</title>

<style>
*{margin:0;padding:0;box-sizing:border-box}
html,body{width:100%;height:100%;overflow:hidden;background:#000;font-family:Arial,sans-serif}
#space{position:fixed;inset:0;width:100%;height:100%;z-index:1}

/* Soft cinematic overlay */
body:after{
  content:"";position:fixed;inset:0;z-index:4;pointer-events:none;
  background:radial-gradient(circle at center,transparent 45%,rgba(0,0,20,.55) 100%);
}

.top{
  position:fixed;top:3.5%;left:50%;transform:translateX(-50%);
  z-index:10;color:#fff;font-size:clamp(11px,1.6vw,18px);
  letter-spacing:7px;text-shadow:0 0 8px #fff,0 0 22px #a855f7,0 0 40px #38bdf8;
  opacity:.9;
}

.message{
  position:fixed;left:50%;bottom:4.5%;transform:translateX(-50%);
  width:min(92%,900px);z-index:10;text-align:center;color:#fff;
  font-size:clamp(10px,1.5vw,17px);line-height:1.7;letter-spacing:1.5px;
  text-shadow:0 0 7px #fff,0 0 18px #a855f7,0 0 28px #38bdf8;
  opacity:0;animation:messageIn 1.5s ease forwards 3.4s;
}
@keyframes messageIn{to{opacity:1;transform:translateX(-50%) translateY(0)}from{opacity:0;transform:translateX(-50%) translateY(15px)}}

.photo{
  position:fixed;z-index:8;width:clamp(90px,13vw,165px);height:clamp(120px,18vw,215px);
  object-fit:cover;border-radius:20px;border:2px solid rgba(255,255,255,.85);
  box-shadow:0 0 12px #fff,0 0 30px #a855f7,0 0 60px #2563eb;
  opacity:0;will-change:transform;
}
.photo1{left:5%;top:33%;animation:photo1in 1.5s ease forwards 3s,photo1fly 7s ease-in-out infinite 4.5s}
.photo2{right:5%;top:34%;animation:photo2in 1.5s ease forwards 3.2s,photo2fly 8s ease-in-out infinite 4.7s}

@keyframes photo1in{from{opacity:0;transform:translate(-180px,80px) rotate(-25deg) scale(.3)}to{opacity:.96;transform:translate(0,0) rotate(-9deg) scale(1)}}
@keyframes photo2in{from{opacity:0;transform:translate(180px,80px) rotate(25deg) scale(.3)}to{opacity:.96;transform:translate(0,0) rotate(9deg) scale(1)}}
@keyframes photo1fly{
  0%,100%{margin-top:0;rotate:-9deg}
  25%{margin-top:-45px;margin-left:18px;rotate:-3deg}
  50%{margin-top:15px;margin-left:-8px;rotate:-14deg}
  75%{margin-top:-30px;margin-left:12px;rotate:-5deg}
}
@keyframes photo2fly{
  0%,100%{margin-top:0;rotate:9deg}
  25%{margin-top:25px;margin-right:18px;rotate:15deg}
  50%{margin-top:-45px;margin-right:-8px;rotate:3deg}
  75%{margin-top:-15px;margin-right:12px;rotate:13deg}
}

.music{
  position:fixed;right:18px;top:18px;z-index:20;
  border:1px solid rgba(255,255,255,.45);border-radius:30px;
  padding:10px 16px;background:rgba(10,5,30,.45);backdrop-filter:blur(10px);
  color:#fff;cursor:pointer;box-shadow:0 0 18px rgba(168,85,247,.55);
}
.music.playing{box-shadow:0 0 30px #38bdf8}

@media(music.mp3:600px){
  .photo1{left:2%;top:24%}.photo2{right:2%;top:25%}
  .top{letter-spacing:4px}
  .message{bottom:3%;letter-spacing:.7px}
}
</style>
</head>

<body>
<canvas id="space"></canvas>

<div class="top">✦ HAU NIA UNIVERSO ✦</div>

<img src="foto1.JPG" class="photo photo1" alt="Foto 1">
<img src="foto2.jpg" class="photo photo2" alt="Foto 2">

<audio id="music" src="music.mp3" loop preload="auto"></audio>
<button id="musicBtn" class="music">🎵 PLAY MUSIC</button>

<div class="message">
  Hau nafatin hili o sai hau nia parseiro moris,<br>
  iha universo hothotu.<br>Maske iha pontos de difisil oinsa mos<br>keta haluha.<br>
  Hau Alex, sei iha.❤️
</div>

<script>
const canvas=document.getElementById("space"),ctx=canvas.getContext("2d");
let W,H,CX,CY;
function resize(){
  W=canvas.width=innerWidth; H=canvas.height=innerHeight;
  CX=W/2; CY=H/2;
}
resize(); addEventListener("resize",resize);

const stars=Array.from({length:1100},()=>({
  x:(Math.random()-.5)*W*2.5,y:(Math.random()-.5)*H*2.5,
  z:Math.random()*W,s:Math.random()*4+1
}));

const dust=Array.from({length:650},()=>({
  a:Math.random()*Math.PI*2,r:Math.random()*Math.max(W,H)*.65,
  s:Math.random()*.0015+.0003,size:Math.random()*2+.2,p:Math.random()*7
}));

/* Create the phrase as particles */
const tc=document.createElement("canvas"),tctx=tc.getContext("2d");
tc.width=1800;tc.height=500;
tctx.fillStyle="#fff";
tctx.font="900 150px Arial";
tctx.textAlign="center";tctx.textBaseline="middle";
tctx.fillText("HADOMI O DOBEN",900,250);

const pix=tctx.getImageData(0,0,tc.width,tc.height).data;
const particles=[];
for(let y=0;y<tc.height;y+=5){
  for(let x=0;x<tc.width;x+=5){
    if(pix[(y*tc.width+x)*4+3]>100){
      particles.push({
        tx:x,ty:y,
        x:CX+(Math.random()-.5)*W*1.7,
        y:CY+(Math.random()-.5)*H*1.7,
        size:Math.random()*2.2+.45,
        phase:Math.random()*Math.PI*2
      });
    }
  }
}

/* 3-second formation */
const start=performance.now();

function draw(now){
  const t=(now-start)/2000;

  const bg=ctx.createRadialGradient(CX,CY,0,CX,CY,Math.max(W,H));
  bg.addColorStop(0,"#180044");bg.addColorStop(.35,"#08001f");bg.addColorStop(1,"#000");
  ctx.fillStyle=bg;ctx.fillRect(0,0,W,H);

  /* flying stars */
  for(const st of stars){
    st.z-=st.s;
    if(st.z<1){st.z=W;st.x=(Math.random()-.5)*W*2.5;st.y=(Math.random()-.5)*H*2.5}
    const sx=CX+st.x*(W/st.z), sy=CY+st.y*(W/st.z);
    const a=1-st.z/W, r=Math.max(.25,(1-st.z/W)*3.5);
    ctx.beginPath();ctx.fillStyle=`rgba(255,255,255,${a})`;
    ctx.shadowBlur=10;ctx.shadowColor="#fff";ctx.arc(sx,sy,r,0,Math.PI*2);ctx.fill();
  }
  ctx.shadowBlur=0;

  /* rotating galaxy dust */
  for(const d of dust){
    d.a+=d.s;
    const x=CX+Math.cos(d.a)*d.r;
    const y=CY+Math.sin(d.a)*d.r*.38;
    const glow=.15+.35*(Math.sin(now*.002+d.p)+1)/2;
    ctx.beginPath();ctx.fillStyle=`rgba(130,180,255,${glow})`;
    ctx.arc(x,y,d.size,0,Math.PI*2);ctx.fill();
  }

  /* phrase */
  const scale=Math.min(W/1800,H/500);
  const progress=Math.min(t/3,1);
  const ease=1-Math.pow(1-progress,3);

  for(const p of particles){
    const targetX=CX+(p.tx-900)*scale;
    const targetY=CY+(p.ty-250)*scale;

    if(t<3){
      p.cx=p.x+(targetX-p.x)*ease;
      p.cy=p.y+(targetY-p.y)*ease;
    }else{
      p.cx=targetX;p.cy=targetY;
    }

    const fx=Math.sin(now*.002+p.phase)*1.2;
    const fy=Math.cos(now*.0017+p.phase)*1.2;

    ctx.beginPath();
    ctx.fillStyle="#fff";
    ctx.shadowBlur=18;ctx.shadowColor="#fff";
    ctx.arc(p.cx+fx,p.cy+fy,p.size,0,Math.PI*2);ctx.fill();
  }
  ctx.shadowBlur=0;

  /* occasional shooting stars */
  if(Math.random()<.012){
    const x=Math.random()*W+150,y=Math.random()*H*.45,len=70+Math.random()*120;
    ctx.beginPath();ctx.moveTo(x,y);ctx.lineTo(x-len,y+len*.55);
    ctx.strokeStyle="rgba(210,240,255,.85)";ctx.lineWidth=2;
    ctx.shadowBlur=16;ctx.shadowColor="#fff";ctx.stroke();ctx.shadowBlur=0;
  }

  requestAnimationFrame(draw);
}
requestAnimationFrame(draw);

/* Music: use your own/authorized local MP3 */
const music=document.getElementById("music"),btn=document.getElementById("musicBtn");
btn.onclick=async()=>{
  if(music.paused){
    try{await music.play();btn.textContent="🔊 MUSIC ON";btn.classList.add("playing")}
    catch(e){alert("Pastikan file music.mp3 ada di folder yang sama dengan index.html.")}
  }else{
    music.pause();btn.textContent="🔇 MUSIC OFF";btn.classList.remove("playing");
  }
};
</script>
</body>
</html>
