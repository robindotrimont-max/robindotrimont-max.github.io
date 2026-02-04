<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>💘 Saint-Valentin 💘</title>
    <style>
        body {
            margin: 0;
            height: 100vh;
            background: linear-gradient(135deg, #ff4d6d, #ff8fab);
            font-family: 'Arial', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            color: white;
        }

        .container {
            text-align: center;
            background: rgba(255, 255, 255, 0.18);
            padding: 40px;
            border-radius: 25px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.25);
            z-index: 2;
        }

        h1 {
            font-size: 2.4em;
            margin-bottom: 15px;
        }

        .message {
            font-size: 1.3em;
            margin-bottom: 30px;
        }

        button {
            padding: 15px 35px;
            font-size: 1.1em;
            border: none;
            border-radius: 30px;
            cursor: pointer;
            transition: transform 0.2s;
            box-shadow: 0 10px 20px rgba(0,0,0,0.2);
            user-select: none;
        }
        
        #yesBtn:hover {
            transform: scale(1.15);
            background-color: #ff2e63;
            color: white;
        }

        #noBtn {
            background-color: #444;
            color: white;
            position: absolute;
            padding: 15px 30px;
            animation: shake 0.3s infinite alternate;
        }

        @keyframes shake {
            from { transform: translateX(-2px); }
            to { transform: translateX(2px); }
        }

        /* Cœurs flottants */
        .heart {
            position: absolute;
            width: 20px;
            height: 20px;
            background: red;
            transform: rotate(45deg);
            animation: float 6s linear infinite;
        }

        .heart::before,
        .heart::after {
            content: '';
            position: absolute;
            width: 20px;
            height: 20px;
            background: red;
            border-radius: 50%;
        }

        .heart::before {
            top: -10px;
            left: 0;
        }

        .heart::after {
            left: -10px;
            top: 0;
        }

        @keyframes float {
            0% {
                transform: translateY(100vh) rotate(45deg);
                opacity: 1;
            }
            100% {
                transform: translateY(-10vh) rotate(45deg);
                opacity: 0;
            }
        }
    </style>
</head>
<body>

<!-- 🎵 Musique romantique -->
<audio id="music" preload="auto" loop>
    <source src="river.mp3" type="audio/mpeg">
</audio>

<div class="container">
    <h1>💘 Veux-tu être ma Valentine ? 💘</h1>

    <!-- 💌 MESSAGE PERSONNALISÉ -->
    <div class="message">
    Une 4ème Saint-Valentin ensemble ?  Essaie de dire non et tu verra !  
    </div>

    <button id="yesBtn">
        OUI 💕
    </button>
    <div id="finalMessage" style="opacity:0; transition:0.5s;"></div>

</div>

<button id="noBtn">Non 💔</button>

<script>
    const noBtn = document.getElementById("noBtn");
    const yesBtn = document.getElementById("yesBtn");
    yesBtn.addEventListener("click", accept);
    const music = document.getElementById("music");

    const phrasesCruelles = [
        "Tu es sûr ? 😏",
        "Réfléchis encore 😈",
        "Impossible 😜",
        "Mauvaise réponse 💔",
        "Essaie encore 😏"
    ];

    noBtn.style.top = "60%";
    noBtn.style.left = "50%";

    // Bouton NON impossible
    document.addEventListener("mousemove", (e) => {
        const rect = noBtn.getBoundingClientRect();
        const distance = Math.hypot(
            e.clientX - (rect.left + rect.width / 2),
            e.clientY - (rect.top + rect.height / 2)
        );

        if (distance < 120) {
            const x = Math.random() * (window.innerWidth - rect.width);
            const y = Math.random() * (window.innerHeight - rect.height);
            noBtn.style.left = `${x}px`;
            noBtn.style.top = `${y}px`;
            noBtn.textContent = phrasesCruelles[Math.floor(Math.random() * phrasesCruelles.length)];
        }
    });

    // Bouton OUI
function accept() {
    yesBtn.style.display = "none";
    noBtn.style.display = "none";

    const finalMessage = document.getElementById("finalMessage");
    finalMessage.innerHTML = `
        <h2>Ouiii ❤️</h2>
        <p>
            Merde… je dois prévoir quelque chose maintenant 😏  
            <br>Un resto vendredi 06/02 ? le 6 😉
        </p>
    `;
    finalMessage.style.opacity = 1;

    // 🎵 MUSIQUE
    music.currentTime = 55; // démarre dans la partie la plus romantique
    music.volume = 0;
    music.play();

    // 🎶 Fade-in doux
    let vol = 0;
    const fade = setInterval(() => {
        if (vol < 1) {
            vol += 0.02;
            music.volume = vol;
        } else {
            clearInterval(fade);
        }
    }, 100);
}



    // Cœurs animés
    function createHeart() {
        const heart = document.createElement("div");
        heart.className = "heart";
        heart.style.left = Math.random() * 100 + "vw";
        heart.style.animationDuration = (Math.random() * 3 + 3) + "s";
        heart.style.opacity = Math.random();
        document.body.appendChild(heart);

        setTimeout(() => heart.remove(), 6000);
    }

    setInterval(createHeart, 300);
</script>

</body>
</html>
