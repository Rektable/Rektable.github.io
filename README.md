<html>
<head>
  <title>Game Collection</title>
  <meta charset="UTF-8">
  <style>
  html, body {
    height: 100%;
    margin: 0;
    font-family: 'Arial', sans-serif;
    overflow: hidden;
  }

  body {
    background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
  }

  #game-container {
    position: relative;
    width: 1000px;
    height: 585px;
  }

  canvas {
    display: block;
    border-radius: 10px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
  }

  /* Загрузочный экран */
  #loading-screen {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background: #000;
    border-radius: 10px;
    z-index: 50;
    overflow: hidden;
  }

  #breach-text {
    font-size: 72px;
    font-weight: bold;
    color: #ff0000;
    text-shadow: 0 0 10px #ff0000, 0 0 20px #ff0000;
    margin-bottom: 50px;
    animation: breachBlink 1.5s infinite;
  }

  @keyframes breachBlink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.3; }
  }

  #loading-bar-container {
    width: 80%;
    height: 20px;
    background: rgba(255, 255, 255, 0.1);
    border-radius: 10px;
    overflow: hidden;
    margin-bottom: 20px;
  }

  #loading-bar {
    height: 100%;
    width: 0%;
    background: linear-gradient(to right, #ff0000, #ff3333);
    border-radius: 10px;
    transition: width 0.1s linear;
  }

  #loading-text {
    font-size: 18px;
    color: #ff0000;
    text-shadow: 0 0 5px #ff0000;
  }

  .glitch-line {
    position: absolute;
    width: 100%;
    height: 2px;
    background: #ff0000;
    opacity: 0;
    animation: glitchLine 0.1s forwards;
  }

  @keyframes glitchLine {
    0% { opacity: 0; }
    50% { opacity: 0.7; }
    100% { opacity: 0; }
  }

  /* Главное меню */
  #main-menu {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: none;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background: rgba(0, 0, 0, 0.9);
    border-radius: 10px;
    z-index: 40;
  }

  #main-menu h1 {
    font-size: 48px;
    margin-bottom: 40px;
    text-shadow: 0 0 10px #00ffff, 0 0 20px #00ffff;
    letter-spacing: 3px;
  }

  .game-option {
    background: linear-gradient(to bottom, #00b4db, #0083b0);
    border: none;
    color: white;
    padding: 15px 40px;
    font-size: 20px;
    border-radius: 50px;
    cursor: pointer;
    box-shadow: 0 0 20px rgba(0, 180, 219, 0.7);
    transition: all 0.3s ease;
    outline: none;
    margin: 10px 0;
    width: 200px;
  }

  .game-option:hover {
    transform: scale(1.05);
    box-shadow: 0 0 30px rgba(0, 180, 219, 0.9);
  }

  #back-button {
    position: absolute;
    top: 20px;
    left: 20px;
    background: rgba(255, 0, 0, 0.7);
    border: none;
    color: white;
    padding: 10px 20px;
    border-radius: 5px;
    cursor: pointer;
    z-index: 45;
    display: none;
  }

  #back-button:hover {
    background: rgba(255, 0, 0, 0.9);
  }

  /* Стили для Pong */
  #pong-game {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: none;
    z-index: 30;
  }

  #pong-start-menu {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: none;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background: rgba(0, 0, 0, 0.7);
    border-radius: 10px;
    z-index: 35;
  }

  #pong-start-button {
    background: linear-gradient(to bottom, #00b4db, #0083b0);
    border: none;
    color: white;
    padding: 15px 40px;
    font-size: 24px;
    border-radius: 50px;
    cursor: pointer;
    box-shadow: 0 0 20px rgba(0, 180, 219, 0.7);
    transition: all 0.3s ease;
    outline: none;
    animation: pulse 2s infinite;
  }

  #pong-start-button:hover {
    transform: scale(1.05);
    box-shadow: 0 0 30px rgba(0, 180, 219, 0.9);
  }

  @keyframes pulse {
    0% {
      transform: scale(1);
      box-shadow: 0 0 20px rgba(0, 180, 219, 0.7);
    }
    50% {
      transform: scale(1.05);
      box-shadow: 0 0 30px rgba(0, 180, 219, 0.9);
    }
    100% {
      transform: scale(1);
      box-shadow: 0 0 20px rgba(0, 180, 219, 0.7);
    }
  }

  #pong-score-display {
    position: absolute;
    top: 20px;
    left: 0;
    width: 100%;
    display: none;
    justify-content: space-between;
    padding: 0 50px;
    box-sizing: border-box;
    font-size: 36px;
    font-weight: bold;
    text-shadow: 0 0 10px rgba(255, 255, 255, 0.7);
    z-index: 32;
  }

  #player-score, #computer-score {
    background: rgba(0, 0, 0, 0.5);
    padding: 5px 20px;
    border-radius: 10px;
  }

  #pong-victory-screen {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: none;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background: rgba(0, 0, 0, 0.85);
    border-radius: 10px;
    z-index: 36;
  }

  #victory-message {
    font-size: 48px;
    margin-bottom: 30px;
    text-shadow: 0 0 10px #ff00ff, 0 0 20px #ff00ff;
    animation: blink 1.5s infinite;
  }

  @keyframes blink {
    0%, 50% {
      opacity: 1;
    }
    51%, 100% {
      opacity: 0.3;
    }
  }

  #final-scores {
    font-size: 32px;
    margin-bottom: 40px;
    text-align: center;
  }

  #pong-restart-button {
    background: #00ffff;
    border: none;
    color: white;
    padding: 15px 40px;
    font-size: 24px;
    border-radius: 50px;
    cursor: pointer;
    box-shadow: 0 0 20px rgba(255, 65, 108, 0.7);
    transition: all 0.3s ease;
    outline: none;
  }

  #pong-restart-button:hover {
    transform: scale(1.05);
    box-shadow: 0 0 30px rgba(255, 65, 108, 0.9);
  }

  #pong-instructions {
    position: absolute;
    bottom: 20px;
    left: 0;
    width: 100%;
    text-align: center;
    font-size: 16px;
    color: rgba(255, 255, 255, 0.7);
  }

  .ball-trail {
    position: absolute;
    width: 10px;
    height: 10px;
    border-radius: 50%;
    background: rgba(255, 255, 255, 0.5);
    pointer-events: none;
    animation: fade 0.5s forwards;
  }

  @keyframes fade {
    to {
      opacity: 0;
      transform: scale(0.5);
    }
  }

  #pong-space-hint {
    position: absolute;
    bottom: 60px;
    left: 0;
    width: 100%;
    text-align: center;
    font-size: 16px;
    color: rgba(255, 255, 255, 0.7);
    animation: fadeInOut 2s infinite;
  }

  @keyframes fadeInOut {
    0%, 100% { opacity: 0.5; }
    50% { opacity: 1; }
  }

  /* Стили для Bouncing Balls */
  #balls-game {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: none;
    z-index: 30;
  }

  #balls-canvas {
    background: #000;
  }
  </style>
</head>
<body>
  <div id="game-container">
    <!-- Загрузочный экран -->
    <div id="loading-screen">
      <div id="breach-text">BREACH</div>
      <div id="loading-bar-container">
        <div id="loading-bar"></div>
      </div>
      <div id="loading-text">Нажмите ENTER для начала загрузки</div>
    </div>

    <!-- Главное меню -->
    <div id="main-menu">
      <h1>ВЫБЕРИТЕ ИГРУ</h1>
      <button class="game-option" id="pong-option">PONG</button>
      <button class="game-option" id="balls-option">BOUNCING BALLS</button>
    </div>

    <!-- Кнопка возврата в меню -->
    <button id="back-button">← МЕНЮ</button>

    <!-- Игра Pong -->
    <div id="pong-game">
      <canvas width="1000" height="585" id="pong-canvas"></canvas>
      
      <div id="pong-start-menu">
        <h1>PONG</h1>
        <button id="pong-start-button">НАЖМИТЕ ДЛЯ НАЧАЛА</button>
        <div id="pong-space-hint">Нажмите SPACE для начала</div>
        <div id="pong-instructions">
          Игрок 1: Клавиши W/S  | Игрок 2: Стрелочки Вверх/Вниз
        </div>
      </div>
      
      <div id="pong-score-display">
        <div id="player-score">0</div>
        <div id="computer-score">0</div>
      </div>
      
      <div id="pong-victory-screen">
        <div id="victory-message">Игрок ПОБЕДИЛ!</div>
        <div id="final-scores">
          Игрок: <span id="final-player-score">0</span><br>
          Соперник: <span id="final-computer-score">0</span>
        </div>
        <button id="pong-restart-button">РЕСТАРТ</button>
        <div id="pong-space-hint">Нажмите SPACE для рестарта</div>
      </div>
    </div>

    <!-- Игра Bouncing Balls -->
    <div id="balls-game">
      <canvas width="1000" height="585" id="balls-canvas"></canvas>
    </div>
  </div>

  <script>
  // ==================== ГЛОБАЛЬНЫЕ ПЕРЕМЕННЫЕ И УПРАВЛЕНИЕ ====================
  let currentGame = null;
  const loadingScreen = document.getElementById('loading-screen');
  const mainMenu = document.getElementById('main-menu');
  const backButton = document.getElementById('back-button');
  const pongOption = document.getElementById('pong-option');
  const ballsOption = document.getElementById('balls-option');
  const pongGame = document.getElementById('pong-game');
  const ballsGame = document.getElementById('balls-game');

  // Переменные для загрузки
  let loading = false;
  let loadingProgress = 0;
  let loadingInterval;

  // ==================== СИСТЕМА ЗАГРУЗКИ ====================
  function createGlitchEffect() {
    const numLines = Math.floor(Math.random() * 5) + 3;
    
    for (let i = 0; i < numLines; i++) {
      const line = document.createElement('div');
      line.className = 'glitch-line';
      line.style.top = Math.random() * 100 + '%';
      line.style.left = Math.random() * 20 + '%';
      line.style.width = Math.random() * 60 + 20 + '%';
      loadingScreen.appendChild(line);
      
      setTimeout(() => {
        if (loadingScreen.contains(line)) {
          loadingScreen.removeChild(line);
        }
      }, 200);
    }
  }

  function startLoading() {
    if (loading) return;
    
    loading = true;
    loadingText.textContent = "ЗАГРУЗКА...";
    
    const loadTime = Math.floor(Math.random() * 10) + 1;
    const stepTime = loadTime * 10;
    
    loadingInterval = setInterval(() => {
      loadingProgress += 1;
      loadingBar.style.width = loadingProgress + '%';
      
      if (Math.random() < 0.3) {
        createGlitchEffect();
      }
      
      if (loadingProgress >= 100) {
        clearInterval(loadingInterval);
        setTimeout(() => {
          loadingScreen.style.display = 'none';
          mainMenu.style.display = 'flex';
        }, 500);
      }
    }, stepTime);
  }

  // ==================== УПРАВЛЕНИЕ ИГРАМИ ====================
  function returnToMainMenu() {
    if (currentGame === 'pong') {
      pongGame.style.display = 'none';
      // Сброс состояния Pong
      resetPongGame();
    } else if (currentGame === 'balls') {
      ballsGame.style.display = 'none';
      // Остановка анимации шариков
      if (ballsAnimationId) {
        cancelAnimationFrame(ballsAnimationId);
        ballsAnimationId = null;
      }
    }
    
    mainMenu.style.display = 'flex';
    backButton.style.display = 'none';
    currentGame = null;
  }

  function startPongGame() {
    // Скрываем главное меню
    mainMenu.style.display = 'none';
    
    // Показываем игру Pong
    pongGame.style.display = 'block';
    backButton.style.display = 'block';
    currentGame = 'pong';
    
    // Показываем стартовое меню Pong
    pongStartMenu.style.display = 'flex';
    pongScoreDisplay.style.display = 'none';
    pongVictoryScreen.style.display = 'none';
    
    // Сброс состояния игры
    resetPongGameState();
  }

  function startBallsGame() {
    // Скрываем главное меню
    mainMenu.style.display = 'none';
    
    // Показываем игру Bouncing Balls
    ballsGame.style.display = 'block';
    backButton.style.display = 'block';
    currentGame = 'balls';
    initBallsGame();
  }

  // Обработчики выбора игры
  pongOption.addEventListener('click', startPongGame);
  ballsOption.addEventListener('click', startBallsGame);

  backButton.addEventListener('click', returnToMainMenu);

  // Обработчик клавиши Escape для возврата в меню
  document.addEventListener('keydown', function(e) {
    if (e.code === 'Escape' && currentGame) {
      returnToMainMenu();
    }
    
    // Обработка Enter на экране загрузки
    if (e.code === 'Enter' && loadingScreen.style.display !== 'none' && !loading) {
      startLoading();
    }
  });

  // Глитч-эффект на экране загрузки
  setInterval(() => {
    if (loadingScreen.style.display !== 'none' && !loading) {
      createGlitchEffect();
    }
  }, 800);

  // ==================== ИГРА PONG ====================
  const pongCanvas = document.getElementById('pong-canvas');
  const pongContext = pongCanvas.getContext('2d');
  const loadingText = document.getElementById('loading-text');
  const loadingBar = document.getElementById('loading-bar');
  const pongStartMenu = document.getElementById('pong-start-menu');
  const pongStartButton = document.getElementById('pong-start-button');
  const pongScoreDisplay = document.getElementById('pong-score-display');
  const playerScoreElement = document.getElementById('player-score');
  const computerScoreElement = document.getElementById('computer-score');
  const pongVictoryScreen = document.getElementById('pong-victory-screen');
  const victoryMessage = document.getElementById('victory-message');
  const finalPlayerScore = document.getElementById('final-player-score');
  const finalComputerScore = document.getElementById('final-computer-score');
  const pongRestartButton = document.getElementById('pong-restart-button');

  const grid = 15;
  const paddleHeight = grid * 5;
  const maxPaddleY = pongCanvas.height - grid - paddleHeight;

  let pongGameStarted = false;
  let pongGameActive = false;
  let playerScore = 0;
  let computerScore = 0;
  let paddleSpeed = 6;
  let ballSpeed = 2;
  let ballTrails = [];

  const leftPaddle = {
    x: grid * 2,
    y: pongCanvas.height / 2 - paddleHeight / 2,
    width: grid,
    height: paddleHeight,
    dy: 0
  };

  const rightPaddle = {
    x: pongCanvas.width - grid * 3,
    y: pongCanvas.height / 2 - paddleHeight / 2,
    width: grid,
    height: paddleHeight,
    dy: 0
  };

  const ball = {
    x: pongCanvas.width / 2,
    y: pongCanvas.height / 2,
    width: grid,
    height: grid,
    resetting: false,
    dx: 0,
    dy: 0
  };

  function resetPongGameState() {
    pongGameStarted = false;
    pongGameActive = false;
    playerScore = 0;
    computerScore = 0;
    ballTrails = [];
    
    leftPaddle.y = pongCanvas.height / 2 - paddleHeight / 2;
    rightPaddle.y = pongCanvas.height / 2 - paddleHeight / 2;
    leftPaddle.dy = 0;
    rightPaddle.dy = 0;
    
    ball.x = pongCanvas.width / 2;
    ball.y = pongCanvas.height / 2;
    ball.resetting = false;
    ball.dx = 0;
    ball.dy = 0;
    
    updateScoreDisplay();
  }

  function resetPongGame() {
    pongVictoryScreen.style.display = 'none';
    pongStartMenu.style.display = 'flex';
    pongScoreDisplay.style.display = 'none';
    resetPongGameState();
  }

  function startPongGameplay() {
    pongGameStarted = true;
    pongGameActive = true;
    pongStartMenu.style.display = 'none';
    pongScoreDisplay.style.display = 'flex';
    
    playerScore = 0;
    computerScore = 0;
    updateScoreDisplay();
    
    resetBall();
  }

  function resetBall() {
    ball.x = pongCanvas.width / 2;
    ball.y = pongCanvas.height / 2;
    ball.resetting = true;
    
    const directions = [-1, 1];
    const randomDirectionX = directions[Math.floor(Math.random() * directions.length)];
    const randomDirectionY = directions[Math.floor(Math.random() * directions.length)];
    
    setTimeout(() => {
      ball.dx = ballSpeed * randomDirectionX;
      ball.dy = ballSpeed * randomDirectionY;
      ball.resetting = false;
    }, 1500);
  }

  function updateScoreDisplay() {
    playerScoreElement.textContent = playerScore;
    computerScoreElement.textContent = computerScore;
  }

  function checkVictory() {
    if (playerScore >= 3 || computerScore >= 3) {
      pongGameActive = false;
      
      finalPlayerScore.textContent = playerScore;
      finalComputerScore.textContent = computerScore;
      
      if (playerScore >= 3) {
        victoryMessage.textContent = "ИГРОК ПОБЕДИЛ!";
        victoryMessage.style.textShadow = "0 0 10px #00ff00, 0 0 20px #00ff00";
      } else {
        victoryMessage.textContent = "СОПЕРНИК ПОБЕДИЛ!";
        victoryMessage.style.textShadow = "0 0 10px #ff0000, 0 0 20px #ff0000";
      }
      
      pongVictoryScreen.style.display = 'flex';
    }
  }

  function restartPongGame() {
    pongVictoryScreen.style.display = 'none';
    startPongGameplay();
  }

  function handleSpacePress() {
    if (!pongGameStarted && pongStartMenu.style.display !== 'none') {
      startPongGameplay();
    } else if (!pongGameActive && pongVictoryScreen.style.display === 'flex') {
      restartPongGame();
    }
  }

  function collides(obj1, obj2) {
    return obj1.x < obj2.x + obj2.width &&
           obj1.x + obj1.width > obj2.x &&
           obj1.y < obj2.y + obj2.height &&
           obj1.y + obj1.height > obj2.y;
  }

  function createBallTrail(x, y) {
    ballTrails.push({
      x: x,
      y: y,
      life: 1
    });
  }

  function updateBallTrails() {
    for (let i = ballTrails.length - 1; i >= 0; i--) {
      ballTrails[i].life -= 0.05;
      if (ballTrails[i].life <= 0) {
        ballTrails.splice(i, 1);
      }
    }
  }

  function drawBallTrails() {
    ballTrails.forEach(trail => {
      const alpha = trail.life * 0.5;
      pongContext.fillStyle = `rgba(255, 255, 255, ${alpha})`;
      pongContext.beginPath();
      pongContext.arc(trail.x, trail.y, 5, 0, Math.PI * 2);
      pongContext.fill();
    });
  }

  function pongLoop() {
    requestAnimationFrame(pongLoop);
    
    if (currentGame !== 'pong' || !pongGameActive) return;
    
    const gradient = pongContext.createLinearGradient(0, 0, 0, pongCanvas.height);
    gradient.addColorStop(0, '#0f0c29');
    gradient.addColorStop(0.5, '#302b63');
    gradient.addColorStop(1, '#24243e');
    pongContext.fillStyle = gradient;
    pongContext.fillRect(0, 0, pongCanvas.width, pongCanvas.height);

    leftPaddle.y += leftPaddle.dy;
    rightPaddle.y += rightPaddle.dy;

    if (leftPaddle.y < grid) {
      leftPaddle.y = grid;
    } else if (leftPaddle.y > maxPaddleY) {
      leftPaddle.y = maxPaddleY;
    }

    if (rightPaddle.y < grid) {
      rightPaddle.y = grid;
    } else if (rightPaddle.y > maxPaddleY) {
      rightPaddle.y = maxPaddleY;
    }

    const paddleGradient = pongContext.createLinearGradient(0, 0, 0, paddleHeight);
    paddleGradient.addColorStop(0, '#00b4db');
    paddleGradient.addColorStop(1, '#0083b0');
    pongContext.fillStyle = paddleGradient;
    pongContext.fillRect(leftPaddle.x, leftPaddle.y, leftPaddle.width, leftPaddle.height);
    pongContext.fillRect(rightPaddle.x, rightPaddle.y, rightPaddle.width, rightPaddle.height);

    if (!ball.resetting) {
      ball.x += ball.dx;
      ball.y += ball.dy;

      createBallTrail(ball.x + ball.width/2, ball.y + ball.height/2);

      if (ball.y < grid) {
        ball.y = grid;
        ball.dy *= -1;
      } else if (ball.y + grid > pongCanvas.height - grid) {
        ball.y = pongCanvas.height - grid * 2;
        ball.dy *= -1;
      }

      if (ball.x < 0 && !ball.resetting) {
        computerScore++;
        updateScoreDisplay();
        checkVictory();
        if (pongGameActive) resetBall();
      } else if (ball.x > pongCanvas.width && !ball.resetting) {
        playerScore++;
        updateScoreDisplay();
        checkVictory();
        if (pongGameActive) resetBall();
      }

      if (collides(ball, leftPaddle)) {
        ball.dx *= -1.05;
        ball.x = leftPaddle.x + leftPaddle.width;
        
        const hitPos = (ball.y - leftPaddle.y) / leftPaddle.height;
        ball.dy = (hitPos - 0.5) * 8;
      } else if (collides(ball, rightPaddle)) {
        ball.dx *= -1.05;
        ball.x = rightPaddle.x - ball.width;
        
        const hitPos = (ball.y - rightPaddle.y) / rightPaddle.height;
        ball.dy = (hitPos - 0.5) * 8;
      }
    }

    pongContext.fillStyle = '#ffffff';
    pongContext.shadowColor = '#00ffff';
    pongContext.shadowBlur = 10;
    pongContext.beginPath();
    pongContext.arc(ball.x + ball.width/2, ball.y + ball.height/2, ball.width/2, 0, Math.PI * 2);
    pongContext.fill();
    pongContext.shadowBlur = 0;

    drawBallTrails();
    updateBallTrails();

    pongContext.fillStyle = 'rgba(255, 255, 255, 0.3)';
    pongContext.fillRect(0, 0, pongCanvas.width, grid);
    pongContext.fillRect(0, pongCanvas.height - grid, pongCanvas.width, pongCanvas.height);

    pongContext.fillStyle = 'rgba(255, 255, 255, 0.2)';
    for (let i = grid; i < pongCanvas.height - grid; i += grid * 2) {
      pongContext.fillRect(pongCanvas.width / 2 - grid / 2, i, grid, grid);
    }
  }

  pongStartButton.addEventListener('click', startPongGameplay);
  pongRestartButton.addEventListener('click', restartPongGame);

  // Обработчики клавиш для Pong
  document.addEventListener('keydown', function(e) {
    if (currentGame !== 'pong') return;
    
    if (e.code === 'Space') {
      handleSpacePress();
      return;
    }

    if (!pongGameActive) return;

    if (e.key === 'ArrowUp') {
      rightPaddle.dy = -paddleSpeed;
    } else if (e.key === 'ArrowDown') {
      rightPaddle.dy = paddleSpeed;
    }

    if (e.key === 'w' || e.key === 'W' || e.key === 'Ц' || e.key === 'ц') {
      leftPaddle.dy = -paddleSpeed;
    } else if (e.key === 's' || e.key === 'S' || e.key === 'Ы' || e.key === 'ы') {
      leftPaddle.dy = paddleSpeed;
    }
  });

  document.addEventListener('keyup', function(e) {
    if (currentGame !== 'pong') return;
    
    if (!pongGameActive) return;

    if (e.key === 'ArrowUp' || e.key === 'ArrowDown') {
      rightPaddle.dy = 0;
    }

    if (e.key === 'w' || e.key === 'W' || e.key === 's' || e.key === 'S' || e.key === 'Ц' || e.key === 'ц' || e.key === 'Ы' || e.key === 'ы') {
      leftPaddle.dy = 0;
    }
  });

  // ==================== ИГРА BOUNCING BALLS ====================
  const ballsCanvas = document.getElementById('balls-canvas');
  const ballsCtx = ballsCanvas.getContext('2d');
  let ballsAnimationId = null;
  let balls = [];

  function initBallsGame() {
    const width = ballsCanvas.width;
    const height = ballsCanvas.height;

    // Очищаем предыдущие шарики
    balls = [];

    // Конструктор шарика
    function Ball(x, y, velX, velY, color, size) {
      this.x = x;
      this.y = y;
      this.velX = velX;
      this.velY = velY;
      this.color = color;
      this.size = size;
    }

    // Метод рисования шарика
    Ball.prototype.draw = function() {
      ballsCtx.beginPath();
      ballsCtx.fillStyle = this.color;
      ballsCtx.arc(this.x, this.y, this.size, 0, 2 * Math.PI);
      ballsCtx.fill();
    }

    // Метод обновления позиции шарика
    Ball.prototype.update = function() {
      // Проверка столкновения с правой/левой границей
      if ((this.x + this.size) >= width || (this.x - this.size) <= 0) {
        this.velX = -(this.velX);    
      }

      // Проверка столкновения с верхней/нижней границей
      if ((this.y + this.size) >= height || (this.y - this.size) <= 0) {
        this.velY = -(this.velY);
      }
      
      this.x += this.velX;
      this.y += this.velY;
    }

    // Метод обнаружения столкновений между шариками
    Ball.prototype.collisionDetect = function() {
      for (let j = 0; j < balls.length; j++) {
        if (!(this === balls[j])) {
          const dx = this.x - balls[j].x;
          const dy = this.y - balls[j].y;
          const distance = Math.sqrt(dx * dx + dy * dy);
          
          if (distance < this.size + balls[j].size) {
            // Изменение цвета при столкновении
            this.color = balls[j].color = 'rgb(' +
              Math.floor(Math.random() * 255) + ',' +
              Math.floor(Math.random() * 255) + ',' +
              Math.floor(Math.random() * 255) + ')';
          }
        }
      }
    }

    // Создание массива шариков
    for (let i = 0; i < 30; i++) {
      let size = Math.random() * 30 + 10;
      let ball = new Ball(
        Math.random() * (width - size * 2) + size,
        Math.random() * (height - size * 2) + size,
        (Math.random() - 0.5) * 5,
        (Math.random() - 0.5) * 5,
        'rgb(' + Math.floor(Math.random() * 255) + ',' +
        Math.floor(Math.random() * 255) + ',' +
        Math.floor(Math.random() * 255) + ')', 
        size
      );
      balls.push(ball);
    }

    // Функция анимации
    function ballsLoop() {
      if (currentGame !== 'balls') return;
      
      // Создание эффекта следа с прозрачностью
      ballsCtx.fillStyle = 'rgba(0, 0, 0, 0.25)';
      ballsCtx.fillRect(0, 0, width, height);

      for (let i = 0; i < balls.length; i++) {
        balls[i].draw();
        balls[i].update();
        balls[i].collisionDetect();
      }
      
      ballsAnimationId = requestAnimationFrame(ballsLoop);
    }

    // Запуск анимации
    ballsLoop();
  }

  // Запуск игрового цикла Pong
  pongLoop();
  </script>
</body>
</html>
