# task2-LGMVIP-JAVA
TI-TAC-TOE Game
#HTML

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tic-Tac-Toe</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <h1>Tic-Tac-Toe</h1>
  <div id="board" class="board">
    <div class="cell" data-cell></div>
    <div class="cell" data-cell></div>
    <div class="cell" data-cell></div>
    <div class="cell" data-cell></div>
    <div class="cell" data-cell></div>
    <div class="cell" data-cell></div>
    <div class="cell" data-cell></div>
    <div class="cell" data-cell></div>
    <div class="cell" data-cell></div>
  </div>
  <script src="script.js"></script>
</body>
</html>


# CSS

body {
  font-family: Arial, sans-serif;
  text-align: center;
}

.board {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  grid-template-rows: repeat(3, 100px);
  gap: 2px;
  margin-top: 20px;
}

.cell {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 2rem;
  background-color: lightgray;
  cursor: pointer;
}

.cell[data-cell]:hover {
  background-color: lightblue;
}


#JAVASCRIPT 

const board = document.getElementById('board');
const cells = document.querySelectorAll('[data-cell]');
const winPatterns = [
  [0, 1, 2],
  [3, 4, 5],
  [6, 7, 8],
  [0, 3, 6],
  [1, 4, 7],
  [2, 5, 8],
  [0, 4, 8],
  [2, 4, 6]
];
let currentPlayer = 'X';
let gameEnded = false;

cells.forEach(cell => cell.addEventListener('click', handleClick));

function handleClick() {
  if (gameEnded) return;

  if (this.textContent === '') {
    this.textContent = currentPlayer;
    if (checkWin(currentPlayer)) {
      alert(`${currentPlayer} wins!`);
      gameEnded = true;
    } else if (isBoardFull()) {
      alert("It's a draw!");
      gameEnded = true;
    } else {
      currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
    }
  }
}

function checkWin(player) {
  return winPatterns.some(pattern => {
    return pattern.every(index => cells[index].textContent === player);
  });
}

function isBoardFull() {
  return [...cells].every(cell => cell.textContent !== '');
}

