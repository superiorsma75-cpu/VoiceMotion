<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AETHER | Professional AI Video Studio</title>
    <link rel="stylesheet" href="style.css">
    <link href="https://cdn.jsdelivr.net/npm/remixicon@3.5.0/fonts/remixicon.css" rel="stylesheet">
</head>
<body>

    <div class="app-wrapper">
        <aside class="sidebar">
            <div class="logo">
                <i class="ri-movie-2-ai-line"></i> <span>AETHER</span>
            </div>
            <ul class="nav-menu">
                <li class="active"><a href="#"><i class="ri-dashboard-line"></i> Studio</a></li>
                <li><a href="#"><i class="ri-gallery-line"></i> Gallery</a></li>
                <li><a href="#"><i class="ri-settings-4-line"></i> Settings</a></li>
                <li><a href="#"><i class="ri-vip-crown-line"></i> Upgrade Pro</a></li>
            </ul>
            <div class="user-profile">
                <img src="https://ui-avatars.com/api/?name=Admin+User&background=6366f1&color=fff" alt="User">
                <div class="user-info">
                    <h4>Creator Mode</h4>
                    <p>Free Tier</p>
                </div>
            </div>
        </aside>

        <main class="main-content">
            
            <header class="top-bar">
                <div class="breadcrumbs">
                    <span>Studio</span> <i class="ri-arrow-right-s-line"></i> <span class="current">Text to Video</span>
                </div>
                <div class="credits">
                    <i class="ri-coins-line"></i> <span>120 Credits Left</span>
                </div>
            </header>

            <div class="studio-grid">
                
                <div class="panel controls-panel">
                    <h3><i class="ri-magic-line"></i> Prompt Engineering</h3>
                    
                    <div class="form-group">
                        <label>Deskripsi Video</label>
                        <textarea id="promptInput" placeholder="Deskripsikan imajinasi Anda sedetail mungkin... (Contoh: Cyberpunk city, neon lights, rainy street, 8k render)"></textarea>
                    </div>

                    <div class="form-group">
                        <label>Negative Prompt (Opsional)</label>
                        <input type="text" id="negativePrompt" placeholder="Apa yang TIDAK ingin Anda lihat? (Contoh: blur, distorted, low quality)">
                    </div>

                    <div class="settings-grid">
                        <div class="setting-item">
                            <label>Rasio Aspek</label>
                            <div class="aspect-selector">
                                <button class="aspect-btn active" data-ratio="16:9">16:9</button>
                                <button class="aspect-btn" data-ratio="9:16">9:16</button>
                                <button class="aspect-btn" data-ratio="1:1">1:1</button>
                            </div>
                        </div>
                        <div class="setting-item">
                            <label>Model Style</label>
                            <select id="styleSelect">
                                <option value="realistic">Hyper Realistic</option>
                                <option value="anime">Japanese Anime</option>
                                <option value="3d">Pixar Style 3D</option>
                                <option value="cyberpunk">Cyberpunk</option>
                            </select>
                        </div>
                    </div>

                    <button id="generateBtn" onclick="startGeneration()">
                        <span>Generate Video</span>
                        <div class="btn-glow"></div>
                    </button>
                </div>

                <div class="panel preview-panel">
                    
                    <div id="placeholderState" class="state-view active">
                        <div class="empty-state">
                            <i class="ri-film-line"></i>
                            <h3>Siap untuk Berkreasi?</h3>
                            <p>Masukkan prompt di panel kiri untuk memulai rendering AI.</p>
                        </div>
                    </div>

                    <div id="processingState" class="state-view">
                        <div class="terminal-loader">
                            <div class="spinner-ring"></div>
                            <div class="terminal-log" id="terminalLog">
                                <p>> Initializing GPU cluster...</p>
                            </div>
                            <div class="progress-container">
                                <div class="progress-bar" id="progressBar"></div>
                            </div>
                        </div>
                    </div>

                    <div id="resultState" class="state-view">
                        <div class="video-container">
                            <video id="outputVideo" controls loop playsinline></video>
                            <div class="video-overlay">
                                <span class="badge">HD 1080p</span>
                            </div>
                        </div>
                        <div class="action-bar">
                            <button class="btn-icon" onclick="downloadVideo()"><i class="ri-download-cloud-2-line"></i> Download</button>
                            <button class="btn-icon"><i class="ri-share-forward-line"></i> Share</button>
                        </div>
                    </div>

                </div>
            </div>

            <section class="history-section">
                <h3>Riwayat Generasi</h3>
                <div class="history-grid" id="historyGrid">
                    </div>
            </section>

        </main>
    </div>

    <div id="toast-container"></div>

    <script src="script.js"></script>
</body>
</html>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');

:root {
    --bg-dark: #09090b;
    --panel-bg: #18181b;
    --border-color: #27272a;
    --primary: #6366f1;
    --primary-glow: rgba(99, 102, 241, 0.4);
    --text-main: #fafafa;
    --text-muted: #a1a1aa;
    --success: #10b981;
}

* { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Inter', sans-serif; }

body {
    background-color: var(--bg-dark);
    color: var(--text-main);
    overflow: hidden; /* App style */
}

/* Layout */
.app-wrapper {
    display: flex;
    height: 100vh;
}

/* Sidebar */
.sidebar {
    width: 260px;
    background: var(--panel-bg);
    border-right: 1px solid var(--border-color);
    padding: 1.5rem;
    display: flex;
    flex-direction: column;
}

.logo {
    font-size: 1.5rem;
    font-weight: 700;
    margin-bottom: 3rem;
    color: var(--text-main);
    display: flex;
    align-items: center;
    gap: 10px;
}

.logo i { color: var(--primary); }

.nav-menu { list-style: none; flex: 1; }
.nav-menu li { margin-bottom: 0.5rem; }

.nav-menu a {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 12px 16px;
    color: var(--text-muted);
    text-decoration: none;
    border-radius: 8px;
    transition: 0.2s;
    font-weight: 500;
}

.nav-menu li.active a, .nav-menu a:hover {
    background: rgba(255, 255, 255, 0.05);
    color: var(--text-main);
}

.user-profile {
    display: flex;
    align-items: center;
    gap: 12px;
    padding-top: 1rem;
    border-top: 1px solid var(--border-color);
}

.user-profile img { width: 40px; border-radius: 50%; }
.user-info h4 { font-size: 0.9rem; }
.user-info p { font-size: 0.8rem; color: var(--text-muted); }

/* Main Content */
.main-content {
    flex: 1;
    padding: 2rem;
    overflow-y: auto;
    position: relative;
}

/* Header */
.top-bar {
    display: flex;
    justify-content: space-between;
    margin-bottom: 2rem;
}

.breadcrumbs { color: var(--text-muted); font-size: 0.9rem; }
.current { color: var(--text-main); font-weight: 500; }
.credits { 
    background: rgba(99, 102, 241, 0.1); 
    color: var(--primary); 
    padding: 6px 12px; 
    border-radius: 20px; 
    font-size: 0.85rem; 
    font-weight: 600;
}

/* Studio Grid */
.studio-grid {
    display: grid;
    grid-template-columns: 350px 1fr;
    gap: 1.5rem;
    height: calc(100vh - 250px);
}

.panel {
    background: #131316;
    border: 1px solid var(--border-color);
    border-radius: 16px;
    padding: 1.5rem;
    display: flex;
    flex-direction: column;
}

/* Left Controls */
.controls-panel h3 { margin-bottom: 1.5rem; font-size: 1.1rem; display: flex; gap: 8px; }

.form-group { margin-bottom: 1.2rem; }
.form-group label { display: block; font-size: 0.85rem; margin-bottom: 0.5rem; color: var(--text-muted); }

textarea, input[type="text"], select {
    width: 100%;
    background: #09090b;
    border: 1px solid var(--border-color);
    color: #fff;
    padding: 12px;
    border-radius: 8px;
    font-size: 0.9rem;
    outline: none;
    transition: 0.2s;
}

textarea { height: 120px; resize: none; }
textarea:focus, input:focus, select:focus { border-color: var(--primary); }

.settings-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 1.5rem; }

.aspect-selector { display: flex; gap: 5px; background: #09090b; padding: 4px; border-radius: 8px; border: 1px solid var(--border-color); }
.aspect-btn {
    flex: 1;
    background: transparent;
    border: none;
    color: var(--text-muted);
    padding: 6px;
    border-radius: 6px;
    cursor: pointer;
    font-size: 0.8rem;
}
.aspect-btn.active { background: #27272a; color: white; }

#generateBtn {
    margin-top: auto;
    width: 100%;
    padding: 14px;
    background: var(--primary);
    color: white;
    border: none;
    border-radius: 10px;
    font-weight: 600;
    cursor: pointer;
    position: relative;
    overflow: hidden;
    transition: 0.3s;
}

#generateBtn:hover { transform: translateY(-2px); box-shadow: 0 5px 20px var(--primary-glow); }

/* Right Preview Panel */
.preview-panel {
    position: relative;
    justify-content: center;
    align-items: center;
    background: radial-gradient(circle at center, #1c1c21 0%, #131316 100%);
}

.state-view { display: none; width: 100%; height: 100%; flex-direction: column; justify-content: center; align-items: center; }
.state-view.active { display: flex; }

/* Empty State */
.empty-state { text-align: center; color: var(--text-muted); }
.empty-state i { font-size: 3rem; margin-bottom: 1rem; opacity: 0.5; }

/* Loading State (Terminal) */
.terminal-loader { width: 100%; max-width: 400px; }
.spinner-ring {
    width: 40px; height: 40px; border: 3px solid var(--border-color);
    border-top: 3px solid var(--primary); border-radius: 50%;
    animation: spin 1s linear infinite; margin: 0 auto 1.5rem auto;
}
.terminal-log {
    background: #000; font-family: 'Courier New', monospace;
    font-size: 0.85rem; color: var(--success); padding: 1rem;
    border-radius: 8px; border: 1px solid var(--border-color);
    height: 100px; overflow: hidden; margin-bottom: 1rem; opacity: 0.8;
}
.progress-container { width: 100%; height: 4px; background: #27272a; border-radius: 2px; }
.progress-bar { height: 100%; background: var(--primary); width: 0%; transition: width 0.2s; }

/* Result State */
.video-container { width: 100%; height: 85%; position: relative; border-radius: 12px; overflow: hidden; box-shadow: 0 10px 30px rgba(0,0,0,0.5); }
video { width: 100%; height: 100%; object-fit: cover; }
.action-bar { margin-top: 1rem; display: flex; gap: 1rem; }
.btn-icon { background: #27272a; color: white; border: none; padding: 10px 20px; border-radius: 8px; cursor: pointer; display: flex; gap: 8px; align-items: center; transition: 0.2s; }
.btn-icon:hover { background: #3f3f46; }

/* History Bottom */
.history-section { margin-top: 2rem; }
.history-section h3 { font-size: 1rem; margin-bottom: 1rem; color: var(--text-muted); }
.history-grid { display: flex; gap: 1rem; overflow-x: auto; padding-bottom: 10px; }
.history-item { min-width: 150px; height: 90px; border-radius: 8px; overflow: hidden; position: relative; cursor: pointer; border: 2px solid transparent; }
.history-item:hover { border-color: var(--primary); }
.history-item img { width: 100%; height: 100%; object-fit: cover; }

/* Toast */
#toast-container { position: fixed; bottom: 20px; right: 20px; z-index: 1000; }
.toast { background: #27272a; color: white; padding: 12px 24px; border-radius: 8px; margin-top: 10px; border-left: 4px solid var(--primary); animation: slideIn 0.3s ease; box-shadow: 0 5px 15px rgba(0,0,0,0.3); }

@keyframes spin { to { transform: rotate(360deg); } }
@keyframes slideIn { from { transform: translateX(100%); } to { transform: translateX(0); } }

/* Responsive */
@media (max-width: 1024px) {
    .app-wrapper { flex-direction: column; height: auto; }
    .sidebar { width: 100%; height: auto; flex-direction: row; justify-content: space-between; align-items: center; padding: 1rem; }
    .nav-menu, .user-profile { display: none; }
    .studio-grid { grid-template-columns: 1fr; height: auto; }
    .main-content { overflow: visible; }
}
// Konfigurasi DOM
const generateBtn = document.getElementById('generateBtn');
const promptInput = document.getElementById('promptInput');
const aspectBtns = document.querySelectorAll('.aspect-btn');
const terminalLog = document.getElementById('terminalLog');
const progressBar = document.getElementById('progressBar');
const outputVideo = document.getElementById('outputVideo');
const historyGrid = document.getElementById('historyGrid');

// Database Sample Video (Simulasi Hasil Berbeda)
const sampleVideos = [
    "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ElephantsDream.mp4",
    "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerBlazes.mp4",
    "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/TearsOfSteel.mp4"
];

// Database Log Messages (Simulasi Terminal)
const logMessages = [
    "Connecting to neural engine...",
    "Tokenizing text prompt...",
    "Generating latent noise...",
    "Denoising step 10/50...",
    "Denoising step 35/50...",
    "Upscaling to 1080p...",
    "Applying post-processing filters...",
    "Rendering final frames..."
];

// Handle Aspect Ratio Selection
aspectBtns.forEach(btn => {
    btn.addEventListener('click', () => {
        document.querySelector('.aspect-btn.active').classList.remove('active');
        btn.classList.add('active');
    });
});

function startGeneration() {
    const text = promptInput.value.trim();

    if (!text) {
        showToast("Error: Masukkan prompt terlebih dahulu!", "error");
        promptInput.focus();
        return;
    }

    // Switch to Loading View
    switchState('processing');
    generateBtn.disabled = true;
    generateBtn.innerHTML = `<i class="ri-loader-4-line"></i> Generating...`;

    // Reset Logs
    terminalLog.innerHTML = `<p>> Job started...</p>`;
    progressBar.style.width = "0%";

    // Jalankan Simulasi
    runSimulation();
}

function runSimulation() {
    let progress = 0;
    let logIndex = 0;

    const interval = setInterval(() => {
        progress += Math.floor(Math.random() * 5) + 2; // Random increment
        
        if (progress > 100) progress = 100;
        progressBar.style.width = `${progress}%`;

        // Tambahkan Log secara bertahap
        if (progress > (logIndex + 1) * 12 && logIndex < logMessages.length) {
            const p = document.createElement('p');
            p.innerText = `> ${logMessages[logIndex]}`;
            terminalLog.appendChild(p);
            terminalLog.scrollTop = terminalLog.scrollHeight; // Auto scroll ke bawah
            logIndex++;
        }

        if (progress === 100) {
            clearInterval(interval);
            finishGeneration();
        }
    }, 150);
}

function finishGeneration() {
    setTimeout(() => {
        switchState('result');
        
        // Pick Random Video
        const randomVid = sampleVideos[Math.floor(Math.random() * sampleVideos.length)];
        outputVideo.src = randomVid;
        outputVideo.play();

        // Reset Button
        generateBtn.disabled = false;
        generateBtn.innerHTML = `<span>Generate Video</span><div class="btn-glow"></div>`;
        
        showToast("Success: Video berhasil dibuat!", "success");
        addToHistory(randomVid);

    }, 1000);
}

function addToHistory(url) {
    // Membuat elemen history item
    const div = document.createElement('div');
    div.className = 'history-item';
    // Karena ini video, kita pakai thumbnail statis placeholder atau video kecil
    div.innerHTML = `<video src="${url}" muted onmouseover="this.play()" onmouseout="this.pause();this.currentTime=0;"></video>`;
    
    // Klik history untuk memuat ulang ke player utama
    div.onclick = () => {
        outputVideo.src = url;
        outputVideo.play();
        switchState('result');
    };

    historyGrid.prepend(div);
}

function downloadVideo() {
    showToast("Memulai unduhan...", "success");
    // Logika unduh fiktif
}

// Helper: Switch View States
function switchState(stateName) {
    document.querySelectorAll('.state-view').forEach(el => el.classList.remove('active'));
    
    if (stateName === 'processing') document.getElementById('processingState').classList.add('active');
    else if (stateName === 'result') document.getElementById('resultState').classList.add('active');
    else document.getElementById('placeholderState').classList.add('active');
}

// Helper: Custom Toast Notification
function showToast(message, type) {
    const container = document.getElementById('toast-container');
    const toast = document.createElement('div');
    toast.className = 'toast';
    toast.innerText = message;
    
    if (type === 'error') toast.style.borderLeftColor = '#ef4444';
    
    container.appendChild(toast);

    setTimeout(() => {
        toast.remove();
    }, 3000);
}
