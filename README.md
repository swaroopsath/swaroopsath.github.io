<!DOCTYPE html>
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
      overflow-x: hidden;
      background-color: #000;
      color: #fff;
      font-family: 'Orbitron', sans-serif;
      scroll-behavior: smooth;
    }

    @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@500&display=swap');

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      z-index: -1;
    }

    .container {
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      text-align: center;
    }

    h1 {
      font-size: 4rem;
      text-shadow: 0 0 20px #00f0ff;
      animation: glow 2s infinite alternate;
    }

    @keyframes glow {
      from {
        text-shadow: 0 0 10px #00f0ff, 0 0 20px #00f0ff;
      }
      to {
        text-shadow: 0 0 30px #00f0ff, 0 0 60px #00f0ff;
      }
    }
  </style>
</head>
<body>
  <canvas id="stars"></canvas>
  <div class="container">
    <h1>Swaroop Sathyanarayanan</h1>
  </div>

  <script>
    const canvas = document.getElementById('stars');
    const ctx = canvas.getContext('2d');
    let w = canvas.width = window.innerWidth;
    let h = canvas.height = window.innerHeight;

    const stars = Array.from({ length: 250 }, () => ({
      x: Math.random() * w,
      y: Math.random() * h,
      r: Math.random() * 1.5,
      d: Math.random() * 1
    }));

    function draw() {
      ctx.clearRect(0, 0, w, h);
      ctx.fillStyle = '#fff';
      stars.forEach(s => {
        ctx.beginPath();
        ctx.arc(s.x, s.y, s.r, 0, Math.PI * 2);
        ctx.fill();
      });
      move();
    }

    function move() {
      stars.forEach(s => {
        s.y += s.d;
        if (s.y > h) {
          s.y = 0;
          s.x = Math.random() * w;
        }
      });
    }

    function animate() {
      draw();
      requestAnimationFrame(animate);
    }

    window.addEventListener('resize', () => {
      w = canvas.width = window.innerWidth;
      h = canvas.height = window.innerHeight;
    });

    animate();
  </script>
</body>
</html>
