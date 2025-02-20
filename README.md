<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  <title>AustinWrap - Casino Chaos</title>
  <link href="https://fonts.googleapis.com/css2?family=Luckiest+Guy&family=Poppins:wght@700&display=swap" rel="stylesheet">
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    html, body {
      width: 100%;
      height: 100%;
      overflow: hidden;
      font-family: 'Poppins', sans-serif;
      background: #2a1b3d; /* Casino purple */
      touch-action: manipulation; /* iPhone optimization */
      -webkit-user-select: none;
      -webkit-tap-highlight-color: transparent;
    }

    /* Animations */
    @keyframes spinReel {
      0% { transform: translateY(0); }
      100% { transform: translateY(-300%); } /* Extended for smooth cycling */
    }
    @keyframes jackpotFlash {
      0% { text-shadow: 0 0 10px #ffd700; }
      50% { text-shadow: 0 0 30px #ff4500, 0 0 50px #ffd700; }
      100% { text-shadow: 0 0 10px #ffd700; }
    }
    @keyframes chaosBg {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }
    @keyframes popIn {
      0% { transform: scale(0); opacity: 0; }
      100% { transform: scale(1); opacity: 1; }
    }

    /* Splash Screen */
    #splash {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: linear-gradient(135deg, #2a1b3d, #ff4500, #ffd700, #2a1b3d);
      background-size: 400% 400%;
      animation: chaosBg 5s infinite;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      z-index: 20;
      transition: opacity 0.8s ease;
    }
    #brand {
      font-family: 'Luckiest Guy', cursive;
      font-size: 14vw;
      color: #fff;
      text-transform: uppercase;
      letter-spacing: 5px;
      text-shadow: 0 0 20px #ff4500, 2px 2px 0 #000;
      animation: jackpotFlash 1s infinite;
    }
    #enterBtn {
      width: 220px;
      height: 90px;
      background: #ffd700;
      border: 4px solid #ff4500;
      border-radius: 15px;
      cursor: pointer;
      position: relative;
      overflow: hidden;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
    }
    #enterBtn::before {
      content: 'HIT THE TABLES';
      position: absolute;
      top: 50%; left: 50%;
      transform: translate(-50%, -50%);
      font-family: 'Luckiest Guy', cursive;
      font-size: 2.2em;
      color: #2a1b3d;
      text-shadow: 0 0 10px #ff4500;
    }
    #enterBtn:hover {
      transform: scale(1.1);
      box-shadow: 0 0 30px #ffd700;
    }

    /* Main Content */
    #main {
      display: none;
      width: 100%;
      height: 100%;
      overflow-y: auto;
      background: #2a1b3d;
      padding: 20px;
      position: relative;
    }
    #bank {
      position: fixed;
      top: 10px; left: 10px;
      font-family: 'Luckiest Guy', cursive;
      font-size: 1.8em;
      color: #ffd700;
      background: rgba(0, 0, 0, 0.9);
      padding: 10px 20px;
      border-radius: 10px;
      border: 2px solid #ff4500;
      z-index: 30;
    }
    .section-heading {
      font-family: 'Luckiest Guy', cursive;
      font-size: 6vw;
      color: #ff4500;
      text-align: center;
      margin: 20px 0;
      text-shadow: 0 0 15px #ffd700;
    }
    .links-container {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 15px;
      margin-bottom: 40px;
    }
    .link-box {
      background: #3e2e5c;
      border: 2px solid #ffd700;
      border-radius: 8px;
      width: 90%;
      max-width: 500px;
      padding: 15px;
      text-align: center;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
    }
    .link-box:hover {
      transform: scale(1.05);
      box-shadow: 0 0 20px #ff4500;
    }
    .link-box a {
      text-decoration: none;
      color: #fff;
      font-size: 1.2em;
      font-weight: 700;
      display: block;
    }

    /* Game Pop-outs */
    .game-popout {
      position: absolute;
      background: #1a1a1a;
      border: 3px solid #ff4500;
      border-radius: 10px;
      padding: 15px;
      color: #fff;
      z-index: 25;
      cursor: move;
      animation: popIn 0.3s ease;
      width: 320px;
      box-shadow: 0 0 15px rgba(255, 69, 0, 0.5);
    }
    .game-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 10px;
    }
    .game-title {
      font-family: 'Luckiest Guy', cursive;
      font-size: 1.6em;
      color: #ffd700;
    }
    .game-controls button {
      background: #ff4500;
      border: none;
      color: #fff;
      padding: 5px 10px;
      cursor: pointer;
      border-radius: 5px;
      font-family: 'Poppins', sans-serif;
      font-weight: 700;
    }
    .game-controls button:hover {
      background: #ffd700;
      color: #2a1b3d;
    }
    .slot-reels {
      display: flex;
      justify-content: center;
      gap: 10px;
      overflow: hidden;
      height: 80px;
      background: #000;
      padding: 10px;
      border-radius: 5px;
    }
    .reel {
      font-size: 2.5em;
      width: 60px;
      height: 60px;
      text-align: center;
      line-height: 60px;
      animation: spinReel 1s infinite linear paused;
    }
    .game-btn {
      background: #ffd700;
      border: none;
      padding: 10px 20px;
      font-family: 'Luckiest Guy', cursive;
      font-size: 1.2em;
      color: #2a1b3d;
      cursor: pointer;
      border-radius: 5px;
      margin: 5px 0;
      width: 100%;
      transition: background 0.3s ease;
    }
    .game-btn:hover {
      background: #ff4500;
      color: #fff;
    }
    #blackjack-hand, #dealer-hand {
      font-size: 1.5em;
      margin: 10px 0;
    }
    #blackjack-result {
      font-size: 1.2em;
      color: #ffd700;
      margin: 10px 0;
    }
    #allin-result {
      font-size: 1.2em;
      color: #ffd700;
      margin: 10px 0;
    }

    /* iPhone Optimization */
    @media (max-width: 600px) {
      #brand { font-size: 12vw; }
      #enterBtn { width: 180px; height: 70px; }
      #enterBtn::before { font-size: 1.8em; }
      #bank { font-size: 1.4em; padding: 5px 15px; }
      .section-heading { font-size: 8vw; }
      .link-box a { font-size: 1em; }
      .game-title { font-size: 1.3em; }
      .reel { font-size: 2em; width: 50px; height: 50px; line-height: 50px; }
      .game-popout { width: 280px; }
      .game-btn { font-size: 1em; }
    }
  </style>
</head>
<body>
  <!-- Splash Screen -->
  <div id="splash">
    <h1 id="brand">AustinWrap</h1>
    <button id="enterBtn"></button>
  </div>

  <!-- Main Content -->
  <div id="main">
    <div id="bank">Bank: 1,000,000</div>
    <div class="section-heading">Casino Chaos</div>
    <div class="links-container">
      <div class="link-box">
        <a href="https://www.etsy.com/listing/1817498956/nice-try-diddy-hoodie-affordable-unisex" target="_blank">Nice Try Diddy Hoodie</a>
      </div>
      <div class="link-box">
        <a href="https://www.etsy.com/listing/1833649264/unisex-heavy-blend-hooded-sweatshirt" target="_blank">Unisex Heavy Blend Hooded Sweatshirt</a>
      </div>
      <div class="link-box">
        <a href="https://austinwrap.github.io/bad-mailman/" target="_blank">Bad Mailman Game</a>
      </div>
      <div class="link-box">
        <a href="https://www.youtube.com/@austinwrap" target="_blank">YouTube</a>
      </div>
      <div class="link-box">
        <a href="https://www.tiktok.com/@austinwrap" target="_blank">TikTok</a>
      </div>
      <div class="link-box">
        <a href="https://www.instagram.com/austinwrap" target="_blank">Instagram</a>
      </div>
      <div class="link-box">
        <a href="https://twitter.com/austinwrap" target="_blank">Twitter</a>
      </div>
      <div class="link-box">
        <a href="https://www.twitch.tv/austinwrap" target="_blank">Twitch</a>
      </div>
      <div class="link-box">
        <a href="https://discord.gg/austinwrap" target="_blank">Discord</a>
      </div>
    </div>

    <!-- Game Pop-outs -->
    <div class="game-popout" id="game-slots" style="left: 50px; top: 50px;">
      <div class="game-header">
        <span class="game-title">Triple Jackpot Slots</span>
        <div class="game-controls">
          <button onclick="this.parentElement.parentElement.parentElement.style.height='30px';">Min</button>
          <button onclick="this.parentElement.parentElement.parentElement.remove();">X</button>
        </div>
      </div>
      <div class="slot-reels" id="reels-slots">
        <div class="reel">🎰</div>
        <div class="reel">🎰</div>
        <div class="reel">🎰</div>
      </div>
      <button class="game-btn" onclick="spinSlots()">Spin (1000)</button>
    </div>
    <div class="game-popout" id="game-blackjack" style="left: 400px; top: 80px;">
      <div class="game-header">
        <span class="game-title">Blackjack Blitz</span>
        <div class="game-controls">
          <button onclick="this.parentElement.parentElement.parentElement.style.height='30px';">Min</button>
          <button onclick="this.parentElement.parentElement.parentElement.remove();">X</button>
        </div>
      </div>
      <div id="blackjack-hand">Your Hand: </div>
      <div id="dealer-hand">Dealer: </div>
      <div id="blackjack-result"></div>
      <button class="game-btn" id="blackjack-bet" onclick="startBlackjack(5000)">Bet 5,000</button>
      <button class="game-btn" id="blackjack-hit" onclick="hitBlackjack()" style="display: none;">Hit</button>
      <button class="game-btn" id="blackjack-stand" onclick="standBlackjack()" style="display: none;">Stand</button>
    </div>
    <div class="game-popout" id="game-allin" style="left: 200px; top: 350px;">
      <div class="game-header">
        <span class="game-title">All In or Nothing</span>
        <div class="game-controls">
          <button onclick="this.parentElement.parentElement.parentElement.style.height='30px';">Min</button>
          <button onclick="this.parentElement.parentElement.parentElement.remove();">X</button>
        </div>
      </div>
      <div id="allin-result"></div>
      <button class="game-btn" onclick="playAllIn()">Go All In</button>
    </div>
  </div>

  <script>
    const enterBtn = document.getElementById('enterBtn');
    const splash = document.getElementById('splash');
    const main = document.getElementById('main');
    const bankDisplay = document.getElementById('bank');
    let bankBalance = 1000000;
    let blackjackState = { playerHand: [], dealerHand: [], bet: 0 };

    enterBtn.addEventListener('click', () => {
      splash.style.opacity = 0;
      setTimeout(() => {
        splash.style.display = 'none';
        main.style.display = 'block';
        document.body.style.overflowY = 'auto';
        document.querySelectorAll('.game-popout').forEach(game => {
          makeDraggable(game);
        });
      }, 800);
    });

    function updateBank(amount) {
      bankBalance += amount;
      bankDisplay.textContent = `Bank: ${bankBalance.toLocaleString()}`;
    }

    // Slots Game
    function spinSlots() {
      if (bankBalance < 1000) {
        alert('Not enough chips, tough luck!');
        return;
      }
      updateBank(-1000);
      const reels = document.querySelectorAll('#reels-slots .reel');
      const emojis = ['🍒', '💰', '🍋', '⭐', '🎰', '💎', '7️⃣'];
      reels.forEach(reel => {
        reel.style.animationPlayState = 'running';
        let spins = Math.floor(Math.random() * 20) + 10; // 10-30 spins
        reel.style.animation = `spinReel ${spins * 0.1}s linear`;
        setTimeout(() => {
          reel.style.animation = 'none';
          reel.textContent = emojis[Math.floor(Math.random() * emojis.length)];
        }, spins * 100);
      });
      setTimeout(() => {
        checkSlotWin(reels);
      }, Math.max(...Array.from(reels).map(() => Math.floor(Math.random() * 20) + 10)) * 100);
    }

    function checkSlotWin(reels) {
      const symbols = Array.from(reels).map(reel => reel.textContent);
      if (symbols[0] === symbols[1] && symbols[1] === symbols[2]) {
        const winnings = symbols[0] === '7️⃣' ? 1000000 : 50000;
        updateBank(winnings);
        alert(`JACKPOT! You won ${winnings.toLocaleString()} chips!`);
      } else if (symbols[0] === symbols[1] || symbols[1] === symbols[2] || symbols[0] === symbols[2]) {
        updateBank(5000);
        alert('Nice! You won 5,000 chips!');
      }
    }

    // Blackjack Game
    function startBlackjack(bet) {
      if (bankBalance < bet) {
        alert('Not enough chips, tough luck!');
        return;
      }
      updateBank(-bet);
      blackjackState.bet = bet;
      const cards = ['A', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K'];
      blackjackState.playerHand = [cards[Math.floor(Math.random() * cards.length)], cards[Math.floor(Math.random() * cards.length)]];
      blackjackState.dealerHand = [cards[Math.floor(Math.random() * cards.length)], '🎴'];
      displayBlackjack();
      document.getElementById('blackjack-bet').style.display = 'none';
      document.getElementById('blackjack-hit').style.display = 'block';
      document.getElementById('blackjack-stand').style.display = 'block';
    }

    function hitBlackjack() {
      const cards = ['A', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K'];
      blackjackState.playerHand.push(cards[Math.floor(Math.random() * cards.length)]);
      displayBlackjack();
      const playerValue = calculateHand(blackjackState.playerHand);
      if (playerValue > 21) {
        endBlackjack('Bust! You lose.');
      }
    }

    function standBlackjack() {
      const cards = ['A', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K'];
      blackjackState.dealerHand[1] = cards[Math.floor(Math.random() * cards.length)];
      let dealerValue = calculateHand(blackjackState.dealerHand);
      while (dealerValue < 17) {
        blackjackState.dealerHand.push(cards[Math.floor(Math.random() * cards.length)]);
        dealerValue = calculateHand(blackjackState.dealerHand);
      }
      displayBlackjack();
      const playerValue = calculateHand(blackjackState.playerHand);
      if (dealerValue > 21 || playerValue > dealerValue) {
        updateBank(blackjackState.bet * 2);
        endBlackjack('You win!');
      } else if (playerValue === dealerValue) {
        updateBank(blackjackState.bet);
        endBlackjack('Push!');
      } else {
        endBlackjack('Dealer wins!');
      }
    }

    function displayBlackjack() {
      document.getElementById('blackjack-hand').textContent = `Your Hand: ${blackjackState.playerHand.join(' ')} (${calculateHand(blackjackState.playerHand)})`;
      document.getElementById('dealer-hand').textContent = `Dealer: ${blackjackState.dealerHand.join(' ')} (${blackjackState.dealerHand[1] === '🎴' ? '?' : calculateHand(blackjackState.dealerHand)})`;
    }

    function endBlackjack(message) {
      document.getElementById('blackjack-result').textContent = message;
      document.getElementById('blackjack-bet').style.display = 'block';
      document.getElementById('blackjack-hit').style.display = 'none';
      document.getElementById('blackjack-stand').style.display = 'none';
    }

    function calculateHand(hand) {
      let value = 0;
      let aces = 0;
      hand.forEach(card => {
        if (card === 'A') {
          aces++;
          value += 11;
        } else if (['J', 'Q', 'K'].includes(card)) {
          value += 10;
        } else if (card !== '🎴') {
          value += parseInt(card);
        }
      });
      while (value > 21 && aces > 0) {
        value -= 10;
        aces--;
      }
      return value;
    }

    // All In or Nothing Game
    function playAllIn() {
      const result = Math.random() < 0.5; // 50/50 chance
      const resultDiv = document.getElementById('allin-result');
      if (result) {
        updateBank(bankBalance); // Double it
        resultDiv.textContent = 'ALL IN WIN! You doubled your bank!';
      } else {
        bankBalance = 0;
        updateBank(0); // Lose it all
        resultDiv.textContent = 'ALL OUT! You lost everything!';
      }
    }

    function makeDraggable(element) {
      let pos1 = 0, pos2 = 0, pos3 = 0, pos4 = 0;
      element.onmousedown = dragMouseDown;

      function dragMouseDown(e) {
        e.preventDefault();
        pos3 = e.clientX;
        pos4 = e.clientY;
        document.onmouseup = closeDragElement;
        document.onmousemove = elementDrag;
      }

      function elementDrag(e) {
        e.preventDefault();
        pos1 = pos3 - e.clientX;
        pos2 = pos4 - e.clientY;
        pos3 = e.clientX;
        pos4 = e.clientY;
        element.style.top = (element.offsetTop - pos2) + "px";
        element.style.left = (element.offsetLeft - pos1) + "px";
      }

      function closeDragElement() {
        document.onmouseup = null;
        document.onmousemove = null;
      }
    }

    // iPhone touch support
    document.addEventListener('touchstart', e => {
      const target = e.target.closest('.game-popout');
      if (target) makeDraggable(target);
    });
  </script>
</body>
</html>
