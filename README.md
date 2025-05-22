<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Swaroop Sathyanarayanan</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    html, body {
      height: 100%;
      overflow: hidden;
      background: black;
      color: white;
      font-family: 'Orbitron', sans-serif;
    }

    canvas {
      position: absolute;
      top: 0;
      left: 0;
      z-index: -2;
    }

    .name {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 3rem;
      color: #0ff;
      text-shadow: 0 0 20px #0ff;
      animation: pulse 2s infinite;
      z-index: 10;
      border-bottom: 2px solid #0ff;
      padding-bottom: 5px;
    }

    @keyframes pulse {
      0%, 100% { text-shadow: 0 0 20px #0ff; }
      50% { text-shadow: 0 0 40px #0ff; }
    }

    #explosion {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%) scale(0);
      width: 600px;
      height: 600px;
      background: radial-gradient(white, orange, red, black);
      border-radius: 50%;
      animation: explode 1.5s ease-out forwards;
      z-index: 5;
    }

    @keyframes explode {
      0% { transform: translate(-50%, -50%) scale(0); opacity: 1; }
      80% { transform: translate(-50%, -50%) scale(1.2); opacity: 0.7; }
      100% { transform: translate(-50%, -50%) scale(1.5); opacity: 0; }
    }
  </style>
</head>
<body>
  <canvas id="stars"></canvas>
  <div id="explosion"></div>
  <div class="name">Swaroop Sathyanarayanan</div>

  <script>
    // Starfield
    const canvas = document.getElementById('stars');
    const ctx = canvas.getContext('2d');
    let stars = [];

    function resizeCanvas() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }

    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    function createStars(count) {
      stars = [];
      for (let i = 0; i < count; i++) {
        stars.push({
          x: Math.random() * canvas.width,
          y: Math.random() * canvas.height,
          r: Math.random() * 1.5,
          alpha: Math.random(),
        });
      }
    }

    function drawStars() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      for (const star of stars) {
        ctx.beginPath();
        ctx.arc(star.x, star.y, star.r, 0, 2 * Math.PI);
        ctx.fillStyle = `rgba(255, 255, 255, ${star.alpha})`;
        ctx.fill();
      }
    }

    function animateStars() {
      for (const star of stars) {
        star.alpha += (Math.random() - 0.5) * 0.05;
        if (star.alpha < 0) star.alpha = 0;
        if (star.alpha > 1) star.alpha = 1;
      }
    }

    function draw() {
      animateStars();
      drawStars();
      requestAnimationFrame(draw);
    }

    createStars(300);
    draw();

    // Random Meteors
    function spawnMeteor() {
      const meteor = document.createElement('div');
      meteor.style.position = 'absolute';
      meteor.style.width = '4px';
      meteor.style.height = '100px';
      meteor.style.background = 'linear-gradient(white, transparent)';
      meteor.style.top = `${Math.random() * window.innerHeight * 0.5}px`;
      meteor.style.left = `${Math.random() * window.innerWidth}px`;
      meteor.style.transform = 'rotate(45deg)';
      meteor.style.zIndex = 1;
      meteor.style.opacity = 0.8;
      meteor.style.transition = 'transform 1s linear, opacity 1s';

      document.body.appendChild(meteor);

      setTimeout(() => {
        meteor.style.transform += ' translateY(300px)';
        meteor.style.opacity = 0;
      }, 10);

      setTimeout(() => {
        meteor.remove();
      }, 1000);
    }

    setInterval(spawnMeteor, 2000); // every 2s
  </script>
</body>
</html>
