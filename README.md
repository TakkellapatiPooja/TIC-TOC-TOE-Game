# TIC-TOC-TOE-Game
A classic Tic Tac Toe game built using HTML, CSS, and JavaScript. It features an interactive UI, smooth gameplay, and real-time win/draw detection. A fun project to understand DOM manipulation and game logic.
code:
<!DOCTYPE html>
<html>
<head>
<title>Tic Tac Toe vs Computer</title>

<style>
body {
    font-family: Arial;
    text-align: center;
    background: #853d3d;
}

.board {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    gap: 10px;
    justify-content: center;
    margin-top: 30px;
}

button.cell {
    width: 100px;
    height: 100px;
    font-size: 36px;
    cursor: pointer;
}

#status {
    margin-top: 20px;
    font-size: 20px;
    font-weight: bold;
}

.reset {
    margin-top: 15px;
    padding: 8px 18px;
}

/* Celebration Overlay */
.overlay {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.85);
    color: white;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}

.overlay h2 {
    font-size: 42px;
    animation: pop 0.8s ease-in-out infinite alternate;
}

/* Fireworks dots */
.spark {
    position: absolute;
    width: 6px;
    height: 6px;
    background: gold;
    border-radius: 50%;
    animation: sparkle 1.2s infinite;
}

@keyframes sparkle {
    0% { transform: scale(0); opacity: 1; }
    100% { transform: scale(2); opacity: 0; }
}

@keyframes pop {
    from { transform: scale(1); }
    to { transform: scale(1.1); }
}
</style>
</head>

<body>

<h1>Tic Tac Toe</h1>
<p>You = X | Computer = O</p>

<div class="board">
    <button class="cell" onclick="playerMove(0)"></button>
    <button class="cell" onclick="playerMove(1)"></button>
    <button class="cell" onclick="playerMove(2)"></button>
    <button class="cell" onclick="playerMove(3)"></button>
    <button class="cell" onclick="playerMove(4)"></button>
    <button class="cell" onclick="playerMove(5)"></button>
    <button class="cell" onclick="playerMove(6)"></button>
    <button class="cell" onclick="playerMove(7)"></button>
    <button class="cell" onclick="playerMove(8)"></button>
</div>

<div id="status">Your Turn</div>
<button class="reset" onclick="resetGame()">Reset Game</button>

<div class="overlay" id="overlay">
    <h2 id="message"></h2>
</div>

<script>
let board = ["","","","","","","","",""];
let gameOver = false;

function playerMove(index) {
    if (board[index] !== "" || gameOver) return;

    board[index] = "X";
    updateBoard();

    if (checkWinner("X")) {
        showWinMessage();
        gameOver = true;
        return;
    }

    if (!board.includes("")) {
        document.getElementById("status").innerText = "It's a Draw!";
        gameOver = true;
        return;
    }

    document.getElementById("status").innerText = "Computer Thinking...";
    setTimeout(computerMove, 500);
}

function computerMove() {
    let empty = board.map((v,i) => v=="" ? i : null).filter(v=>v!==null);
    let move = empty[Math.floor(Math.random() * empty.length)];
    board[move] = "O";
    updateBoard();

    if (checkWinner("O")) {
        showLoseMessage();
        gameOver = true;
        return;
    }

    if (!board.includes("")) {
        document.getElementById("status").innerText = "It's a Draw!";
        gameOver = true;
        return;
    }

    document.getElementById("status").innerText = "Your Turn";
}

function updateBoard() {
    document.querySelectorAll(".cell").forEach((btn,i)=>{
        btn.innerText = board[i];
    });
}

function checkWinner(p) {
    const wins = [
        [0,1,2],[3,4,5],[6,7,8],
        [0,3,6],[1,4,7],[2,5,8],
        [0,4,8],[2,4,6]
    ];
    return wins.some(w => w.every(i => board[i] === p));
}

/* WIN animation */
function showWinMessage() {
    const overlay = document.getElementById("overlay");
    document.getElementById("message").innerText = "You Won 🎊";
    overlay.style.display = "flex";

    for (let i=0;i<25;i++) {
        let s = document.createElement("div");
        s.className = "spark";
        s.style.top = Math.random()*100 + "%";
        s.style.left = Math.random()*100 + "%";
        overlay.appendChild(s);
    }
}

/* LOSE message */
function showLoseMessage() {
    document.getElementById("status").innerText = "Try Again 🐥";
}

function resetGame() {
    board = ["","","","","","","","",""];
    gameOver = false;
    document.getElementById("status").innerText = "Your Turn";
    updateBoard();
    const overlay = document.getElementById("overlay");
    overlay.style.display = "none";
    overlay.innerHTML = '<h2 id="message"></h2>';
}
</script>

</body>
</html>
Pictures:
<img width="1147" height="821" alt="image" src="https://github.com/user-attachments/assets/c01cddcf-da7e-4e8a-b935-9196b371ad28" />
<img width="1172" height="831" alt="image" src="https://github.com/user-attachments/assets/a356d111-9d29-41d5-af9f-d188170988d2" />
<img width="1243" height="748" alt="image" src="https://github.com/user-attachments/assets/90ed3852-13d3-4113-8960-65bf01132146" />



