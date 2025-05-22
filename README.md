<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Swaroop Sathyanarayanan</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>swaroop sathyanarayanan</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    html, body {
      height: 100%;
      margin: 0;
      padding: 0;
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
      color: #003366;
      font-family: 'Courier New', Courier, monospace;
      text-transform: lowercase;
    }

    .name {
    h1 {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 3rem;
      color: darkblue;
      text-shadow: 0 0 20px darkblue;
      animation: pulse 2s infinite;
      z-index: 10;
      top: 40%;
      width: 100%;
      text-align: center;
      font-size: 3em;
      color: #003366;
      text-shadow: 0 0 30px #003366;
    }

    @keyframes pulse {
      0%, 100% { text-shadow: 0 0 20px darkblue; }
      50% { text-shadow: 0 0 40px darkblue; }
    }

    #explosion {
    canvas {
      display: block;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%) scale(0);
      width: 1000px;
      height: 1000px;
      background: radial-gradient(circle, white, orange, red, darkred, black);
      border-radius: 50%;
      animation: explode 2s ease-out forwards;
      z-index: 5;
    }

    @keyframes explode {
      0% { transform: translate(-50%, -50%) scale(0); opacity: 1; }
      80% { transform: translate(-50%, -50%) scale(1.4); opacity: 0.7; }
      100% { transform: translate(-50%, -50%) scale(1.7); opacity: 0; }
      top: 0;
      left: 0;
    }
  </style>
</head>
<body>
  <canvas id="stars"></canvas>
  <div id="explosion"></div>
  <div class="name">Swaroop Sathyanarayanan</div>
  <canvas id="canvas"></canvas>
  <h1>swaroop sathyanarayanan</h1>

  <script>
    // Starfield
    const canvas = document.getElementById('stars');
    const canvas = document.getElementById('canvas');
    const ctx = canvas.getContext('2d');
    let stars = [];
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    function resizeCanvas() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    const stars = Array.from({length: 400}, () => ({
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      r: Math.random() * 1.5,
      o: Math.random()
    }));

    const meteors = [];

    function spawnMeteor() {
      meteors.push({
        x: Math.random() * canvas.width,
        y: -50,
        vx: -2 - Math.random() * 4,
        vy: 5 + Math.random() * 4,
        length: 80 + Math.random() * 50,
        size: 3 + Math.random() * 2
      });
    }

    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    function createStars(count) {
      stars = [];
      for (let i = 0; i < count; i++) {
        stars.push({
          x: Math.random() * canvas.width,
          y: Math.random() * canvas.height,
          r: Math.random() * 2 + 1,
          alpha: Math.random(),
    function explosion(x, y) {
      for (let i = 0; i < 80; i++) {
        meteors.push({
          x,
          y,
          vx: (Math.random() - 0.5) * 10,
          vy: (Math.random() - 0.5) * 10,
          length: 10 + Math.random() * 10,
          size: 2,
          life: 30
        });
      }
    }

    function drawStars() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      for (const star of stars) {
    explosion(canvas.width / 2, canvas.height / 2);

    document.addEventListener('mousemove', (e) => {
      explosion(e.clientX, e.clientY);
    });

    setInterval(spawnMeteor, 500);

    function draw() {
      ctx.fillStyle = 'rgba(0, 0, 0, 0.2)';
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      stars.forEach(star => {
        ctx.beginPath();
        ctx.arc(star.x, star.y, star.r, 0, 2 * Math.PI);
        ctx.fillStyle = `rgba(255, 255, 255, ${star.alpha})`;
        ctx.globalAlpha = star.o;
        ctx.arc(star.x, star.y, star.r, 0, Math.PI * 2);
        ctx.fillStyle = '#ffffff';
        ctx.fill();
      }
    }
        ctx.globalAlpha = 1.0;
      });

    function animateStars() {
      for (const star of stars) {
        star.alpha += (Math.random() - 0.5) * 0.05;
        star.alpha = Math.max(0.2, Math.min(1, star.alpha));
      }
    }
      meteors.forEach((m, i) => {
        ctx.beginPath();
        ctx.moveTo(m.x, m.y);
        ctx.lineTo(m.x + m.vx * m.length, m.y + m.vy * m.length);
        ctx.strokeStyle = '#ffcc00';
        ctx.lineWidth = m.size;
        ctx.stroke();

        m.x += m.vx;
        m.y += m.vy;

        if (m.life !== undefined) {
          m.life--;
          if (m.life <= 0) meteors.splice(i, 1);
        }
      });

    function draw() {
      animateStars();
      drawStars();
      requestAnimationFrame(draw);
    }

    createStars(1000);
    draw();

    // Random Meteors
    function spawnMeteor() {
      const meteor = document.createElement('div');
      meteor.style.position = 'absolute';
      meteor.style.width = '6px';
      meteor.style.height = '160px';
      meteor.style.background = 'linear-gradient(white, transparent)';
      meteor.style.top = `${Math.random() * window.innerHeight * 0.5}px`;
      meteor.style.left = `${Math.random() * window.innerWidth}px`;
      meteor.style.transform = 'rotate(45deg)';
      meteor.style.zIndex = 1;
      meteor.style.opacity = 0.9;
      meteor.style.transition = 'transform 1.2s linear, opacity 1.2s';

      document.body.appendChild(meteor);

      setTimeout(() => {
        meteor.style.transform += ' translateY(500px)';
        meteor.style.opacity = 0;
      }, 10);

      setTimeout(() => {
        meteor.remove();
      }, 1200);
    }

    setInterval(spawnMeteor, 300); // way more meteors now
    window.addEventListener('resize', () => {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    });
  </script>
</body>
</html>
