from IPython.display import HTML

html_code = """
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Interactive Stopwatch</title>
<style>
  body {
    font-family: "Poppins", sans-serif;
    background: linear-gradient(135deg, #6a11cb, #2575fc);
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: white;
  }

  .stopwatch {
    background: rgba(255, 255, 255, 0.1);
    padding: 30px;
    border-radius: 20px;
    text-align: center;
    box-shadow: 0 4px 15px rgba(0,0,0,0.3);
    width: 320px;
  }

  h1 {
    font-size: 2.5rem;
    margin-bottom: 20px;
  }

  .time-display {
    font-size: 2.5rem;
    margin: 10px 0;
    letter-spacing: 2px;
  }

  .buttons button {
    margin: 8px;
    padding: 10px 18px;
    border: none;
    border-radius: 8px;
    font-size: 1rem;
    cursor: pointer;
    transition: 0.3s;
  }

  .buttons button:hover {
    transform: scale(1.1);
  }

  .start { background: #4CAF50; color: white; }
  .pause { background: #FF9800; color: white; }
  .reset { background: #f44336; color: white; }
  .lap { background: #2196F3; color: white; }

  ul {
    list-style: none;
    padding: 0;
    margin-top: 15px;
    max-height: 150px;
    overflow-y: auto;
  }

  li {
    background: rgba(255, 255, 255, 0.2);
    padding: 8px;
    margin: 4px 0;
    border-radius: 6px;
  }
</style>
</head>
<body>
  <div class="stopwatch">
    <h1>Stopwatch</h1>
    <div class="time-display" id="display">00:00:00.000</div>
    <div class="buttons">
      <button class="start" onclick="start()">Start</button>
      <button class="pause" onclick="pause()">Pause</button>
      <button class="lap" onclick="lap()">Lap</button>
      <button class="reset" onclick="reset()">Reset</button>
    </div>
    <ul id="laps"></ul>
  </div>

<script>
  let startTime = 0, elapsedTime = 0, timerInterval;
  const display = document.getElementById("display");
  const lapsList = document.getElementById("laps");

  function timeToString(time) {
    const diffInHrs = time / 3600000;
    const hh = Math.floor(diffInHrs);
    const diffInMin = (diffInHrs - hh) * 60;
    const mm = Math.floor(diffInMin);
    const diffInSec = (diffInMin - mm) * 60;
    const ss = Math.floor(diffInSec);
    const ms = Math.floor((diffInSec - ss) * 1000);

    const formattedHH = hh.toString().padStart(2, "0");
    const formattedMM = mm.toString().padStart(2, "0");
    const formattedSS = ss.toString().padStart(2, "0");
    const formattedMS = ms.toString().padStart(3, "0");

    return `${formattedHH}:${formattedMM}:${formattedSS}.${formattedMS}`;
  }

  function print(txt) {
    display.innerHTML = txt;
  }

  function start() {
    startTime = Date.now() - elapsedTime;
    timerInterval = setInterval(() => {
      elapsedTime = Date.now() - startTime;
      print(timeToString(elapsedTime));
    }, 10);
  }

  function pause() {
    clearInterval(timerInterval);
  }

  function reset() {
    clearInterval(timerInterval);
    print("00:00:00.000");
    elapsedTime = 0;
    lapsList.innerHTML = "";
  }

  function lap() {
    const li = document.createElement("li");
    li.textContent = `Lap ${lapsList.children.length + 1}: ${timeToString(elapsedTime)}`;
    lapsList.appendChild(li);
  }
</script>
</body>
</html>
"""

display(HTML(html_code))
