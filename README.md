<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<title>مقبرة فري فاير</title>

<style>
*{box-sizing:border-box}
html,body{margin:0;width:100%;height:100%;overflow:hidden}

body{
  background:#020305;
  color:#eaf2ff;
  font-family:Arial,sans-serif
}

#app{
  height:100%;
  position:relative;
  background:
    radial-gradient(circle at 50% 40%,#101827 0,#030507 52%,#000 100%)
}

.scan{
  position:absolute;
  inset:0;
  pointer-events:none;
  background:repeating-linear-gradient(
    0deg,
    rgba(255,0,0,.025) 0 1px,
    transparent 1px 4px
  );
  mix-blend-mode:screen
}

.noise{
  position:absolute;
  inset:-50%;
  opacity:.07;
  pointer-events:none;
  background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='160' height='160'%3E%3Cfilter id='n'%3E%3CfeTurbulence baseFrequency='.9' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='%23n' opacity='.7'/%3E%3C/svg%3E");
  animation:noise .18s steps(2) infinite
}

@keyframes noise{
  to{transform:translate(4%,2%)}
}

.screen{
  height:100%;
  display:flex;
  align-items:center;
  justify-content:center;
  padding:18px
}

.card{
  width:min(760px,94vw);
  border:1px solid #273143;
  background:rgba(3,6,11,.9);
  box-shadow:0 0 50px rgba(255,0,0,.12);
  padding:22px;
  border-radius:14px
}

.top{
  display:flex;
  justify-content:space-between;
  gap:12px;
  font-size:12px;
  color:#738098;
  border-bottom:1px solid #202938;
  padding-bottom:12px
}

.badge{
  color:#ff3333;
  font-weight:bold;
  letter-spacing:1px
}

h1{
  font-size:clamp(30px,8vw,68px);
  margin:25px 0 8px;
  color:#ff2929;
  text-shadow:0 0 12px #f00,0 0 35px rgba(255,0,0,.6);
  animation:glitch .09s infinite alternate
}

@keyframes glitch{
  from{transform:translateX(-2px)}
  to{transform:translateX(2px)}
}

.sub{
  color:#b8c1d0;
  font-size:clamp(15px,3.5vw,21px);
  min-height:30px
}

.terminal{
  margin-top:22px;
  background:#010204;
  border:1px solid #1b2431;
  border-radius:8px;
  padding:14px;
  font-family:monospace;
  color:#8cffae;
  font-size:12px;
  line-height:1.8;
  height:145px;
  overflow:hidden;
  text-align:left;
  direction:ltr
}

.line.red{color:#ff5555}
.line.gray{color:#657184}

.progress{
  height:10px;
  background:#151a21;
  border-radius:99px;
  overflow:hidden;
  margin-top:20px
}

.fill{
  height:100%;
  width:0;
  background:linear-gradient(90deg,#7a0000,#ff2020,#ff8a8a);
  box-shadow:0 0 18px red;
  transition:width .15s
}

.row{
  display:flex;
  justify-content:space-between;
  margin-top:8px;
  color:#778398;
  font-size:12px
}

.fake-data{
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:8px;
  margin-top:18px
}

.box{
  border:1px solid #202a39;
  padding:10px;
  border-radius:7px;
  background:#070b11
}

.box b{
  display:block;
  color:#dce5f5;
  font-size:12px
}

.box span{
  color:#66748b;
  font-size:11px
}

#final{
  display:none;
  text-align:center
}

.safe{
  color:#3dff7b!important;
  text-shadow:0 0 20px rgba(0,255,100,.5)!important
}

button{
  margin-top:20px;
  background:#101722;
  border:1px solid #3d4b61;
  color:#dbe6f5;
  border-radius:8px;
  padding:11px 18px;
  cursor:pointer
}

.flash{
  position:absolute;
  inset:0;
  background:red;
  opacity:0;
  pointer-events:none
}
</style>
</head>

<body>

<div id="app">

<div class="scan"></div>
<div class="noise"></div>
<div id="flash" class="flash"></div>

<div class="screen">

<div class="card">

<div id="fake">

<div class="top">
<span>FREE FIRE SECURITY NODE</span>
<span class="badge">● CONNECTION ACTIVE</span>
</div>

<h1>⚠ تم اختراق هاتفك ⚠</h1>

<div class="sub" id="status">
جاري التحقق من الجهاز...
</div>

<div class="terminal" id="terminal"></div>

<div class="progress">
<div class="fill" id="fill"></div>
</div>

<div class="row">
<span id="percent">0%</span>
<span id="stage">INITIALIZING</span>
</div>

<div class="fake-data">

<div class="box">
<b>DEVICE</b>
<span>ANDROID / MOBILE</span>
</div>

<div class="box">
<b>SECURITY</b>
<span id="sec">SCANNING</span>
</div>

<div class="box">
<b>FILES</b>
<span id="files">0 ITEMS</span>
</div>

</div>
</div>

<div id="final">

<h1 class="safe">😂 مقلب!</h1>

<p class="sub">
ما تخافش، ما صرا والو 😎
</p>

<p style="color:#8d98a9">
هذي صفحة تمثيلية فقط، وما عندها حتى وصول لهاتفك أو ملفاتك.
</p>

<button onclick="location.reload()">
عاود المقلب
</button>

</div>

</div>
</div>
</div>

<script>

const fill=document.getElementById('fill'),
percent=document.getElementById('percent');

const status=document.getElementById('status'),
stage=document.getElementById('stage');

const files=document.getElementById('files'),
sec=document.getElementById('sec'),
term=document.getElementById('terminal');

const flash=document.getElementById('flash');

const lines=[
['SYSTEM INIT','gray'],
['Checking device integrity...',''],
['Mounting secure session...',''],
['Analyzing system partitions...',''],
['Reading protected index...',''],
['Bypassing visual security layer...','red'],
['Simulating file enumeration...',''],
['Generating fake telemetry...','gray'],
['Finalizing simulation...','red']
];

let i=0,p=0;

function addLine(){

  if(i<lines.length){

    let d=document.createElement('div');

    d.className='line '+lines[i][1];

    d.textContent='> '+lines[i][0];

    term.appendChild(d);

    term.scrollTop=term.scrollHeight;

    i++;
  }
}

const timer=setInterval(()=>{

  p+=2;

  fill.style.width=p+'%';

  percent.textContent=p+'%';

  if(p<25){

    status.textContent='جاري فحص نظام الحماية...';

    stage.textContent='SECURITY SCAN';

  }else if(p<55){

    status.textContent='جاري تحليل ملفات الجهاز...';

    stage.textContent='FILE ANALYSIS';

  }else if(p<80){

    status.textContent='جاري محاكاة الوصول للنظام...';

    stage.textContent='ACCESS SIMULATION';

  }else{

    status.textContent='⚠ اكتملت المحاكاة...';

    stage.textContent='FINALIZING';
  }

  if(p%8===0){
    addLine();
  }

  files.textContent=Math.floor(p*31.7)+' ITEMS';

  sec.textContent=p>75?'ALERT':'SCANNING';

  if(p===72){

    flash.style.opacity='.18';

    setTimeout(()=>{
      flash.style.opacity='0'
    },90);
  }

  if(p>=100){

    clearInterval(timer);

    setTimeout(()=>{

      document.getElementById('fake').style.display='none';

      document.getElementById('final').style.display='block';

    },900);
  }

},120);

addLine();

</script>

</body>
</html># -
