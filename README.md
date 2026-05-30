# Sjjs
Jajs
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>🔒 DIZX RANSOMWARE</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: none;
        }
        
        body {
            background: black;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            font-family: 'Courier New', monospace;
        }
        
        /* Overlay utama - z-index tertinggi */
        .ransomware {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(45deg, #000000, #1a0000);
            z-index: 2147483647;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }
        
        .box {
            background: rgba(0,0,0,0.95);
            border: 3px solid #ff0000;
            border-radius: 20px;
            padding: 40px;
            max-width: 450px;
            width: 90%;
            text-align: center;
            box-shadow: 0 0 100px rgba(255,0,0,0.5);
        }
        
        .icon {
            font-size: 70px;
            animation: shake 0.3s infinite;
        }
        
        @keyframes shake {
            0%,100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }
        
        h1 {
            color: #ff0000;
            font-size: 26px;
            margin: 20px 0;
        }
        
        .message {
            color: #ff6666;
            margin: 15px 0;
            line-height: 1.6;
            font-size: 13px;
        }
        
        .code-input {
            width: 100%;
            padding: 15px;
            font-size: 32px;
            text-align: center;
            background: #111;
            border: 2px solid #ff0000;
            color: #00ff00;
            font-family: monospace;
            letter-spacing: 10px;
            margin: 20px 0;
            border-radius: 10px;
        }
        
        button {
            background: #ff0000;
            color: white;
            border: none;
            padding: 15px;
            font-size: 18px;
            font-weight: bold;
            border-radius: 10px;
            cursor: pointer;
            width: 100%;
        }
        
        button:hover {
            background: #cc0000;
        }
        
        .attempts {
            color: #ff6666;
            font-size: 12px;
            margin-top: 15px;
        }
        
        .timer {
            color: #ff0000;
            font-size: 20px;
            font-weight: bold;
            margin: 15px 0;
            background: rgba(255,0,0,0.2);
            padding: 10px;
            border-radius: 10px;
        }
    </style>
</head>
<body>
    <div class="ransomware" id="ransomScreen">
        <div class="box">
            <div class="icon">🔒💀🔥</div>
            <h1>⚠️ SISTEM TERKUNCI ⚠️</h1>
            <div class="message">
                <strong>DIZX RANSOMWARE v5.0</strong><br><br>
                Semua file, foto, dan data pribadi anda<br>
                telah dienkripsi dengan AES-256.<br><br>
                <span style="color: yellow;">🔐 KODE DEKRIPSI: <span style="color: #00ff00;">123</span></span>
            </div>
            
            <div class="timer" id="timerDisplay">⏰ WAKTU: 05:00</div>
            
            <input type="text" class="code-input" id="codeInput" maxlength="3" placeholder="___" autocomplete="off">
            
            <button id="unlockBtn">🔓 UNLOCK & EXIT</button>
            
            <div class="attempts" id="attemptDisplay">❌ PERCOBAAN: 0/3 ❌</div>
        </div>
    </div>

    <script>
        (function() {
            // VARIABEL
            const CORRECT_CODE = "123";
            let attempts = 0;
            let timeLeft = 300; // 5 menit = 300 detik
            let unlocked = false;
            
            const ransomScreen = document.getElementById('ransomScreen');
            const codeInput = document.getElementById('codeInput');
            const unlockBtn = document.getElementById('unlockBtn');
            const attemptDisplay = document.getElementById('attemptDisplay');
            const timerDisplay = document.getElementById('timerDisplay');
            
            // ========== 1. LOCK SCREEN - GAK BISA KELUAR ==========
            
            // Fullscreen paksa
            function forceFullscreen() {
                const doc = document.documentElement;
                if (doc.requestFullscreen) doc.requestFullscreen();
                else if (doc.webkitRequestFullscreen) doc.webkitRequestFullscreen();
                else if (doc.msRequestFullscreen) doc.msRequestFullscreen();
            }
            
            // Paksa fullscreen setiap detik
            setInterval(forceFullscreen, 1000);
            
            // Block semua tombol keyboard
            document.addEventListener('keydown', function(e) {
                // Block F5, F12, F11, Escape, Alt+F4, Ctrl+R, Ctrl+W, Ctrl+Tab
                const blockedKeys = ['F5', 'F11', 'F12', 'Escape', 'Alt', 'Control', 'Meta', 'Tab'];
                
                if (blockedKeys.includes(e.key)) {
                    e.preventDefault();
                    e.stopPropagation();
                    return false;
                }
                
                if (e.ctrlKey && (e.key === 'r' || e.key === 'R' || e.key === 'w' || e.key === 'W')) {
                    e.preventDefault();
                    return false;
                }
                
                if (e.altKey && e.key === 'F4') {
                    e.preventDefault();
                    return false;
                }
                
                if (e.key === 'F12') {
                    e.preventDefault();
                    return false;
                }
            });
            
            // Block right click
            document.addEventListener('contextmenu', function(e) {
                e.preventDefault();
                return false;
            });
            
            // Block history back
            history.pushState(null, null, location.href);
            window.addEventListener('popstate', function() {
                if (!unlocked) {
                    history.pushState(null, null, location.href);
                }
            });
            
            // Block close tab
            window.addEventListener('beforeunload', function(e) {
                if (!unlocked) {
                    e.preventDefault();
                    e.returnValue = '⚠️ JANGAN TUTUP! Masukkan kode 123 untuk keluar!';
                    return '⚠️ JANGAN TUTUP! Masukkan kode 123 untuk keluar!';
                }
            });
            
            // ========== 2. TIMER ==========
            function updateTimer() {
                if (unlocked) return;
                
                const minutes = Math.floor(timeLeft / 60);
                const seconds = timeLeft % 60;
                timerDisplay.textContent = `⏰ WAKTU: ${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
                
                if (timeLeft <= 0) {
                    // Timer habis -> reset attempts dan timer (biar masih terjebak)
                    timeLeft = 300;
                    attempts = 0;
                    attemptDisplay.innerHTML = '❌ PERCOBAAN: 0/3 ❌';
                    attemptDisplay.style.color = '#ff6666';
                    codeInput.disabled = false;
                    unlockBtn.disabled = false;
                    codeInput.value = '';
                    timerDisplay.textContent = '⏰ WAKTU: 05:00';
                } else {
                    timeLeft--;
                }
            }
            
            setInterval(updateTimer, 1000);
            
            // ========== 3. UNLOCK FUNCTION ==========
            function unlockSystem() {
                if (unlocked) return;
                
                const inputCode = codeInput.value;
                
                if (inputCode === CORRECT_CODE) {
                    // BENAR - KELUAR DARI RANSOMWARE
                    unlocked = true;
                    
                    // Hapus beforeunload biar bisa keluar
                    window.removeEventListener('beforeunload', () => {});
                    
                    // Exit fullscreen
                    if (document.exitFullscreen) document.exitFullscreen();
                    if (document.webkitExitFullscreen) document.webkitExitFullscreen();
                    
                    // Redirect ke Google (keluar dari web ini)
                    window.location.href = 'https://www.google.com';
                    
                } else {
                    // SALAH
                    attempts++;
                    attemptDisplay.innerHTML = `❌ PERCOBAAN: ${attempts}/3 ❌`;
                    attemptDisplay.style.color = '#ff0000';
                    codeInput.value = '';
                    
                    // Efek geter
                    const box = document.querySelector('.box');
                    box.style.transform = 'translateX(10px)';
                    setTimeout(() => { box.style.transform = 'translateX(-10px)'; }, 50);
                    setTimeout(() => { box.style.transform = 'translateX(0)'; }, 100);
                    
                    if (attempts >= 3) {
                        // Percobaan habis - disable sementara 30 detik
                        codeInput.disabled = true;
                        unlockBtn.disabled = true;
                        attemptDisplay.innerHTML = '⏳ TERKUNCI 30 DETIK... ⏳';
                        
                        setTimeout(() => {
                            attempts = 0;
                            attemptDisplay.innerHTML = '❌ PERCOBAAN: 0/3 ❌';
                            attemptDisplay.style.color = '#ff6666';
                            codeInput.disabled = false;
                            unlockBtn.disabled = false;
                            codeInput.value = '';
                        }, 30000);
                    }
                }
            }
            
            // Event
            unlockBtn.addEventListener('click', unlockSystem);
            codeInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter') unlockSystem();
            });
            
            // Auto focus terus
            setInterval(() => {
                if (!unlocked && document.activeElement !== codeInput) {
                    codeInput.focus();
                }
            }, 100);
            
            console.log('%c🔒 DIZX RANSOMWARE - KODE: 123 🔒', 'color: red; font-size: 20px');
        })();
    </script>
</body>
</html>
