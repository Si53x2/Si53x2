- 👋 Hi, I’m @Si53x2
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Si53x2/Si53x2 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

var ball = createSprite(200,200,10,10);
var playerPaddle = createSprite(200,375,40,10);
var computerPaddle = createSprite(200,25,40,10);
var goal1 = createSprite(200, 395,100,10);
var goal2 = createSprite(200, 5,100,10);
var border1 = createSprite(360, 200,10,800);
var border2 = createSprite(40, 200,10,800);
var debug1 = createSprite(18, 200,35,800);
var debug2 = createSprite(382, 200,35,800);


debug1.shapeColor = 'green';
debug2.shapeColor = 'green';
border1.shapeColor = 'white';
border2.shapeColor = 'white';
ball.shapeColor = 'white';
playerPaddle.shapeColor = 'white';
computerPaddle.shapeColor = 'red';
goal1.shapeColor = 'yellow';
goal2.shapeColor = 'yellow';


//variable to store different state of game
var gameState = "serve";
var computerScore = 0;
var playerScore = 0;
if (gameState === "play" || gameState === "serve") {
  


playSound("Ufff.mp3", true);
playSound("sound://category_nature/fire_loop.mp3", true);
}
function draw() {
  //clear the screen
  createEdgeSprites();
  textSize(20);
  background("green");
ball.bounceOff(border1);
ball.bounceOff(border2);
if (ball.isTouching(goal1)) {
  playSound("sound://category_tap/negative_select_2.mp3", false);
  
}
if (ball.isTouching(goal2)) {
  playSound("sound://category_tap/negative_select_1.mp3", false);
  
}
if (ball.isTouching(playerPaddle)) {
  playSound("sound://default.mp3", false);
  ball.velocityX - 1;
  ball.velocityY - 1;
}
if (ball.isTouching(computerPaddle)) {
  playSound("sound://default.mp3", false);
  ball.velocityX + 1;
  ball.velocityY + 1;
}

if (ball.isTouching(border1)) {
  playSound("sound://default.mp3", false);
  
}
if (ball.isTouching(border2)) {
  playSound("sound://default.mp3", false);
  
}
if (ball.isTouching(edges)) {
  playSound("sound://default.mp3", false);
  
}
if (ball.isTouching(debug1)) {
  gameState = "serve";
}
if (ball.isTouching(debug2)) {
  gameState = "serve";
}


  //place info text in the center
  if (gameState === "serve") {
    text("Press Space to Serve",150,180);
  }
   text(computerScore, 60, 172);
   text(playerScore, 60, 222);
  
  //make the player paddle move with the mouse's y position
  playerPaddle.x = World.mouseX;
  
  //AI for the computer paddle
  //make it move with the ball's y position
  computerPaddle.x = ball.x;
  
  //draw line at the centre
  drawnet();
 
  
  
  //create edge boundaries
  //make the ball bounce with the top and the bottom edges
  createEdgeSprites();
  ball.bounceOff(edges);
  ball.bounceOff(playerPaddle);
  ball.bounceOff(computerPaddle);
 
  
  //serve the ball when space is pressed
  if (keyDown("space") && gameState === "serve") {
    serve();
    gameState = "play";
  }
  
 
  //reset the ball to the centre if it crosses the screen
  if(ball.isTouching(goal1) || ball.isTouching(goal2)) {
    
    if (ball.isTouching(goal1)) {
      computerScore = computerScore + 1;
    }
  if (ball.isTouching(goal2)) {
      playerScore = playerScore + 1;
  }
      reset();
    gameState = "serve";
  }
  
  if (playerScore === 20 || computerScore === 20) {
    gameState = "over";
    text("Game Over", 115, 160);
    text("Press 'Up Arrow' to restart game", 65, 180);
    
  }
  if (keyDown("UP_ARROW") && gameState === "over") {
    gameState = 'serve';
    computerScore = 0;
    playerScore = 0;
  }
  
  drawSprites();
}

function drawnet(){
 for (var i = 0; i < 400; i=i+20) {
    line(i,200,i+10,200);
  }
}
function serve() {
  ball.velocityX = 9;
  ball.velocityY = 5;
}

function reset() {
  ball.x = 200;
  ball.y = 200;
  ball.velocityX = 0;
  ball.velocityY = 0;
}

