<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Will You Be My Valentine?</title>

<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: linear-gradient(135deg, #ff6fb1, #ffb6d5, #ffc3e6);
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  overflow: hidden;
}

/* Floating hearts */
.heart {
  position: fixed;
  bottom: -20px;
  font-size: 22px;
  animation: floatUp linear infinite;
  opacity: 0.9;
}

@keyframes floatUp {
  from { transform: translateY(0); }
  to { transform: translateY(-110vh); }
}

/* Main card */
.container {
  text-align: center;
  background: linear-gradient(135deg, rgba(255,255,255,0.35), rgba(255,255,255,0.15));
  backdrop-filter: blur(10px);
  padding: 35px;
  border-radius: 25px;
  border: 2px solid rgba(255,255,255,0.4);
  box-shadow: 0 0 30px rgba(255,0,150,0.4);
  width: 330px;
  z-index: 2;
}

h1 {
  color: #ff007f;
  margin-bottom: 10px;
}

.heartsRow {
  font-size: 26px;
  margin-bottom: 15px;
}

button {
  font-size: 18px;
  padding: 12px 26px;
  margin: 10px;
  border: none;
  border-radius: 15px;
  cursor: pointer;
  transition: 0.25s;
}

#yesBtn {
  background: linear-gradient(135deg,#ff4da6,#ff1493);
  color: white;
  box-shadow: 0 0 12px rgba(255,0,150,0.6);
}

#noBtn {
  background: linear-gradient(135deg,#888,#555);
  color: white;
}

#tryBtn {
  background: linear-gradient(135deg,#ff4da6,#ff1493);
  color: white;
}

#musicBtn {
  background: linear-gradient(135deg,#ff9acb,#ff4da6);
  color: white;
  font-size: 14px;
  margin-top: 15px;
}

button:hover {
  transform: scale(1.15);
}

/* Explosion hearts */
.boom {
  position: fixed;
  font-size: 30px;
  animation: explode 1s forwards;
  pointer-events: none;
}

@keyframes explode {
  from { transform: scale(1); opacity: 1; }
  to { transform: scale(2) translate(var(--x), var(--y)); opacity: 0; }
}
</style>
</head>

<body>

<!-- Music -->
<audio id="bgMusic" autoplay loop>
  <source src="https://www.dropbox.com/scl/fi/0knhtf1x5opqzgj6v6b6b/cupid.mp3?raw=1" type="audio/mpeg">
</audio>

<div class="container">
  <div class="heartsRow">💖 💕 💗 💘 💝 💞 💓 💜 💟</div>
  <h1 id="text"></h1>

  <div id="buttons">
    <button id="yesBtn" onclick="yesClick()">Yes 💘</button>
    <button id="noBtn" onclick="noClick()">No 💔</button>
  </div>

  <button id="musicBtn" onclick="toggleMusic()">🔊 Music ON</button>
</div>

<script>
/* NAME PERSONALIZATION */
const herName = "Her Name";   // ✨ CHANGE THIS TO HER NAME ✨

document.getElementById("text").innerHTML =
  herName + ", will you be my Valentine? 💕";

function yesClick() {
  document.getElementById("text").innerHTML =
    "Thank you " + herName + " for being my first Valentine 💖💝";
  document.getElementById("buttons").innerHTML = "";
  heartExplosion();
}

function noClick() {
  document.getElementById("text").innerHTML =
    "Why 😢 Please try again 💕";
  document.getElementById("buttons").innerHTML =
    '<button id="tryBtn" onclick="reset()">Try Again 🔄</button>';
}

function reset() {
  document.getElementById("text").innerHTML =
    herName + ", will you be my Valentine? 💕";
  document.getElementById("buttons").innerHTML =
    '<button id="yesBtn" onclick="yesClick()">Yes 💘</button>' +
    '<button id="noBtn" onclick="noClick()">No 💔</button>';
}

/* Floating hearts */
function createHeart() {
  const hearts = ["💖","💕","💗","💘","💝","💞","💓","💜","💟"];
  const heart = document.createElement("div");
  heart.className = "heart";
  heart.innerHTML = hearts[Math.floor(Math.random()*hearts.length)];
  heart.style.left = Math.random()*100 + "vw";
  heart.style.animationDuration = (2 + Math.random()*4) + "s";
  document.body.appendChild(heart);
  setTimeout(()=>{heart.remove();},6000);
}
setInterval(createHeart, 250);

/* Heart explosion */
function heartExplosion() {
  const hearts = ["💖","💕","💗","💘","💝","💞","💓","💜","💟"];
  for(let i=0;i<45;i++){
    const boom = document.createElement("div");
    boom.className = "boom";
    boom.innerHTML = hearts[Math.floor(Math.random()*hearts.length)];
    boom.style.left="50%";
    boom.style.top="50%";
    boom.style.setProperty("--x",(Math.random()*500-250)+"px");
    boom.style.setProperty("--y",(Math.random()*500-250)+"px");
    document.body.appendChild(boom);
    setTimeout(()=>{boom.remove();},1000);
  }
}

/* Music ON / OFF */
const music = document.getElementById("bgMusic");
let musicOn = true;

function toggleMusic() {
  if (musicOn) {
    music.pause();
    document.getElementById("musicBtn").innerHTML = "🔇 Music OFF";
  } else {
    music.play();
    document.getElementById("musicBtn").innerHTML = "🔊 Music ON";
  }
  musicOn = !musicOn;
}
</script>

</body>
</html>
