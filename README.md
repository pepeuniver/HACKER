<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>H4CK3R M0D3</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      background: black;
      color: #00ff00;
      font-family: 'Courier New', monospace;
      overflow: hidden;
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      z-index: 0;
    }

    .login-screen, .terminal-screen {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      z-index: 1;
      background: rgba(0, 0, 0, 0.8);
      padding: 30px;
      border: 2px solid #00ff00;
      display: none;
    }

    .login-screen {
      display: block;
    }

    input {
      background: black;
      color: #00ff00;
      border: 1px solid #00ff00;
      padding: 8px;
      width: 100%;
      margin-top: 10px;
      font-size: 1em;
    }

    button {
      margin-top: 15px;
      background: black;
      color: #00ff00;
      border: 1px solid #00ff00;
      padding: 8px 16px;
      cursor: pointer;
    }

    .terminal {
      white-space: pre-wrap;
      font-size: 1.1em;
    }

    .cursor {
      display: inline-block;
      width: 10px;
      height: 20px;
      background: #00ff00;
      animation: blink 1s step-start infinite;
      margin-left: 5px;
    }

    @keyframes blink {
      50% {
        opacity: 0;
      }
    }
  </style>
</head>
<body>
  <canvas id="matrixCanvas"></canvas>

  <div class="login-screen" id="loginScreen">
    <h2>ACESSO RESTRITO</h2>
    <input type="password" id="passwordInput" placeholder="Insira a senha...">
    <button onclick="checkPassword()">Entrar</button>
  </div>

  <div class="terminal-screen" id="terminalScreen">
    <div class="terminal" id="terminal">
      Inicializando conexão...
    </div>
    <div class="cursor"></div>
  </div>

  <audio id="typingSound" src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_dbb5d5e648.mp3?filename=keyboard-typing-7-182429.mp3" preload="auto"></audio>

  <script>
    // Matrix Rain
    const canvas = document.getElementById("matrixCanvas");
    const ctx = canvas.getContext("2d");

    canvas.height = window.innerHeight;
    canvas.width = window.innerWidth;

    const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
    const fontSize = 16;
    const columns = canvas.width / fontSize;

    const drops = Array.from({length: columns}).fill(1);

    function drawMatrix() {
      ctx.fillStyle = "rgba(0, 0, 0, 0.05)";
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      ctx.fillStyle = "#0F0";
      ctx.font = fontSize + "px Courier New";

      for (let i = 0; i < drops.length; i++) {
        const text = letters[Math.floor(Math.random() * letters.length)];
        ctx.fillText(text, i * fontSize, drops[i] * fontSize);

        if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
          drops[i] = 0;
        }

        drops[i]++;
      }
    }

    setInterval(drawMatrix, 33);

    // Login & Terminal
    const terminalScreen = document.getElementById('terminalScreen');
    const loginScreen = document.getElementById('loginScreen');
    const terminal = document.getElementById('terminal');
    const typingSound = document.getElementById('typingSound');

    const terminalLines = [
      'Acessando base de dados...',
      'Decodificando arquivos secretos...',
      'Bypass de firewall...',
      'Conexão segura estabelecida.',
      'Bem-vindo, agente 404.',
    ];

    let lineIndex = 0;

    function checkPassword() {
      const input = document.getElementById('passwordInput').value;

      if (input === "1234") { // você pode mudar essa senha
        loginScreen.style.display = "none";
        terminalScreen.style.display = "block";
        setTimeout(typeLines, 1000);
      } else {
        alert("Senha incorreta. Tente novamente.");
      }
    }

    function typeLines() {
      if (lineIndex < terminalLines.length) {
        terminal.innerHTML += '\n' + terminalLines[lineIndex];
        typingSound.play();
        lineIndex++;
        setTimeout(typeLines, 1500);
      }
    }
  </script>
</body>
</html>
