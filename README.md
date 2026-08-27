# Ma-Sarah-
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Bouquet de Compliments</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;1,400&family=Great+Vibes&family=Plus+Jakarta+Sans:wght@300;400&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg-cream: #FAF6F0;
      --pink-soft: #F4E3E3;
      --pink-accent: #E8A0BF;
      --red-soft: #C96868;
      --gold-accent: #D4AF37;
      --gold-light: #F3E5AB;
      --text-dark: #4A3E3D;
      --stem-green: #A8BBA2;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background-color: var(--bg-cream);
      color: var(--text-dark);
      font-family: 'Plus Jakarta Sans', sans-serif;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 20px;
      overflow-x: hidden;
      position: relative;
    }

    /* Particules d'arrière-plan */
    .particle {
      position: absolute;
      background: var(--gold-accent);
      border-radius: 50%;
      opacity: 0.3;
      pointer-events: none;
      animation: floatUp 8s infinite linear;
    }

    @keyframes floatUp {
      0% { transform: translateY(100vh) rotate(0deg); opacity: 0; }
      50% { opacity: 0.5; }
      100% { transform: translateY(-10vh) rotate(360deg); opacity: 0; }
    }

    .container {
      max-width: 800px;
      width: 100%;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 30px;
      z-index: 10;
    }

    header {
      text-align: center;
    }

    h1 {
      font-family: 'Great Vibes', cursive;
      font-size: 3.2rem;
      color: var(--red-soft);
      font-weight: normal;
      margin-bottom: 8px;
      text-shadow: 1px 1px 2px rgba(0,0,0,0.05);
    }

    .subtitle {
      font-family: 'Cormorant Garamond', serif;
      font-style: italic;
      font-size: 1.2rem;
      color: #7A6A69;
    }

    /* Zone des fleurs */
    .flowers-container {
      display: flex;
      justify-content: center;
      align-items: flex-end;
      gap: 25px;
      margin: 20px 0;
      min-height: 220px;
      flex-wrap: wrap;
    }

    .flower-wrapper {
      display: flex;
      flex-direction: column;
      align-items: center;
      cursor: pointer;
      transition: transform 0.3s ease;
      position: relative;
    }

    .flower-wrapper:hover {
      transform: translateY(-8px) scale(1.03);
    }

    .flower-wrapper.disabled {
      cursor: default;
      pointer-events: none;
    }

    .flower-svg {
      width: 100px;
      height: 100px;
      filter: drop-shadow(0 4px 8px rgba(0,0,0,0.06));
    }

    .petal {
      transform-origin: center;
      transition: transform 0.5s ease, opacity 0.5s ease;
      fill: var(--pink-accent);
    }

    .flower-wrapper:nth-child(even) .petal {
      fill: #F0B2B2;
    }

    .stem {
      width: 4px;
      height: 80px;
      background: linear-gradient(to bottom, var(--stem-green), #8A9A85);
      border-radius: 2px;
      margin-top: -10px;
      position: relative;
      z-index: -1;
    }

    .leaf {
      position: absolute;
      width: 16px;
      height: 8px;
      background-color: var(--stem-green);
      border-radius: 16px 0;
    }

    .leaf.left {
      left: -14px;
      top: 30px;
      transform: rotate(-25deg);
    }

    .leaf.right {
      right: -14px;
      top: 45px;
      transform: rotate(205deg);
    }

    /* Animation de chute de pétale */
    .petal-falling {
      animation: fallAndFade 1.2s forwards cubic-bezier(0.25, 0.46, 0.45, 0.94);
    }

    @keyframes fallAndFade {
      0% {
        transform: translate(0, 0) rotate(0deg);
        opacity: 1;
      }
      100% {
        transform: translate(var(--dx), 150px) rotate(var(--rot));
        opacity: 0;
      }
    }

    /* Cartes de compliments */
    .compliments-list {
      width: 100%;
      display: flex;
      flex-direction: column;
      gap: 15px;
    }

    .compliment-card {
      background: rgba(255, 255, 255, 0.7);
      backdrop-filter: blur(8px);
      border: 1px solid rgba(212, 175, 55, 0.2);
      border-left: 4px solid var(--red-soft);
      border-radius: 12px;
      padding: 18px 24px;
      box-shadow: 0 4px 15px rgba(0, 0, 0, 0.03);
      opacity: 0;
      transform: translateY(20px);
      transition: opacity 0.8s ease, transform 0.8s ease;
      display: none;
    }

    .compliment-card.visible {
      display: block;
      opacity: 1;
      transform: translateY(0);
    }

    .compliment-card p {
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.35rem;
      line-height: 1.5;
      color: var(--text-dark);
    }

    .compliment-number {
      font-family: 'Great Vibes', cursive;
      font-size: 1.4rem;
      color: var(--gold-accent);
      margin-bottom: 4px;
    }

    /* Carte finale récapitulative */
    .final-card {
      background: linear-gradient(135deg, #FFF9F9 0%, #FFF0F5 100%);
      border: 2px solid var(--gold-accent);
      border-radius: 20px;
      padding: 35px 25px;
      text-align: center;
      box-shadow: 0 10px 30px rgba(212, 175, 55, 0.15);
      opacity: 0;
      transform: scale(0.9);
      transition: all 1s ease;
      margin-top: 20px;
      display: none;
    }

    .final-card.visible {
      display: block;
      opacity: 1;
      transform: scale(1);
    }

    .final-card h2 {
      font-family: 'Great Vibes', cursive;
      font-size: 2.8rem;
      color: var(--red-soft);
      margin-bottom: 15px;
    }

    .final-card p {
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.3rem;
      line-height: 1.6;
      color: var(--text-dark);
    }

    .gold-ring {
      display: inline-block;
      margin-top: 15px;
      font-size: 1.8rem;
    }

    /* Responsif */
    @media (max-width: 600px) {
      h1 { font-size: 2.5rem; }
      .flower-svg { width: 75px; height: 75px; }
      .stem { height: 65px; }
      .flowers-container { gap: 12px; }
      .compliment-card p { font-size: 1.15rem; }
      .final-card h2 { font-size: 2.2rem; }
    }
  </style>
</head>
<body>

  <!-- Particules dorées -->
  <div id="particles"></div>

  <div class="container">
    <header>
      <h1>Effeuille les fleurs</h1>
      <p class="subtitle">Clique sur une fleur pour découvrir ce qu'elle cache...</p>
    </header>

    <!-- Zone des 4 fleurs -->
    <div class="flowers-container">
      <!-- Fleur 1 -->
      <div class="flower-wrapper" data-index="0">
        <svg class="flower-svg" viewBox="0 0 100 100">
          <g class="petals">
            <circle class="petal" cx="50" cy="25" r="16" />
            <circle class="petal" cx="75" cy="50" r="16" />
            <circle class="petal" cx="50" cy="75" r="16" />
            <circle class="petal" cx="25" cy="50" r="16" />
            <circle class="petal" cx="68" cy="32" r="15" />
            <circle class="petal" cx="68" cy="68" r="15" />
            <circle class="petal" cx="32" cy="68" r="15" />
            <circle class="petal" cx="32" cy="32" r="15" />
          </g>
          <circle cx="50" cy="50" r="14" fill="var(--gold-accent)" />
          <circle cx="50" cy="50" r="10" fill="var(--gold-light)" />
        </svg>
        <div class="stem">
          <div class="leaf left"></div>
          <div class="leaf right"></div>
        </div>
      </div>

      <!-- Fleur 2 -->
      <div class="flower-wrapper" data-index="1">
        <svg class="flower-svg" viewBox="0 0 100 100">
          <g class="petals">
            <circle class="petal" cx="50" cy="25" r="16" />
            <circle class="petal" cx="75" cy="50" r="16" />
            <circle class="petal" cx="50" cy="75" r="16" />
            <circle class="petal" cx="25" cy="50" r="16" />
            <circle class="petal" cx="68" cy="32" r="15" />
            <circle class="petal" cx="68" cy="68" r="15" />
            <circle class="petal" cx="32" cy="68" r="15" />
            <circle class="petal" cx="32" cy="32" r="15" />
          </g>
          <circle cx="50" cy="50" r="14" fill="var(--gold-accent)" />
          <circle cx="50" cy="50" r="10" fill="var(--gold-light)" />
        </svg>
        <div class="stem">
          <div class="leaf left"></div>
          <div class="leaf right"></div>
        </div>
      </div>

      <!-- Fleur 3 -->
      <div class="flower-wrapper" data-index="2">
        <svg class="flower-svg" viewBox="0 0 100 100">
          <g class="petals">
            <circle class="petal" cx="50" cy="25" r="16" />
            <circle class="petal" cx="75" cy="50" r="16" />
            <circle class="petal" cx="50" cy="75" r="16" />
            <circle class="petal" cx="25" cy="50" r="16" />
            <circle class="petal" cx="68" cy="32" r="15" />
            <circle class="petal" cx="68" cy="68" r="15" />
            <circle class="petal" cx="32" cy="68" r="15" />
            <circle class="petal" cx="32" cy="32" r="15" />
          </g>
          <circle cx="50" cy="50" r="14" fill="var(--gold-accent)" />
          <circle cx="50" cy="50" r="10" fill="var(--gold-light)" />
        </svg>
        <div class="stem">
          <div class="leaf left"></div>
          <div class="leaf right"></div>
        </div>
      </div>

      <!-- Fleur 4 -->
      <div class="flower-wrapper" data-index="3">
        <svg class="flower-svg" viewBox="0 0 100 100">
          <g class="petals">
            <circle class="petal" cx="50" cy="25" r="16" />
            <circle class="petal" cx="75" cy="50" r="16" />
            <circle class="petal" cx="50" cy="75" r="16" />
            <circle class="petal" cx="25" cy="50" r="16" />
            <circle class="petal" cx="68" cy="32" r="15" />
            <circle class="petal" cx="68" cy="68" r="15" />
            <circle class="petal" cx="32" cy="68" r="15" />
            <circle class="petal" cx="32" cy="32" r="15" />
          </g>
          <circle cx="50" cy="50" r="14" fill="var(--gold-accent)" />
          <circle cx="50" cy="50" r="10" fill="var(--gold-light)" />
        </svg>
        <div class="stem">
          <div class="leaf left"></div>
          <div class="leaf right"></div>
        </div>
      </div>
    </div>

    <!-- Liste des compliments -->
    <div class="compliments-list">
      <div class="compliment-card" id="compliment-0">
        <div class="compliment-number">Premier pétale</div>
        <p>« J’aime trop tes yeux, d’une douceur incroyable. Ton regard ultra captivant qui me donne l’impression de nager dans un bonheur ultime. »</p>
      </div>

      <div class="compliment-card" id="compliment-1">
        <div class="compliment-number">Deuxième pétale</div>
        <p>« Ton visage tellement rayonnant qui me réconforte dans le reste de mes journées. J’aime absolument tous les traits de ton visage, avec des lèvres si douces et une teinte parfaite. »</p>
      </div>

      <div class="compliment-card" id="compliment-2">
        <div class="compliment-number">Troisième pétale</div>
        <p>« Tes cheveux sont splendides, j’aime trop, ils sont tellement magnifiques et d’une douceur incroyable. »</p>
      </div>

      <div class="compliment-card" id="compliment-3">
        <div class="compliment-number">Quatrième pétale</div>
        <p>« Tes toutes petites mains magnifiques, douces et réconfortantes, je voudrais les tenir tout le temps dans mes mains et ne jamais les lâcher, puis quand il y aura cette bague autour du doigt, alors elles seront plus que parfaite. »</p>
      </div>
    </div>

    <!-- Carte récapitulative finale -->
    <div class="final-card" id="final-card">
      <h2>Pour Toujours...</h2>
      <p>Chaque fleur effeuillée ne fait que confirmer ce que mon cœur sait déjà. Tu es ma plus belle certitude.</p>
      <span class="gold-ring">💍</span>
    </div>
  </div>

  <script>
    // Génération de particules lumineuses d'ambiance
    const particlesContainer = document.getElementById('particles');
    for (let i = 0; i < 20; i++) {
      const particle = document.createElement('div');
      particle.classList.add('particle');
      const size = Math.random() * 6 + 2;
      particle.style.width = `${size}px`;
      particle.style.height = `${size}px`;
      particle.style.left = `${Math.random() * 100}vw`;
      particle.style.animationDuration = `${Math.random() * 5 + 5}s`;
      particle.style.animationDelay = `${Math.random() * 5}s`;
      particlesContainer.appendChild(particle);
    }

    // Gestion de l'ordre des compliments et de l'animation d'effeuillage
    let currentStep = 0;
    const totalFlowers = 4;
    const flowers = document.querySelectorAll('.flower-wrapper');

    flowers.forEach(flower => {
      flower.addEventListener('click', function() {
        if (currentStep >= totalFlowers || this.classList.contains('disabled')) return;

        this.classList.add('disabled');
        const petals = Array.from(this.querySelectorAll('.petal'));

        // Animation d'effeuillage progressif des pétales de la fleur cliquée
        petals.forEach((petal, index) => {
          setTimeout(() => {
            const dx = (Math.random() - 0.5) * 120;
            const rot = (Math.random() - 0.5) * 360;
            petal.style.setProperty('--dx', `${dx}px`);
            petal.style.setProperty('--rot', `${rot}deg`);
            petal.classList.add('petal-falling');
          }, index * 80);
        });

        // Disparition douce de la tige après la chute des pétales
        setTimeout(() => {
          this.style.transition = 'opacity 0.8s ease, transform 0.8s ease';
          this.style.opacity = '0.15';
          this.style.transform = 'scale(0.8)';
        }, petals.length * 80 + 200);

        // Affichage du compliment correspondant à l'étape actuelle
        const cardToShow = document.getElementById(`compliment-${currentStep}`);
        if (cardToShow) {
          setTimeout(() => {
            cardToShow.classList.add('visible');
            cardToShow.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
          }, 300);
        }

        currentStep++;

        // Affichage de la carte récapitulative finale après le retrait de la 4ème fleur
        if (currentStep === totalFlowers) {
          setTimeout(() => {
            const finalCard = document.getElementById('final-card');
            finalCard.classList.add('visible');
            finalCard.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
          }, 1200);
        }
      });
    });
  </script>
</body>
</html>
