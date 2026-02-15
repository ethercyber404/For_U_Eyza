<html lang="en">
<head>
<meta charset="UTF-8">
<title>Custom Flappy Bird</title>
<style>
  body {
    margin: 0;
    background: skyblue;
    overflow: hidden;
    text-align: center;
    font-family: sans-serif;
  }
  canvas {
    background: linear-gradient(#87CEEB, #fff);
    display: block;
    margin: 0 auto;
  }
</style>
</head>
<body>

<canvas id="gameCanvas" width="400" height="600"></canvas>

<script>
// ====== CONFIG ======
const birdImageSrc = "bird.png"; // এখানে তোমার ছবি নাম দাও
const flapSoundSrc = "flap.mp3"; // ট্যাপ করলে বাজবে
const hitSoundSrc = "hit.mp3";   // গেম শেষ হলে বাজবে

// ====== GAME VARIABLES ======
const canvas = document.getElementById("gameCanvas");
const ctx = canvas.getContext("2d");

let bird = { x: 80, y: 300, width: 40, height: 40, gravity: 0.6, lift: -10, velocity: 0 };
let pipes = [];
let frame = 0;
let score = 0;
let gameOver = false;

// ====== LOAD ASSETS ======
const birdImg = new Image();
birdImg.src = birdImageSrc;

const flapSound = new Audio(flapSoundSrc);
const hitSound = new Audio(hitSoundSrc);

// ====== PIPE FUNCTIONS ======
function createPipe() {
  const topHeight = Math.random() * 200 + 50;
  const gap = 150;
  pipes.push({ x: canvas.width, y: 0, width: 50, height: topHeight });
  pipes.push({ x: canvas.width, y: topHeight + gap, width: 50, height: canvas.height - (topHeight + gap) });
}

// ====== GAME LOOP ======
function draw() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // Draw bird
  ctx.drawImage(birdImg, bird.x, bird.y, bird.width, bird.height);

  // Bird physics
  bird.velocity += bird.gravity;
  bird.y += bird.velocity;

  // Draw pipes
  for (let i = 0; i < pipes.length; i++) {
    let p = pipes[i];
    ctx.fillStyle = "green";
    ctx.fillRect(p.x, p.y, p.width, p.height);

    // Move pipes
    p.x -= 2;

    // Collision
    if (bird.x + bird.width > p.x && bird.x < p.x + p.width &&
        bird.y + bird.height > p.y && bird.y < p.y + p.height) {
      gameOver = true;
    }

    // Score
    if (!p.scored && p.x + p.width < bird.x) {
      score++;
      p.scored = true;
    }
  }

  // New pipe
  if (frame % 90 === 0) createPipe();

  // Score
  ctx.fillStyle = "black";
  ctx.font = "20px Arial";
  ctx.fillText("Score: " + score, 10, 30);

  // Check game over
  if (bird.y + bird.height > canvas.height || bird.y < 0) gameOver = true;

  if (gameOver) {
    hitSound.play();
    ctx.fillStyle = "red";
    ctx.font = "40px Arial";
    ctx.fillText("GAME OVER", 80, canvas.height / 2);
    return;
  }

  frame++;
  requestAnimationFrame(draw);
}

// ====== CONTROLS ======
document.addEventListener("keydown", flap);
document.addEventListener("click", flap);

function flap() {
  bird.velocity = bird.lift;
  flapSound.play();
}

// ====== START GAME ======
draw();
</script>

</body>
</html>




