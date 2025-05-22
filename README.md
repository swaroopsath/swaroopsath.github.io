<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Swaroop Sathyanarayanan</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      overflow: hidden;
      background: black;
      font-family: 'Orbitron', sans-serif;
      color: white;
    }

    @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@600&display=swap');

    canvas {
      position: absolute;
      top: 0;
      left: 0;
      z-index: -1;
    }

    .name {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 4em;
      text-shadow: 0 0 20px #0ff, 0 0 40px #0ff;
      animation: glow 2s infinite alternate;
    }

    @keyframes glow {
      from {
        text-shadow: 0 0 10px #0ff;
      }
      to {
        text-shadow: 0 0 40px #0ff, 0 0 80px #0ff;
      }
    }
  </style>
</head>
<body>
  <canvas id="universe"></canvas>
  <div class="name">Swaroop Sathyanarayanan</div>

  <script>
    const canvas = document.getElementById('universe');
    const ctx = canvas.getContext('2d');
    let w = canvas.width = window.innerWidth;
    let h = canvas.height = window.innerHeight;

    window.addEventListener('resize', () => {
      w = canvas.width = window.innerWidth;
      h = canvas.height = window.innerHeight;
    });

    const stars = Array.from({ length: 500 }, () => ({
      x: Math.random() * w,
      y: Math.random() * h,
      r: Math.random() * 1.5,
      alpha: Math.random()
    }));

    const meteors = [];

    function createMeteor() {
      meteors.push({
        x: Math.random() * w,
        y: -20,
        vx: -4 - Math.random() * 2,
        vy: 6 + Math.random() * 4,
        length: 80 + Math.random() * 40,
        alpha: 1
      });
    }

    function explosion(x, y) {
      for (let i = 0; i < 50; i++) {
        particles.push({
          x, y,
          vx: (Math.random() - 0.5) * 10,
          vy: (Math.random() - 0.5) * 10,
          alpha: 1,
          r: 2 + Math.random() * 3
        });
      }
    }

    const particles = [];

    // Trigger a big explosion on load
    window.addEventListener('load', () => {
      explosion(w / 2, h / 2);
    });

    function draw() {
      ctx.fillStyle = 'rgba(0, 0, 0, 0.3)';
      ctx.fillRect(0, 0, w, h);

      // Stars
      ctx.fillStyle = 'white';
      stars.forEach(s => {
        ctx.globalAlpha = s.alpha;
        ctx.beginPath();
        ctx.arc(s.x, s.y, s.r, 0, Math.PI * 2);
        ctx.fill();
      });

      // Meteors
      ctx.strokeStyle = '#f0f';
      meteors.forEach((m, i) => {
        ctx.globalAlpha = m.alpha;
        ctx.beginPath();
        ctx.moveTo(m.x, m.y);
        ctx.lineTo(m.x + m.vx * m.length, m.y + m.vy * m.length);
        ctx.stroke();
        m.x += m.vx;
        m.y += m.vy;
        m.alpha -= 0.005;
        if (m.y > h || m.alpha <= 0) meteors.splice(i, 1);
      });

      // Explosion particles
      ctx.fillStyle = '#ff0';
      particles.forEach((p, i) => {
        ctx.globalAlpha = p.alpha;
        ctx.beginPath();
        ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
        ctx.fill();
        p.x += p.vx;
        p.y += p.vy;
        p.alpha -= 0.01;
        if (p.alpha <= 0) particles.splice(i, 1);
      });

      ctx.globalAlpha = 1;
    }

    function animate() {
      draw();
      if (Math.random() < 0.01) createMeteor();
      requestAnimationFrame(animate);
    }

    animate();
  </script>
</body>
</html>
