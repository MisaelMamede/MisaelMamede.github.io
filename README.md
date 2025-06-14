<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <title>Mensagem com Amor</title>
  <style>
    :root {
      --matrix-red: #ff4444;
    }

    @import url('https://fonts.googleapis.com/css2?family=Great+Vibes&display=swap');

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background: #000;
      font-family: 'Great Vibes', cursive;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      overflow: hidden;
      position: relative;
    }

    /* Container das palavras "Love" */
    .love-container {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw; 
      height: 100vh;
      pointer-events: none; /* palavras não bloqueiam cliques */
      overflow: hidden;
      z-index: 1;
    }

    .floating-love {
      position: absolute;
      font-size: 3rem;
      color: var(--matrix-red);
      font-family: 'Great Vibes', cursive;
      text-shadow:
        0 0 8px var(--matrix-red),
        0 0 20px var(--matrix-red),
        0 0 30px var(--matrix-red);
      animation: floatLove 10s infinite ease-in-out;
      opacity: 0.8;
      user-select: none;
      white-space: nowrap;
      width: max-content;
      height: max-content;
    }

    @keyframes floatLove {
      0% {
        transform: translate(0, 0) rotate(0deg);
      }
      25% {
        transform: translate(20px, -10px) rotate(10deg);
      }
      50% {
        transform: translate(-20px, 15px) rotate(-10deg);
      }
      75% {
        transform: translate(10px, 5px) rotate(15deg);
      }
      100% {
        transform: translate(0, 0) rotate(0deg);
      }
    }

    /* Envelope */
    .envelope-wrapper {
      perspective: 1000px;
      z-index: 10;
      position: relative;
    }

    .envelope {
      width: 320px;
      height: 200px;
      background: linear-gradient(135deg, #111, #222);
      border-radius: 10px;
      box-shadow: 0 0 20px var(--matrix-red);
      position: relative;
      cursor: pointer;
      user-select: none;
    }

    /* Tampa do envelope */
    .flap {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: #e60073;
      border-radius: 10px;
      backface-visibility: hidden;
      transform-origin: top center;
      transition: transform 1s;
      z-index: 2;
    }

    /* Quando aberto, tampa levanta */
    .envelope.open .flap {
      transform: rotateX(-135deg);
    }

    /* Conteúdo da carta */
    .card {
      position: relative;
      width: 100%;
      height: 100%;
      background: #111;
      color: var(--matrix-red);
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 15px var(--matrix-red);
      animation: pulseMatrix 2s infinite;
      z-index: 1;
      user-select: auto;
    }

    .message {
      font-size: 2rem;
      margin-bottom: 1rem;
      text-align: center;
      text-shadow: 0 0 8px var(--matrix-red);
    }

    textarea {
      width: 90%;
      height: 80px;
      background: #000;
      border: 1px solid var(--matrix-red);
      border-radius: 5px;
      padding: 10px;
      color: var(--matrix-red);
      font-family: 'Great Vibes', cursive;
      font-size: 1.2rem;
      resize: none;
      box-shadow: 0 0 10px var(--matrix-red);
      transition: box-shadow 0.3s;
    }

    textarea:focus {
      outline: none;
      box-shadow: 0 0 15px var(--matrix-red);
    }

    /* Animação pulsante estilo Matrix */
    @keyframes pulseMatrix {
      0%, 100% {
        color: var(--matrix-red);
        border-color: var(--matrix-red);
        text-shadow: 0 0 5px var(--matrix-red), 0 0 15px var(--matrix-red);
      }
      50% {
        color: #ff7777;
        border-color: #ff7777;
        text-shadow: 0 0 10px #ff7777, 0 0 25px #ff7777;
      }
    }

    /* Botão da música */
    .music-control {
      position: fixed;
      top: 20px;
      right: 20px;
      background: transparent;
      border: 2px solid var(--matrix-red);
      color: var(--matrix-red);
      padding: 10px 15px;
      border-radius: 50%;
      cursor: pointer;
      font-size: 1.2rem;
      animation: pulseMatrix 2s infinite;
      z-index: 999;
      box-shadow: 0 0 10px var(--matrix-red);
      transition: background-color 0.3s;
      user-select: none;
    }

    .music-control:hover {
      background-color: rgba(255, 68, 68, 0.1);
    }
  </style>
</head>
<body>

  <!-- Container das palavras Love -->
  <div class="love-container"></div>

  <!-- Música de fundo -->
  <audio id="bg-music" loop>
    <source src="https://cdn.pixabay.com/download/audio/2022/02/16/audio_2438f87db1.mp3?filename=romantic-background-116199.mp3" type="audio/mpeg" />
    Seu navegador não suporta áudio.
  </audio>

  <!-- Botão para controlar música -->
  <button class="music-control" onclick="toggleMusic()" aria-label="Tocar/Pausar música">🎵</button>

  <!-- Envelope -->
  <div class="envelope-wrapper">
    <div class="envelope" tabindex="0" role="button" aria-pressed="false" aria-label="Clique para abrir/fechar envelope"
         onclick="this.classList.toggle('open'); toggleAria(this)"
         onkeydown="if(event.key==='Enter' || event.key===' ') { event.preventDefault(); this.classList.toggle('open'); toggleAria(this); }">
      <div class="flap"></div>
      <div class="card">
        <div class="message">Eu te amo  </div>
        <textarea placeholder= Fico triste por não puder te dar nada,porém prefiro fazer esse simples gesto de amor e carinho. Não sei te descrever em palavras mas vc é tudo que alguém sonha, te agradeço por me dar colo no momento que eu mais precisei,agradeço pot não ne deixar, vc foi e irá ser a única que realmente me conhecez espero que dê tudo certo, quero um dia casar com vc. Não sou bom com palavras mas foi de coração, bom trabalho minha princesa, EU TE AMO,isso qur tenho vontade de gritar ao mundo.></textarea>
      </div>
    </div>
  </div>

  <script>
    // Música de fundo controle
    const music = document.getElementById('bg-music');
    const btn = document.querySelector('.music-control');
    let isPlaying = false;

    function toggleMusic() {
      if (isPlaying) {
        music.pause();
        btn.textContent = '🎵';
      } else {
        music.play();
        btn.textContent = '⏸️';
      }
      isPlaying = !isPlaying;
    }

    // Para atualizar aria-pressed do envelope para acessibilidade
    function toggleAria(el) {
      const pressed = el.getAttribute('aria-pressed') === 'true';
      el.setAttribute('aria-pressed', !pressed);
    }

    // Lógica para as palavras Love flutuantes
    const container = document.querySelector('.love-container');
    const count = 50; // número de "Love"
    let placedPositions = [];

    function isOverlapping(x1, y1, w1, h1, x2, y2, w2, h2) {
      return !(x1 + w1 < x2 || x1 > x2 + w2 || y1 + h1 < y2 || y1 > y2 + h2);
    }

    function generateLoves() {
      container.innerHTML = '';
      placedPositions = [];

      for(let i=0; i<count; i++) {
        const love = document.createElement('div');
        love.classList.add('floating-love');
        love.textContent = 'Love';
        container.appendChild(love);

        // Obter tamanho após renderizar
        const rect = love.getBoundingClientRect();
        const w = rect.width;
        const h = rect.height;

        let tries = 0;
        const maxTries = 100;
        let posX, posY;
        let overlapping;

        do {
          posX = Math.random() * (window.innerWidth - w);
          posY = Math.random() * (window.innerHeight - h);
          overlapping = false;

          for (const pos of placedPositions) {
            if (isOverlapping(posX, posY, w, h, pos.x, pos.y, pos.w, pos.h)) {
              overlapping = true;
              break;
            }
          }

          tries++;
          if (tries > maxTries) {
            overlapping = false;
            break;
          }
        } while (overlapping);

        placedPositions.push({x: posX, y: posY, w: w, h: h});
        love.style.left = posX + 'px';
        love.style.top = posY + 'px';
        love.style.animationDelay = `${Math.random() * 10}s`;
      }
    }

    // Inicializa as palavras Love
    generateLoves();

    // Atualiza no resize da janela
    window.addEventListener('resize', () => {
      generateLoves();
    });
  </script>
</body>
</html>
