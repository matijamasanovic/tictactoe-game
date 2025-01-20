# tictactoe-game

A simple and interactive Tic Tac Toe game built using HTML, CSS, and JavaScript.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [How to Play](#how-to-play)
- [Game Logic](#game-logic)
- [Getting Started](#getting-started)
- [Preview](#preview)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

This is a browser-based implementation of the classic Tic Tac Toe game. It allows two players to take turns and play on a 3x3 grid. The game declares a winner when a player successfully aligns three marks horizontally, vertically, or diagonally. If the grid is filled without a winner, the game ends in a draw.

## Features

- Interactive game board
- Real-time status updates for the current player's turn
- Winner and draw detection
- Restart functionality to play again

## How to Play

1. Open the game in a web browser.
2. Player X goes first. Click on any empty cell to make your move.
3. Players take turns marking a cell until one player wins or the game ends in a draw.
4. If you want to restart the game, click the **Restart** button.

## Game Logic

The game's logic is implemented in JavaScript with the following key components:

- **Win Conditions**: An array defining all possible winning combinations of cells.
- **State Management**: The `options` array keeps track of the current state of the board.
- **Winner Detection**: Checks if any player meets a win condition after each move.
- **Restart Functionality**: Resets the board and game state for a new round.

### Code Highlights

#### Initialize the Game
```javascript
function initializeGame(){
    cells.forEach(cell => cell.addEventListener('click', cellClicked));
    restartBtn.addEventListener('click', restartGame);
    statusText.textContent = `${currentPlayer}'s turn!`;
    running = true;
}
```

#### Cell Click Logic
```javascript
function cellClicked(cellIndex) { 
     cellIndex = this.getAttribute("cellIndex");

    if(options[cellIndex] != "" || !running) {
        return;
    }

    updateCell(this, cellIndex);
    CheckWinner();
}
```

#### Check Winner
```javascript
function CheckWinner() {
    let roundWon = false;

    for(let i = 0; i < winConditions.length; i++) {
        const condition = winConditions[i];
        const cellA = options[condition[0]];
        const cellB = options[condition[1]];
        const cellC = options[condition[2]];

        if (cellA == '' || cellB == '' || cellC == '') {
            continue;
        } 
        if(cellA == cellB && cellB == cellC) {
            roundWon = true;
            break;
        }
    }

    if (roundWon) {
        statusText.textContent = `${currentPlayer} wins!`;
        restartBtn.style.backgroundColor = 'green';
        running = false;
    } else if(!options.includes('')) {
        statusText.textContent = `Draw!`;
        restartBtn.style.backgroundColor = 'green';
    } else {
        changePlayer();
    }
}
```
