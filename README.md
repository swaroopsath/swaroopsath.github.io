<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>swaroop sathyanarayanan</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      overflow: hidden;
      background: black;
      color: #003366;
      font-family: 'Courier New', Courier, monospace;
      text-transform: lowercase;
    }

    h1 {
      position: absolute;
      top: 40%;
      width: 100%;
      text-align: center;
      font-size: 3em;
      color: #003366;
      text-shadow: 0 0 30px #003366;
    }

    canvas {
      display: block;
      position: absolute;
      top: 0;
      left: 0;
    }
  </style>
</head>
<body>
  <canvas id="canvas"></canvas>
  <h1>swaroop sathyanarayanan</h1>

  <script>
    const canvas = document.getElementById('canvas');
    const ctx = canvas.getContext('2d');
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
        ctx.globalAlpha = star.o;
        ctx.arc(star.x, star.y, star.r, 0, Math.PI * 2);
        ctx.fillStyle = '#ffffff';
        ctx.fill();
        ctx.globalAlpha = 1.0;
      });

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

      requestAnimationFrame(draw);
    }

    draw();

    window.addEventListener('resize', () => {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    });
  </script>
</body>
</html>
