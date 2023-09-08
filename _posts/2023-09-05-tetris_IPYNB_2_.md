---

---

```python
%%html
<!DOCTYPE html>
<html>
<head>
    <title>Tetris Game</title>
    <style>
        /* Add your Tetris CSS styling here */
        /* ... */
    </style>
</head>
<body>
    <div class="game-container">
        <canvas id="tetris"></canvas>
    </div>
    <div class="score-container">
        <p>Score: <span id="score">0</span></p>
        <p id="game-over">Game Over</p>
    </div>

    <div class="high-scores">
        <h2>High Scores</h2>
        <ul id="high-scores-list"></ul>
    </div>

    <script>
        const canvas = document.getElementById("tetris");
        const context = canvas.getContext("2d");
        const scoreElement = document.getElementById("score");
        const gameOverElement = document.getElementById("game-over");

        const ROWS = 20;
        const COLUMNS = 10;
        const BLOCK_SIZE = 30;
        const EMPTY = 0;

        const tetrisMatrix = Array.from({ length: ROWS }, () => Array(COLUMNS).fill(EMPTY));

        let score = 0;
        let gamePaused = false;
        let gameOver = false;
        let level = 1;
        let speed = 1000; // Initial speed in milliseconds

        // Tetrominos and their colors
        const tetrominos = {
            // Define Tetrominos here (I, J, L, O, S, T, Z)
        };

        const tetrominoColors = {
            // Define colors here
        };

        // Function to draw a single square
        function drawSquare(x, y, color) {
            context.fillStyle = color;
            context.fillRect(x * BLOCK_SIZE, y * BLOCK_SIZE, BLOCK_SIZE, BLOCK_SIZE);
            context.strokeStyle = "#444";
            context.strokeRect(x * BLOCK_SIZE, y * BLOCK_SIZE, BLOCK_SIZE, BLOCK_SIZE);
        }

        // Function to draw the Tetris matrix
        function drawMatrix(matrix, offset) {
            matrix.forEach((row, y) => {
                row.forEach((value, x) => {
                    if (value !== EMPTY) {
                        drawSquare(x + offset.x, y + offset.y, tetrominoColors[value]);
                    }
                });
            });
        }

        // Function to merge Tetromino with the matrix
        function merge(matrix, offset) {
            matrix.forEach((row, y) => {
                row.forEach((value, x) => {
                    if (value !== EMPTY) {
                        tetrisMatrix[y + offset.y][x + offset.x] = value;
                    }
                });
            });
        }

        // Function to rotate a Tetromino
        function rotate(matrix) {
            const rotated = matrix.map((_, index) =>
                matrix.map(col => matrix[col][index]).reverse()
            );
            return rotated;
        }

        // Function to check for collisions
        function collide(matrix, offset) {
            for (let y = 0; y < matrix.length; y++) {
                for (let x = 0; x < matrix[y].length; x++) {
                    if (matrix[y][x] !== EMPTY &&
                        (tetrisMatrix[y + offset.y] &&
                            tetrisMatrix[y + offset.y][x + offset.x]) !== EMPTY) {
                        return true;
                    }
                }
            }
            return false;
        }

        // Function to clear rows and update the score
        function clearRows() {
            outer: for (let y = ROWS - 1; y >= 0; y--) {
                for (let x = 0; x < COLUMNS; x++) {
                    if (tetrisMatrix[y][x] === EMPTY) {
                        continue outer;
                    }
                }
                const row = tetrisMatrix.splice(y, 1)[0].fill(EMPTY);
                tetrisMatrix.unshift(row);
                score += 100;
            }
            scoreElement.textContent = score;
            if (score % 500 === 0) { // Increase difficulty every 500 points
                level++;
                speed -= 100;
            }
        }

        // Function to update the game
        function update() {
            if (!gamePaused && !gameOver) {
                draw();
                moveDown();
                requestAnimationFrame(update);
            }
        }

        // ... (Keyboard controls, game over handling, etc.)

        // Start the game
        update();
    </script>
</body>
</html>

```
