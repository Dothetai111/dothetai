<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Panel FF - Với Menu</title>
<style>
  body{
    background: #000;
    display:flex;
    justify-content:center;
    align-items:center;
    height:100vh;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    margin: 0;
  }

  .panel{
    position: relative;
    padding: 20px;
    border-radius: 12px;
    background: rgba(20,20,20,0.9);
    box-shadow: 0 6px 18px rgba(0,0,0,0.2);
    border: 2px solid gold;
    animation: glow 2s infinite alternate;
    width: 350px;
    height: 550px;
    overflow: hidden;
  }
  @keyframes glow {
    0% { box-shadow: 0 0 10px gold, 0 0 20px orange; border-color: gold; }
    100% { box-shadow: 0 0 20px orange, 0 0 40px gold; border-color: orange; }
  }

  .menu-icon {
    position: absolute;
    top: 12px;
    right: 12px;
    font-size: 22px;
    color: gold;
    cursor: pointer;
    z-index: 5;
    user-select: none;
  }
  .menu-panel {
    position: absolute;
    top: 46px;
    right: 12px;
    background: rgba(30,30,30,0.98);
    border: 1px solid gold;
    border-radius: 8px;
    overflow: hidden;
    display: none;
    flex-direction: column;
    z-index: 6;
    min-width: 120px;
    box-shadow: 0 8px 20px rgba(0,0,0,0.5);
  }
  .menu-panel button {
    background: none;
    border: none;
    color: #fff;
    padding: 10px 14px;
    font-size: 14px;
    cursor: pointer;
    text-align: left;
    transition: background 0.15s;
    width: 100%;
  }
  .menu-panel button:hover { background: rgba(255,255,255,0.06); }

  .page {
    position: relative;
    z-index: 2;
    display: none;
    height: 100%;
    width: 100%;
    box-sizing: border-box;
    padding-top: 6px;
    padding-bottom: 6px;
  }
  .page.active { display: block; }

  .content {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 12px;
    height: 100%;
  }
  .title { margin: 0; font-size: 22px; font-weight: bold; color: gold; }
  .sub { font-size: 13px; color: #ccc; margin-bottom: 4px; text-align: center;}
  .container {
    display: flex;
    flex-direction: column;
    align-items: stretch;
    width: 100%;
    gap: 14px;
    margin-top: 6px;
    padding: 0 6px;
  }
  .switch {
    display: flex;
    justify-content: space-between;
    align-items: center;
    cursor: pointer;
    user-select: none;
    padding: 10px 14px;
    border-radius: 10px;
    transition: background .15s;
  }
  .switch:hover { background: rgba(255,255,255,0.03); }
  .switch input { display: none; }
  .slider {
    width: 48px;
    height: 26px;
    background-color: #ccc;
    transition: .25s;
    border-radius: 26px;
    position: relative;
    flex: 0 0 auto;
  }
  .slider::before {
    position: absolute;
    content: "";
    height: 20px;
    width: 20px;
    left: 3px; top: 3px;
    background-color: #ffd400;
    transition: .25s;
    border-radius: 50%;
    box-shadow: 0 2px 6px rgba(0,0,0,0.45);
  }
  .switch input:checked + .slider { background-color: #ffd400; }
  .switch input:checked + .slider::before { transform: translateX(22px); }
  .label-text {
    font-size: 15px;
    font-weight: 700;
    color: #fff;
    flex: 1;
    text-align: right;
  }
  .fov-container {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    width: 100%;
    margin: 10px 0;
    padding: 0 6px;
  }
  .fov-container .label-text {
    text-align: left;
    margin-bottom: 6px;
  }
  .slider-box {
    display: flex;
    align-items: center;
    gap: 10px;
    width: 100%;
  }
  .fov-slider {
    -webkit-appearance: none;
    width: 100%;
    height: 6px;
    border-radius: 5px;
    background: #ccc;
    outline: none;
  }
  .fov-slider::-webkit-slider-thumb {
    -webkit-appearance: none;
    width: 18px;
    height: 18px;
    border-radius: 50%;
    background: #4CAF50;
    cursor: pointer;
  }
  .fov-slider::-moz-range-thumb {
    width: 18px;
    height: 18px;
    border-radius: 50%;
    background: #4CAF50;
    cursor: pointer;
  }
  #fovValue, #sensValue { margin-top: 8px; font-size: 14px; color: #fff; padding-left: 6px; }
  canvas {
    position: absolute;
    top:0; left:0;
    width: 100%;
    height: 100%;
    z-index: 1;
  }

  .social-links {
    text-align: center;
    display: flex;
    flex-direction: column;
    gap: 20px;
    align-items: center;
    flex: 1;
  justify-content: center
  }

  .page#page2 .content {
  display: flex;
  flex-direction: column;
  height: 100%;
}

  .social-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    text-decoration: none;
    font-size: 16px;
    font-weight: 700;
    padding: 12px;
    border-radius: 10px;
    transition: 0.25s;
    color: #fff;
    width: 180px;
    text-align: center;
  }
  .social-btn i { font-size: 18px; }
  .social-btn.fb { background: #1877f2; }
  .social-btn.fb:hover { background: #0d5bd6; box-shadow: 0 0 12px #1877f2; }
  .social-btn.zalo { background: #0084ff; }
  .social-btn.zalo:hover { background: #0069d9; box-shadow: 0 0 12px #0084ff; }
  .social-btn.yt { background: #ff0000; }
  .social-btn.yt:hover { background: #cc0000; box-shadow: 0 0 12px #ff0000; }

  @media (max-width: 420px) {
    .panel { width: 320px; height: 520px; }
  }

</style>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
</head>
<body>
<div class="panel" id="panelRoot">
  <canvas id="particleCanvas"></canvas>

  <i class="fa-solid fa-bars menu-icon" id="menuToggle" title="Menu"></i>
  <div class="menu-panel" id="menuPanel" aria-hidden="true">
    <button type="button" data-page="1">Menu</button>
    <button type="button" data-page="2">Liên hệ</button>
  </div>

  <!-- Trang 1 -->
  <div class="page active" id="page1">
    <div class="content">
      <div class="header">
        <h1 class="title">MENU HACK FF</h1>
        <div class="sub">TIẾN BỜ RAI</div>
      </div>

      <div class="container">
        <label class="switch">
          <input type="checkbox" id="aimbotChk" />
          <span class="slider"></span>
          <span class="label-text">AIMBOT</span>
        </label>
        <label class="switch">
          <input type="checkbox" id="wallChk" />
          <span class="slider"></span>
          <span class="label-text">WALLHACK</span>
        </label>
        <label class="switch">
          <input type="checkbox" id="autoFireChk" />
          <span class="slider"></span>
          <span class="label-text">AUTO FIRE</span>
        </label>
        <label class="switch">
          <input type="checkbox" id="headshotChk" />
          <span class="slider"></span>
          <span class="label-text">HEADSHOT 80%</span>
        </label>
        <label class="switch">
          <input type="checkbox" id="noLagChk" />
          <span class="slider"></span>
          <span class="label-text">NO LAG</span>
        </label>
      </div>

      <div class="fov-container">
        <label class="label-text">AIMFOV</label>
        <div class="slider-box">
          <input type="range" min="0" max="180" value="0" class="fov-slider" id="fovRange">
        </div>
        <div id="fovValue">0°</div>
      </div>

      <div class="fov-container">
        <label class="label-text">SENSITIVITY</label>
        <div class="slider-box">
          <input type="range" min="0" max="200" value="0" class="fov-slider" id="sensRange">
        </div>
        <div id="sensValue">0</div>
      </div>
    </div>
  </div>

  <div class="page" id="page2">
    <div class="content">
      <div class="header">
        <h1 class="title">Tiến Bờ Rai</h1>
        <div class="sub">Mua đồ chơi liên hệ</div>
      </div>
      <div class="social-links">
        <a href="https://www.facebook.com/share/1ARiBqpBNV/?mibextid=wwXIfr" target="_blank" class="social-btn fb">
          <i class="fa-brands fa-facebook-f"></i> Facebook
        </a>
        <a href="https://zalo.me/0385614724" target="_blank" class="social-btn zalo">
          <i class="fa-solid fa-comment-dots"></i> Zalo
        </a>
        <a href="https://youtube.com/@tienboraiday?si=YN_2gEiqXT9mS6Kq" target="_blank" class="social-btn yt">
          <i class="fa-brands fa-youtube"></i> YouTube
        </a>
      </div>
    </div>
  </div>
</div>

<script>
  const menuToggle = document.getElementById("menuToggle");
  const menuPanel = document.getElementById("menuPanel");
  const panelRoot = document.getElementById("panelRoot");

  menuToggle.addEventListener("click", (e) => {
    const isOpen = menuPanel.style.display === "flex";
    menuPanel.style.display = isOpen ? "none" : "flex";
    menuPanel.setAttribute("aria-hidden", isOpen ? "true" : "false");
    e.stopPropagation();
  });

  document.addEventListener("click", (e) => {
    if (!panelRoot.contains(e.target)) {
      menuPanel.style.display = "none";
      menuPanel.setAttribute("aria-hidden", "true");
    }
  });

  menuPanel.querySelectorAll("button[data-page]").forEach(btn => {
    btn.addEventListener("click", () => {
      const page = btn.getAttribute("data-page");
      document.querySelectorAll(".page").forEach(p => p.classList.remove("active"));
      document.getElementById("page" + page).classList.add("active");
      menuPanel.style.display = "none";
      menuPanel.setAttribute("aria-hidden", "true");
    });
  });

  const fovRange = document.getElementById("fovRange");
  const fovValue = document.getElementById("fovValue");
  fovRange.addEventListener("input", () => {
    fovValue.textContent = fovRange.value + "°";
  });

  const sensRange = document.getElementById("sensRange");
  const sensValue = document.getElementById("sensValue");
  let sensitivity = Number(sensRange.value);
  sensRange.addEventListener("input", () => {
    sensitivity = Number(sensRange.value);
    sensValue.textContent = sensitivity;
  });

  const canvas = document.getElementById("particleCanvas");
  const ctx = canvas.getContext("2d");
  function resizeCanvas() {
    canvas.width = canvas.offsetWidth;
    canvas.height = canvas.offsetHeight;
  }
  resizeCanvas();
  window.addEventListener("resize", resizeCanvas);

  class Particle {
    constructor() {
      this.x = Math.random() * canvas.width;
      this.y = Math.random() * canvas.height;
      this.vx = (Math.random() - 0.5) * 0.8;
      this.vy = (Math.random() - 0.5) * 0.8;
      this.size = 2;
    }
    update() {
      this.x += this.vx;
      this.y += this.vy;
      if (this.x < 0 || this.x > canvas.width) this.vx *= -1;
      if (this.y < 0 || this.y > canvas.height) this.vy *= -1;
    }
    draw() {
      ctx.beginPath();
      ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
      ctx.fillStyle = "#00ffff";
      ctx.shadowBlur = 8;
      ctx.shadowColor = "#00ffff";
      ctx.fill();
    }
  }
  const particles = [];
  for (let i = 0; i < 40; i++) particles.push(new Particle());
  function connectParticles() {
    for (let a = 0; a < particles.length; a++) {
      for (let b = a+1; b < particles.length; b++) {
        let dx = particles[a].x - particles[b].x;
        let dy = particles[a].y - particles[b].y;
        let dist = Math.sqrt(dx*dx + dy*dy);
        if (dist < 80) {
          ctx.beginPath();
          ctx.strokeStyle = "rgba(0,255,255,0.2)";
          ctx.lineWidth = 1;
          ctx.moveTo(particles[a].x, particles[a].y);
          ctx.lineTo(particles[b].x, particles[b].y);
          ctx.stroke();
        }
      }
    }
  }
  function animate() {
    ctx.clearRect(0,0,canvas.width,canvas.height);
    particles.forEach(p => { p.update(); p.draw(); });
    connectParticles();
    requestAnimationFrame(animate);
  }
  animate();

  const motionValues = {x:0,y:0,z:0};
  if (window.DeviceMotionEvent) {
    window.addEventListener("devicemotion", (event) => {
      motionValues.x = (event.accelerationIncludingGravity?.x || 0) * sensitivity;
      motionValues.y = (event.accelerationIncludingGravity?.y || 0) * sensitivity;
      motionValues.z = (event.accelerationIncludingGravity?.z || 0) * sensitivity;
    });
  }

  document.addEventListener("keydown", (e) => {
    if (e.key === "Escape") {
      menuPanel.style.display = "none";
      menuPanel.setAttribute("aria-hidden", "true");
    }
  });
</script>
</body>
</html>
