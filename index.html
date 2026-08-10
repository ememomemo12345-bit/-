<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>نواة الذكاء الكمّي | AI NEXUS</title>
    <!-- خطوط عصرية -->
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;700;900&family=Orbitron:wght@500;900&display=swap" rel="stylesheet">
    <!-- مكتبة Three.js للرسوميات 3D -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <style>
        :root {
            --primary: #00f0ff;
            --secondary: #ff003c;
            --dark: #050510;
            --glass: rgba(10, 15, 30, 0.6);
            --border: rgba(0, 240, 255, 0.3);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body, html {
            width: 100%; height: 100%;
            background-color: var(--dark);
            color: #fff;
            font-family: 'Cairo', sans-serif;
            overflow: hidden; /* يمنع التمرير العادي */
        }

        /* خلفية الـ 3D */
        #webgl-container {
            position: absolute;
            top: 0; left: 0;
            width: 100%; height: 100%;
            z-index: 1;
        }

        /* واجهة المستخدم الشفافة */
        .ui-layer {
            position: absolute;
            top: 0; left: 0;
            width: 100%; height: 100%;
            z-index: 2;
            display: grid;
            grid-template-rows: auto 1fr auto;
            padding: 20px;
            pointer-events: none; /* لتمرير اللمس للخلفية */
        }

        .hud-element {
            pointer-events: auto; /* تفعيل اللمس للعناصر فقط */
            background: var(--glass);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid var(--border);
            border-radius: 15px;
            box-shadow: 0 0 20px rgba(0, 240, 255, 0.1);
        }

        /* الهيدر */
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 25px;
        }

        .brand h1 {
            font-family: 'Orbitron', sans-serif;
            font-size: 24px;
            letter-spacing: 3px;
            color: var(--primary);
            text-shadow: 0 0 10px var(--primary);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .brand h1::before {
            content: '';
            width: 12px; height: 12px;
            background: var(--secondary);
            border-radius: 50%;
            box-shadow: 0 0 10px var(--secondary);
            animation: pulse 1s infinite;
        }

        @keyframes pulse { 0%,100% { opacity: 1; transform: scale(1); } 50% { opacity: 0.5; transform: scale(1.2); } }

        .sys-stats {
            font-family: 'Orbitron', sans-serif;
            font-size: 12px;
            color: #00ffaa;
            text-align: left;
        }

        /* منطقة المحادثة والذكاء الاصطناعي */
        .ai-core {
            align-self: center;
            justify-self: center;
            width: 100%;
            max-width: 800px;
            height: 60vh;
            display: flex;
            flex-direction: column;
            margin-top: 20px;
            position: relative;
        }

        .chat-box {
            flex-grow: 1;
            padding: 20px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 15px;
            /* Scrollbar */
            scrollbar-width: thin;
            scrollbar-color: var(--primary) transparent;
        }
        .chat-box::-webkit-scrollbar { width: 5px; }
        .chat-box::-webkit-scrollbar-thumb { background: var(--primary); border-radius: 10px; }

        .message {
            max-width: 85%;
            padding: 12px 18px;
            border-radius: 12px;
            font-size: 15px;
            line-height: 1.6;
            animation: fadeIn 0.4s ease-out;
        }

        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        .msg-user {
            background: rgba(0, 240, 255, 0.1);
            border-right: 3px solid var(--primary);
            align-self: flex-start;
            border-bottom-right-radius: 0;
        }

        .msg-ai {
            background: rgba(255, 0, 60, 0.1);
            border-left: 3px solid var(--secondary);
            align-self: flex-end;
            border-bottom-left-radius: 0;
            color: #ddd;
        }

        /* لوحة الإدخال */
        .input-panel {
            display: flex;
            gap: 10px;
            padding: 15px;
            border-top: 1px solid var(--border);
            background: rgba(0,0,0,0.5);
            border-bottom-left-radius: 15px;
            border-bottom-right-radius: 15px;
        }

        input[type="text"] {
            flex-grow: 1;
            background: transparent;
            border: 1px solid var(--border);
            color: #fff;
            padding: 12px 20px;
            border-radius: 8px;
            font-family: inherit;
            font-size: 15px;
            outline: none;
            transition: 0.3s;
        }
        input[type="text"]:focus { border-color: var(--primary); box-shadow: 0 0 15px rgba(0, 240, 255, 0.3); }

        button {
            background: var(--primary);
            color: #000;
            border: none;
            padding: 0 25px;
            border-radius: 8px;
            font-family: inherit;
            font-weight: 900;
            cursor: pointer;
            transition: 0.3s;
            font-size: 15px;
            text-transform: uppercase;
        }
        button:hover {
            background: #fff;
            box-shadow: 0 0 20px var(--primary);
        }
        button:active { transform: scale(0.95); }

        /* تأثيرات مسح البيانات */
        .scanning-line {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 2px;
            background: var(--primary);
            box-shadow: 0 0 20px var(--primary);
            animation: scan 3s linear infinite;
            opacity: 0.5;
            pointer-events: none;
        }
        @keyframes scan { 0% { top: 0; opacity: 0; } 10% { opacity: 1; } 90% { opacity: 1; } 100% { top: 100%; opacity: 0; } }

        /* شاشة التحميل */
        #loader {
            position: fixed; inset: 0; background: var(--dark);
            display: flex; justify-content: center; align-items: center;
            z-index: 9999; color: var(--primary); font-family: 'Orbitron';
            font-size: 24px; font-weight: 900; letter-spacing: 5px;
            transition: opacity 1s;
        }
    </style>
</head>
<body>

<!-- شاشة التحميل الأولية -->
<div id="loader">INITIALIZING NEXUS CORE...</div>

<!-- الرسوميات ثلاثية الأبعاد -->
<div id="webgl-container"></div>

<!-- واجهة المستخدم -->
<div class="ui-layer">
    
    <header class="hud-element">
        <div class="brand">
            <h1>AI.NEXUS_</h1>
        </div>
        <div class="sys-stats" id="stats">
            CPU: 0%<br>RAM: 0GB<br>UPLINK: ONLINE
        </div>
    </header>

    <div class="ai-core hud-element">
        <div class="scanning-line"></div>
        <div class="chat-box" id="chatBox">
            <div class="message msg-ai">
                <strong>الأنظمة تعمل بكفاءة 100% 🤖</strong><br>
                مرحباً بك في واجهة الذكاء الكمّي. أنا متصل بقاعدة البيانات العالمية.<br>
                اسألني عن أي شيء (مثال: الثقب الأسود، الذكاء الاصطناعي، فلسطين...).
            </div>
        </div>
        
        <div class="input-panel">
            <input type="text" id="userInput" placeholder="أدخل استعلامك هنا للبحث في الشبكة..." autocomplete="off">
            <button id="sendBtn" onclick="processQuery()">إرسال Data</button>
        </div>
    </div>

</div>

<script>
    /* =========================================
       1. إزالة شاشة التحميل
    ========================================= */
    window.onload = () => {
        setTimeout(() => {
            const loader = document.getElementById('loader');
            loader.style.opacity = '0';
            setTimeout(() => loader.remove(), 1000);
        }, 1500);
    };

    /* =========================================
       2. نظام الإحصائيات الوهمي الاحترافي
    ========================================= */
    setInterval(() => {
        const cpu = (Math.random() * 20 + 5).toFixed(1);
        const ram = (Math.random() * 4 + 2).toFixed(2);
        document.getElementById('stats').innerHTML = `CPU: ${cpu}%<br>RAM: ${ram} TB<br>UPLINK: SECURE`;
    }, 1000);

    /* =========================================
       3. محرك الرسوميات الثلاثي الأبعاد (الشبكة العصبية)
    ========================================= */
    const container = document.getElementById('webgl-container');
    const scene = new THREE.Scene();
    scene.fog = new THREE.FogExp2(0x050510, 0.002);

    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 1, 2000);
    camera.position.z = 400;

    const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
    renderer.setPixelRatio(window.devicePixelRatio);
    renderer.setSize(window.innerWidth, window.innerHeight);
    container.appendChild(renderer.domElement);

    // إنشاء الجسيمات (Particles)
    const particleCount = 400;
    const geometry = new THREE.BufferGeometry();
    const positions = new Float32Array(particleCount * 3);
    const velocities = [];

    for (let i = 0; i < particleCount; i++) {
        positions[i * 3] = (Math.random() - 0.5) * 1000;
        positions[i * 3 + 1] = (Math.random() - 0.5) * 1000;
        positions[i * 3 + 2] = (Math.random() - 0.5) * 1000;
        velocities.push({
            x: (Math.random() - 0.5) * 1,
            y: (Math.random() - 0.5) * 1,
            z: (Math.random() - 0.5) * 1
        });
    }

    geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));

    // مادة الجسيمات
    const pMaterial = new THREE.PointsMaterial({
        color: 0x00f0ff,
        size: 3,
        transparent: true,
        opacity: 0.8,
        blending: THREE.AdditiveBlending
    });

    const particles = new THREE.Points(geometry, pMaterial);
    scene.add(particles);

    // خطوط الربط بين الجسيمات
    const lineMaterial = new THREE.LineBasicMaterial({
        color: 0x00f0ff,
        transparent: true,
        opacity: 0.15
    });

    // تفاعل الماوس / اللمس
    let mouseX = 0, mouseY = 0;
    document.addEventListener('mousemove', (e) => {
        mouseX = (e.clientX - window.innerWidth / 2) * 0.5;
        mouseY = (e.clientY - window.innerHeight / 2) * 0.5;
    });
    document.addEventListener('touchmove', (e) => {
        mouseX = (e.touches[0].clientX - window.innerWidth / 2) * 0.5;
        mouseY = (e.touches[0].clientY - window.innerHeight / 2) * 0.5;
    });

    // حلقة التحريك (Animation Loop)
    function animate() {
        requestAnimationFrame(animate);

        camera.position.x += (mouseX - camera.position.x) * 0.05;
        camera.position.y += (-mouseY - camera.position.y) * 0.05;
        camera.lookAt(scene.position);

        const positions = particles.geometry.attributes.position.array;
        
        for (let i = 0; i < particleCount; i++) {
            positions[i * 3] += velocities[i].x;
            positions[i * 3 + 1] += velocities[i].y;
            positions[i * 3 + 2] += velocities[i].z;

            // ارتداد عند الحواف
            if (Math.abs(positions[i * 3]) > 500) velocities[i].x *= -1;
            if (Math.abs(positions[i * 3 + 1]) > 500) velocities[i].y *= -1;
            if (Math.abs(positions[i * 3 + 2]) > 500) velocities[i].z *= -1;
        }
        
        particles.geometry.attributes.position.needsUpdate = true;
        particles.rotation.y += 0.001;

        renderer.render(scene, camera);
    }
    animate();

    // توافقية الشاشة
    window.addEventListener('resize', () => {
        camera.aspect = window.innerWidth / window.innerHeight;
        camera.updateProjectionMatrix();
        renderer.setSize(window.innerWidth, window.innerHeight);
    });

    /* =========================================
       4. محرك الذكاء الاصطناعي والمحادثة
    ========================================= */
    const chatBox = document.getElementById('chatBox');
    const userInput = document.getElementById('userInput');

    // إرسال بالضغط على Enter
    userInput.addEventListener('keypress', function (e) {
        if (e.key === 'Enter') processQuery();
    });

    async function processQuery() {
        const text = userInput.value.trim();
        if (!text) return;

        // طباعة رسالة المستخدم
        appendMessage(text, 'msg-user');
        userInput.value = '';

        // رسالة جارِ البحث
        const loadingMsgId = 'loading-' + Date.now();
        appendMessage('يتم فحص قواعد البيانات العالمية وبناء الاستجابة...', 'msg-ai', loadingMsgId);

        try {
            // جلب البيانات الحقيقية من ويكيبيديا (العربية)
            const endpoint = `https://ar.wikipedia.org/api/rest_v1/page/summary/${encodeURIComponent(text)}`;
            const response = await fetch(endpoint);
            
            let reply = "";
            if (response.ok) {
                const data = await response.json();
                if (data.extract) {
                    reply = `<strong>تم العثور على تطابق:</strong><br>${data.extract}`;
                } else {
                    reply = "لا توجد بيانات دقيقة حول هذا الموضوع في السجلات الحالية. حاول مصطلحاً آخر.";
                }
            } else {
                reply = "لم أتمكن من العثور على الموضوع. يرجى التأكد من الإملاء أو المحاولة بكلمات مفتاحية أخرى.";
            }

            // تحديث الرسالة بتأثير الكتابة
            document.getElementById(loadingMsgId).innerHTML = '';
            typeWriterEffect(reply, loadingMsgId);

        } catch (error) {
            document.getElementById(loadingMsgId).innerHTML = "⚠️ فشل الاتصال بالسيرفر. النظام يعاني من تداخل إشارات.";
        }
    }

    function appendMessage(text, className, id = '') {
        const div = document.createElement('div');
        div.className = `message ${className}`;
        if (id) div.id = id;
        div.innerHTML = text;
        chatBox.appendChild(div);
        chatBox.scrollTop = chatBox.scrollHeight;
    }

    // تأثير الآلة الكاتبة للذكاء الاصطناعي
    function typeWriterEffect(htmlText, elementId) {
        const el = document.getElementById(elementId);
        let i = 0;
        el.innerHTML = '';
        
        // نتعامل مع الـ HTML كطريقة بسيطة (عرض الكلمات وليس الحروف لتسريع العملية ومنع كسر الوسوم)
        const tokens = htmlText.split(/(<[^>]+>| )/);
        
        function type() {
            if (i < tokens.length) {
                el.innerHTML += tokens[i];
                i++;
                chatBox.scrollTop = chatBox.scrollHeight;
                setTimeout(type, 15); // سرعة الكتابة
            }
        }
        type();
    }
</script>

</body>
</html>
