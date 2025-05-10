<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Retro Counter-Strike (2D)</title>
  <style>
    html, body {
      margin: 0;
      background: black;
      color: white;
      font-family: monospace;
      overflow: hidden;
    }

    canvas {
      display: block;
      margin: 0 auto;
      background-color: #1a1a1a;
      image-rendering: pixelated;
      border: 4px solid #fff;
    }
  </style>
</head>
<body>
<canvas id="game" width="512" height="384"></canvas>

<script>
  const canvas = document.getElementById('game');
  const ctx = canvas.getContext('2d');

  const player = {
    x: 250,
    y: 180,
    size: 16,
    color: "#00ff00",
    speed: 2,
    health: 100,
    bullets: [],
  };

  const enemies = [
    { x: 100, y: 100, alive: true },
    { x: 400, y: 150, alive: true },
    { x: 300, y: 300, alive: true }
  ];

  const keys = {};
  const shootSound = new Audio("https://www.soundjay.com/mechanical/sounds/mechanical-gunshot-01.mp3");

  document.addEventListener('keydown', e => keys[e.key] = true);
  document.addEventListener('keyup', e => keys[e.key] = false);

  canvas.addEventListener('click', () => {
    shootSound.currentTime = 0;
    shootSound.play();
    player.bullets.push({
      x: player.x + player.size / 2,
      y: player.y + player.size / 2,
      dx: 4,
      dy: 0,
      life: 100
    });
  });

  function drawPlayer() {
    ctx.fillStyle = player.color;
    ctx.fillRect(player.x, player.y, player.size, player.size);
  }

  function drawEnemies() {
    enemies.forEach(e => {
      if (e.alive) {
        ctx.fillStyle = "red";
        ctx.fillRect(e.x, e.y, player.size, player.size);
      }
    });
  }

  function drawBullets() {
    ctx.fillStyle = "yellow";
    player.bullets.forEach(b => {
      ctx.fillRect(b.x, b.y, 4, 2);
    });
  }

  function updateBullets() {
    player.bullets.forEach(b => {
      b.x += b.dx;
      b.y += b.dy;
      b.life--;
    });

    // Remove bullets that are "dead"
    player.bullets = player.bullets.filter(b => b.life > 0);

    // Collision with enemies
    player.bullets.forEach(b => {
      enemies.forEach(e => {
        if (
          e.alive &&
          b.x < e.x + player.size &&
          b.x + 4 > e.x &&
          b.y < e.y + player.size &&
          b.y + 2 > e.y
        ) {
          e.alive = false;
          b.life = 0;
        }
      });
    });
  }

  function updatePlayer() {
    if (keys["w"]) player.y -= player.speed;
    if (keys["s"]) player.y += player.speed;
    if (keys["a"]) player.x -= player.speed;
    if (keys["d"]) player.x += player.speed;
  }

  function gameLoop() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    updatePlayer();
    updateBullets();

    drawPlayer();
    drawEnemies();
    drawBullets();

    requestAnimationFrame(gameLoop);
  }

  gameLoop();
</script>
</body>
</html>


<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Retro Game Launcher</title>
  <style>
    body {
      margin: 0;
      font-family: 'Courier New', monospace;
      background-color: black;
      color: lime;
      text-align: center;
    }

    h1 {
      font-size: 3em;
      margin-top: 40px;
      text-shadow: 0 0 5px red;
    }

    .menu {
      margin-top: 40px;
    }

    button {
      background: #111;
      color: lime;
      border: 2px solid lime;
      padding: 15px 30px;
      margin: 10px;
      font-size: 1.2em;
      cursor: pointer;
      border-radius: 10px;
      transition: 0.2s;
    }

    button:hover {
      background: lime;
      color: black;
    }

    iframe {
      border: none;
      width: 100%;
      height: 90vh;
    }
  </style>
</head>
<body>

<h1>🎮 Retro Game Launcher</h1>

<div class="menu">
  <button onclick="loadGame('resident.html')

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Retro Game Launcher</title>
  <style>
    body {
      margin: 0;
      font-family: 'Courier New', monospace;
      background-color: black;
      color: lime;
      text-align: center;
    }

    h1 {
      font-size: 3em;
      margin-top: 30px;
      text-shadow: 0 0 5px red;
    }

    .game-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 20px;
      padding: 20px;
      max-width: 1200px;
      margin: auto;
    }

    .game-card {
      background: #111;
      border: 2px solid lime;
      padding: 10px;
      border-radius: 10px;
      transition: 0.2s;
    }

    .game-card:hover {
      background: lime;
      color: black;
    }

    .game-card img {
      width: 100%;
      height: 150px;
      object-fit: cover;
      image-rendering: pixelated;
      border: 1px solid #333;
    }

    .game-card button {
      background: black;
      color: lime;
      border: 2px solid lime;
      padding: 10px 20px;
      margin-top: 10px;
      font-size: 1em;
      cursor: pointer;
      border-radius: 8px;
    }

    iframe {
      border: none;
      width: 100%;
      height: 85vh;
      display: none;
    }
  </style>
</head>
<body>

<h1>🎮 Retro Game Launcher</h1>

<div class="game-grid">
  <div class="game-card">
    <img src="https://i.imgur.com/ijU8Oyd.png" alt="Mom Is Wearing a Dress">
    <h3>Mom Is Wearing a Dress</h3>
    <button onclick="loadGame('mom-dress.html')">Play</button>
  </div>

  <div class="game-card">
    <img src="https://i.imgur.com/7kk2DQz.png" alt="Helicopter Haser">
    <h3>Helicopter Haser</h3>
    <button onclick="loadGame('helicopter-haser.html')">Play</button>
  </div>

  <div class="game-card">
    <img src="https://i.imgur.com/7lZkPOz.png" alt="Laser Points">
    <h3>Laser Points</h3>
    <button onclick="loadGame('laser-points.html')">Play</button>
  </div>

  <div class="game-card">
    <img src="https://i.imgur.com/kXHkOoG.png" alt="Laser Trash">
    <h3>Laser Trash</h3>
    <button onclick="loadGame('laser-trash.html')">Play</button>
  </div>
</div>

<iframe id="gameFrame" src=""></iframe>

<script>
  function loadGame(file) {
    const frame = document.getElementById("gameFrame");
    frame.src = file;
    frame.style.display = "block";
    window.scrollTo(0, 0);
  }
</script>

</body>
</html>





