<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Vision - Text to Video</title>
    <link rel="stylesheet" href="style.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
</head>
<body>

    <nav class="navbar">
        <div class="logo">
            <i class="fa-solid fa-robot"></i> AI Vision
        </div>
        <ul class="nav-links">
            <li><a href="#">Beranda</a></li>
            <li><a href="#">Fitur</a></li>
            <li><a href="#">Harga</a></li>
            <li><a href="#" class="btn-login">Masuk</a></li>
        </ul>
    </nav>

    <header class="hero">
        <h1>Ubah Imajinasi Menjadi <span class="gradient-text">Video Realistis</span></h1>
        <p>Ketik deskripsi teks apa saja, dan AI kami akan merendernya menjadi video dalam hitungan detik.</p>
    </header>

    <main class="app-container">
        
        <section class="input-section">
            <div class="input-group">
                <label for="prompt">Deskripsi Video (Prompt)</label>
                <textarea id="prompt" placeholder="Contoh: Seekor kucing astronot sedang berjalan di permukaan bulan dengan latar belakang bumi..."></textarea>
            </div>

            <div class="options-group">
                <div class="select-box">
                    <label>Gaya Visual</label>
                    <select id="style-select">
                        <option value="realistic">Realistis</option>
                        <option value="anime">Anime / Kartun</option>
                        <option value="cinematic">Sinematik 4K</option>
                        <option value="3d">3D Render</option>
                    </select>
                </div>
                <div class="select-box">
                    <label>Durasi</label>
                    <select id="duration-select">
                        <option value="5">5 Detik</option>
                        <option value="10">10 Detik</option>
                    </select>
                </div>
            </div>

            <button id="generate-btn" onclick="generateVideo()">
                <i class="fa-solid fa-wand-magic-sparkles"></i> Buat Video Sekarang
            </button>
        </section>

        <section class="output-section" id="output-area">
            
            <div id="placeholder-view" class="view-state active">
                <i class="fa-solid fa-film"></i>
                <p>Video hasil akan muncul di sini</p>
            </div>

            <div id="loading-view" class="view-state">
                <div class="loader"></div>
                <p id="loading-text">Sedang memproses AI...</p>
                <div class="progress-bar">
                    <div class="progress-fill" id="progress-fill"></div>
                </div>
            </div>

            <div id="result-view" class="view-state">
                <div class="video-wrapper">
                    <video id="final-video" controls loop>
                        <source src="https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4" type="video/mp4">
                        Browser Anda tidak mendukung video tag.
                    </video>
                </div>
                <div class="action-buttons">
                    <button class="btn-secondary" onclick="resetApp()">Buat Lagi</button>
                    <button class="btn-primary">Unduh HD <i class="fa-solid fa-download"></i></button>
                </div>
            </div>

        </section>
    </main>

    <section class="features">
        <div class="feature-card">
            <i class="fa-solid fa-bolt"></i>
            <h3>Cepat</h3>
            <p>Rendering dalam hitungan detik.</p>
        </div>
        <div class="feature-card">
            <i class="fa-solid fa-image"></i>
            <h3>Kualitas Tinggi</h3>
            <p>Mendukung hingga resolusi 4K.</p>
        </div>
        <div class="feature-card">
            <i class="fa-solid fa-lock"></i>
            <h3>Aman</h3>
            <p>Data prompt Anda terenkripsi.</p>
        </div>
    </section>

    <footer>
        <p>&copy; 2024 AI Vision Generator. Dibuat dengan Kode HTML/CSS/JS.</p>
    </footer>

    <script src="script.js"></script>
</body>
</html>
/* Reset & Variabel */
:root {
    --bg-color: #0f0f12;
    --card-bg: #1a1a20;
    --primary: #6c5ce7;
    --primary-hover: #5649c0;
    --text-main: #ffffff;
    --text-muted: #a0a0a0;
    --border: #2d2d35;
    --gradient: linear-gradient(45deg, #6c5ce7, #a29bfe);
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

body {
    background-color: var(--bg-color);
    color: var(--text-main);
    display: flex;
    flex-direction: column;
    min-height: 100vh;
}

/* Navbar */
.navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1.5rem 5%;
    border-bottom: 1px solid var(--border);
}

.logo {
    font-size: 1.5rem;
    font-weight: bold;
    color: var(--primary);
}

.nav-links {
    list-style: none;
    display: flex;
    gap: 20px;
}

.nav-links a {
    text-decoration: none;
    color: var(--text-muted);
    transition: 0.3s;
}

.nav-links a:hover {
    color: var(--text-main);
}

.btn-login {
    background: var(--card-bg);
    padding: 8px 20px;
    border-radius: 5px;
    border: 1px solid var(--border);
}

/* Hero Section */
.hero {
    text-align: center;
    padding: 3rem 1rem;
}

.hero h1 {
    font-size: 2.5rem;
    margin-bottom: 1rem;
}

.gradient-text {
    background: var(--gradient);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
}

.hero p {
    color: var(--text-muted);
}

/* App Container */
.app-container {
    display: flex;
    flex-wrap: wrap;
    gap: 2rem;
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem;
    width: 100%;
}

/* Input Section */
.input-section {
    flex: 1;
    background: var(--card-bg);
    padding: 2rem;
    border-radius: 15px;
    border: 1px solid var(--border);
    min-width: 300px;
}

.input-group label, .select-box label {
    display: block;
    margin-bottom: 0.5rem;
    color: var(--text-muted);
    font-size: 0.9rem;
}

textarea {
    width: 100%;
    height: 150px;
    background: #0f0f12;
    border: 1px solid var(--border);
    border-radius: 10px;
    color: white;
    padding: 1rem;
    resize: none;
    font-size: 1rem;
}

textarea:focus {
    outline: 2px solid var(--primary);
    border-color: transparent;
}

.options-group {
    display: flex;
    gap: 1rem;
    margin-top: 1rem;
}

.select-box {
    flex: 1;
}

select {
    width: 100%;
    padding: 10px;
    background: #0f0f12;
    border: 1px solid var(--border);
    border-radius: 8px;
    color: white;
}

#generate-btn {
    width: 100%;
    margin-top: 2rem;
    padding: 15px;
    background: var(--gradient);
    border: none;
    border-radius: 10px;
    color: white;
    font-size: 1.1rem;
    font-weight: bold;
    cursor: pointer;
    transition: transform 0.2s;
}

#generate-btn:hover {
    transform: scale(1.02);
    opacity: 0.9;
}

/* Output Section */
.output-section {
    flex: 1;
    background: var(--card-bg);
    border-radius: 15px;
    border: 1px solid var(--border);
    min-width: 300px;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 400px;
    position: relative;
    overflow: hidden;
}

.view-state {
    display: none; /* Sembunyikan semua state secara default */
    text-align: center;
    width: 100%;
    padding: 1rem;
}

.view-state.active {
    display: block;
}

#placeholder-view i {
    font-size: 4rem;
    color: var(--border);
    margin-bottom: 1rem;
}

/* Loader Animation */
.loader {
    border: 4px solid var(--border);
    border-top: 4px solid var(--primary);
    border-radius: 50%;
    width: 50px;
    height: 50px;
    animation: spin 1s linear infinite;
    margin: 0 auto 1rem auto;
}

@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}

.progress-bar {
    width: 80%;
    height: 6px;
    background: var(--border);
    border-radius: 3px;
    margin: 10px auto;
    overflow: hidden;
}

.progress-fill {
    height: 100%;
    width: 0%;
    background: var(--primary);
    transition: width 0.3s ease;
}

/* Result Video */
.video-wrapper video {
    width: 100%;
    border-radius: 10px;
    box-shadow: 0 4px 20px rgba(0,0,0,0.5);
}

.action-buttons {
    margin-top: 1.5rem;
    display: flex;
    gap: 1rem;
    justify-content: center;
}

.btn-secondary, .btn-primary {
    padding: 10px 20px;
    border-radius: 8px;
    cursor: pointer;
    font-weight: bold;
}

.btn-secondary {
    background: transparent;
    border: 1px solid var(--border);
    color: var(--text-main);
}

.btn-primary {
    background: var(--primary);
    border: none;
    color: white;
}

/* Features & Footer */
.features {
    display: flex;
    justify-content: center;
    gap: 2rem;
    padding: 4rem 2rem;
    flex-wrap: wrap;
}

.feature-card {
    background: var(--card-bg);
    padding: 2rem;
    border-radius: 10px;
    text-align: center;
    width: 250px;
    border: 1px solid var(--border);
}

.feature-card i {
    font-size: 2rem;
    color: var(--primary);
    margin-bottom: 1rem;
}

footer {
    text-align: center;
    padding: 2rem;
    border-top: 1px solid var(--border);
    margin-top: auto;
    color: var(--text-muted);
}

/* Responsiveness */
@media (max-width: 768px) {
    .app-container {
        flex-direction: column;
    }
}
// Mengambil elemen dari DOM
const generateBtn = document.getElementById('generate-btn');
const promptInput = document.getElementById('prompt');
const outputArea = document.getElementById('output-area');

// View States
const placeholderView = document.getElementById('placeholder-view');
const loadingView = document.getElementById('loading-view');
const resultView = document.getElementById('result-view');

// Loading Elements
const progressFill = document.getElementById('progress-fill');
const loadingText = document.getElementById('loading-text');

function generateVideo() {
    const text = promptInput.value.trim();

    // Validasi Input
    if (text === "") {
        alert("Silakan masukkan deskripsi video terlebih dahulu!");
        return;
    }

    // 1. Ubah tampilan ke Loading
    switchView('loading');
    generateBtn.disabled = true;
    generateBtn.innerText = "Sedang Memproses...";

    // 2. Simulasi Proses Loading (Timer 3-5 detik)
    let progress = 0;
    const interval = setInterval(() => {
        progress += Math.floor(Math.random() * 10) + 5;
        
        if (progress > 100) progress = 100;
        
        // Update Progress Bar
        progressFill.style.width = `${progress}%`;
        
        // Update Teks Loading agar terlihat hidup
        if (progress < 30) loadingText.innerText = "Menganalisis prompt teks...";
        else if (progress < 70) loadingText.innerText = "Merender frame video...";
        else loadingText.innerText = "Menyelesaikan detail akhir...";

        // Jika selesai
        if (progress === 100) {
            clearInterval(interval);
            setTimeout(() => {
                // 3. Tampilkan Hasil
                switchView('result');
                generateBtn.disabled = false;
                generateBtn.innerHTML = '<i class="fa-solid fa-wand-magic-sparkles"></i> Buat Video Sekarang';
                
                // Mulai putar video otomatis (karena ini sample)
                const video = document.getElementById('final-video');
                video.play();
            }, 800); // Sedikit delay setelah 100%
        }
    }, 300); // Update setiap 300ms
}

function resetApp() {
    promptInput.value = "";
    switchView('placeholder');
}

// Fungsi Helper untuk mengganti tampilan (Placeholder -> Loading -> Result)
function switchView(viewName) {
    // Sembunyikan semua
    placeholderView.classList.remove('active');
    loadingView.classList.remove('active');
    resultView.classList.remove('active');

    // Tampilkan yang diminta
    if (viewName === 'placeholder') {
        placeholderView.classList.add('active');
    } else if (viewName === 'loading') {
        loadingView.classList.add('active');
        // Reset progress bar
        progressFill.style.width = '0%';
    } else if (viewName === 'result') {
        resultView.classList.add('active');
    }
}
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<title>AI Video Player</title>
<style>
body {
  background: #0f172a;
  color: white;
  font-family: Arial, sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.container {
  width: 700px;
  text-align: center;
}

canvas {
  background: black;
  margin-top: 15px;
  border-radius: 10px;
}

.subtitle {
  margin-top: 10px;
  font-size: 18px;
  color: #00ffcc;
}
</style>
</head>
<body>

<div class="container">
  <h1>🤖 AI Generated Video</h1>
  <canvas id="canvas" width="640" height="360"></canvas>
  <div class="subtitle" id="subtitle"></div>
</div>

<script>
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");
const subtitle = document.getElementById("subtitle");

const text =
"Selamat datang. Ini adalah contoh video AI yang dibuat menggunakan HTML, JavaScript, dan suara otomatis.";

let x = canvas.width;
let frame = 0;

// AI VOICE
function speakAI(text){
  const u = new SpeechSynthesisUtterance(text);
  u.lang = "id-ID";
  u.rate = 0.95;
  u.pitch = 1;
  speechSynthesis.speak(u);
}

// VIDEO ANIMATION
function playVideo(){
  subtitle.innerText = text;

  const anim = setInterval(() => {
    ctx.fillStyle = "black";
    ctx.fillRect(0,0,canvas.width,canvas.height);

    ctx.fillStyle = "white";
    ctx.font = "32px Arial";
    ctx.textAlign = "center";
    ctx.fillText("AI VIDEO DEMO", canvas.width/2, 80);

    ctx.font = "24px Arial";
    ctx.fillText(text, x, canvas.height/2);

    x -= 2;
    frame++;

    if(frame > 300){
      clearInterval(anim);
    }
  }, 33);
}

// AUTO PLAY
setTimeout(() => {
  speakAI(text);
  playVideo();
}, 500);
</script>

</body>
</html>
/* Reset & Variabel */
:root {
    --bg-color: #0f0f12;
    --card-bg: #1a1a20;
    --primary: #6c5ce7;
    --primary-hover: #5649c0;
    --text-main: #ffffff;
    --text-muted: #a0a0a0;
    --border: #2d2d35;
    --gradient: linear-gradient(45deg, #6c5ce7, #a29bfe);
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

body {
    background-color: var(--bg-color);
    color: var(--text-main);
    display: flex;
    flex-direction: column;
    min-height: 100vh;
}

/* Navbar */
.navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1.5rem 5%;
    border-bottom: 1px solid var(--border);
}

.logo {
    font-size: 1.5rem;
    font-weight: bold;
    color: var(--primary);
}

.nav-links {
    list-style: none;
    display: flex;
    gap: 20px;
}

.nav-links a {
    text-decoration: none;
    color: var(--text-muted);
    transition: 0.3s;
}

.nav-links a:hover {
    color: var(--text-main);
}

.btn-login {
    background: var(--card-bg);
    padding: 8px 20px;
    border-radius: 5px;
    border: 1px solid var(--border);
}

/* Hero Section */
.hero {
    text-align: center;
    padding: 3rem 1rem;
}

.hero h1 {
    font-size: 2.5rem;
    margin-bottom: 1rem;
}

.gradient-text {
    background: var(--gradient);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
}

.hero p {
    color: var(--text-muted);
}

/* App Container */
.app-container {
    display: flex;
    flex-wrap: wrap;
    gap: 2rem;
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem;
    width: 100%;
}

/* Input Section */
.input-section {
    flex: 1;
    background: var(--card-bg);
    padding: 2rem;
    border-radius: 15px;
    border: 1px solid var(--border);
    min-width: 300px;
}

.input-group label, .select-box label {
    display: block;
    margin-bottom: 0.5rem;
    color: var(--text-muted);
    font-size: 0.9rem;
}

textarea {
    width: 100%;
    height: 150px;
    background: #0f0f12;
    border: 1px solid var(--border);
    border-radius: 10px;
    color: white;
    padding: 1rem;
    resize: none;
    font-size: 1rem;
}

textarea:focus {
    outline: 2px solid var(--primary);
    border-color: transparent;
}

.options-group {
    display: flex;
    gap: 1rem;
    margin-top: 1rem;
}

.select-box {
    flex: 1;
}

select {
    width: 100%;
    padding: 10px;
    background: #0f0f12;
    border: 1px solid var(--border);
    border-radius: 8px;
    color: white;
}

#generate-btn {
    width: 100%;
    margin-top: 2rem;
    padding: 15px;
    background: var(--gradient);
    border: none;
    border-radius: 10px;
    color: white;
    font-size: 1.1rem;
    font-weight: bold;
    cursor: pointer;
    transition: transform 0.2s;
}

#generate-btn:hover {
    transform: scale(1.02);
    opacity: 0.9;
}

/* Output Section */
.output-section {
    flex: 1;
    background: var(--card-bg);
    border-radius: 15px;
    border: 1px solid var(--border);
    min-width: 300px;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 400px;
    position: relative;
    overflow: hidden;
}

.view-state {
    display: none; /* Sembunyikan semua state secara default */
    text-align: center;
    width: 100%;
    padding: 1rem;
}

.view-state.active {
    display: block;
}

#placeholder-view i {
    font-size: 4rem;
    color: var(--border);
    margin-bottom: 1rem;
}

/* Loader Animation */
.loader {
    border: 4px solid var(--border);
    border-top: 4px solid var(--primary);
    border-radius: 50%;
    width: 50px;
    height: 50px;
    animation: spin 1s linear infinite;
    margin: 0 auto 1rem auto;
}

@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}

.progress-bar {
    width: 80%;
    height: 6px;
    background: var(--border);
    border-radius: 3px;
    margin: 10px auto;
    overflow: hidden;
}

.progress-fill {
    height: 100%;
    width: 0%;
    background: var(--primary);
    transition: width 0.3s ease;
}

/* Result Video */
.video-wrapper video {
    width: 100%;
    border-radius: 10px;
    box-shadow: 0 4px 20px rgba(0,0,0,0.5);
}

.action-buttons {
    margin-top: 1.5rem;
    display: flex;
    gap: 1rem;
    justify-content: center;
}

.btn-secondary, .btn-primary {
    padding: 10px 20px;
    border-radius: 8px;
    cursor: pointer;
    font-weight: bold;
}

.btn-secondary {
    background: transparent;
    border: 1px solid var(--border);
    color: var(--text-main);
}

.btn-primary {
    background: var(--primary);
    border: none;
    color: white;
}

/* Features & Footer */
.features {
    display: flex;
    justify-content: center;
    gap: 2rem;
    padding: 4rem 2rem;
    flex-wrap: wrap;
}

.feature-card {
    background: var(--card-bg);
    padding: 2rem;
    border-radius: 10px;
    text-align: center;
    width: 250px;
    border: 1px solid var(--border);
}

.feature-card i {
    font-size: 2rem;
    color: var(--primary);
    margin-bottom: 1rem;
}

footer {
    text-align: center;
    padding: 2rem;
    border-top: 1px solid var(--border);
    margin-top: auto;
    color: var(--text-muted);
}

/* Responsiveness */
@media (max-width: 768px) {
    .app-container {
        flex-direction: column;
    }
}
// Mengambil elemen dari DOM
const generateBtn = document.getElementById('generate-btn');
const promptInput = document.getElementById('prompt');
const outputArea = document.getElementById('output-area');

// View States
const placeholderView = document.getElementById('placeholder-view');
const loadingView = document.getElementById('loading-view');
const resultView = document.getElementById('result-view');

// Loading Elements
const progressFill = document.getElementById('progress-fill');
const loadingText = document.getElementById('loading-text');

function generateVideo() {
    const text = promptInput.value.trim();

    // Validasi Input
    if (text === "") {
        alert("Silakan masukkan deskripsi video terlebih dahulu!");
        return;
    }

    // 1. Ubah tampilan ke Loading
    switchView('loading');
    generateBtn.disabled = true;
    generateBtn.innerText = "Sedang Memproses...";

    // 2. Simulasi Proses Loading (Timer 3-5 detik)
    let progress = 0;
    const interval = setInterval(() => {
        progress += Math.floor(Math.random() * 10) + 5;
        
        if (progress > 100) progress = 100;
        
        // Update Progress Bar
        progressFill.style.width = `${progress}%`;
        
        // Update Teks Loading agar terlihat hidup
        if (progress < 30) loadingText.innerText = "Menganalisis prompt teks...";
        else if (progress < 70) loadingText.innerText = "Merender frame video...";
        else loadingText.innerText = "Menyelesaikan detail akhir...";

        // Jika selesai
        if (progress === 100) {
            clearInterval(interval);
            setTimeout(() => {
                // 3. Tampilkan Hasil
                switchView('result');
                generateBtn.disabled = false;
                generateBtn.innerHTML = '<i class="fa-solid fa-wand-magic-sparkles"></i> Buat Video Sekarang';
                
                // Mulai putar video otomatis (karena ini sample)
                const video = document.getElementById('final-video');
                video.play();
            }, 800); // Sedikit delay setelah 100%
        }
    }, 300); // Update setiap 300ms
}

function resetApp() {
    promptInput.value = "";
    switchView('placeholder');
}

// Fungsi Helper untuk mengganti tampilan (Placeholder -> Loading -> Result)
function switchView(viewName) {
    // Sembunyikan semua
    placeholderView.classList.remove('active');
    loadingView.classList.remove('active');
    resultView.classList.remove('active');

    // Tampilkan yang diminta
    if (viewName === 'placeholder') {
        placeholderView.classList.add('active');
    } else if (viewName === 'loading') {
        loadingView.classList.add('active');
        // Reset progress bar
        progressFill.style.width = '0%';
    } else if (viewName === 'result') {
        resultView.classList.add('active');
    }
}
