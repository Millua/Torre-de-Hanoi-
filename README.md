[index.html](https://github.com/user-attachments/files/23112316/index.html)
import ThumbmarkjsThumbmarkjs from "https://esm.sh/@thumbmarkjs/thumbmarkjs";
import SpeechkitSpeechkitAudioPlayer from "https://esm.sh/@speechkit/speechkit-audio-player";[script.js](https://github.com/user-attachments/files/23112328/script.js)
<!DOCTYPE html>
<html lang="en">

  <head>
    <meta charset="UTF-8">
    <title>Torre de Hanoi</title>
    

  </head>
    
  <body>
  <!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Torre de Hanoi - Edição Global</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Poppins', sans-serif;
      min-height: 100vh;
      background: linear-gradient(145deg, #0f2027, #203a43, #2c5364);
      color: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 40px 20px;
      overflow-x: hidden;
      transition: all 0.5s ease;
    }

    h1 {
      font-size: 2.8rem;
      margin-bottom: 25px;
      text-transform: uppercase;
      letter-spacing: 3px;
      text-shadow: 0 3px 15px rgba(0, 0, 0, 0.6);
      animation: fadeInTitle 1s ease-in-out;
    }

    @keyframes fadeInTitle {
      from { opacity: 0; transform: translateY(-20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .container {
      background: rgba(255, 255, 255, 0.08);
      border-radius: 25px;
      padding: 35px;
      backdrop-filter: blur(12px);
      box-shadow: 0 15px 40px rgba(0, 0, 0, 0.4);
      width: 100%;
      max-width: 950px;
      transition: transform 0.3s ease;
    }

    .stats {
      display: flex;
      justify-content: space-around;
      margin-bottom: 25px;
      font-size: 1.2rem;
      background: rgba(0, 0, 0, 0.25);
      padding: 20px;
      border-radius: 15px;
      box-shadow: inset 0 2px 10px rgba(0, 0, 0, 0.2);
    }

    #scoreboard {
      text-align: center;
      margin: 25px 0;
      font-size: 1.1rem;
      color: #a3bffa;
      font-weight: 600;
    }

    #game-area {
      display: flex;
      justify-content: space-between;
      width: 100%;
      height: 400px;
      position: relative;
      perspective: 1200px;
    }

    .tower {
      width: 30%;
      display: flex;
      flex-direction: column-reverse;
      align-items: center;
      justify-content: flex-start;
      background: linear-gradient(180deg, rgba(255, 255, 255, 0.12), transparent);
      border-radius: 15px;
      border-bottom: 15px solid #8d5524;
      position: relative;
      cursor: pointer;
      transition: transform 0.4s ease, border-bottom-color 0.4s ease;
    }

    .tower:hover {
      transform: translateY(-8px);
    }

    .tower::after {
      content: '';
      position: absolute;
      bottom: -60px;
      width: 14px;
      height: 120px;
      background: linear-gradient(#8d5524, #5d4037);
      border-radius: 8px;
      box-shadow: 0 5px 20px rgba(0, 0, 0, 0.4);
    }

    .tower.active {
      border-bottom-color: #f1c40f;
      transform: scale(1.06);
    }

    .disk {
      height: 40px;
      margin: 5px 0;
      border-radius: 30px;
      transition: all 0.5s ease;
      color: #fff;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 700;
      text-shadow: 0 2px 5px rgba(0, 0, 0, 0.6);
      box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
      animation: slideIn 0.4s ease;
    }

    @keyframes slideIn {
      from { transform: translateY(-30px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }

    .selected {
      transform: scale(1.2) rotate(3deg);
      box-shadow: 0 0 25px rgba(241, 196, 15, 0.9);
    }

    .controls {
      display: flex;
      flex-wrap: wrap;
      gap: 20px;
      justify-content: center;
      margin-top: 35px;
    }

    button, select {
      padding: 14px 30px;
      font-size: 1.1rem;
      border: none;
      border-radius: 50px;
      background: linear-gradient(45deg, #f1c40f, #e67e22);
      color: #fff;
      cursor: pointer;
      transition: all 0.4s ease;
      box-shadow: 0 6px 20px rgba(0, 0, 0, 0.25);
      text-transform: uppercase;
      font-weight: 700;
      position: relative;
      overflow: hidden;
    }

    button:hover, select:hover {
      transform: translateY(-4px);
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.35);
      background: linear-gradient(45deg, #f39c12, #d35400);
    }

    button::after {
      content: '';
      position: absolute;
      top: 50%;
      left: 50%;
      width: 0;
      height: 0;
      background: rgba(255, 255, 255, 0.3);
      border-radius: 50%;
      transform: translate(-50%, -50%);
      transition: width 0.6s ease, height 0.6s ease;
    }

    button:hover::after {
      width: 200%;
      height: 200%;
    }

    select {
      background: #34495e;
      appearance: none;
      padding-right: 40px;
    }

    .language-select {
      position: relative;
    }

    .language-select::after {
      content: '\f078';
      font-family: 'Font Awesome 6 Free';
      font-weight: 900;
      position: absolute;
      right: 15px;
      top: 50%;
      transform: translateY(-50%);
      color: #fff;
      pointer-events: none;
    }

    .modal {
      display: none;
      position: fixed;
      z-index: 1000;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.95);
      animation: fadeIn 0.4s ease;
    }

    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }

    .modal-content {
      background: #1c2526;
      margin: 10% auto;
      padding: 35px;
      border-radius: 20px;
      width: 90%;
      max-width: 600px;
      box-shadow: 0 15px 50px rgba(0, 0, 0, 0.6);
      position: relative;
      animation: modalPop 0.4s ease;
    }

    @keyframes modalPop {
      from { transform: scale(0.9); opacity: 0; }
      to { transform: scale(1); opacity: 1; }
    }

    .close {
      position: absolute;
      top: 15px;
      right: 25px;
      font-size: 35px;
      color: #fff;
      cursor: pointer;
      transition: color 0.3s ease;
    }

    .close:hover {
      color: #f1c40f;
    }

    .high-contrast {
      background: #000;
      color: #ffeb3b;
    }

    .high-contrast button, .high-contrast select {
      background: #ffeb3b;
      color: #000;
    }

    @media (max-width: 768px) {
      h1 { font-size: 2.2rem; }
      .tower { height: 300px; }
      .disk { height: 32px; font-size: 1rem; }
      button, select { padding: 12px 25px; font-size: 1rem; }
      .stats { flex-direction: column; text-align: center; gap: 15px; }
    }
  </style>
</head>
<body>
  <h1 data-i18n="title">Torre de Hanoi - Edição Global</h1>
  <div class="container">
    <div class="stats">
      <div data-i18n="time">Tempo: <span id="time">00:00</span></div>
      <div id="timeLimitContainer" style="display:none;" data-i18n="remaining">Restante: <span id="timeRemaining">00:00</span></div>
      <div data-i18n="moves">Movimentos: <span id="moves">0</span></div>
    </div>

    <div id="scoreboard"></div>

    <div id="game-area">
      <div class="tower" data-tower="1"></div>
      <div class="tower" data-tower="2"></div>
      <div class="tower" data-tower="3"></div>
    </div>

    <div class="controls">
      <button id="startGame"><i class="fas fa-play"></i> <span data-i18n="newGame">Novo Jogo</span></button>
      <div>
        <select id="diskCount">
          <option>3</option>
          <option>4</option>
          <option>5</option>
          <option>6</option>
        </select>
      </div>
      <div>
        <select id="difficulty">
          <option value="normal" data-i18n="normal">Normal</option>
          <option value="desafio" data-i18n="challenge">Desafio</option>
        </select>
      </div>
      <div class="language-select">
        <select id="language">
          <option value="pt">🇧🇷 Português</option>
          <option value="en">🇺🇸 English</option>
          <option value="es">🇪🇸 Español</option>
        </select>
      </div>
      <button id="toggleContrast"><i class="fas fa-eye"></i> <span data-i18n="contrast">Contraste</span></button>
      <button id="openTutorial"><i class="fas fa-question"></i> <span data-i18n="tutorial">Tutorial</span></button>
    </div>

    <div id="tutorialModal" class="modal">
      <div class="modal-content">
        <span class="close" id="closeTutorial">×</span>
        <h2 data-i18n="tutorialTitle">Tutorial</h2>
        <p data-i18n="welcome"></p>
        <ul>
          <li data-i18n="rule1"></li>
          <li data-i18n="rule2"></li>
          <li data-i18n="rule3"></li>
          <li data-i18n="rule4"></li>
          <li data-i18n="rule5"></li>
        </ul>
      </div>
    </div>
  </div>

  <audio id="audioSelect" src="https://www.soundjay.com/buttons/beep-01a.mp3" preload="auto"></audio>
  <audio id="audioMove" src="https://www.soundjay.com/buttons/beep-07.mp3" preload="auto"></audio>
  <audio id="audioWin" src="https://www.soundjay.com/misc/sounds/bell-ring-01.mp3" preload="auto"></audio>

  <script>
    const translations = {
      pt: {
        title: "Torre de Hanoi - Edição Global",
        time: "Tempo:",
        remaining: "Restante:",
        moves: "Movimentos:",
        newGame: "Novo Jogo",
        normal: "Normal",
        challenge: "Desafio",
        contrast: "Contraste",
        tutorial: "Tutorial",
        tutorialTitle: "Tutorial",
        welcome: "Desafie-se na Torre de Hanoi!",
        rule1: "Mova todos os discos da torre 1 para a torre 3.",
        rule2: "Um disco maior nunca pode ficar sobre um menor.",
        rule3: "Clique para selecionar e mover discos.",
        rule4: "No modo Desafio, o tempo é seu inimigo!",
        rule5: "Movimentos ideais: 2ⁿ - 1.",
        invalidMove: "Movimento inválido!",
        perfectWin: "🎉 Vitória Perfeita!",
        win: "✅ Você venceu!",
        ideal: "ideal",
        in: "em",
        timeUp: "⏰ Tempo esgotado!"
      },
      en: {
        title: "Tower of Hanoi - Global Edition",
        time: "Time:",
        remaining: "Remaining:",
        moves: "Moves:",
        newGame: "New Game",
        normal: "Normal",
        challenge: "Challenge",
        contrast: "Contrast",
        tutorial: "Tutorial",
        tutorialTitle: "Tutorial",
        welcome: "Challenge yourself in Tower of Hanoi!",
        rule1: "Move all disks from tower 1 to tower 3.",
        rule2: "A larger disk cannot be placed on a smaller one.",
        rule3: "Click to select and move disks.",
        rule4: "In Challenge mode, time is your enemy!",
        rule5: "Ideal moves: 2ⁿ - 1.",
        invalidMove: "Invalid move!",
        perfectWin: "🎉 Perfect Victory!",
        win: "✅ You won!",
        ideal: "ideal",
        in: "in",
        timeUp: "⏰ Time's up!"
      },
      es: {
        title: "Torre de Hanói - Edición Global",
        time: "Tiempo:",
        remaining: "Restante:",
        moves: "Movimientos:",
        newGame: "Nuevo Juego",
        normal: "Normal",
        challenge: "Desafío",
        contrast: "Contraste",
        tutorial: "Tutorial",
        tutorialTitle: "Tutorial",
        welcome: "¡Desafíate en la Torre de Hanói!",
        rule1: "Mueve todos los discos de la torre 1 a la torre 3.",
        rule2: "Un disco mayor no puede estar sobre uno menor.",
        rule3: "Haz clic para seleccionar y mover discos.",
        rule4: "¡En modo Desafío, el tiempo es tu enemigo!",
        rule5: "Movimientos ideales: 2ⁿ - 1.",
        invalidMove: "¡Movimiento inválido!",
        perfectWin: "🎉 ¡Victoria Perfecta!",
        win: "✅ ¡Ganaste!",
        ideal: "ideal",
        in: "en",
        timeUp: "⏰ ¡Tiempo agotado!"
      }
    };

    let towers = [[], [], []];
    let selectedDisk = null;
    let selectedTowerIndex = null;
    let moves = 0;
    let timerInterval;
    let startTime;
    let timeLimit = 0;
    let currentDifficulty = "normal";

    function updateLanguage() {
      const lang = document.getElementById('language').value;
      document.querySelectorAll('[data-i18n]').forEach(element => {
        const key = element.getAttribute('data-i18n');
        element.innerHTML = translations[lang][key] || element.innerHTML;
        if (element.tagName === 'DIV' || element.tagName === 'SPAN') {
          element.innerHTML = `${translations[lang][key]} <span id="${key === 'time' ? 'time' : key === 'remaining' ? 'timeRemaining' : 'moves'}">${document.getElementById(key === 'time' ? 'time' : key === 'remaining' ? 'timeRemaining' : 'moves').textContent}</span>`;
        }
      });
      document.title = translations[lang].title;
    }

    function formatTime(seconds) {
      const m = Math.floor(seconds / 60);
      const s = seconds % 60;
      return `${String(m).padStart(2, '0')}:${String(s).padStart(2, '0')}`;
    }

    function updateScoreboard(diskCount, elapsedSeconds, moves) {
      const keyTime = "bestTime_" + diskCount;
      const keyMoves = "bestMoves_" + diskCount;
      let bestTime = localStorage.getItem(keyTime) || Infinity;
      let bestMoves = localStorage.getItem(keyMoves) || Infinity;
      if (elapsedSeconds < bestTime) localStorage.setItem(keyTime, elapsedSeconds);
      if (moves < bestMoves) localStorage.setItem(keyMoves, moves);
      document.getElementById('scoreboard').innerHTML = `
        Best: ${formatTime(parseInt(localStorage.getItem(keyTime)) || 0)} | ${localStorage.getItem(keyMoves) || 0} moves
      `;
    }

    function createDisks(count) {
      towers = [[], [], []];
      document.querySelectorAll('.tower').forEach(tower => {
        tower.innerHTML = '';
        tower.classList.remove('active');
      });
      const colors = ['#e74c3c', '#3498db', '#2ecc71', '#f1c40f', '#9b59b6', '#e67e22'];
      const tower1 = document.querySelector('[data-tower="1"]');
      for (let i = count; i > 0; i--) {
        const disk = document.createElement('div');
        disk.className = 'disk';
        disk.style.width = `${i * 50 + 60}px`;
        disk.style.background = `linear-gradient(45deg, ${colors[(i - 1) % colors.length]}, ${colors[i % colors.length]})`;
        disk.dataset.size = i;
        disk.textContent = i;
        tower1.appendChild(disk);
        towers[0].push(disk);
      }
    }

    function resetSelection() {
      if (selectedDisk) {
        selectedDisk.classList.remove('selected');
        const originalTower = document.querySelector(`[data-tower="${selectedTowerIndex + 1}"]`);
        originalTower.appendChild(selectedDisk);
        towers[selectedTowerIndex].push(selectedDisk);
      }
      selectedDisk = null;
      selectedTowerIndex = null;
      document.querySelectorAll('.tower').forEach(t => t.classList.remove('active'));
    }

    function handleTowerClick(towerElement, towerIndex) {
      if (selectedDisk) {
        if (towerIndex === selectedTowerIndex) {
          resetSelection();
          return;
        }
        const destinationTower = towers[towerIndex];
        const topDisk = destinationTower[destinationTower.length - 1];
        if (!topDisk || parseInt(selectedDisk.dataset.size) < parseInt(topDisk.dataset.size)) {
          destinationTower.push(selectedDisk);
          towerElement.appendChild(selectedDisk);
          moves++;
          document.getElementById('moves').textContent = moves;
          document.getElementById('audioMove').play();
          selectedDisk.classList.remove('selected');
          selectedDisk = null;
          selectedTowerIndex = null;
          document.querySelectorAll('.tower').forEach(t => t.classList.remove('active'));
          checkWin();
        } else {
          alert(translations[document.getElementById('language').value].invalidMove);
          resetSelection();
        }
      } else if (towers[towerIndex].length > 0) {
        selectedDisk = towers[towerIndex].pop();
        selectedTowerIndex = towerIndex;
        selectedDisk.classList.add('selected');
        document.getElementById('audioSelect').play();
        document.querySelector(`[data-tower="${towerIndex + 1}"]`).classList.add('active');
      }
    }

    function vibrateDevice(pattern = [100, 50, 100]) {
      if ('vibrate' in navigator) {
        navigator.vibrate(pattern); // Padrão de vibração: 100ms, pausa 50ms, 100ms
      }
    }

    function checkWin() {
      const lang = document.getElementById('language').value;
      const diskCount = parseInt(document.getElementById('diskCount').value);
      if (towers[2].length === diskCount) {
        clearInterval(timerInterval);
        const elapsedSeconds = Math.floor((new Date() - startTime) / 1000);
        const perfectMoves = Math.pow(2, diskCount) - 1;
        document.getElementById('audioWin').play();
        vibrateDevice([200, 100, 200, 100, 200]); // Vibração de vitória mais elaborada
        setTimeout(() => {
          alert(moves === perfectMoves
            ? `${translations[lang].perfectWin} ${moves} ${translations[lang].moves.toLowerCase()} ${translations[lang].in} ${formatTime(elapsedSeconds)}!`
            : `${translations[lang].win} ${moves} ${translations[lang].moves.toLowerCase()} (${perfectMoves} ${translations[lang].ideal}) ${translations[lang].in} ${formatTime(elapsedSeconds)}!`);
          updateScoreboard(diskCount, elapsedSeconds, moves);
        }, 100);
      }
    }

    function updateTimer() {
      const elapsedSeconds = Math.floor((new Date() - startTime) / 1000);
      document.getElementById('time').textContent = formatTime(elapsedSeconds);
      if (currentDifficulty === "desafio") {
        const remaining = timeLimit - elapsedSeconds;
        if (remaining <= 0) {
          clearInterval(timerInterval);
          alert(translations[document.getElementById('language').value].timeUp);
          return;
        }
        document.getElementById('timeRemaining').textContent = formatTime(remaining);
      }
    }

    document.querySelectorAll('.tower').forEach(tower => {
      tower.addEventListener('click', function() {
        const towerIndex = parseInt(this.dataset.tower) - 1;
        handleTowerClick(this, towerIndex);
      });
    });

    document.getElementById('openTutorial').addEventListener('click', () => {
      document.getElementById('tutorialModal').style.display = 'block';
    });

    document.getElementById('closeTutorial').addEventListener('click', () => {
      document.getElementById('tutorialModal').style.display = 'none';
    });

    window.addEventListener('click', (event) => {
      if (event.target === document.getElementById('tutorialModal')) {
        document.getElementById('tutorialModal').style.display = 'none';
      }
    });

    document.getElementById('toggleContrast').addEventListener('click', () => {
      document.body.classList.toggle('high-contrast');
    });

    document.getElementById('startGame').addEventListener('click', () => {
      const diskCount = parseInt(document.getElementById('diskCount').value);
      currentDifficulty = document.getElementById('difficulty').value;
      clearInterval(timerInterval);
      moves = 0;
      document.getElementById('moves').textContent = '0';
      createDisks(diskCount);
      startTime = new Date();
      timeLimit = currentDifficulty === "desafio" ? diskCount * 60 : 0;
      document.getElementById('timeLimitContainer').style.display = currentDifficulty === "desafio" ? 'block' : 'none';
      timerInterval = setInterval(updateTimer, 1000);
    });

    document.getElementById('language').addEventListener('change', updateLanguage);

    // Inicialização
    createDisks(3);
    updateLanguage();
  </script>
</body>
</html>
    <script type="module" src="./script.js"></script>

  </body>
  
</html>
