# my-valentinesdasdasdasdad
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For My Favorite Person ❤️</title>
    <style>
        :root {
            --pink: #ff4d6d;
            --dark-pink: #c9184a;
            --white: #fff0f3;
        }

        body {
            margin: 0; padding: 0;
            background-color: var(--white);
            font-family: 'Segoe UI', sans-serif;
            overflow-x: hidden;
            display: flex; flex-direction: column; align-items: center;
        }

        .hidden { display: none !important; }

        /* Question Card */
        #main-card {
            height: 100vh;
            display: flex; flex-direction: column; justify-content: center; align-items: center;
        }

        .container {
            background: white; padding: 2.5rem; border-radius: 30px;
            box-shadow: 0 15px 35px rgba(255, 77, 109, 0.15);
            text-align: center; max-width: 400px; z-index: 10;
        }

        .buttons { display: flex; gap: 20px; justify-content: center; margin-top: 20px; }
        button { padding: 12px 28px; border-radius: 50px; border: none; cursor: pointer; font-weight: bold; }
        #yes-btn { background: var(--pink); color: white; }
        #no-btn { background: #adb5bd; color: white; }

        /* Success Section */
        #content-section { width: 90%; max-width: 800px; padding: 50px 0; text-align: center; }

        /* Love Counter */
        .counter-container {
            background: white; padding: 20px; border-radius: 20px;
            margin-bottom: 40px; box-shadow: 0 10px 20px rgba(0,0,0,0.05);
        }
        #timer { display: flex; justify-content: center; gap: 15px; font-size: 1.2rem; color: var(--dark-pink); font-weight: bold; }

        /* Love Letter */
        .message-area {
            background: #fff; padding: 30px; border-radius: 15px;
            border-left: 5px solid var(--pink); margin-bottom: 40px;
            text-align: left; line-height: 1.6; font-style: italic;
        }

        /* Photo Album */
        .photo-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; }
        .polaroid {
            background: white; padding: 10px 10px 30px 10px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1); transform: rotate(var(--r));
        }
        .polaroid img { width: 100%; height: 200px; object-fit: cover; }

        .heart { position: fixed; top: -10vh; color: var(--pink); z-index: 1; animation: fall linear forwards; }
        @keyframes fall { to { transform: translateY(110vh) rotate(360deg); } }
    </style>
</head>
<body>

    <audio id="bg-music" loop><source src="oursong.mp3" type="audio/mpeg"></audio>

    <div id="main-card">
        <div class="container">
            <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExOHpueGZ3bmZqZzR4eXpueGZ3bmZqZzR4eXpueGZ3bmZqZzR4eCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9cw/cLS1cfxvGOPVpf9g3y/giphy.gif" width="100">
            <h1>Will you be my Valentine? ❤️</h1>
            <div class="buttons">
                <button id="yes-btn">YES</button>
                <button id="no-btn">NO</button>
            </div>
        </div>
    </div>

    <div id="content-section" class="hidden">
        <div class="counter-container">
            <h3>Time we've spent together:</h3>
            <div id="timer">Loading time...</div>
        </div>

        <div class="message-area">
            <p id="typed-message"></p>
        </div>

        <div class="photo-grid">
            <div class="polaroid" style="--r: -2deg;"><img src="photo1.jpg"><p>Us ❤️</p></div>
            <div class="polaroid" style="--r: 3deg;"><img src="photo2.jpg"><p>Happy Moments</p></div>
        </div>
    </div>

    <script>
        // --- SETTINGS ---
        const anniversaryDate = "2023-05-20T00:00:00"; // YYYY-MM-DD format
        const loveLetter = "My Dearest, \n\nEvery day with you feels like a dream. Thank you for being my favorite person and my best friend. I love you more than code! \n\nAlways, Yours.";

        const noBtn = document.getElementById('no-btn');
        const yesBtn = document.getElementById('yes-btn');
        const mainCard = document.getElementById('main-card');
        const contentSection = document.getElementById('content-section');
        const music = document.getElementById('bg-music');

        // Teleport No Button
        noBtn.addEventListener('mouseover', moveButton);
        noBtn.addEventListener('touchstart', moveButton);

        function moveButton() {
            const x = Math.random() * (window.innerWidth - noBtn.offsetWidth);
            const y = Math.random() * (window.innerHeight - noBtn.offsetHeight);
            noBtn.style.position = 'fixed';
            noBtn.style.left = x + 'px';
            noBtn.style.top = y + 'px';
        }

        yesBtn.addEventListener('click', () => {
            mainCard.classList.add('hidden');
            contentSection.classList.remove('hidden');
            music.play();
            updateTimer();
            setInterval(updateTimer, 1000);
            typeWriter();
            setInterval(createHeart, 300);
        });

        function updateTimer() {
            const start = new Date(anniversaryDate);
            const now = new Date();
            const diff = now - start;

            const days = Math.floor(diff / (1000 * 60 * 60 * 24));
            const hours = Math.floor((diff / (1000 * 60 * 60)) % 24);
            const mins = Math.floor((diff / (1000 * 60)) % 60);
            const secs = Math.floor((diff / 1000) % 60);

            document.getElementById('timer').innerHTML = 
                `<div>${days}d</div><div>${hours}h</div><div>${mins}m</div><div>${secs}s</div>`;
        }

        let i = 0;
        function typeWriter() {
            if (i < loveLetter.length) {
                document.getElementById("typed-message").innerHTML += loveLetter.charAt(i);
                i++;
                setTimeout(typeWriter, 50);
            }
        }

        function createHeart() {
            const heart = document.createElement('div');
            heart.classList.add('heart');
            heart.innerHTML = '❤️';
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = (Math.random() * 3 + 2) + 's';
            document.body.appendChild(heart);
            setTimeout(() => heart.remove(), 5000);
        }
    </script>
</body>
</html>
