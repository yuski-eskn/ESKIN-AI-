<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ESKİN AI - Yapay Zeka Sohbet</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrious/4.0.2/qrious.min.js"></script>
    <style>
        :root { --bg-color: #131314; --chat-bg: #1e1f20; --text-color: #e3e3e3; --accent-color: #4b9fee; }
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: sans-serif; }
        body { background-color: var(--bg-color); color: var(--text-color); display: flex; height: 100vh; overflow: hidden; }
        
        /* Sidebar */
        .sidebar { position: fixed; top: 0; left: -260px; width: 260px; height: 100%; background: #0f0f10; transition: 0.3s; z-index: 100; padding: 20px; }
        .sidebar.open { left: 0; }
        
        /* Main */
        .main-chat { flex-grow: 1; display: flex; flex-direction: column; height: 100%; }
        .top-bar { height: 60px; display: flex; justify-content: space-between; align-items: center; padding: 0 20px; background: var(--chat-bg); }
        .chat-container { flex-grow: 1; overflow-y: auto; padding: 20px; display: flex; flex-direction: column; gap: 15px; }
        .input-container { padding: 20px; }
        .input-box { max-width: 800px; margin: 0 auto; display: flex; background: #282a2d; border-radius: 30px; padding: 10px; }
        input { flex-grow: 1; background: none; border: none; color: white; padding: 5px 15px; outline: none; }
        button { background: var(--accent-color); color: white; border: none; padding: 10px 20px; border-radius: 20px; cursor: pointer; }
    </style>
</head>
<body>

    <div class="sidebar" id="sidebar">
        <h3 style="margin-bottom:20px;">Sohbet Geçmişi</h3>
        <button onclick="toggleSidebar()">Kapat</button>
    </div>

    <div class="main-chat">
        <div class="top-bar">
            <button onclick="toggleSidebar()">☰ ESKİN AI</button>
            <canvas id="qrcode" style="width:40px; height:40px; background:white; padding:2px;"></canvas>
        </div>
        <div class="chat-container" id="chatContainer">
            <div class="message">Selam! Ben ESKİN AI. Ne hakkında konuşalım?</div>
        </div>
        <div class="input-container">
            <div class="input-box">
                <input type="text" id="userInput" placeholder="Mesajını yaz...">
                <button onclick="sendMessage()">Gönder</button>
            </div>
        </div>
    </div>

    <script>
        const API_KEY = "BURAYA_API_ANAHTARINI_YAZ";
        function toggleSidebar() { document.getElementById('sidebar').classList.toggle('open'); }
        
        async function sendMessage() {
            const input = document.getElementById('userInput');
            if(!input.value) return;
            const msg = input.value;
            input.value = '';
            
            const chat = document.getElementById('chatContainer');
            chat.innerHTML += `<div style="text-align:right; color:#4b9fee;">${msg}</div>`;
            
            const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${API_KEY}`, {
                method: 'POST',
                headers: {'Content-Type': 'application/json'},
                body: JSON.stringify({contents: [{parts: [{text: msg}]}]})
            });
            const data = await response.json();
            const reply = data.candidates[0].content.parts[0].text;
            chat.innerHTML += `<div style="margin-top:10px;">${reply}</div>`;
        }

        window.onload = () => {
            new QRious({ element: document.getElementById('qrcode'), value: window.location.href, size: 100 });
        };
    </script>
</body>
</html>
