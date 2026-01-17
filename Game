<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Haunted Memory</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">

<style>
body {
  margin: 0;
  background: black;
  overflow: hidden;
  touch-action: none;
}
canvas {
  display: block;
}
#ui {
  position: fixed;
  bottom: 20px;
  left: 20px;
  z-index: 10;
}
.btn {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  background: rgba(255,255,255,0.2);
  color: white;
  text-align: center;
  line-height: 60px;
  font-size: 24px;
  margin-bottom: 10px;
}
</style>
</head>

<body>

<canvas id="game"></canvas>

<div id="ui">
  <div class="btn" id="up">▲</div>
  <div class="btn" id="down">▼</div>
</div>

<script>
const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

function resize(){
  canvas.width = innerWidth;
  canvas.height = innerHeight;
}
resize();
addEventListener("resize", resize);

// MAP (1 = wall)
const map = [
  [1,1,1,1,1,1,1],
  [1,0,0,0,0,0,1],
  [1,0,0,0,0,0,1],
  [1,0,0,0,0,0,1],
  [1,1,1,1,1,1,1],
];

// PLAYER
let px = 3.5, py = 3.5;
let angle = 0;

// CONTROLS
document.getElementById("up").ontouchstart = () => move(0.1);
document.getElementById("down").ontouchstart = () => move(-0.1);

function move(speed){
  px += Math.cos(angle) * speed;
  py += Math.sin(angle) * speed;
}

// RENDER
function draw(){
  ctx.fillStyle = "black";
  ctx.fillRect(0,0,canvas.width,canvas.height);

  const fov = Math.PI / 3;
  const rays = canvas.width;

  for(let i=0;i<rays;i++){
    const rayAngle = angle - fov/2 + fov*i/rays;
    let dist = 0;

    while(dist < 20){
      const rx = px + Math.cos(rayAngle)*dist;
      const ry = py + Math.sin(rayAngle)*dist;

      if(map[Math.floor(ry)][Math.floor(rx)] === 1) break;
      dist += 0.05;
    }

    const wallHeight = canvas.height / (dist+0.1);
    ctx.fillStyle = `rgb(${200/dist},${200/dist},${200/dist})`;
    ctx.fillRect(i, canvas.height/2 - wallHeight/2, 1, wallHeight);
  }

  requestAnimationFrame(draw);
}
draw();
</script>

</body>
</html>
