<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ma Valentine ? ❤️</title>
    <style>
        /* Style général */
        body {
            background-color: #ffe4e1; /* Rose pâle */
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            font-family: 'Segoe UI', cursive, sans-serif;
            overflow: hidden;
        }

        /* La petite carte centrale */
        .card {
            background: white;
            padding: 40px;
            border-radius: 30px;
            box-shadow: 0 15px 35px rgba(214, 51, 132, 0.2);
            text-align: center;
            z-index: 10;
            min-width: 300px;
        }

        h1 {
            color: #d63384;
            margin-bottom: 40px;
            font-size: 1.8rem;
        }

        /* Conteneur des boutons */
        .buttons-container {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 20px;
            height: 50px; /* Hauteur fixe pour éviter les sauts de mise en page */
        }

        button {
            padding: 12px 25px;
            font-size: 1.1rem;
            font-weight: bold;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: transform 0.2s, background-color 0.3s;
        }

        #yes-btn {
            background-color: #ff4d6d;
            color: white;
        }

        #yes-btn:hover {
            transform: scale(1.1);
            background-color: #ff758f;
        }

        #no-btn {
            background-color: #adb5bd;
            color: white;
            z-index: 100;
        }

        /* Style des coeurs flottants */
        .heart {
            position: absolute;
            color: #ffb3c1;
            font-size: 20px;
            pointer-events: none;
            animation: float Up 4s linear forwards;
        }

        @keyframes floatUp {
            0% { transform: translateY(100vh) rotate(0deg); opacity: 1; }
            100% { transform: translateY(-10vh) rotate(360deg); opacity: 0; }
        }

        img {
            border-radius: 15px;
            margin-top: 15px;
        }
    </style>
</head>
<body>

    <div class="card" id="main-card">
        <h1>Veux-tu être ma Valentine ? ❤️</h1>
        <div class="buttons-container">
            <button id="yes-btn" onclick="celebrate()">OUI !</button>
            <button id="no-btn">Non</button>
        </div>
    </div>

    <script>
        const noBtn = document.getElementById('no-btn');
        const yesBtn = document.getElementById('yes-btn');

        // Fonction pour déplacer le bouton "Non"
        function moveButton() {
            // On le passe en absolute dès le premier mouvement
            noBtn.style.position = 'absolute';
            
            // On calcule des positions aléatoires
            // On garde une petite marge de 50px pour ne pas qu'il sorte trop de l'écran
            const maxX = window.innerWidth - noBtn.offsetWidth - 50;
            const maxY = window.innerHeight - noBtn.offsetHeight - 50;
            
            const randomX = Math.floor(Math.random() * maxX);
            const randomY = Math.floor(Math.random() * maxY);
            
            noBtn.style.left = randomX + 'px';
            noBtn.style.top = randomY + 'px';
        }

        // Événement au survol (PC) et au toucher (Mobile)
        noBtn.addEventListener('mouseover', moveButton);
        noBtn.addEventListener('touchstart', (e) => {
            e.preventDefault(); // Empêche le clic accidentel sur mobile
            moveButton();
        });

        // Action quand on clique sur "Oui"
        function celebrate() {
            const card = document.getElementById('main-card');
            card.innerHTML = `
                <h1 style="font-size: 2.5rem;">Yééé ! 🥰</h1>
                <p style="color: #ff4d6d; font-size: 1.2rem; font-weight: bold;">C'était le seul bon choix ! ❤️</p>
                <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExOHpndW1uNHFqZ3J3ZzR3Z3R3Z3R3Z3R3Z3R3Z3R3Z3R3Z3R3Z3R3JpZCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/KztT2c4u8mYYUiMKdJ/giphy.gif" width="250">
            `;
            
            // Explosion massive de coeurs
            setInterval(createHeart, 150);
        }

        // Création des coeurs d'arrière-plan
        function createHeart() {
            const heart = document.createElement('div');
            heart.classList.add('heart');
            heart.innerHTML = '❤️';
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.fontSize = (Math.random() * 20 + 10) + 'px';
            heart.style.animationDuration = (Math.random() * 3 + 2) + 's';
            document.body.appendChild(heart);

            // On retire le coeur après l'animation pour ne pas alourdir la page
            setTimeout(() => { heart.remove(); }, 4000);
        }

        // Lancer quelques coeurs au démarrage
        for(let i=0; i<15; i++) {
            setTimeout(createHeart, i * 300);
        }
    </script>
</body>
</html>
