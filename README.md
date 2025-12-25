# VoiceMotion2025
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VoiceMotion - Pro Dashboard</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700&family=Playfair+Display:ital,wght@1,700&family=JetBrains+Mono:wght@500&display=swap" rel="stylesheet">
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons+Round" rel="stylesheet">
    <style>
        :root {
            --primary: #8b5cf6;
            --primary-glow: rgba(139, 92, 246, 0.5);
            --secondary: #06b6d4;
            --bg-dark: #020617;
            --glass-bg: rgba(15, 23, 42, 0.6);
            --glass-border: rgba(255, 255, 255, 0.1);
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --danger: #ef4444;
            --success: #22c55e;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Plus Jakarta Sans', sans-serif; }

        body {
            background-color: var(--bg-dark);
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(139, 92, 246, 0.15) 0%, transparent 40%),
                radial-gradient(circle at 90% 80%, rgba(6, 182, 212, 0.15) 0%, transparent 40%);
            color: var(--text-main);
            height: 100vh;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }

        /* --- Components --- */
        .btn-icon {
            background: rgba(255,255,255,0.05);
            border: 1px solid var(--glass-border);
            color: white;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.2s;
        }
        .btn-icon:hover { background: rgba(255,255,255,0.1); border-color: var(--primary); }

        /* --- Header --- */
        header {
            height: 70px;
            background: rgba(2, 6, 23, 0.8);
            backdrop-filter: blur(10px);
            border-bottom: 1px solid var(--glass-border);
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 2rem;
            z-index: 50;
        }

        .brand {
            display: flex;
            align-items: center;
            gap: 10px;
            font-weight: 800;
            font-size: 1.5rem;
            letter-spacing: -0.02em;
        }
        .brand span { background: linear-gradient(135deg, #a78bfa, #22d3ee); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }

        /* Profile Menu */
        .profile-container { position: relative; }
        .avatar {
            width: 40px; height: 40px;
            border-radius: 50%;
            background: linear-gradient(135deg, #6366f1, #a855f7);
            display: flex; align-items: center; justify-content: center;
            font-weight: bold; cursor: pointer;
            border: 2px solid rgba(255,255,255,0.2);
        }
        .dropdown-menu {
            position: absolute;
            top: 50px; right: 0;
            width: 200px;
            background: rgba(30, 41, 59, 0.95);
            backdrop-filter: blur(15px);
            border: 1px solid var(--glass-border);
            border-radius: 12px;
            padding: 0.5rem;
            display: none;
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);
            animation: slideDown 0.2s ease;
        }
        .dropdown-menu.active { display: block; }
        .dropdown-item {
            padding: 0.75rem 1rem;
            display: flex;
            align-items: center;
            gap: 10px;
            cursor: pointer;
            border-radius: 8px;
            font-size: 0.9rem;
            color: var(--text-muted);
            transition: all 0.2s;
        }
        .dropdown-item:hover { background: rgba(255,255,255,0.05); color: white; }
        .dropdown-divider { height: 1px; background: var(--glass-border); margin: 0.5rem 0; }

        /* --- Main Layout --- */
        main { display: flex; flex: 1; overflow: hidden; position: relative; }

        /* --- Sidebar --- */
        .sidebar {
            width: 400px;
            background: var(--glass-bg);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border-right: 1px solid var(--glass-border);
            padding: 1.5rem;
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
            overflow-y: auto;
            z-index: 40;
        }
        .sidebar::-webkit-scrollbar { width: 5px; }
        .sidebar::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.1); border-radius: 3px; }

        .badge {
            font-size: 0.7rem;
            padding: 2px 8px;
            border-radius: 4px;
            background: var(--primary);
            color: white;
            margin-left: auto;
        }

        /* Admin Updates Section */
        .updates-list { display: flex; flex-direction: column; gap: 0.8rem; }
        .update-card {
            background: rgba(255,255,255,0.03);
            border: 1px solid var(--glass-border);
            padding: 1rem;
            border-radius: 0.75rem;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .update-card:hover { background: rgba(255,255,255,0.08); border-color: var(--secondary); }
        .update-icon {
            width: 32px; height: 32px;
            background: rgba(6, 182, 212, 0.2);
            color: var(--secondary);
            border-radius: 8px;
            display: flex; align-items: center; justify-content: center;
            font-size: 1.2rem;
        }

        /* Standard Section Styles */
        .section-group {
            background: rgba(255,255,255,0.03);
            border: 1px solid var(--glass-border);
            border-radius: 1rem;
            padding: 1.5rem;
        }
        .section-title {
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 0.1em;
            color: var(--secondary);
            margin-bottom: 1rem;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .input-group { display: flex; flex-direction: column; gap: 0.5rem; margin-bottom: 1rem; }
        .input-group:last-child { margin-bottom: 0; }
        
        label { font-size: 0.85rem; color: var(--text-muted); font-weight: 500; }
        
        input[type="text"], textarea, select {
            background: rgba(0, 0, 0, 0.3);
            border: 1px solid var(--glass-border);
            color: white;
            padding: 0.8rem 1rem;
            border-radius: 0.5rem;
            outline: none;
            font-size: 0.9rem;
            width: 100%;
            transition: all 0.3s ease;
            font-family: inherit;
        }
        input[type="text"]:focus, textarea:focus, select:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 2px rgba(139, 92, 246, 0.2);
        }
        textarea { resize: vertical; min-height: 90px; }

        /* Style Grid */
        .style-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 0.8rem; }
        .style-card {
            background: rgba(255,255,255,0.03);
            border: 1px solid var(--glass-border);
            border-radius: 0.75rem;
            padding: 1rem;
            cursor: pointer;
            text-align: center;
            font-size: 0.85rem;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .style-card:hover { background: rgba(255,255,255,0.08); transform: translateY(-2px); }
        .style-card.active {
            background: linear-gradient(135deg, rgba(139, 92, 246, 0.2), rgba(6, 182, 212, 0.1));
            border-color: var(--primary);
            color: white;
            font-weight: 600;
            box-shadow: 0 4px 12px rgba(0,0,0,0.2);
        }

        /* --- Preview Area --- */
        .preview-area {
            flex: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            position: relative;
            padding: 2rem;
            background: radial-gradient(circle at center, rgba(255,255,255,0.03) 0%, transparent 70%);
        }
        .canvas-container {
            position: relative;
            width: 100%;
            max-width: 1000px;
            aspect-ratio: 16/9;
            border-radius: 1rem;
            overflow: hidden;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.8), 0 0 0 1px rgba(255,255,255,0.1);
            background: #000;
        }
        canvas { width: 100%; height: 100%; display: block; }

        /* Control Bar */
        .control-bar {
            position: absolute;
            bottom: 40px;
            background: rgba(15, 23, 42, 0.9);
            backdrop-filter: blur(12px);
            border: 1px solid var(--glass-border);
            padding: 1rem 1.5rem;
            border-radius: 3rem;
            display: flex;
            gap: 1rem;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.5);
            transform: translateY(0);
            transition: transform 0.3s ease;
        }
        .btn {
            border: none;
            padding: 0.75rem 1.5rem;
            border-radius: 2rem;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 0.6rem;
            font-size: 0.9rem;
            transition: all 0.2s;
        }
        .btn:active { transform: scale(0.95); }
        .btn-primary {
            background: linear-gradient(135deg, var(--primary), var(--primary-dark));
            color: white;
            box-shadow: 0 4px 15px rgba(139, 92, 246, 0.4);
        }
        .btn-primary:hover { box-shadow: 0 6px 20px rgba(139, 92, 246, 0.6); }
        .btn-outline {
            background: transparent;
            border: 1px solid rgba(255,255,255,0.2);
            color: white;
        }
        .btn-outline:hover { background: rgba(255,255,255,0.1); border-color: white; }

        /* Footer */
        footer {
            height: 40px;
            background: rgba(2, 6, 23, 0.9);
            border-top: 1px solid var(--glass-border);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.8rem;
            color: var(--text-muted);
            z-index: 50;
        }
        footer span { color: var(--primary); font-weight: 600; }

        /* --- Modals --- */
        .modal-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.7);
            backdrop-filter: blur(5px);
            z-index: 100;
            display: none;
            align-items: center;
            justify-content: center;
        }
        .modal-overlay.active { display: flex; animation: fadeIn 0.3s; }
        .modal-content {
            background: #0f172a;
            border: 1px solid var(--glass-border);
            width: 400px;
            padding: 2rem;
            border-radius: 1rem;
            box-shadow: 0 20px 25px rgba(0,0,0,0.5);
            position: relative;
        }
        .modal-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 1.5rem; }
        .modal-title { font-size: 1.25rem; font-weight: 700; }
        .close-btn { cursor: pointer; color: var(--text-muted); }

        /* --- AI Assistant (Trial Limit) --- */
        .ai-assistant-overlay {
            position: fixed; bottom: 20px; right: 20px;
            display: flex; flex-direction: column; align-items: flex-end;
            z-index: 90;
            pointer-events: none; /* Let clicks pass through unless on bubble */
        }
        .ai-bubble {
            background: linear-gradient(135deg, #1e1b4b, #312e81);
            border: 1px solid rgba(139, 92, 246, 0.5);
            padding: 1rem 1.5rem;
            border-radius: 1rem 1rem 0 1rem;
            max-width: 320px;
            margin-bottom: 1rem;
            box-shadow: 0 10px 15px rgba(0,0,0,0.3);
            color: white;
            pointer-events: auto;
            display: none;
            animation: popIn 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }
        .ai-avatar {
            width: 60px; height: 60px;
            background: linear-gradient(135deg, #6366f1, #a855f7);
            border-radius: 50%;
            display: flex; align-items: center; justify-content: center;
            box-shadow: 0 0 20px rgba(139, 92, 246, 0.6);
            pointer-events: auto;
            cursor: pointer;
            position: relative;
        }
        .ai-avatar::after {
            content: ''; position: absolute; top: 2px; right: 2px; width: 12px; height: 12px;
            background: #22c55e; border-radius: 50%; border: 2px solid #0f172a;
        }

        /* Animations */
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        @keyframes slideDown { from { opacity: 0; transform: translateY(-10px); } to { opacity: 1; transform: translateY(0); } }
        @keyframes popIn { from { opacity: 0; transform: scale(0.8) translateY(20px); } to { opacity: 1; transform: scale(1) translateY(0); } }

        /* Mobile Responsive */
        @media (max-width: 1000px) {
            main { flex-direction: column; overflow-y: auto; }
            .sidebar { width: 100%; height: auto; border-right: none; border-bottom: 1px solid var(--glass-border); }
            .preview-area { padding: 1rem; }
            .control-bar { position: fixed; bottom: 50px; width: 90%; justify-content: center; z-index: 60; }
            .ai-assistant-overlay { bottom: 100px; }
            footer { position: fixed; bottom: 0; width: 100%; z-index: 60; }
        }
    </style>
</head>
<body>

    <!-- Header -->
    <header>
        <div class="brand">
            <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="url(#grad1)" stroke-width="2">
                <defs><linearGradient id="grad1" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" style="stop-color:#a78bfa"/><stop offset="100%" style="stop-color:#22d3ee"/></linearGradient></defs>
                <path d="M12 2a3 3 0 0 0-3 3v8a3 3 0 0 0 6 0V4a3 3 0 0 0-3-3z"></path>
                <path d="M19 10v2a7 7 0 0 1-14 0v-2"></path>
                <line x1="12" y1="19" x2="12" y2="23"></line>
                <line x1="8" y1="23" x2="16" y2="23"></line>
            </svg>
            VoiceMotion
        </div>
        
        <div class="profile-container">
            <div class="avatar" id="userAvatar">US</div>
            <div class="dropdown-menu" id="profileDropdown">
                <div class="dropdown-item">
                    <span class="material-icons-round">person</span> Profil Saya
                </div>
                <div class="dropdown-item" onclick="openSettings()">
                    <span class="material-icons-round">settings</span> Setelan
                </div>
                <div class="dropdown-divider"></div>
                <div class="dropdown-item" style="color: var(--danger);">
                    <span class="material-icons-round">logout</span> Keluar
                </div>
            </div>
        </div>
    </header>

    <main>
        <!-- Sidebar -->
        <div class="sidebar">
            
            <!-- 1. Admin Updates Section (Dynamic) -->
            <div class="section-group">
                <div class="section-title">
                    <span class="material-icons-round" style="font-size:16px">auto_awesome</span>
                    Fitur & Update
                    <span class="badge">New</span>
                </div>
                <div class="updates-list" id="adminUpdatesList">
                    <!-- Items injected via JS -->
                </div>
            </div>

            <!-- 2. Content Editor -->
            <div class="section-group">
                <div class="section-title">
                    <span class="material-icons-round" style="font-size:16px">edit_note</span>
                    Editor Konten
                </div>
                <div class="input-group">
                    <label>Judul Utama</label>
                    <input type="text" id="mainText" value="Hello World">
                </div>
                <div class="input-group">
                    <label>Deskripsi (Suara AI)</label>
                    <textarea id="subText">Selamat datang di dashboard pembuatan video berbasis kecerdasan buatan.</textarea>
                </div>
            </div>

            <!-- 3. Voice Settings -->
            <div class="section-group">
                <div class="section-title">
                    <span class="material-icons-round" style="font-size:16px">graphic_eq</span>
                    Suara AI
                </div>
                <div class="input-group">
                    <label>Voice Actor</label>
                    <select id="voiceSelect"><option>Memuat...</option></select>
                </div>
                <div class="input-group">
                    <label>Pitch <span id="pitchVal" style="color:var(--primary)">1.0</span></label>
                    <input type="range" id="pitch" min="0.5" max="2" value="1" step="0.1">
                </div>
                <div class="input-group">
                    <label>Speed <span id="rateVal" style="color:var(--primary)">1.0x</span></label>
                    <input type="range" id="rate" min="0.5" max="2" value="1" step="0.1">
                </div>
            </div>

            <!-- 4. Visual Style -->
            <div class="section-group">
                <div class="section-title">
                    <span class="material-icons-round" style="font-size:16px">palette</span>
                    Gaya Visual
                </div>
                <div class="style-grid" id="styleGrid">
                    <div class="style-card active" data-style="neon">Neon</div>
                    <div class="style-card" data-style="typewriter">Typewriter</div>
                    <div class="style-card" data-style="minimal">Minimal</div>
                    <div class="style-card" data-style="cinematic">Cinematic</div>
                </div>
                <div class="input-group" style="margin-top: 1rem;">
                    <label>Warna Utama</label>
                    <div style="display:flex; gap:10px; align-items:center;">
                        <input type="color" id="colorMain" value="#ffffff" style="height:40px; width:60px; padding:0; border:none; background:none;">
                        <input type="text" value="#ffffff" readonly style="flex:1; background:transparent; border:none; color:white;">
                    </div>
                </div>
            </div>
        </div>

        <!-- Preview Area -->
        <div class="preview-area">
            <div class="canvas-container">
                <canvas id="videoCanvas" width="1920" height="1080"></canvas>
            </div>

            <div class="control-bar">
                <button class="btn btn-outline" id="btnPreview">
                    <span class="material-icons-round">play_arrow</span> Preview
                </button>
                <button class="btn btn-primary" id="btnExport">
                    <span class="material-icons-round">download</span> Render Video
                </button>
            </div>
        </div>
    </main>

    <!-- Footer -->
    <footer>
        &copy; <span id="currentYear"></span> VoiceMotion AI. All rights reserved.
    </footer>

    <!-- Settings Modal -->
    <div class="modal-overlay" id="settingsModal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">Pengaturan Akun</div>
                <div class="close-btn" onclick="closeSettings()">
                    <span class="material-icons-round">close</span>
                </div>
            </div>
            <div class="input-group">
                <label>Nama Pengguna</label>
                <input type="text" value="Pengguna Gratis">
            </div>
            <div class="input-group">
                <label>Sisa Uji Coba</label>
                <input type="text" id="trialDisplay" value="2 / 2" readonly style="background: rgba(0,0,0,0.2); color: var(--success);">
            </div>
            <div class="input-group">
                <label>Resolusi Default</label>
                <select>
                    <option>HD (720p)</option>
                    <option selected>Full HD (1080p)</option>
                </select>
            </div>
            <button class="btn btn-primary" style="width:100%; justify-content:center; margin-top:1rem;">Simpan Perubahan</button>
        </div>
    </div>

    <!-- AI Assistant Overlay -->
    <div class="ai-assistant-overlay" id="aiAssistant">
        <div class="ai-bubble" id="aiMessage">
            <strong>Halo! Saya Asisten AI.</strong><br>
            Sepertinya Anda sudah menggunakan kuota uji coba gratis (2x). Silakan upgrade ke Premium untuk terus membuat video keren!
        </div>
        <div class="ai-avatar" title="Klik untuk bantuan">
            <span class="material-icons-round" style="font-size:32px; color:white;">smart_toy</span>
        </div>
    </div>

    <script>
        // --- 1. Konfigurasi Admin (Simulasi Update Manual) ---
        // Di sini Admin bisa menambah menu baru tanpa mengubah HTML utama
        const ADMIN_FEATURES = [
            { title: "Tutorial: Cara Membuat Video", icon: "school", action: () => alert("Membuka Tutorial...") },
            { title: "Template Baru: Tahun Baru 2025", icon: "celebration", action: () => alert("Membuka Template...") },
            { title: "Unduh Assets (PNG/SVG)", icon: "folder_zip", action: () => alert("Mengunduh Assets...") }
        ];

        function renderAdminMenu() {
            const container = document.getElementById('adminUpdatesList');
            container.innerHTML = '';
            ADMIN_FEATURES.forEach(feature => {
                const div = document.createElement('div');
                div.className = 'update-card';
                div.onclick = feature.action;
                div.innerHTML = `
                    <div class="update-icon"><span class="material-icons-round">${feature.icon}</span></div>
                    <div style="font-size:0.9rem; font-weight:500;">${feature.title}</div>
                `;
                container.appendChild(div);
            });
        }
        renderAdminMenu();

        // --- 2. Sistem Trial (2x Gratis) ---
        const MAX_TRIAL = 2;
        let trialCount = parseInt(localStorage.getItem('voiceMotionTrial')) || 0;

        function updateTrialDisplay() {
            document.getElementById('trialDisplay').value = `${MAX_TRIAL - trialCount} / ${MAX_TRIAL}`;
            if (MAX_TRIAL - trialCount === 0) {
                document.getElementById('trialDisplay').style.color = 'var(--danger)';
            }
        }
        updateTrialDisplay();

        function checkTrialLimit() {
            if (trialCount >= MAX_TRIAL) {
                // Tampilkan Asisten AI
                const aiBubble = document.getElementById('aiMessage');
                aiBubble.style.display = 'block';
                return false; // Blokir render
            }
            return true; // Izinkan render
        }

        function incrementTrial() {
            trialCount++;
            localStorage.setItem('voiceMotionTrial', trialCount);
            updateTrialDisplay();
        }

        // --- 3. Profile & Settings Logic ---
        const profileDropdown = document.getElementById('profileDropdown');
        const userAvatar = document.getElementById('userAvatar');
        const settingsModal = document.getElementById('settingsModal');

        userAvatar.addEventListener('click', (e) => {
            e.stopPropagation();
            profileDropdown.classList.toggle('active');
        });

        window.addEventListener('click', () => {
            profileDropdown.classList.remove('active');
        });

        function openSettings() { settingsModal.classList.add('active'); }
        function closeSettings() { settingsModal.classList.remove('active'); }

        // --- 4. Core Logic (Canvas & TTS) - Ringkasan ---
        const canvas = document.getElementById('videoCanvas');
        const ctx = canvas.getContext('2d');
        const synth = window.speechSynthesis;
        let voices = [];

        // UI Elements
        const voiceSelect = document.getElementById('voiceSelect');
        const pitchInput = document.getElementById('pitch');
        const rateInput = document.getElementById('rate');
        const mainTextInput = document.getElementById('mainText');
        const subTextInput = document.getElementById('subText');
        const colorInput = document.getElementById('colorMain');
        const styleGrid = document.getElementById('styleGrid');

        let state = {
            text: mainTextInput.value,
            subText: subTextInput.value,
            color: colorInput.value,
            style: 'neon',
            isPlaying: false,
            isRecording: false,
            startTime: 0,
            duration: 8000
        };

        // Populate Voices
        function populateVoices() {
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
        populateVoices();
        speechSynthesis.onvoiceschanged = populateVoices;

        function speak(text) {
            if (synth.speaking) synth.cancel();
            if (text !== '') {
                const u = new SpeechSynthesisUtterance(text);
                u.voice = voices.find(v => v.name === voiceSelect.value);
                u.pitch = pitchInput.value;
                u.rate = rateInput.value;
                synth.speak(u);
            }
        }

        // Input Handlers
        [mainTextInput, subTextInput, colorInput].forEach(el => {
            el.addEventListener('input', () => {
                state.text = mainTextInput.value;
                state.subText = subTextInput.value;
                state.color = colorInput.value;
                if (!state.isPlaying) renderFrame(0);
            });
        });

        styleGrid.addEventListener('click', (e) => {
            if(e.target.classList.contains('style-card')) {
                document.querySelectorAll('.style-card').forEach(c => c.classList.remove('active'));
                e.target.classList.add('active');
                state.style = e.target.dataset.style;
                if (!state.isPlaying) renderFrame(0);
            }
        });

        // Animation Loop (Simplified for brevity)
        function loop(timestamp) {
            if (!state.startTime) state.startTime = timestamp;
            const elapsed = timestamp - state.startTime;
            const time = elapsed % (state.duration + 2000);
            renderFrame(time);
            if (state.isPlaying || state.isRecording) requestAnimationFrame(loop);
            else if (elapsed > state.duration + 2000) stopPreview();
        }

        function stopPreview() {
            state.isPlaying = false;
            state.isRecording = false;
            cancelAnimationFrame(state.animationFrame);
            synth.cancel();
        }

        function renderFrame(timeMs) {
            ctx.clearRect(0,0, canvas.width, canvas.height);
            // Background Logic (Minimal example)
            ctx.fillStyle = state.style === 'neon' ? '#111' : '#222';
            ctx.fillRect(0,0,canvas.width, canvas.height);
            // Text Logic
            ctx.textAlign = 'center';
            ctx.textBaseline = 'middle';
            ctx.fillStyle = state.color;
            ctx.font = `bold 80px sans-serif`;
            ctx.fillText(state.text.toUpperCase(), canvas.width/2, canvas.height/2);
            ctx.font = `40px sans-serif`;
            ctx.fillStyle = '#ccc';
            ctx.fillText(state.subText, canvas.width/2, canvas.height/2 + 100);
        }

        // --- Preview & Export with Trial Check ---
        document.getElementById('btnPreview').addEventListener('click', () => {
            if(state.isPlaying) stopPreview();
            state.isPlaying = true;
            state.startTime = 0;
            speak(state.subText);
            loop();
        });

        document.getElementById('btnExport').addEventListener('click', () => {
            // Cek Limit Trial
            if (!checkTrialLimit()) return;

            if(state.isPlaying) stopPreview();
            
            // Logic Render sederhana (Simulasi)
            state.isRecording = true;
            state.isPlaying = true;
            speak(state.subText);
            loop();

            setTimeout(() => {
                stopPreview();
                incrementTrial(); // Tambah hitungan trial
                alert("Video Selesai diunduh! (Simulasi)");
            }, 3000);
        });

        // Footer Tahun
        document.getElementById('currentYear').textContent = new Date().getFullYear();

    </script>
</body>
</html>
