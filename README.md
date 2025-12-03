<!DOCTYPE html>
<html lang="en">
<head> 
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Circle Game</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: 100vh;
      /* 🎨 Faster colorful animated gradient background */
      background: linear-gradient(135deg, #ff9a9e, #fad0c4, #fbc2eb, #a6c1ee);
      background-size: 400% 400%;
      animation: gradientBG 6s ease infinite; /* was 15s, now faster */
      overflow: hidden;
      font-family: Arial, sans-serif;
      color: black; /* all text is black */
    }

    @keyframes gradientBG {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    h1 { margin-bottom: 20px; }

    .button {
      display: inline-block;
      margin: 10px;
      padding: 12px 25px;
      font-size: 18px;
      font-weight: bold;
      color: black; /* button text black */
      background-color: #f0f0f0; /* light background so black text is visible */
      border: 2px solid #333;
      border-radius: 8px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
    .button:hover { background-color: #ddd; }
    .credit { background-color: #c8e6c9; }
    .credit:hover { background-color: #a5d6a7; }
    .stop { background-color: #ffcdd2; }
    .stop:hover { background-color: #ef9a9a; }

    .container {
      position: absolute;
      top: 0;
      left: 0;
      height: 100%;
      width: 100%;
      display: none; /* hidden until Play is clicked */
      justify-content: center;
      align-items: center;
    }

    .circle {
      position: absolute;
      background: transparent;
      width: calc(var(--i) * 2.5vmin);
      aspect-ratio: 2;
      border-radius: 75%;
      border: 3px solid rgb(0, 255, 13);
      transform-style: preserve-3d;
      transform: rotateX(70deg) translateZ(60px);
      animation: animate 2s ease-in-out calc(var(--i) * 0.05s) infinite; /* faster animation */
      box-shadow: 0 0 15px rgb(124, 124, 124),
                  inset 0 0 15px rgb(124, 124, 124);
    }

    @keyframes animate {
      0%, 100% {
        transform: rotateX(70deg) translateZ(50px) translateY(0);
        filter: hue-rotate(0);
      }
      50% {
        transform: rotateX(60deg) translateZ(50px) translateY(-50vmin);
        filter: hue-rotate(360deg);
      }
    }
  </style>
</head>
<body>
  <h1 id="title">My Circle Game</h1>
  <div id="buttons">
    <button class="button" onclick="startGame()">Play</button>
    <a href="credit.html"><button class="button credit">Credit</button></a>
  </div>

  <div class="container" id="gameContainer"></div>

  <script>
    function startGame() {
      document.getElementById("title").style.display = "none";
      document.getElementById("buttons").style.display = "none";

      const container = document.getElementById("gameContainer");
      container.style.display = "flex";
      container.innerHTML = "";

      // Generate circles dynamically
      for (let i = 0; i <= 100; i++) {
        const circle = document.createElement("div");
        circle.className = "circle";
        circle.style.setProperty("--i", i);
        container.appendChild(circle);
      }

      // Add Stop button
      const stopBtn = document.createElement("button");
      stopBtn.className = "button stop";
      stopBtn.textContent = "Stop";
      stopBtn.style.position = "absolute";
      stopBtn.style.top = "20px";
      stopBtn.style.right = "20px";
      stopBtn.onclick = stopGame;
      container.appendChild(stopBtn);
    }

    function stopGame() {
      const container = document.getElementById("gameContainer");
      container.style.display = "none";
      container.innerHTML = "";

      document.getElementById("title").style.display = "block";
      document.getElementById("buttons").style.display = "block";
    }
  </script>
</body>
</html>
