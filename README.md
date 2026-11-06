<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>¡Feliz Vuelta al Sol! ☀️</title>
    <!-- Script para el efecto de confeti -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <style>
        :root {
            --bg-blue-light: #e6f0fa;
            --bg-blue-dark: #b8d4f2;
            --card-bg: #ffffff;
            --text-main: #334155;
            --accent-pink: #ff6b8b;
            --accent-yellow: #ffd166;
            --accent-blue: #4cc9f0;
            --border-paper: #cbd5e1;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background-color: var(--bg-blue-light);
            background-image: 
                linear-gradient(90deg, rgba(184, 212, 242, 0.6) 50%, transparent 50%),
                linear-gradient(rgba(184, 212, 242, 0.6) 50%, transparent 50%);
            background-size: 40px 40px;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            color: var(--text-main);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            position: relative;
            overflow-x: hidden;
        }

        /* Reproductor de música flotante */
        .music-player {
            position: fixed;
            top: 20px;
            right: 20px;
            background: rgba(255, 255, 255, 0.9);
            padding: 8px 14px;
            border-radius: 30px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            display: flex;
            align-items: center;
            gap: 10px;
            z-index: 100;
            cursor: pointer;
            border: 2px solid #bae6fd;
            transition: transform 0.2s;
        }

        .music-player:hover {
            transform: scale(1.05);
        }

        .music-icon {
            font-size: 1.2rem;
            animation: pulse 1.5s infinite;
        }

        .music-text {
            font-size: 0.85rem;
            font-weight: 600;
            color: #0369a1;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.15); }
            100% { transform: scale(1); }
        }

        /* Estrellitas flotantes de fondo */
        .star {
            position: absolute;
            font-size: 20px;
            user-select: none;
            animation: float 4s ease-in-out infinite alternate;
            z-index: 1;
        }
        .star-1 { top: 8%; left: 8%; animation-delay: 0s; }
        .star-2 { top: 15%; right: 10%; animation-delay: 1s; }
        .star-3 { bottom: 12%; left: 10%; animation-delay: 2s; }
        .star-4 { bottom: 8%; right: 8%; animation-delay: 1.5s; }

        @keyframes float {
            0% { transform: translateY(0px) rotate(0deg); }
            100% { transform: translateY(-12px) rotate(15deg); }
        }

        /* Contenedor principal estilo Tarjeta Scrapbook */
        .card-container {
            position: relative;
            z-index: 10;
            background: var(--card-bg);
            max-width: 520px;
            width: 100%;
            border-radius: 24px;
            padding: 35px 25px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
            border: 4px solid #ffffff;
            text-align: center;
        }

        /* Encabezado de letras tipo recortes de papel */
        .scrapbook-title {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 6px;
            margin-bottom: 25px;
        }

        .letter-tile {
            display: inline-block;
            padding: 6px 12px;
            font-weight: 900;
            font-size: 1.2rem;
            color: #ffffff;
            border-radius: 6px;
            box-shadow: 2px 3px 0px rgba(0,0,0,0.15);
            text-transform: uppercase;
        }

        .c-1 { background-color: #ff595e; transform: rotate(-3deg); }
        .c-2 { background-color: #ffca3a; transform: rotate(2deg); color: #444; }
        .c-3 { background-color: #8ac926; transform: rotate(-2deg); }
        .c-4 { background-color: #1982c4; transform: rotate(4deg); }
        .c-5 { background-color: #6a4c93; transform: rotate(-1deg); }

        /* Mensaje principal */
        .message-body {
            font-size: 1.05rem;
            line-height: 1.75;
            color: #475569;
            text-align: justify;
            text-align-last: center;
            margin-bottom: 25px;
            background-color: #f8fafc;
            padding: 20px;
            border-radius: 16px;
            border: 1px dashed var(--border-paper);
        }

        /* Cuadro de texto bíblico */
        .bible-box {
            background-color: #f0f9ff;
            border: 2px solid #bae6fd;
            border-radius: 16px;
            padding: 18px;
            margin-bottom: 25px;
            position: relative;
        }

        .bible-title {
            font-size: 0.85rem;
            font-weight: 700;
            color: #0284c7;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 8px;
        }

        .bible-text {
            font-style: italic;
            color: #0369a1;
            font-size: 1rem;
            line-height: 1.5;
        }

        /* Botón de confeti */
        .celebrate-btn {
            background: linear-gradient(135deg, #ff6b8b, #ff8e53);
            color: white;
            border: none;
            padding: 14px 28px;
            font-size: 1.05rem;
            font-weight: 700;
            border-radius: 50px;
            cursor: pointer;
            box-shadow: 0 6px 20px rgba(255, 107, 139, 0.35);
            transition: all 0.2s ease;
            width: 100%;
        }

        .celebrate-btn:hover {
            transform: translateY(-2deg);
            box-shadow: 0 8px 25px rgba(255, 107, 139, 0.45);
        }

        .celebrate-btn:active {
            transform: translateY(1deg);
        }
    </style>
</head>
<body>

    <!-- Reproductor de Música Flotante -->
    <div class="music-player" onclick="toggleAudio()" id="playButton">
        <span class="music-icon" id="iconStatus">🎵</span>
        <span class="music-text" id="textStatus">Reproducir música</span>
    </div>

    <!-- Etiqueta de audio (puedes cambiar el link por un archivo .mp3 tuyo o de una canción que le guste) -->
    <audio id="bgMusic" loop>
        <source src="https://www.bensound.com/bensound-music/bensound-ofeliasdream.mp3" type="audio/mp3">
        Tu navegador no soporta audio.
    </audio>

    <!-- Estrellas flotantes de fondo -->
    <div class="star star-1">⭐</div>
    <div class="star star-2">✨</div>
    <div class="star star-3">🌟</div>
    <div class="star star-4">💖</div>

    <div class="card-container">
        <!-- Encabezado estilo recortes: FELIZ VUELTA AL SOL -->
        <div class="scrapbook-title">
            <span class="letter-tile c-1">F</span>
            <span class="letter-tile c-2">E</span>
            <span class="letter-tile c-3">L</span>
            <span class="letter-tile c-4">I</span>
            <span class="letter-tile c-5">Z</span>
            <span style="width: 100%; height: 0;"></span>
            <span class="letter-tile c-2">V</span>
            <span class="letter-tile c-3">U</span>
            <span class="letter-tile c-4">E</span>
            <span class="letter-tile c-1">L</span>
            <span class="letter-tile c-5">T</span>
            <span class="letter-tile c-2">A</span>
            <span style="width: 100%; height: 0;"></span>
            <span class="letter-tile c-3">A</span>
            <span class="letter-tile c-4">L</span>
            <span style="width: 8px;"></span>
            <span class="letter-tile c-1">S</span>
            <span class="letter-tile c-5">O</span>
            <span class="letter-tile c-2">L</span>
            <span class="letter-tile c-3">☀️</span>
        </div>

        <!-- Mensaje personalizado -->
        <div class="message-body">
            Hoy celebro tu vida y doy gracias por la hermosa bendición que es tenerte en mi camino. Admiro profundamente la ternura y la entrega con la que te preparas día a día para cuidar a los demás. Tienes un corazón puro y una vocación admirable.<br><br>
            Gracias por ser esa amiga incondicional, esa hermanita que siempre está presente con una sonrisa, con nuevas ocurrencias y la mejor energía. Pido a Dios por cada anhelo que tienes en tu corazón se cumpla según su propósito.<br><br>
            <strong>¡Te quiero mucho, hermanita! ❤️</strong>
        </div>

        <!-- Cuadro con el texto bíblico -->
        <div class="bible-box">
            <div class="bible-title">📖 Salmos 20:4</div>
            <div class="bible-text">
                «Que Dios te conceda los deseos de tu corazón y haga que todos tus planes triunfen.»
            </div>
        </div>

        <!-- Botón para lanzar confeti -->
        <button class="celebrate-btn" onclick="throwConfetti()">¡Lanzar Confeti! 🎉</button>
    </div>

    <script>
        const music = document.getElementById('bgMusic');
        const playButton = document.getElementById('playButton');
        const iconStatus = document.getElementById('iconStatus');
        const textStatus = document.getElementById('textStatus');
        let isPlaying = false;

        function toggleAudio() {
            if (!isPlaying) {
                music.play().then(() => {
                    isPlaying = true;
                    iconStatus.textContent = "⏸️";
                    textStatus.textContent = "Pausar música";
                }).catch(e => {
                    console.log("Error al reproducir audio:", e);
                });
            } else {
                music.pause();
                isPlaying = false;
                iconStatus.textContent = "🎵";
                textStatus.textContent = "Reproducir música";
            }
        }

        // Confeti automático al cargar la página
        window.onload = () => {
            throwConfetti();
        };

        function throwConfetti() {
            confetti({
                particleCount: 100,
                spread: 70,
                origin: { y: 0.6 },
                colors: ['#ff595e', '#ffca3a', '#8ac926', '#1982c4', '#6a4c93']
            });
        }
    </script>
</body>
</html>
