# CODECRAFT_WD_02
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Stopwatch</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="stopwatch">
    <h1>Stopwatch</h1>
    <div id="display">00:00:00</div>
    <div class="buttons">
      <button id="start">Start</button>
      <button id="pause">Pause</button>
      <button id="reset">Reset</button>
    </div>
    <ul id="laps"></ul>
  </div>
  <script src="script.js"></script>
</body>
</html>

body {
  font-family: Arial, sans-serif;
  text-align: center;
  background-color: #f0f0f0;
  margin: 0;
  padding: 0;
}

.stopwatch {
  margin-top: 50px;
}

#display {
  font-size: 3em;
  margin: 20px 0;
}

.buttons button {
  font-size: 1em;
  padding: 10px 20px;
  margin: 5px;
  cursor: pointer;
}

#laps {
  list-style: none;
  padding: 0;
  margin-top: 20px;
}

#laps li {
  background: #ffffff;
  margin: 5px auto;
  padding: 10px;
  width: 200px;
  border: 1px solid #ddd;
  border-radius: 4px;
}
let timer;
let elapsedSeconds = 0;
let isRunning = false;

const display = document.getElementById("display");
const laps = document.getElementById("laps");

function updateTime() {
  const hours = String(Math.floor(elapsedSeconds / 3600)).padStart(2, "0");
  const minutes = String(Math.floor((elapsedSeconds % 3600) / 60)).padStart(2, "0");
  const seconds = String(elapsedSeconds % 60).padStart(2, "0");
  display.textContent = `${hours}:${minutes}:${seconds}`;
}

function startTimer() {
  if (!isRunning) {
    isRunning = true;
    timer = setInterval(() => {
      elapsedSeconds++;
      updateTime();
    }, 1000);
  }
}

function pauseTimer() {
  if (isRunning) {
    clearInterval(timer);
    isRunning = false;
  }
}

function resetTimer() {
  clearInterval(timer);
  elapsedSeconds = 0;
  isRunning = false;
  updateTime();
  laps.innerHTML = "";
}

function recordLap() {
  const lapTime = display.textContent;
  const lapItem = document.createElement("li");
  lapItem.textContent = `Lap: ${lapTime}`;
  laps.appendChild(lapItem);
}

document.getElementById("start").addEventListener("click", startTimer);
document.getElementById("pause").addEventListener("click", pauseTimer);
document.getElementById("reset").addEventListener("click", resetTimer);


