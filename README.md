<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>swaroop sathyanarayanan</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      overflow: hidden;
      background-color: black;
      color: #00bfff;
      font-family: 'Courier New', Courier, monospace;
      text-transform: lowercase;
    }

    a {
      color: #00bfff;
      text-decoration: none;
    }

    #logo {
      position: absolute;
      top: 20px;
      left: 20px;
      font-size: 2rem;
      text-shadow: 0 0 15px #00bfff;
    }

    .center-name {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 2rem;
      display: flex;
      gap: 5px;
    }

    .center-name span {
      display: inline-block;
      animation: floaty 3s infinite ease-in-out;
    }

    @keyframes floaty {
      0% { transform: translateY(0px) translateX(0px); }
      25% { transform: translateY(-5px) translateX(3px); }
      50% { transform: translateY(0px) translateX(0px); }
      75% { transform: translateY(5px) translateX(-3px); }
      100% { transform: translateY(0px) translateX(0px); }
    }

    canvas {
      position: absolute;
      top: 0;
      left: 0;
      z-index: -1;
    }
  </style>
</head>
<body>
  <a id="logo" href="https://github.com/swaroopsath">swaroop</a>
  <div class="center-name">
    <span>s</span><span>w</span><span>a</span><span>r</span><span>o</span><span>o</span><span>p</span>
    <span> </span>
    <span>s</span><span>a</span><span>t</span><span>h</span><span>y</span><span>a</span><span>n</span><span>a</span><span>r</span><span>a</span><span>y</span><span>a</span><span>n</span><span>a</span><span>n</span>
  </div>
  <canvas id="bg"></canvas>
  <script>
    const canvas = document.getElementById("bg");
    const ctx = canvas.getContext("2d");
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    const stars = Array.from({ length: 200 }, () => ({
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      r: Math.random() * 1.5,
    }));

    const meteors = Array.from({ length: 50 }, () => ({
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      vx: -Math.random() * 5 - 2,
      vy: Math.random() * 2 - 1,
      length: Math.random() * 20 + 10,
    }));

    function drawStars() {
      ctx.fillStyle = "white";
      stars.forEach(star => {
        ctx.beginPath();
        ctx.arc(star.x, star.y, star.r, 0, Math.PI * 2);
        ctx.fill();
      });
    }

    function drawMeteors() {
      meteors.forEach(m => {
        ctx.strokeStyle = "#aaaaaa";
        ctx.beginPath();
        ctx.moveTo(m.x, m.y);
        ctx.lineTo(m.x + m.vx * 2, m.y + m.vy * 2);
        ctx.stroke();
        m.x += m.vx;
        m.y += m.vy;

        if (m.x < 0 || m.y < 0 || m.y > canvas.height) {
          m.x = canvas.width + 100;
          m.y = Math.random() * canvas.height;
        }
      });
    }

    function explosion() {
      for (let i = 0; i < 200; i++) {
        const x = canvas.width / 2;
        const y = canvas.height / 2;
        const angle = Math.random() * 2 * Math.PI;
        const speed = Math.random() * 6 + 2;
        meteors.push({
          x,
          y,
          vx: Math.cos(angle) * speed,
          vy: Math.sin(angle) * speed,
          length: Math.random() * 20 + 10
        });
      }
    }

    let explosionDone = false;
    function animate() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      drawStars();
      drawMeteors();
      requestAnimationFrame(animate);
    }

    explosion();
    animate();

    document.addEventListener("mousemove", e => {
      const star = {
        x: e.clientX,
        y: e.clientY,
        r: 1 + Math.random() * 1,
      };
      stars.push(star);
      if (stars.length > 250) stars.shift();
    });

    window.addEventListener("resize", () => {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    });
  </script>
</body>
</html>
