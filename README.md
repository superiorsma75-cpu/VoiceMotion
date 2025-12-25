<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VoiceMotion - 2026 Edition</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;500;700&family=Plus+Jakarta+Sans:wght@400;600;700&display=swap" rel="stylesheet">
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons+Round" rel="stylesheet">
    <style>
        :root {
            --primary: #6366f1;
            --primary-glow: rgba(99, 102, 241, 0.6);
            --secondary: #06b6d4;
            --accent-2025: #d946ef; /* Fuchsia */
            --accent-2026: #fbbf24; /* Amber/Gold */
            --bg-dark: #030712;
            --glass-bg: rgba(17, 24, 39, 0.7);
            --glass-border: rgba(255, 255, 255, 0.08);
            --text-main: #f9fafb;
            --text-muted: #9ca3af;
            --success: #10b981;
            --danger: #ef4444;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Plus Jakarta Sans', sans-serif; }

        body {
            background-color: var(--bg-dark);
            background-image: 
                radial-gradient(circle at 0% 0%, rgba(99, 102, 241, 0.15) 0%, transparent 50%),
                radial-gradient(circle at 100% 100%, rgba(217, 70, 239, 0.1) 0%, transparent 50%);
            color: var(--text-main);
            height: 100vh;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }

        /* --- Components --- */
        .btn-icon {
            background: rgba(255,255,255,0.03);
            border: 1px solid var(--glass-border);
            color: white;
            width: 36px; height: 36px;
            border-radius: 8px;
            display: flex; align-items: center; justify-content: center;
            cursor: pointer; transition: 0.2s;
        }
        .btn-icon:hover { background: rgba(255,255,255,0.1); border-color: var(--primary); }

        /* --- Header --- */
        header {
            height: 64px;
            background: rgba(3, 7, 18, 0.8);
            backdrop-filter: blur(12px);
            border-bottom: 1px solid var(--glass-border);
            display: flex; align-items: center; justify-content: space-between;
            padding: 0 1.5rem;
            z-index: 50;
        }
        .brand {
            display: flex; align-items: center; gap: 10px;
            font-family: 'Orbitron', sans-serif;
            font-weight: 900;
            font-size: 1.4rem;
            letter-spacing: 1px;
            text-transform: uppercase;
        }
        .brand span { color: var(--secondary); }

        /* Profile & Dropdown */
        .profile-container { position: relative; }
        .avatar {
            width: 38px; height: 38px;
            border-radius: 8px;
            background: linear-gradient(135deg, #4f46e5, #9333ea);
            display: flex; align-items: center; justify-content: center;
            font-weight: bold; font-family: 'Orbitron'; cursor: pointer;
            border: 1px solid rgba(255,255,255,0.2);
        }
        .dropdown-menu {
            position: absolute; top: 50px; right: 0; width: 240px;
            background: rgba(17, 24, 39, 0.95);
            backdrop-filter: blur(16px);
            border: 1px solid var(--glass-border);
            border-radius: 12px; padding: 0.5rem;
            display: none;
            box-shadow: 0 20px 40px rgba(0,0,0,0.6);
            transform-origin: top right;
            animation: popIn 0.2s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }
        .dropdown-menu.active { display: block; }
        .dropdown-item {
            padding: 0.75rem 1rem; display: flex; align-items: center; gap: 10px;
            cursor: pointer; border-radius: 6px; font-size: 0.9rem; color: var(--text-muted);
            transition: 0.2s;
        }
        .dropdown-item:hover { background: rgba(255,255,255,0.05); color: white; }
        .dropdown-divider { height: 1px; background: var(--glass-border); margin: 0.3rem 0; }

        /* --- Layout --- */
        main { display: flex; flex: 1; overflow: hidden; }

        /* --- Sidebar --- */
        .sidebar {
            width: 380px;
            background: var(--glass-bg);
            backdrop-filter: blur(24px);
            border-right: 1px solid var(--glass-border);
            padding: 1.5rem;
            display: flex; flex-direction: column; gap: 1.5rem;
            overflow-y: auto;
            z-index: 40;
        }
        .sidebar::-webkit-scrollbar { width: 4px; }
        .sidebar::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.1); border-radius: 2px; }

        .section-header {
            display: flex; justify-content: space-between; align-items: center;
            margin-bottom: 0.8rem;
        }
        .section-title {
            font-size: 0.7rem; text-transform: uppercase; letter-spacing: 0.1em;
            color: var(--text-muted); font-weight: 700;
            display: flex; align-items: center; gap: 6px;
        }

        /* Inputs */
        .input-group { display: flex; flex-direction: column; gap: 0.5rem; margin-bottom: 1rem; }
        label { font-size: 0.8rem; color: var(--text-muted); font-weight: 500; }
        input[type="text"], textarea, select {
            background: rgba(0, 0, 0, 0.4);
            border: 1px solid var(--glass-border);
            color: white; padding: 0.75rem; border-radius: 8px;
            outline: none; font-size: 0.9rem; width: 100%; transition: 0.3s;
        }
        input:focus, textarea:focus { border-color: var(--primary); box-shadow: 0 0 0 2px rgba(99, 102, 241, 0.2); }
        textarea { resize: vertical; min-height: 80px; }

        /* Template Cards (New for 2025/2026) */
        .template-grid {
            display: grid; grid-template-columns: 1fr 1fr; gap: 0.8rem;
        }
        .template-card {
            background: rgba(255,255,255,0.02);
            border: 1px solid var(--glass-border);
            border-radius: 12px; padding: 1rem;
            cursor: pointer; position: relative; overflow: hidden;
            transition: all 0.3s ease;
            text-align: center;
        }
        .template-card:hover { transform: translateY(-3px); border-color: rgba(255,255,255,0.2); }
        .template-card.active { border-color: var(--primary); background: rgba(99, 102, 241, 0.1); }
        .template-card.active::after {
            content: 'AKTIF'; position: absolute; top: 6px; right: 6px;
            font-size: 0.6rem; background: var(--primary); color: white;
            padding: 2px 6px; border-radius: 4px; font-weight: bold;
        }
        .template-icon { font-size: 1.5rem; margin-bottom: 0.5rem; display: block; }
        .template-name { font-size: 0.85rem; font-weight: 600; }
        .template-year { font-size: 0.65rem; color: var(--text-muted); text-transform: uppercase; letter-spacing: 1px; }

        /* Preview Area */
        .preview-area {
            flex: 1; display: flex; flex-direction: column;
            align-items: center; justify-content: center;
            position: relative; padding: 2rem;
        }
        .canvas-wrapper {
            width: 100%; max-width: 900px;
            aspect-ratio: 16/9;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 20px 50px rgba(0,0,0,0.5), 0 0 0 1px rgba(255,255,255,0.05);
            background: #000;
            position: relative;
        }
        canvas { width: 100%; height: 100%; display: block; }

        .control-dock {
            position: absolute; bottom: 30px;
            background: rgba(17, 24, 39, 0.9);
            backdrop-filter: blur(16px);
            border: 1px solid var(--glass-border);
            padding: 0.8rem 1.5rem;
            border-radius: 2rem;
            display: flex; gap: 1rem;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }

        .btn { border: none; padding: 0.7rem 1.4rem; border-radius: 1.5rem; font-weight: 600; cursor: pointer; display: flex; align-items: center; gap: 0.5rem; font-size: 0.9rem; transition: 0.2s; }
        .btn-primary { background: var(--primary); color: white; box-shadow: 0 4px 15px rgba(99, 102, 241, 0.4); }
        .btn-primary:hover { background: #4f46e5; }
        .btn-outline { background: transparent; border: 1px solid var(--glass-border); color: white; }
        .btn-outline:hover { background: rgba(255,255,255,0.05); border-color: white; }

        /* --- Modal Settings --- */
        .modal-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.8); backdrop-filter: blur(5px);
            z-index: 100; display: none; align-items: center; justify-content: center;
        }
        .modal-overlay.active { display: flex; animation: fadeIn 0.3s; }
        .modal-content {
            background: #111827; width: 420px; padding: 2rem;
            border-radius: 16px; border: 1px solid var(--glass-border);
            box-shadow: 0 25px 50px rgba(0,0,0,0.5);
        }
        .setting-row {
            display: flex; justify-content: space-between; align-items: center;
            padding: 1rem 0; border-bottom: 1px solid var(--glass-border);
        }
        .setting-row:last-child { border-bottom: none; }
        .toggle-switch {
            width: 44px; height: 24px; background: #374151;
            border-radius: 20px; position: relative; cursor: pointer; transition: 0.3s;
        }
        .toggle-switch.active { background: var(--success); }
        .toggle-switch::after {
            content: ''; position: absolute; top: 2px; left: 2px;
            width: 20px; height: 20px; background: white;
            border-radius: 50%; transition: 0.3s;
        }
        .toggle-switch.active::after { left: 22px; }

        /* Animations */
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        @keyframes popIn { from { opacity: 0; transform: scale(0.9) translateY(10px); } to { opacity: 1; transform: scale(1) translateY(0); } }

        @media (max-width: 900px) {
            main { flex-direction: column; overflow-y: auto; }
            .sidebar { width: 100%; border-right: none; border-bottom: 1px solid var(--glass-border); height: auto; }
            .preview-area { padding: 1rem; }
            .control-dock { position: fixed; bottom: 20px; width: 90%; z-index: 60; justify-content: center; }
        }
    </style>
</head>
<body>

    <header>
        <div class="brand">
            <span class="material-icons-round" style="color:var(--primary)">movie_filter</span>
            VoiceMotion <span>PRO</span>
        </div>
        <div class="profile-container">
            <div class="avatar" id="userAvatar">AD</div>
            <div class="dropdown-menu" id="profileDropdown">
                <div class="dropdown-item">
                    <span class="material-icons-round" style="font-size:18px">account_circle</span> Profil Admin
                </div>
                <div class="dropdown-item" onclick="openSettings()">
                    <span class="material-icons-round" style="font-size:18px">tune</span> Pengaturan & Fitur
                </div>
                <div class="dropdown-divider"></div>
                <div class="dropdown-item" style="color: var(--danger);">
                    <span class="material-icons-round" style="font-size:18px">logout</span> Keluar
                </div>
            </div>
        </div>
    </header>

    <main>
        <!-- Sidebar -->
        <div class="sidebar">
            
            <!-- Template Selector (NEW 2025/2026) -->
            <div>
                <div class="section-header">
                    <div class="section-title"><span class="material-icons-round" style="font-size:14px">layers</span> Pilih Template</div>
                </div>
                <div class="template-grid" id="templateGrid">
                    <!-- Template Default -->
                    <div class="template-card active" data-template="classic">
                        <span class="template-icon" style="color:var(--text-muted)">play_circle</span>
                        <div class="template-name">Classic</div>
                        <div class="template-year">Standar</div>
                    </div>
                    
                    <!-- Template 2025 -->
                    <div class="template-card" data-template="cyber2025">
                        <span class="template-icon" style="color:var(--accent-2025)">bug_report</span>
                        <div class="template-name">Cyber Glitch</div>
                        <div class="template-year" style="color:var(--accent-2025)">EDISI 2025</div>
                    </div>

                    <!-- Template 2026 -->
                    <div class="template-card" data-template="space2026">
                        <span class="template-icon" style="color:var(--accent-2026)">rocket_launch</span>
                        <div class="template-name">Galactic</div>
                        <div class="template-year" style="color:var(--accent-2026)">EDISI 2026</div>
                    </div>

                    <!-- Template Neon -->
                    <div class="template-card" data-template="neon">
                        <span class="template-icon" style="color:#06b6d4">lightbulb</span>
                        <div class="template-name">Neon Pulse</div>
                        <div class="template-year">Energetik</div>
                    </div>
                </div>
            </div>

            <!-- Content Inputs -->
            <div style="background: rgba(255,255,255,0.02); padding: 1.25rem; border-radius: 12px; border: 1px solid var(--glass-border);">
                <div class="section-title" style="margin-bottom:1rem;">Konten Video</div>
                <div class="input-group">
                    <label>Headline</label>
                    <input type="text" id="mainText" value="FUTURE IS NOW">
                </div>
                <div class="input-group">
                    <label>Deskripsi (Dibaca AI)</label>
                    <textarea id="subText">Selamat datang di masa depan teknologi. Video ini dibuat dengan template terbaru 2026.</textarea>
                </div>
            </div>

            <!-- Voice Settings -->
            <div style="background: rgba(255,255,255,0.02); padding: 1.25rem; border-radius: 12px; border: 1px solid var(--glass-border);">
                <div class="section-title" style="margin-bottom:1rem;">Suara AI</div>
                <div class="input-group">
                    <select id="voiceSelect"><option>Memuat suara...</option></select>
                </div>
                <div class="input-group">
                    <label>Kecepatan: <span id="rateVal" style="color:var(--primary); font-size:0.7rem;">1.0x</span></label>
                    <input type="range" id="rate" min="0.5" max="2" value="1" step="0.1" style="width:100%; accent-color:var(--primary)">
                </div>
            </div>

        </div>

        <!-- Preview Area -->
        <div class="preview-area">
            <div class="canvas-wrapper">
                <canvas id="videoCanvas" width="1920" height="1080"></canvas>
            </div>

            <div class="control-dock">
                <button class="btn btn-outline" id="btnPreview">
                    <span class="material-icons-round">visibility</span> Preview
                </button>
                <button class="btn btn-primary" id="btnExport">
                    <span class="material-icons-round">movie_creation</span> Buat Video
                </button>
            </div>
        </div>
    </main>

    <!-- Settings Modal (Updated) -->
    <div class="modal-overlay" id="settingsModal">
        <div class="modal-content">
            <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:1.5rem;">
                <h3 style="font-weight:700; font-size:1.2rem;">Pengaturan</h3>
                <div class="btn-icon" onclick="closeSettings()" style="width:32px; height:32px;"><span class="material-icons-round" style="font-size:18px">close</span></div>
            </div>

            <div class="setting-row">
                <div>
                    <div style="font-weight:600; font-size:0.9rem;">Mode Kontras Tinggi</div>
                    <div style="font-size:0.75rem; color:var(--text-muted);">Teks lebih jelas di latar gelap</div>
                </div>
                <div class="toggle-switch active" onclick="toggleSwitch(this)"></div>
            </div>

            <div class="setting-row">
                <div>
                    <div style="font-weight:600; font-size:0.9rem;">Kualitas HD (1080p)</div>
                    <div style="font-size:0.75rem; color:var(--text-muted);">Menggunakan resolusi tinggi</div>
                </div>
                <div class="toggle-switch active" onclick="toggleSwitch(this)"></div>
            </div>

            <div class="setting-row">
                <div>
                    <div style="font-weight:600; font-size:0.9rem;">Auto-Simpan Proyek</div>
                    <div style="font-size:0.75rem; color:var(--text-muted);">Menyimpan otomatis setiap 30 detik</div>
                </div>
                <div class="toggle-switch" onclick="toggleSwitch(this)"></div>
            </div>
            
            <div class="setting-row">
                <div>
                    <div style="font-weight:600; font-size:0.9rem;">Efek Partikel</div>
                    <div style="font-size:0.75rem; color:var(--text-muted);">Hidupkan animasi latar belakang</div>
                </div>
                <div class="toggle-switch active" onclick="toggleSwitch(this)"></div>
            </div>

            <button class="btn btn-primary" style="width:100%; justify-content:center; margin-top:1rem;" onclick="closeSettings()">Tutup</button>
        </div>
    </div>

    <script>
        // --- 1. KONFIGURASI STATE ---
        const canvas = document.getElementById('videoCanvas');
        const ctx = canvas.getContext('2d');
        const synth = window.speechSynthesis;
        let voices = [];

        let state = {
            text: document.getElementById('mainText').value,
            subText: document.getElementById('subText').value,
            template: 'classic', // classic, cyber2025, space2026, neon
            isPlaying: false,
            startTime: 0,
            stars: [] // Untuk efek 2026
        };

        // Init Stars for 2026 Template
        for(let i=0; i<100; i++) {
            state.stars.push({
                x: Math.random() * canvas.width,
                y: Math.random() * canvas.height,
                z: Math.random() * 2 // Depth
            });
        }

        // --- 2. MANAJEMEN TEMPLATES ---
        const templateCards = document.querySelectorAll('.template-card');
        templateCards.forEach(card => {
            card.addEventListener('click', () => {
                templateCards.forEach(c => c.classList.remove('active'));
                card.classList.add('active');
                state.template = card.dataset.template;
                renderFrame(0); // Update tampilan segera
            });
        });

        // --- 3. MANAJEMEN SUARA (TTS) ---
        const voiceSelect = document.getElementById('voiceSelect');
        const rateInput = document.getElementById('rate');
        const rateVal = document.getElementById('rateVal');

        function loadVoices() {
            voices = synth.getVoices();
            voiceSelect.innerHTML = '';
            const idVoices = voices.filter(v => v.lang.includes('id') || v.lang.includes('ID'));
            if (idVoices.length > 0) {
                idVoices.forEach(v => {
                    const opt = document.createElement('option');
                    opt.textContent = v.name;
                    opt.value = v.name;
                    voiceSelect.appendChild(opt);
                });
            } else {
                voices.forEach(v => {
                    const opt = document.createElement('option');
                    opt.textContent = v.name;
                    opt.value = v.name;
                    voiceSelect.appendChild(opt);
                });
            }
        }
        loadVoices();
        if (speechSynthesis.onvoiceschanged !== undefined) speechSynthesis.onvoiceschanged = loadVoices;

        rateInput.addEventListener('input', (e) => {
            rateVal.textContent = e.target.value + 'x';
            if (state.isPlaying) { synth.cancel(); speak(state.subText); }
        });

        function speak(text) {
            if (synth.speaking) synth.cancel();
            if (text !== '') {
                const u = new SpeechSynthesisUtterance(text);
                u.voice = voices.find(v => v.name === voiceSelect.value);
                u.rate = rateInput.value;
                synth.speak(u);
            }
        }

        // --- 4. SISTEM INPUT & PREVIEW ---
        [document.getElementById('mainText'), document.getElementById('subText')].forEach(el => {
            el.addEventListener('input', () => {
                state.text = document.getElementById('mainText').value;
                state.subText = document.getElementById('subText').value;
                if (!state.isPlaying) renderFrame(0); // Live preview saat ngetik
            });
        });

        // --- 5. ENGINE RENDERING VISUAL ---
        function loop(timestamp) {
            if (!state.startTime) state.startTime = timestamp;
            const elapsed = timestamp - state.startTime;
            // Loop every 10 seconds for preview
            const time = elapsed % 10000;
            
            renderFrame(time);
            if (state.isPlaying) requestAnimationFrame(loop);
        }

        function renderFrame(timeMs) {
            const w = canvas.width;
            const h = canvas.height;
            ctx.clearRect(0, 0, w, h);

            // === LOGIKA TEMPLATE ===
            switch (state.template) {
                case 'cyber2025':
                    drawCyber2025(timeMs, w, h);
                    break;
                case 'space2026':
                    drawSpace2026(timeMs, w, h);
                    break;
                case 'neon':
                    drawNeon(timeMs, w, h);
                    break;
                default:
                    drawClassic(timeMs, w, h);
            }
        }

        // --- TEMPLATE FUNCTIONS ---

        function drawClassic(timeMs, w, h) {
            ctx.fillStyle = '#111827';
            ctx.fillRect(0, 0, w, h);
            
            // Text
            ctx.fillStyle = '#fff';
            ctx.font = 'bold 120px "Plus Jakarta Sans"';
            ctx.textAlign = 'center';
            ctx.textBaseline = 'middle';
            ctx.fillText(state.text.toUpperCase(), w/2, h/2 - 50);
            
            ctx.fillStyle = '#9ca3af';
            ctx.font = '60px "Plus Jakarta Sans"';
            ctx.fillText(state.subText, w/2, h/2 + 80);
        }

        function drawCyber2025(timeMs, w, h) {
            // Background Grid
            ctx.fillStyle = '#000';
            ctx.fillRect(0,0,w,h);
            
            ctx.strokeStyle = 'rgba(217, 70, 239, 0.3)';
            ctx.lineWidth = 2;
            const gridSize = 50;
            const offset = (timeMs / 20) % gridSize;
            
            for(let x=0; x<w; x+=gridSize) {
                ctx.beginPath(); ctx.moveTo(x + offset - gridSize, 0); ctx.lineTo(x + offset - gridSize, h); ctx.stroke();
            }

            // Glitch Text
            const txt = state.text.toUpperCase();
            const split = Math.floor(timeMs / 200) % 2;
            
            ctx.textAlign = 'center'; ctx.textBaseline = 'middle';
            ctx.font = 'bold 140px "Orbitron"';

            // Red Shift
            if (split) {
                ctx.fillStyle = 'rgba(239, 68, 68, 0.7)';
                ctx.fillText(txt, w/2 + 4, h/2);
            }
            // Cyan Shift
            if (!split) {
                ctx.fillStyle = 'rgba(6, 182, 212, 0.7)';
                ctx.fillText(txt, w/2 - 4, h/2);
            }
            
            // Main Text
            ctx.fillStyle = '#fff';
            ctx.fillText(txt, w/2, h/2);

            // Subtext
            ctx.font = '50px "Rajdhani"';
            ctx.fillStyle = 'rgba(255,255,255,0.7)';
            ctx.fillText(state.subText, w/2, h/2 + 120);
        }

        function drawSpace2026(timeMs, w, h) {
            // Deep Space Background
            const grad = ctx.createRadialGradient(w/2, h/2, 0, w/2, h/2, w);
            grad.addColorStop(0, '#1e1b4b');
            grad.addColorStop(1, '#020617');
            ctx.fillStyle = grad;
            ctx.fillRect(0,0,w,h);

            // Warp Stars
            ctx.fillStyle = '#fff';
            state.stars.forEach(star => {
                // Simple star logic
                star.x -= star.z * 2; 
                if(star.x < 0) star.x = w;
                
                const size = Math.max(1, star.z * 1.5);
                ctx.beginPath(); ctx.arc(star.x, star.y, size, 0, Math.PI*2); ctx.fill();
            });

            // Floating Text
            ctx.textAlign = 'center'; ctx.textBaseline = 'middle';
            ctx.font = 'bold 130px "Orbitron"';
            
            // Glow
            ctx.shadowColor = '#fbbf24';
            ctx.shadowBlur = 30 + 10 * Math.sin(timeMs/500);
            ctx.fillStyle = '#fff';
            ctx.fillText(state.text, w/2, h/2);
            
            ctx.shadowBlur = 0;
            ctx.font = '60px "Rajdhani"';
            ctx.fillStyle = '#fbbf24';
            ctx.fillText(state.subText, w/2, h/2 + 100);
        }

        function drawNeon(timeMs, w, h) {
            const hue = (timeMs / 10) % 360;
            ctx.fillStyle = `hsl(${hue}, 60%, 10%)`;
            ctx.fillRect(0,0,w,h);

            ctx.shadowColor = `hsl(${hue}, 100%, 50%)`;
            ctx.shadowBlur = 20;
            ctx.fillStyle = '#fff';
            ctx.font = 'bold 120px sans-serif';
            ctx.textAlign = 'center';
            ctx.fillText(state.text, w/2, h/2);
            
            ctx.shadowBlur = 0;
        }

        // --- 6. MENU PROFILE & SETTINGS ---
        const userAvatar = document.getElementById('userAvatar');
        const profileDropdown = document.getElementById('profileDropdown');
        const settingsModal = document.getElementById('settingsModal');

        userAvatar.addEventListener('click', (e) => {
            e.stopPropagation();
            profileDropdown.classList.toggle('active');
        });
        window.addEventListener('click', () => profileDropdown.classList.remove('active'));

        function openSettings() { settingsModal.classList.add('active'); }
        function closeSettings() { settingsModal.classList.remove('active'); }
        function toggleSwitch(el) { el.classList.toggle('active'); }

        // --- 7. BUTTON ACTIONS ---
        const btnPreview = document.getElementById('btnPreview');
        const btnExport = document.getElementById('btnExport');

        btnPreview.addEventListener('click', () => {
            if(state.isPlaying) {
                state.isPlaying = false; synth.cancel();
                btnPreview.innerHTML = `<span class="material-icons-round">visibility</span> Preview`;
            } else {
                state.isPlaying = true;
                state.startTime = 0;
                speak(state.subText);
                loop();
                btnPreview.innerHTML = `<span class="material-icons-round">pause</span> Stop`;
            }
        });

        btnExport.addEventListener('click', () => {
            alert("Simulasi Rendering: Video berhasil dibuat! (Fitur perekam suara dan visual aktif)");
        });

        // Start static frame
        renderFrame(0);

    </script>
</body>
</html>
