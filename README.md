# Deserae-s-Projects
Some of my coding projects I have done

#Project Number #1: A collection style game
//Move the catcher with the left and right arrow keys to catch the falling objects. 

/* VARIABLES */
let catcher, fallingObject;
let score = 0;
let bird, fallingObjectImg, catcherImg;

/* PRELOAD LOADS FILES */
function preload(){
  birdImg = loadImage("assets/bird.png");
  fallingObjectImg = loadImage("assets/bird-second.png");
  catcherImg = loadImage("assets/nest.png");
}

/* SETUP RUNS ONCE */
function setup() {
  createCanvas(400,400);
  //Change the size of the image
  birdImg.resize(50,0)
  fallingObjectImg.resize(150, 0)
  catcherImg.resize(200,0)
  
  //Create catcher 
  catcher = new Sprite(catcherImg, 200,380,100,20, "k");
  catcher.color = color(95,158,160);
  
  //Create falling object
  fallingObject = new Sprite(fallingObjectImg, 100,0,10);
  fallingObject.color = color(0,128,128);
  fallingObject.vel.y = 2;
  fallingObject.rotationLock = true;
  fallingObject.speed = 5;
}

/* DRAW LOOP REPEATS */
function draw() {
  background('pink');
  image(birdImg, 350, 2)
  
  // Draw directions to screen
  fill('white');
  textSize(13);
  text("Move the \ncatcher with the \nleft and right \narrow keys to \ncatch the falling \nobjects.", width-100, 20);


  if (fallingObject.y >=  height) {
    fallingObject.y = 0;
    fallingObject.x = random(width);
    fallingObject.vel.y = random(1,5);

    //Missed
    score = score -1 
  }
  //Move catcher
  if (kb.pressing("left")) {
    catcher.vel.x = -3;
  } else if (kb.pressing("right")){
    catcher.vel.x = 3;
  } else {
    catcher.vel.x = 0;
  }
  //Stop catcher at the edges of screen
  if (catcher.x < 50) {
    catcher.x = 50;
  } else if (catcher.x > 350) {
    catcher.x = 350;
  }
  // If fallingObject collides with catcher, move back to random position at top and change the speed
  if (fallingObject.collides(catcher)) {
    fallingObject.y = 0;
    fallingObject.x = random(width);
    fallingObject.vel.y = random(1,5);
    fallingObject.direction = "down";
    score = score + 1;
    fallingObject.speed = 7;
  }
  //Draw the score to the screen
  fill('black');
  textSize(20);
  text("Score = " + score, 10, 30); 
    if (score <0){
      background('pink');
      
      catcher.x = 400;
      catcher.y = 450;
      fallingObject.x = 400;
      fallingObject.y = 450;
      fill("black");
      textSize(20);
      text("Game Over", 100, 200);
  } 
  if (score == 8){
      background('pink');

      catcher.x = 600;
      catcher.y = -300;
      fallingObject.x = -100;
      fallingObject.y = 0;
      fill('white');
      textSize(20);
      text("You win!!", width/2 - 50, height/2 - 30);
  }
  allSprites.debug = mouse.pressing();
  }
