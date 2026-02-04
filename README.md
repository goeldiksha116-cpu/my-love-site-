<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Our Story ❤️</title>

<link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Poppins:wght@300;600&display=swap" rel="stylesheet">

<style>
body{
  margin:0;
  font-family:Poppins;
  color:white;
  text-align:center;
  background:#07060d;
  overflow-x:hidden;
}

/* cinematic stars */
.bg{
  position:fixed;
  width:100%;
  height:100%;
  background:url("stars.png");
  opacity:.25;
  animation:move 160s linear infinite;
  z-index:-1;
}
@keyframes move{
  from{transform:translateY(0)}
  to{transform:translateY(-3000px)}
}

.scene{
  display:none;
  min-height:100vh;
  padding:30px 20px;
  max-width:900px;
  margin:auto;
  animation:fade 1s ease;
}
.active{display:block;}

@keyframes fade{
  from{opacity:0; transform:translateY(20px)}
  to{opacity:1; transform:translateY(0)}
}

button{
  padding:14px 22px;
  border:none;
  border-radius:30px;
  background:#ff4da6;
  color:white;
  font-size:16px;
  margin:10px;
  cursor:pointer;
}

.card{
  background:rgba(255,255,255,.08);
  padding:20px;
  border-radius:18px;
  backdrop-filter:blur(8px);
}

.letter{
  background:#f5e6c8;
  color:#3b2a1a;
  font-family:'Great Vibes',cursive;
  font-size:28px;
  line-height:1.7;
  padding:28px;
  border-radius:12px;
  text-align:left;
}

.gallery img, .gallery video{
  width:100%;
  border-radius:12px;
  margin-top:12px;
}

input{
  padding:12px;
  border-radius:12px;
  border:none;
  width:220px;
}
</style>
</head>

<body>

<div class="bg"></div>

<!-- 🎵 MUSIC (click-to-play safe) -->
<audio id="introMusic" src="intro.mp3" loop></audio>
<audio id="letterMusic" src="letter.mp3" loop></audio>
<audio id="memoryMusic" src="memory.mp3" loop></audio>

<!-- 🔐 LOCK -->
<div id="lock" class="scene active">
  <h1>A Small Movie For You 🎬</h1>
  <p>Main character only</p>
  <input type="password" id="pw">
  <br>
  <button onclick="unlock()">Enter Story</button>
</div>

<!-- 🎬 START -->
<div id="scene1" class="scene">
  <h1>Hi You 🌙</h1>
  <div class="card">
    This is a small cinematic journey of how I feel about you.
  </div>

  <button onclick="playIntro()">Start With Music 🎵</button>
  <button onclick="go('scene2')">Continue →</button>
</div>

<!-- 💌 LETTER -->
<div id="scene2" class="scene">
  <h2>The Letter 💌</h2>
  <button onclick="playLetter()">Play Letter Music 🎶</button>
  <div class="letter" id="typeText"></div>
  <button onclick="burst()">Feel This 💞</button>
  <button onclick="go('scene3')">Next →</button>
</div>

<!-- 📸 MEMORIES -->
<div id="scene3" class="scene">
  <h2>Our Frames 📸</h2>
  <button onclick="playMemory()">Play Memory Music 🎵</button>

  <div class="gallery">
    <img src="her.jpg">
    <img src="us.jpg">
    <img src="ss1.jpg">
    <video controls src="vid1.mp4"></video>
  </div>

  <button onclick="go('scene4')">Next →</button>
</div>

<!-- 🧩 MYSTERY -->
<div id="scene4" class="scene">
  <h2>Cute Mystery 🕯️</h2>
  <p>Who makes my ordinary days special?</p>
  <button onclick="go('scene5')">You</button>
  <button onclick="go('scene5')">Only You</button>
</div>

<!-- ❤️ REVEAL -->
<div id="scene5" class="scene">
  <h2>Truth Scene ❤️</h2>
  <div class="card">
    You are comfort, chaos, calm, and happiness — all in one.
  </div>
  <button onclick="burst()">Tap My Heart</button>
  <button onclick="go('secret')">Secret Ending 🎁</button>
</div>

<!-- 🎁 SECRET -->
<div id="secret" class="scene">
  <h2>Secret Ending 💗</h2>
  <div class="card">
    No puzzle here. Just feelings — very real ones.
  </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

<script>
const PASS="cutemovie"; // change password

const letterMsg = `
WRITE YOUR FULL EMOTIONAL LETTER HERE.
MULTIPLE LINES WORK.
MAKE IT CUTE + DEEP.
`;

function stopAll(){
  introMusic.pause();
  letterMusic.pause();
  memoryMusic.pause();
}

function playIntro(){ stopAll(); introMusic.play(); }
function playLetter(){ stopAll(); letterMusic.play(); typeWriter(); }
function playMemory(){ stopAll(); memoryMusic.play(); }

function go(id){
  document.querySelectorAll(".scene").forEach(s=>s.classList.remove("active"));
  document.getElementById(id).classList.add("active");
}

function unlock(){
  if(document.getElementById("pw").value === PASS){
    go("scene1");
  } else {
    alert("Wrong password 😌");
  }
}

function burst(){
  confetti({particleCount:180,spread:140});
}

/* typewriter */
let typed=false;
function typeWriter(){
  if(typed) return;
  typed=true;
  let i=0;
  function t(){
    if(i<letterMsg.length){
      typeText.innerHTML += letterMsg.charAt(i);
      i++;
      setTimeout(t,30);
    }
  }
  t();
}

/* heart click effect */
document.addEventListener("click", e=>{
  let h=document.createElement("div");
  h.innerHTML="💗";
  h.style.position="fixed";
  h.style.left=e.clientX+"px";
  h.style.top=e.clientY+"px";
  document.body.appendChild(h);
  setTimeout(()=>h.remove(),700);
});
</script>

</body>
</html>
