<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Our Little Movie ❤️</title>

<link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Poppins:wght@300;600&display=swap" rel="stylesheet">

<style>
body{
  margin:0;
  font-family:Poppins;
  color:white;
  text-align:center;
  background:radial-gradient(circle at 30% 20%, #2a1639, #07060d 60%);
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

.gallery img{
  width:100%;
  border-radius:12px;
  margin-top:12px;
}

.story{
  margin:50px 0;
  padding:20px;
  border-radius:18px;
  background:rgba(255,255,255,.07);
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

<audio id="music"></audio>

<!-- LOCK -->
<div id="lock" class="scene active">
  <h1>Private Love Movie 🎬</h1>
  <input id="pw" type="password" placeholder="Password">
  <br>
  <button onclick="unlock()">Enter</button>
</div>

<!-- HOME -->
<div id="home" class="scene">
  <h1>Hi My Favorite Person 💗</h1>

  <div class="card">
    Every click here reveals a piece of my heart.
  </div>

  <button onclick="playList('intro')">Play Music 🎵</button>
  <button onclick="go('letter')">Open Letter 💌</button>
  <button onclick="go('story')">Story Mode 📖</button>
  <button onclick="go('quiz1')">Love Quiz 💞</button>
  <button onclick="go('gallery')">Memories 📸</button>
</div>

<!-- LETTER -->
<div id="letter" class="scene">
  <h2>My Letter To You</h2>
  <button onclick="playList('letter')">Letter Music 🎶</button>
  <div class="letter" id="typeText"></div>
  <button onclick="burst()">Feel This ❤️</button>
  <button onclick="go('home')">Back</button>
</div>

<!-- STORY MODE -->
<div id="story" class="scene">
  <h2>Our Story 🌙</h2>

  <div class="story">Chapter 1 — How it started ✨<br>WRITE HERE</div>
  <div class="story">Chapter 2 — When you became special 💗<br>WRITE HERE</div>
  <div class="story">Chapter 3 — What you mean to me ❤️<br>WRITE HERE</div>

  <button onclick="go('clue1')">Continue →</button>
</div>

<!-- GALLERY -->
<div id="gallery" class="scene">
  <h2>Our Moments 📸</h2>
  <button onclick="playList('memory')">Memory Music 🎵</button>

  <div class="gallery">
    <img src="her.jpg">
    <img src="us.jpg">
    <img src="ss1.jpg">
    <img src="ss2.jpg">
  </div>

  <button onclick="go('home')">Back</button>
</div>

<!-- QUIZ CHAIN -->
<div id="quiz1" class="scene">
  <h2>Love Quiz 💞</h2>
  <p>Who owns my smile?</p>
  <button onclick="go('quiz2')">You</button>
  <button onclick="go('quiz2')">Still You</button>
</div>

<div id="quiz2" class="scene">
  <p>When do I think about you?</p>
  <button onclick="go('quiz3')">Sometimes</button>
  <button onclick="go('quiz3')">All the time</button>
</div>

<div id="quiz3" class="scene">
  <p>Type what I feel:</p>
  <input id="loveAns">
  <button onclick="checkLove()">Submit</button>
</div>

<!-- CLUE GAME -->
<div id="clue1" class="scene">
  <h2>Hidden Feeling 🕵️</h2>
  <button onclick="wrong()">Like</button>
  <button onclick="wrong()">Crush</button>
  <button onclick="go('clue2')">Love</button>
</div>

<div id="clue2" class="scene">
  <p>Type the deepest word:</p>
  <input id="finalAns">
  <button onclick="unlockEnd()">Unlock</button>
</div>

<!-- FINAL -->
<div id="final" class="scene">
  <h2>Final Scene 🎁</h2>
  <div class="card">
    You are not temporary to me.  
    Not casual.  
    Not ordinary.  
    You are my chosen person. ❤️
  </div>
  <button onclick="burst()">Hold My Heart</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

<script>
const PASS="lovemovie"; // change

const tracks={
 intro:["intro1.mp3","intro2.mp3"],
 letter:["letter1.mp3","letter2.mp3"],
 memory:["memory1.mp3","memory2.mp3"]
};

let list=[],i=0;

function playList(name){
 list=tracks[name]; i=0; nextTrack();
}
function nextTrack(){
 if(!list.length) return;
 music.src=list[i];
 music.play();
}
music.onended=()=>{
 i=(i+1)%list.length;
 nextTrack();
};

function go(id){
 document.querySelectorAll(".scene").forEach(s=>s.classList.remove("active"));
 document.getElementById(id).classList.add("active");
}

function unlock(){
 if(pw.value===PASS) go("home");
 else alert("Wrong password 😌");
}

function burst(){
 confetti({particleCount:180,spread:140});
}

function wrong(){ alert("Close — but deeper 💗"); }

function checkLove(){
 if(loveAns.value.toLowerCase().includes("love")){
  burst(); go("story");
 } else alert("Hint: starts with L");
}

function unlockEnd(){
 if(finalAns.value.toLowerCase().includes("love")){
  burst(); go("final");
 }
}

/* typewriter letter */
const letterMsg = `
WRITE YOUR FULL EMOTIONAL LETTER HERE.
MULTI LINE OK.
CUTE + DEEP + PERSONAL.
`;

let done=false;
function typeWriter(){
 if(done) return;
 done=true;
 let t=0;
 function step(){
  if(t<letterMsg.length){
   typeText.innerHTML+=letterMsg[t++];
   setTimeout(step,30);
  }
 }
 step();
}
document.getElementById("letter").onclick=typeWriter;

/* heart clicks */
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
