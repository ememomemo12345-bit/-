<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>المنصة المتقدمة | الأخبار واللعبة 3D</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700;900&display=swap" rel="stylesheet">
<!-- مكتبة Three.js للألعاب ثلاثية الأبعاد الحديثة -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<style>
  :root {
    --bg: #090d16;
    --panel: #111827;
    --border: #1f2937;
    --accent: #ff2a5f;
    --cyan: #00f5d4;
    --text: #e5e7eb;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Cairo', sans-serif;
    padding: 20px;
    max-width: 1100px;
    margin: 0 auto;
  }

  header {
    text-align: center;
    padding: 20px 0;
    border-bottom: 1px solid var(--border);
    margin-bottom: 30px;
  }

  header h1 {
    color: #fff;
    font-size: 32px;
    font-weight: 900;
  }

  .status {
    font-size: 13px;
    color: #9ca3af;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 5px;
  }

  .dot {
    width: 8px;
    height: 8px;
    background: #10b981;
    border-radius: 50%;
    animation: pulse 1.5s infinite;
  }

  @keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: 0.3; } }

  .layout {
    display: grid;
    grid-template-columns: 1fr;
    gap: 30px;
  }

  @media(min-width: 850px) {
    .layout {
      grid-template-columns: 1fr 1fr;
    }
  }

  .section-title {
    font-size: 20px;
    font-weight: 700;
    color: var(--cyan);
    margin-bottom: 15px;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  /* قسم الأخبار */
  .news-container {
    display: flex;
    flex-direction: column;
    gap: 15px;
    max-height: 550px;
    overflow-y: auto;
    padding-right: 5px;
  }

  .news-card {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 18px;
    transition: 0.3s;
  }

  .news-card:hover {
    border-color: var(--accent);
  }

  .news-card h3 {
    color: #fff;
    font-size: 16px;
    margin-bottom: 8px;
    line-height: 1.5;
  }

  .news-card p {
    font-size: 13px;
    color: #9ca3af;
    line-height: 1.6;
    margin-bottom: 10px;
  }

  .news-card a {
    color: var(--accent);
    text-decoration: none;
    font-weight: bold;
    font-size: 12px;
  }

  /* قسم اللعبة ثلاثية الأبعاد */
  .game-wrapper {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 15px;
    text-align: center;
    position: relative;
  }

  #canvas-container {
    width: 100%;
    height: 400px;
    border-radius: 10px;
    overflow: hidden;
    background: #000;
    position: relative;
  }

  .game-ui {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 15px;
    padding: 0 10px;
  }

  .score-board {
    font-size: 18px;
    font-weight: 900;
    color: var(--cyan);
  }

  .controls-hint {
    font-size: 12px;
    color: #6b7280;
  }
</style>
</head>
<body>

<header>
  <h1>الرصد الإخباري التفاعلي 3D</h1>
  <div class="status">
    <span class="dot"></span>
    <span>تحديث أخبار مستمر + منطقة الترفيه 3D</span>
  </div>
</header>

<div class="layout">
  
  <!-- قسم الأخبار التلقائية -->
  <div>
    <div class="section-title">📰 أحدث الأخبار المباشرة</div>
    <div class="news-container" id="newsContainer">
      <div style="text-align:center; padding: 40px; color:#6b7280;">جاري تحميل الأخبار...</div>
    </div>
  </div>

  <!-- قسم اللعبة المتطورة 3D -->
  <div>
    <div class="section-title">🎮 معركة الفضاء 3D (حرك الماوس للتوجيه)</div>
    <div class="game-wrapper">
      <div id="canvas-container"></div>
      <div class="game-ui">
        <div class="score-board" id="scoreDisplay">النقاط: 0</div>
        <div class="controls-hint">وجه بالماوس للتصويب والتدمير</div>
      </div>
    </div>
  </div>

</div>

<script>
  /* --- 1. محرك الأخبار التلقائي --- */
  const RSS_URL = 'https://api.rss2json.com/v1/api.json?rss_url=https://www.aljazeera.net/aljazeerarss/a8c6f800-2f50-4596-9f1e-f3f1e9444458/6c85e2e8-d6a4-4f81-80cf-f8c6b75f8263';

  async function fetchNews() {
    try {
      const res = await fetch(RSS_URL);
      const data = await res.json();
      const container = document.getElementById('newsContainer');
      
      if (data.status === 'ok') {
        container.innerHTML = data.items.map(item => `
          <div class="news-card">
            <h3>${item.title}</h3>
            <p>${item.description.replace(/<[^>]*>?/gm, '').substring(0, 130)}...</p>
            <a href="${item.link}" target="_blank">قراءة التفاصيل ←</a>
          </div>
        `).join('');
      }
    } catch (e) {
      console.log('جاري إعادة المحاولة...');
    }
  }

  fetchNews();
  setInterval(fetchNews, 60000); // تحديث تلقائي كل 60 ثانية

  /* --- 2. محرك اللعبة ثلاثي الأبعاد 3D (Three.js) --- */
  const container = document.getElementById('canvas-container');
  const scoreDisplay = document.getElementById('scoreDisplay');
  let score = 0;

  // Scene, Camera, Renderer
  const scene = new THREE.Scene();
  const camera = new THREE.PerspectiveCamera(60, container.clientWidth / container.clientHeight, 0.1, 1000);
  camera.position.z = 7;

  const renderer = new THREE.WebGLRenderer({ antialias: true });
  renderer.setSize(container.clientWidth, container.clientHeight);
  container.appendChild(renderer.domElement);

  // Lighting
  const light = new THREE.PointLight(0x00f5d4, 2, 50);
  light.position.set(0, 0, 5);
  scene.add(light);
  scene.add(new THREE.AmbientLight(0xffffff, 0.4));

  // Player Ship (3D Pyramid Mesh)
  const shipGeo = new THREE.ConeGeometry(0.4, 1.2, 4);
  const shipMat = new THREE.MeshPhongMaterial({ color: 0x00f5d4, wireframe: false });
  const ship = new THREE.Mesh(shipGeo, shipMat);
  ship.rotation.x = Math.PI / 2;
  scene.add(ship);

  // Targets (Enemies)
  const enemies = [];
  function spawnEnemy() {
    const geo = new THREE.DodecahedronGeometry(0.4);
    const mat = new THREE.MeshPhongMaterial({ color: 0xff2a5f, flatShading: true });
    const enemy = new THREE.Mesh(geo, mat);
    enemy.position.x = (Math.random() - 0.5) * 8;
    enemy.position.y = (Math.random() - 0.5) * 5;
    enemy.position.z = -15;
    scene.add(enemy);
    enemies.push(enemy);
  }

  // Starfield Background
  const starsGeo = new THREE.BufferGeometry();
  const starsCount = 400;
  const starPos = new Float32Array(starsCount * 3);
  for(let i=0; i<starsCount*3; i++) starPos[i] = (Math.random() - 0.5) * 40;
  starsGeo.setAttribute('position', new THREE.BufferAttribute(starPos, 3));
  const starsMat = new THREE.PointsMaterial({ color: 0xffffff, size: 0.05 });
  const starField = new THREE.Points(starsGeo, starsMat);
  scene.add(starField);

  // Controls (Mouse Movement)
  let mouse = { x: 0, y: 0 };
  container.addEventListener('mousemove', (e) => {
    const rect = container.getBoundingClientRect();
    mouse.x = ((e.clientX - rect.left) / container.clientWidth) * 2 - 1;
    mouse.y = -((e.clientY - rect.top) / container.clientHeight) * 2 + 1;
  });

  // Game Loop
  let frame = 0;
  function animate() {
    requestAnimationFrame(animate);
    frame++;

    // Ship follow mouse
    ship.position.x += (mouse.x * 4 - ship.position.x) * 0.1;
    ship.position.y += (mouse.y * 3 - ship.position.y) * 0.1;
    ship.rotation.z = -ship.position.x * 0.2;

    // Spawn enemies
    if(frame % 30 === 0) spawnEnemy();

    // Move & Collision Check
    enemies.forEach((enemy, index) => {
      enemy.position.z += 0.25;
      enemy.rotation.x += 0.02;
      enemy.rotation.y += 0.02;

      // Hit check
      const dist = ship.position.distanceTo(enemy.position);
      if(dist < 0.8) {
        scene.remove(enemy);
        enemies.splice(index, 1);
        score += 10;
        scoreDisplay.textContent = 'النقاط: ' + score;
      } else if(enemy.position.z > 8) {
        scene.remove(enemy);
        enemies.splice(index, 1);
      }
    });

    // Animate stars
    starField.rotation.z += 0.001;

    renderer.render(scene, camera);
  }

  animate();

  // Responsive Canvas
  window.addEventListener('resize', () => {
    if(!container) return;
    camera.aspect = container.clientWidth / container.clientHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(container.clientWidth, container.clientHeight);
  });
</script>

</body>
</html>
