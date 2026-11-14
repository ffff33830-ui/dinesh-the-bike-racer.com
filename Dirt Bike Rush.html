<!doctype html>
<html lang="en"><head><meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Dirt Bike Rush</title>
<style>
:root{--ink:#fff;--panel:rgba(20,28,40,.78);--hot:#ff6b2c;--btn:rgba(255,255,255,.22);--btn-on:rgba(255,107,44,.85)}
@media (prefers-color-scheme: dark){:root:not([data-theme="light"]){--panel:rgba(8,12,20,.82)}}
:root[data-theme="dark"]{--panel:rgba(8,12,20,.82)}
html,body{height:100%;margin:0;background:#1d2b3d;overflow:hidden;touch-action:none;-webkit-user-select:none;user-select:none;font-family:"Trebuchet MS","Segoe UI",Arial,sans-serif;color:var(--ink)}
canvas{position:fixed;inset:0;width:100%;height:100%;display:block}
#hud{position:fixed;left:calc(12px + env(safe-area-inset-left,0px));top:calc(10px + env(safe-area-inset-top,0px));font-weight:700;font-size:18px;text-shadow:0 2px 4px rgba(0,0,0,.5);line-height:1.35}
#mute{position:fixed;right:calc(12px + env(safe-area-inset-right,0px));top:calc(8px + env(safe-area-inset-top,0px));width:44px;height:44px;border-radius:22px;border:0;background:var(--btn);color:var(--ink);font-size:20px}
#pad{position:fixed;left:0;right:0;bottom:0;display:flex;justify-content:space-between;padding:0 calc(14px + env(safe-area-inset-right,0px)) calc(14px + env(safe-area-inset-bottom,0px)) calc(14px + env(safe-area-inset-left,0px))}
.g{display:flex;gap:10px}
#pad button{width:78px;height:78px;border-radius:20px;border:2px solid rgba(255,255,255,.35);background:var(--btn);color:var(--ink);font:700 15px "Trebuchet MS",Arial,sans-serif;touch-action:none}
#pad button.gas{width:104px;background:rgba(255,107,44,.45);font-size:20px}
#pad button.d{background:var(--btn-on)}
#ov{position:fixed;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:12px;background:var(--panel);text-align:center;padding:20px}
#ov h1{margin:0;font-size:clamp(30px,8vw,54px);letter-spacing:1px;font-style:italic}
#ov p{margin:0;max-width:420px;line-height:1.5;font-size:16px}
#go{padding:14px 34px;border:0;border-radius:30px;background:var(--hot);color:#fff;font:700 20px "Trebuchet MS",Arial,sans-serif}
.hide{display:none!important}
</style></head><body>
<canvas id="c"></canvas>
<div id="hud"><div id="hd">0 m</div><div id="hc">Coins 0</div></div>
<button id="mute" aria-label="Toggle sound">🔊</button>
<div id="pad">
 <div class="g"><button data-k="back">Lean back</button><button data-k="fwd">Lean fwd</button></div>
 <div class="g"><button data-k="brake">Brake</button><button data-k="gas" class="gas">GAS</button></div>
</div>
<div id="ov"><h1>Dirt Bike Rush</h1><p id="msg">Hold GAS to climb the hills. Lean in the air to land on both wheels. Keep your head off the ground and grab the coins.<br>Keyboard: arrows or WASD.</p><button id="go">Tap to ride</button></div>
<script>
const cv=document.getElementById('c'),ctx=cv.getContext('2d');
const $=id=>document.getElementById(id);
let W,H,S,DPR;
function rs(){DPR=Math.min(2,devicePixelRatio||1);W=innerWidth;H=innerHeight;cv.width=W*DPR;cv.height=H*DPR;S=Math.min(H/460,W/560);}
addEventListener('resize',rs);rs();
const R=14,G=650,KS=600,KD=40,DR=520,I=1800,STEP=1/180;
const K={gas:0,brake:0,back:0,fwd:0};
let state='menu',B,got,coins,dist,camX,camY,best=0,over=0,muted=false;
try{best=+localStorage.getItem('dbr_best')||0}catch(e){}
function terr(x){const t=Math.max(0,Math.min(1,x/500)),e=t*t*(3-2*t),d=Math.min(1,x/9000);
 return 420+e*(Math.sin(x*.0042)*55+Math.sin(x*.011+1.3)*26+Math.sin(x*.027)*7*(.3+d))*(.5+.7*d);}
function reset(){B={x:60,y:terr(60)-R-2,vx:0,vy:0,a:0,w:0,wa:0,air:0,mvy:0,t:0};got=new Set();coins=0;dist=0;camX=B.x;camY=B.y;}
reset();
/* ---------- audio ---------- */
let AC,eng,engG,nb;
function initAudio(){
 if(AC){AC.resume();return}
 try{AC=new(window.AudioContext||window.webkitAudioContext)()}catch(e){return}
 eng=AC.createOscillator();eng.type='sawtooth';
 const f=AC.createBiquadFilter();f.type='lowpass';f.frequency.value=520;
 engG=AC.createGain();engG.gain.value=0;eng.connect(f);f.connect(engG);engG.connect(AC.destination);eng.start();
 nb=AC.createBuffer(1,AC.sampleRate*.6,AC.sampleRate);const d=nb.getChannelData(0);for(let i=0;i<d.length;i++)d[i]=Math.random()*2-1;
}
function tone(fr,dur,type,vol,to){if(!AC||muted)return;const t=AC.currentTime,o=AC.createOscillator(),g=AC.createGain();
 o.type=type;o.frequency.setValueAtTime(fr,t);if(to)o.frequency.exponentialRampToValueAtTime(to,t+dur);
 g.gain.setValueAtTime(vol,t);g.gain.exponentialRampToValueAtTime(.001,t+dur);o.connect(g);g.connect(AC.destination);o.start(t);o.stop(t+dur);}
function noise(dur,vol,fc){if(!AC||muted)return;const t=AC.currentTime,s=AC.createBufferSource(),g=AC.createGain(),f=AC.createBiquadFilter();
 s.buffer=nb;f.type='lowpass';f.frequency.value=fc;g.gain.setValueAtTime(vol,t);g.gain.exponentialRampToValueAtTime(.001,t+dur);
 s.connect(f);f.connect(g);g.connect(AC.destination);s.start(t);s.stop(t+dur);}
const sCoin=()=>{tone(880,.09,'square',.1);setTimeout(()=>tone(1320,.16,'square',.1),70)};
const sLand=v=>{tone(120,.18,'sine',.35*v+.1,45);noise(.14,.3*v+.05,900)};
const sCrash=()=>{noise(.6,.55,1600);tone(170,.5,'sawtooth',.25,35)};
const sStart=()=>{tone(300,.12,'square',.1);setTimeout(()=>tone(450,.12,'square',.1),110);setTimeout(()=>tone(700,.2,'square',.1),220)};
/* ---------- input ---------- */
document.querySelectorAll('#pad button').forEach(b=>{const k=b.dataset.k;
 b.addEventListener('pointerdown',e=>{e.preventDefault();K[k]=1;b.classList.add('d')});
 ['pointerup','pointercancel','pointerleave'].forEach(n=>b.addEventListener(n,()=>{K[k]=0;b.classList.remove('d')}));});
const KM={ArrowRight:'gas',d:'gas',D:'gas',ArrowLeft:'brake',a:'brake',A:'brake',ArrowUp:'back',w:'back',W:'back',ArrowDown:'fwd',s:'fwd',S:'fwd'};
addEventListener('keydown',e=>{if(KM[e.key]){K[KM[e.key]]=1;e.preventDefault()}if((e.key===' '||e.key==='Enter')&&state!=='play'&&!$('ov').classList.contains('hide'))start();});
addEventListener('keyup',e=>{if(KM[e.key])K[KM[e.key]]=0});
document.addEventListener('contextmenu',e=>e.preventDefault());
$('mute').onclick=()=>{muted=!muted;$('mute').textContent=muted?'🔇':'🔊';if(engG)engG.gain.value=0};
document.addEventListener('visibilitychange',()=>{if(AC){document.hidden?AC.suspend():AC.resume()}});
function start(){initAudio();reset();state='play';$('ov').classList.add('hide');sStart();}
$('go').onclick=start;
/* ---------- physics ---------- */
function step(dt){
 const b=B,play=state==='play',thr=play&&K.gas?1:0,br=play&&K.brake;
 const ca=Math.cos(b.a),sa=Math.sin(b.a);
 let ax=-b.vx*.05,ay=G,tq=0,gr=0;
 for(const sg of[-1,1]){
  const rx=sg*24*ca,ry=sg*24*sa,wx=b.x+rx,wy=b.y+ry,pen=wy+R-terr(wx);
  if(pen>0){
   gr++;
   const sl=(terr(wx+2)-terr(wx-2))/4,nl=Math.hypot(1,sl),nx=sl/nl,ny=-1/nl,tx=1/nl,ty=sl/nl;
   const vx=b.vx-b.w*ry,vy=b.vy+b.w*rx,vn=vx*nx+vy*ny,vt=vx*tx+vy*ty;
   const Fn=Math.max(0,KS*Math.min(pen,18)-KD*vn);
   let Ft=-vt*.15;
   if(sg<0&&thr)Ft+=DR*Math.max(0,1-vt/720);
   if(br)Ft-=vt*5;
   const Fx=Fn*nx+Ft*tx,Fy=Fn*ny+Ft*ty;
   ax+=Fx;ay+=Fy;tq+=rx*Fy-ry*Fx;
   if(pen>22)b.y-=(pen-22)*.5;
  }
 }
 const lean=play?(K.fwd?1:0)-(K.back?1:0):0;
 b.vx+=ax*dt;b.vy+=ay*dt;b.w+=tq/I*dt+lean*(gr?4:7)*dt;
 if(gr&&thr)b.w-=1.2*dt;
 b.w-=b.w*(gr?2:.2)*dt;
 b.x+=b.vx*dt;b.y+=b.vy*dt;b.a+=b.w*dt;b.wa+=b.vx/R*dt;b.t+=dt;
 if(gr){if(b.air>.25)sLand(Math.min(1,b.mvy/700));b.air=0;b.mvy=0}
 else{b.air+=dt;b.mvy=Math.max(b.mvy,b.vy)}
 if(play){
  dist=Math.max(dist,(b.x-60)/28);
  const i0=Math.floor((b.x-500)/260);
  for(let i=Math.max(0,i0-1);i<=i0+2;i++){if(got.has(i))continue;
   const cx=500+i*260,cy=terr(cx)-65-((i*7)%4)*22;
   if(Math.hypot(b.x-cx,b.y-18-cy)<30){got.add(i);coins++;sCoin()}}
  const hx=b.x+4*Math.cos(b.a)+34*Math.sin(b.a),hy=b.y+4*Math.sin(b.a)-34*Math.cos(b.a);
  if(b.t>.4&&hy+7>terr(hx)){crash()}
 }
}
function crash(){
 state='over';sCrash();K.gas=K.brake=0;
 const sc=Math.floor(dist+coins*20);
 if(sc>best){best=sc;try{localStorage.setItem('dbr_best',best)}catch(e){}}
 setTimeout(()=>{$('msg').innerHTML='Crashed after '+Math.floor(dist)+' m with '+coins+' coins.<br>Score '+sc+' · Best '+best;
  $('h1')&&0;$('go').textContent='Ride again';$('ov').classList.remove('hide')},900);
}
/* ---------- render ---------- */
function bg(){
 ctx.setTransform(DPR,0,0,DPR,0,0);
 const g=ctx.createLinearGradient(0,0,0,H);g.addColorStop(0,'#2b6fb3');g.addColorStop(.7,'#f3b76b');g.addColorStop(1,'#f7d9a0');
 ctx.fillStyle=g;ctx.fillRect(0,0,W,H);
 ctx.fillStyle='rgba(255,240,200,.9)';ctx.beginPath();ctx.arc(W*.78,H*.22,34,0,7);ctx.fill();
 for(const[c,sc,amp,y]of[['#6a5a8f',.18,50,.62],['#4c4375',.35,40,.72]]){
  ctx.fillStyle=c;ctx.beginPath();ctx.moveTo(0,H);
  for(let x=0;x<=W+10;x+=10)ctx.lineTo(x,H*y+Math.sin((x+camX*sc)*.006)*amp+Math.sin((x+camX*sc)*.017)*amp*.3);
  ctx.lineTo(W,H);ctx.fill();}
}
function world(){
 ctx.setTransform(DPR*S,0,0,DPR*S,DPR*(W*.3-camX*S),DPR*(H*.58-camY*S));
 const x0=camX-W*.3/S-20,x1=camX+W*.7/S+20,yb=camY+H/S;
 ctx.beginPath();ctx.moveTo(x0,yb);
 for(let x=x0;x<=x1;x+=8)ctx.lineTo(x,terr(x));
 ctx.lineTo(x1,yb);ctx.closePath();ctx.fillStyle='#6b3f26';ctx.fill();
 ctx.beginPath();for(let x=x0;x<=x1;x+=8){x===x0?ctx.moveTo(x,terr(x)):ctx.lineTo(x,terr(x))}
 ctx.strokeStyle='#4fae3c';ctx.lineWidth=9;ctx.lineJoin='round';ctx.stroke();
 const i0=Math.floor((x0-500)/260),i1=Math.ceil((x1-500)/260),tm=performance.now()/1000;
 for(let i=Math.max(0,i0);i<=i1;i++){if(got.has(i))continue;
  const cx=500+i*260,cy=terr(cx)-65-((i*7)%4)*22,sw=Math.abs(Math.cos(tm*3+i));
  ctx.fillStyle='#ffc61a';ctx.strokeStyle='#b8860b';ctx.lineWidth=2;
  ctx.beginPath();ctx.ellipse(cx,cy,10*sw+2,10,0,0,7);ctx.fill();ctx.stroke();}
 drawBike();
}
function drawBike(){
 const b=B;ctx.save();ctx.translate(b.x,b.y);ctx.rotate(b.a);ctx.lineCap='round';ctx.lineJoin='round';
 for(const sx of[-24,24]){ctx.save();ctx.translate(sx,0);ctx.rotate(b.wa);
  ctx.strokeStyle='#111';ctx.lineWidth=5;ctx.beginPath();ctx.arc(0,0,R-2,0,7);ctx.stroke();
  ctx.strokeStyle='#ccc';ctx.lineWidth=1.5;ctx.beginPath();
  for(let i=0;i<3;i++){const q=i*Math.PI/3,c=Math.cos(q)*(R-3),s=Math.sin(q)*(R-3);ctx.moveTo(c,s);ctx.lineTo(-c,-s)}
  ctx.stroke();ctx.restore();}
 const ln=(w,c,pts)=>{ctx.strokeStyle=c;ctx.lineWidth=w;ctx.beginPath();pts.forEach((p,i)=>i?ctx.lineTo(p[0],p[1]):ctx.moveTo(p[0],p[1]));ctx.stroke()};
 ln(5,'#ff6b2c',[[-24,0],[2,-2],[-8,-14],[12,-16],[24,0]]);
 ln(4,'#333',[[-12,-15],[-1,-15]]);
 ln(5,'#2d4a7a',[[-4,-14],[6,-8],[4,-2]]);
 ln(8,'#2d6cdf',[[-6,-16],[3,-30]]);
 ln(4,'#2d6cdf',[[3,-27],[14,-20],[12,-16]]);
 ctx.fillStyle='#e8b98c';ctx.beginPath();ctx.arc(4,-34,7,0,7);ctx.fill();
 ctx.strokeStyle='#d62828';ctx.lineWidth=4;ctx.beginPath();ctx.arc(4,-34,7.5,Math.PI,0);ctx.stroke();
 ctx.restore();
}
/* ---------- loop ---------- */
let last=0,acc=0,hdT=0;
function loop(t){
 const dt=Math.min(.05,(t-last)/1000||0);last=t;acc+=dt;
 while(acc>=STEP){step(STEP);acc-=STEP}
 const k=Math.min(1,dt*5);camX+=(B.x+B.vx*.25-camX)*k;camY+=(B.y-camY)*Math.min(1,dt*3);
 bg();world();
 if(AC&&engG){const sp=Math.abs(B.vx),th=state==='play'&&K.gas?1:0,n=AC.currentTime;
  eng.frequency.setTargetAtTime(48+sp*.09+th*26,n,.05);
  engG.gain.setTargetAtTime(muted||state==='over'?0:(state==='play'?.05+th*.05:.02),n,.08);}
 hdT+=dt;if(hdT>.1){hdT=0;$('hd').textContent=Math.floor(dist)+' m';$('hc').textContent='Coins '+coins}
 requestAnimationFrame(loop);
}
requestAnimationFrame(loop);
</script></body></html>
