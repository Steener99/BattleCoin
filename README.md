# BattleCoin
BattleCoin is a competitive arena game where players use abilities, strategy, and skill to outlast opponents in fast-paced matches with no pay-to-win mechanics.
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>BattleCoin Demo</title>
<style>
body {
  margin: 0;
  font-family: Arial;
  background: #0b0f1a;
  color: white;
  text-align: center;
}

/* MENU */
.menu {
  padding-top: 50px;
}

.card {
  display: inline-block;
  padding: 20px;
  margin: 10px;
  border: 2px solid #00d1ff;
  border-radius: 10px;
  cursor: pointer;
}

.card:hover {
  background: #00d1ff;
  color: black;
}

button {
  margin-top: 20px;
  padding: 10px 20px;
  cursor: pointer;
}

/* GAME */
.game {
  display: none;
  width: 100vw;
  height: 100vh;
  position: relative;
}

.top-bar {
  position: absolute;
  top: 10px;
  width: 100%;
  display: flex;
  justify-content: space-between;
  padding: 0 20px;
}

.ability-bar {
  position: absolute;
  bottom: 20px;
  width: 100%;
  display: flex;
  justify-content: center;
  gap: 20px;
}

.ability {
  width: 60px;
  height: 60px;
  border: 2px solid #00d1ff;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}

.cooldown {
  opacity: 0.5;
}

.crosshair {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 10px;
  height: 10px;
  background: white;
  border-radius: 50%;
}
</style>
</head>

<body>

<!-- MENU -->
<div class="menu" id="menu">
  <h1>BATTLECOIN</h1>

  <h2>Select Character</h2>
  <div>
    <div class="card" onclick="selectCharacter('Fiery Fox')">🦊 Fiery Fox</div>
    <div class="card" onclick="selectCharacter('Lunar Lynx')">🐱 Lunar Lynx</div>
    <div class="card" onclick="selectCharacter('Mighty Moose')">🫎 Mighty Moose</div>
  </div>

  <h2>Select Arena</h2>
  <div>
    <div class="card" onclick="selectArena('Ice Kingdom')">❄️ Ice Kingdom</div>
    <div class="card" onclick="selectArena('Doom Dungeon')">🔥 Doom Dungeon</div>
  </div>

  <button onclick="startGame()">Start Match</button>
</div>

<!-- GAME -->
<div class="game" id="game">
  <div class="top-bar">
    <div id="lives">❤️❤️❤️❤️</div>
    <div id="timer">03:00</div>
    <div id="info"></div>
  </div>

  <div class="crosshair"></div>

  <div class="ability-bar">
    <div class="ability" onclick="cooldown(this,3000)">Q</div>
    <div class="ability" onclick="cooldown(this,5000)">E</div>
    <div class="ability" onclick="cooldown(this,4000)">Shift</div>
  </div>
</div>

<script>
let character = null;
let arena = null;

function selectCharacter(name) {
  character = name;
  alert("Selected: " + name);
}

function selectArena(name) {
  arena = name;
  alert("Arena: " + name);
}

function startGame() {
  if (!character || !arena) {
    alert("Select character and arena!");
    return;
  }

  document.getElementById("menu").style.display = "none";
  document.getElementById("game").style.display = "block";

  document.getElementById("info").innerText =
    character + " | " + arena;

  startTimer();
}

function startTimer() {
  let time = 180;
  let timer = document.getElementById("timer");

  setInterval(() => {
    let m = Math.floor(time / 60);
    let s = time % 60;
    timer.innerText = m + ":" + (s < 10 ? "0" + s : s);
    time--;
  }, 1000);
}

function cooldown(el, ms) {
  el.classList.add("cooldown");
  setTimeout(() => el.classList.remove("cooldown"), ms);
}
</script>

</body>
</html>
