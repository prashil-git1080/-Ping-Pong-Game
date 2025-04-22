# -Ping-Pong-Game
html code:
<!DOCTYPE html>

<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ping Pong Game</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="game-container">
        <div class="paddle left-paddle"></div>
        <div class="paddle right-paddle"></div>
        <div class="ball"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>
js.code :
const gameContainer = document.querySelector('.game-container');

const leftPaddle = document.querySelector('.left-paddle');

const rightPaddle = document.querySelector('.right-paddle');
const ball = document.querySelector('.ball');

let ballX = 392.5;
let ballY = 192.5;
let ballSpeedX = 4;
let ballSpeedY = 4;

let leftPaddleY = 160;
let rightPaddleY = 160;

const paddleSpeed = 10;
const paddleHeight = 80;
const gameHeight = 400;
const gameWidth = 800;

document.addEventListener('keydown', (event) => {
    switch(event.key) {
        case 'w':
            leftPaddleY = Math.max(leftPaddleY - paddleSpeed, 0);
            break;
        case 's':
            leftPaddleY = Math.min(leftPaddleY + paddleSpeed, gameHeight - paddleHeight);
            break;
        case 'ArrowUp':
            rightPaddleY = Math.max(rightPaddleY - paddleSpeed, 0);
            break;
        case 'ArrowDown':
            rightPaddleY = Math.min(rightPaddleY + paddleSpeed, gameHeight - paddleHeight);
            break;
    }
    leftPaddle.style.top = `${leftPaddleY}px`;
    rightPaddle.style.top = `${rightPaddleY}px`;
});

function updateBall() {
    ballX += ballSpeedX;
    ballY += ballSpeedY;

    // Ball collision with top and bottom walls
    if (ballY <= 0 || ballY >= gameHeight - 15) {
        ballSpeedY = -ballSpeedY;
    }

    // Ball collision with paddles
    if (ballX <= 20 && ballY >= leftPaddleY && ballY <= leftPaddleY + paddleHeight) {
        ballSpeedX = -ballSpeedX;
    }

    if (ballX >= gameWidth - 35 && ballY >= rightPaddleY && ballY <= rightPaddleY + paddleHeight) {
        ballSpeedX = -ballSpeedX;
    }

    // Ball out of bounds
    if (ballX <= 0 || ballX >= gameWidth - 15) {
        resetBall();
    }

    ball.style.left = `${ballX}px`;
    ball.style.top = `${ballY}px`;
}

function resetBall() {
    ballX = 392.5;
    ballY = 192.5;
    ballSpeedX = -ballSpeedX;
}

function gameLoop() {
    updateBall();
    requestAnimationFrame(gameLoop);
}

gameLoop();
