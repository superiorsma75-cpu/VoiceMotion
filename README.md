text-to-video-pro/
├── index.html
├── style.css
└── script.js
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<title>Text to Video PRO</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<div class="app">
    <h1>🎬 Text to Video PRO</h1>

    <textarea id="textInput" placeholder="Masukkan teks..."></textarea>

    <select id="animation">
        <option value="slide">Slide</option>
        <option value="fade">Fade</option>
        <option value="zoom">Zoom</option>
    </select>

    <select id="resolution">
        <option value="640x360">480p</option>
        <option value="1280x720">720p</option>
    </select>

    <input type="file" id="music" accept="audio/*">

    <button onclick="generate()">🎥 Buat Video</button>

    <canvas id="canvas"></canvas>

    <a id="download" download="video-pro.webm">⬇ Download Video</a>
</div>

<script src="script.js"></script>
</body>
</html>
body {
    background: linear-gradient(135deg,#0f2027,#203a43,#2c5364);
    font-family: Arial;
    color: white;
}

.app {
    max-width: 800px;
    margin: auto;
    padding: 20px;
    text-align: center;
}

textarea, select, input {
    width: 100%;
    margin-bottom: 10px;
    padding: 10px;
}

button {
    background: #00c6ff;
    border: none;
    padding: 12px;
    font-size: 16px;
    cursor: pointer;
}

canvas {
    margin-top: 15px;
    background: black;
}

#download {
    display: none;
    color: #00ffcc;
    font-weight: bold;
}
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");
const download = document.getElementById("download");

function speak(text){
    let u = new SpeechSynthesisUtterance(text);
    u.lang = "id-ID";
    speechSynthesis.speak(u);
}

function generate(){
    const text = textInput.value;
    const anim = animation.value;
    const [w,h] = resolution.value.split("x");

    canvas.width = w;
    canvas.height = h;

    speak(text);

    const stream = canvas.captureStream(30);
    const recorder = new MediaRecorder(stream);
    let chunks = [];

    recorder.ondataavailable = e => chunks.push(e.data);
    recorder.onstop = () => {
        const blob = new Blob(chunks,{type:"video/webm"});
        download.href = URL.createObjectURL(blob);
        download.style.display = "block";
    };

    recorder.start();

    let frame = 0;
    let scale = 1;
    let alpha = 1;

    const interval = setInterval(()=>{
        ctx.fillStyle = "black";
        ctx.fillRect(0,0,w,h);

        ctx.fillStyle = `rgba(255,255,255,${alpha})`;
        ctx.font = `${40*scale}px Arial`;
        ctx.textAlign = "center";

        if(anim === "slide") ctx.fillText(text,w-frame*5,h/2);
        if(anim === "fade"){ alpha -= 0.01; ctx.fillText(text,w/2,h/2); }
        if(anim === "zoom"){ scale += 0.01; ctx.fillText(text,w/2,h/2); }

        frame++;
        if(frame > 300){
            clearInterval(interval);
            recorder.stop();
        }
    },33);
}
package com.texttovideo.pro;

import android.os.Bundle;
import android.webkit.WebSettings;
import android.webkit.WebView;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle b) {
        super.onCreate(b);

        WebView web = new WebView(this);
        WebSettings s = web.getSettings();
        s.setJavaScriptEnabled(true);
        s.setAllowFileAccess(true);
        s.setMediaPlaybackRequiresUserGesture(false);

        web.loadUrl("file:///android_asset/index.html");
        setContentView(web);
    }
}
