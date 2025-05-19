# Stop-Watch-web-App
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Stopwatch App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #121212;
      color: #fff;
      text-align: center;
      padding: 50px;
    }

    #display {
      font-size: 48px;
      margin-bottom: 20px;
    }

    button {
      font-size: 16px;
      margin: 5px;
      padding: 10px 20px;
      cursor: pointer;
      border: none;
      border-radius: 4px;
      background-color: #3498db;
      color: white;
      transition: background-color 0.2s ease;
    }

    button:hover {
      background-color: #2980b9;
    }

    #laps {
      margin-top: 20px;
      max-height: 200px;
      overflow-y: auto;
    }

    .lap {
      background: #1f1f1f;
      padding: 8px;
      margin: 5px auto;
      width: 200px;
      border-radius: 4px;
    }
  </style>
</head>
<body>

  <h1>Stopwatch Web Application</h1>
  <div id="display">00:00:00</div>
  <button onclick="startTimer()">Start</button>
  <button onclick="pauseTimer()">Pause</button>
  <button onclick="resetTimer()">Reset</button>
  <button onclick="recordLap()">Lap</button>

  <div id="laps"></div>

  <script>
    let startTime = 0;
    let elapsedTime = 0;
    let interval = null;
    let running = false;

    function updateDisplay() {
      const time = elapsedTime;
      const minutes = String(Math.floor(time / 60000)).padStart(2, '0');
      const seconds = String(Math.floor((time % 60000) / 1000)).padStart(2, '0');
      const milliseconds = String(Math.floor((time % 1000) / 10)).padStart(2, '0');
      document.getElementById("display").textContent = `${minutes}:${seconds}:${milliseconds}`;
    }

    function startTimer() {
      if (!running) {
        running = true;
        startTime = Date.now() - elapsedTime;
        interval = setInterval(() => {
          elapsedTime = Date.now() - startTime;
          updateDisplay();
        }, 10);
      }
    }

    function pauseTimer() {
      if (running) {
        running = false;
        clearInterval(interval);
      }
    }

    function resetTimer() {
      running = false;
      clearInterval(interval);
      elapsedTime = 0;
      updateDisplay();
      document.getElementById("laps").innerHTML = '';
    }

    function recordLap() {
      if (running) {
        const lap = document.createElement('div');
        lap.className = 'lap';
        lap.textContent = document.getElementById("display").textContent;
        document.getElementById("laps").appendChild(lap);
      }
    }

    window.onload = updateDisplay;
  </script>
</body>
</html>
