# ICS10-dragons-adventures
ICS10 game
/*
Modified:

Start screen
3 levels
Red sticks
Walls
Flag = finish
*/

//Lose, win, level 

var Lose = false;

var Win = false;

var lvl1 = false;
var lvl2 = false;
var lvl3 = false;

var wallHit = false;
var onWall = false;
var belowWall = false;

//Beaver ///////////////////////////////////

    
var Beaver = function(x, y) {
    this.x = x;
    this.y = y;
    this.img = getImage("creatures/Hopper-Happy");
    this.sticks = 0;
};

Beaver.prototype.draw = function() {
    fill(255, 0, 0);
    this.y = constrain(this.y, 0, height-50);
    image(this.img, this.x, this.y, 40, 40);
};

Beaver.prototype.hop = function() {
    this.img = getImage("avatars/piceratops-ultimate");
    if(belowWall){
        
    } else {
        this.y -= 5;
    }
};

Beaver.prototype.fall = function() {
    this.img = getImage("avatars/piceratops-ultimate");
    if(onWall) {
    } else {
    this.y += 5;
    }
};

Beaver.prototype.checkForStickGrab = function(stick) {
    if ((stick.x >= this.x && stick.x <= (this.x + 40)) &&
        (stick.y >= this.y && stick.y <= (this.y + 40))) {
        stick.y = -400;
        this.sticks++;
    }
};

Beaver.prototype.checkForBadStickGrab = function(badstick) {
    if ((badstick.x >= this.x && badstick.x <= (this.x + 40)) &&
        (badstick.y >= this.y && badstick.y <= (this.y + 40))) {
        badstick.y = -400;
        this.sticks--;
    }
};

Beaver.prototype.checkForWallHit = function(wall) {
    if ((wall.x >= (this.x+30) && wall.x <= (this.x+40)) && ((wall.y+35) >= (this.y) && (wall.y-35) <= (this.y+40)))
         {
        wallHit = true;
    } 

};

//Sticks ///////////////////////////////////
var Stick = function(x, y) {
    this.x = x;
    this.y = y;
};

Stick.prototype.draw = function() {
    fill(89, 71, 0);
    rectMode(CENTER);
    rect(this.x, this.y, 5, 40);
};

var badStick = function(x, y) {
    this.x = x;
    this.y = y;
};

badStick.prototype.draw = function() {
    fill(255, 8, 8);
    rectMode(CENTER);
    rect(this.x, this.y, 5, 40);
};

var beaver = new Beaver(200, 300);

var sticksNumber = 40;

var sticks = [];
for (var i = 0; i < sticksNumber; i++) {  
    sticks.push(new Stick(i * 40 + 500, random(20, 260)));
}

var badsticks = [];
for (var i = 0; i < 10; i++) {  
    badsticks.push(new badStick(i * 160 + 500, random(20, 260)));

}


//Wall /////////////////////////////////////

var Wall = function(x, y) {
    this.x = x;
    this.y = y;
};

Wall.prototype.draw = function() {
    fill(89, 71, 0);
    rectMode(CENTER);
    //rows of bricks width:20, height:75
    
    rect(this.x-5, this.y-35, 10, 5);
    rect(this.x+5, this.y-35, 10, 5);
    
    rect(this.x-7.5, this.y-30, 5, 5);
    rect(this.x, this.y-30, 10, 5);
    rect(this.x+7.5, this.y-30, 5, 5);
    
    rect(this.x-5, this.y-25, 10, 5);
    rect(this.x+5, this.y-25, 10, 5);
    
    rect(this.x-7.5, this.y-20, 5, 5);
    rect(this.x, this.y-20, 10, 5);
    rect(this.x+7.5, this.y-20, 5, 5);
    
    rect(this.x-5, this.y-15, 10, 5);
    rect(this.x+5, this.y-15, 10, 5);
    
    rect(this.x-7.5, this.y-10, 5, 5);
    rect(this.x, this.y-10, 10, 5);
    rect(this.x+7.5, this.y-10, 5, 5);
    
    rect(this.x-5, this.y-5, 10, 5);
    rect(this.x+5, this.y-5, 10, 5);
    
    rect(this.x-7.5, this.y, 5, 5);
    rect(this.x, this.y, 10, 5);
    rect(this.x+7.5, this.y, 5, 5);
    
    rect(this.x-5, this.y+5, 10, 5);
    rect(this.x+5, this.y+5, 10, 5);
    
    rect(this.x-7.5, this.y+10, 5, 5);
    rect(this.x, this.y+10, 10, 5);
    rect(this.x+7.5, this.y+10, 5, 5);
    
    rect(this.x-5, this.y+15, 10, 5);
    rect(this.x+5, this.y+15, 10, 5);
    
    rect(this.x-7.5, this.y+20, 5, 5);
    rect(this.x, this.y+20, 10, 5);
    rect(this.x+7.5, this.y+20, 5, 5);
    
    rect(this.x-5, this.y+25, 10, 5);
    rect(this.x+5, this.y+25, 10, 5);
    
    rect(this.x-7.5, this.y+30, 5, 5);
    rect(this.x, this.y+30, 10, 5);
    rect(this.x+7.5, this.y+30, 5, 5);
    
    rect(this.x-5, this.y+35, 10, 5);
    rect(this.x+5, this.y+35, 10, 5);
};

var wallsNumber = 22;

var walls = [];

//Grass ///////////////////////////////////
var grassXs = [];
for (var i = 0; i < 25; i++) { 
    grassXs.push(i*20);
}


//Flag ///////////////////////////////////

var Flag = function(x, y) {
    this.x = x;
    this.y = y;
};

Flag.prototype.draw = function() {
    fill(0, 0, 0);
    rectMode(CENTER);
    rect(this.x, this.y, 2, 40);
    rect(this.x+13, this.y-20, 29, 2);
    rect(this.x+13, this.y, 29, 2);
    rect(this.x+28, this.y-10, 2, 22);
    //top row
    rect(this.x+6, this.y-16, 4, 4);
    rect(this.x+14, this.y-16, 4, 4);
    rect(this.x+22, this.y-16, 4, 4);
    //2nd row
    rect(this.x+2, this.y-12, 4, 4);
    rect(this.x+10, this.y-12, 4, 4);
    rect(this.x+18, this.y-12, 4, 4);
    rect(this.x+26, this.y-12, 4, 4);
    //3rd row
    rect(this.x+6, this.y-8, 4, 4);
    rect(this.x+14, this.y-8, 4, 4);
    rect(this.x+22, this.y-8, 4, 4);
    //last row
    rect(this.x+2, this.y-4, 4, 4);
    rect(this.x+10, this.y-4, 4, 4);
    rect(this.x+18, this.y-4, 4, 4);
    rect(this.x+26, this.y-4, 4, 4);
};
    var flag = new Flag(sticksNumber*40+600,340);

//Win OR Lose /////////////////////

var winLevel = function(){
    fill(56, 3, 3);
    textAlign(CENTER,CENTER);
    text("level complete!",200,100);
    textSize(14);
    stroke(29, 74, 7);
    fill(227, 254, 255);
    rectMode(CORNER);
    rect(110,115,80,30);
    rect(210,115,80,30);
    fill(56, 3, 3);
    text("Next level",150,130);
    text("You lose!Try again",250,130);
    
};

var finalWin = function(){
    background(74, 107, 240);
    fill(56, 3, 3);
    textAlign(CENTER,CENTER);
    textSize(22);
    text("YOU CAN NOT BE STOPPED!!!",200,100);
    beaver.x = mouseX;
    beaver.y = mouseY;
    flag.x = -100;
    
};

var loseLevel = function(){
    fill(56, 3, 3);
    textAlign(CENTER,CENTER);
    text("You Lose the level",200,100);
    textSize(14);
    stroke(29, 74, 7);
    fill(227, 254, 255);
    rectMode(CORNER);
    rect(160,115,80,30);
    fill(56, 3, 3);
    text("Try again?",200,130);
    
};



//various variables ///////////////////

var moveSpeed = 1;

var scoreX = 20;
var scoreY = 30;

var Target = 0;

var levelBadSticks = 0;

var badSticksPlacement = 0;

var levelWalls = 0;

var wallsPlacement = 0;

var restart = function(){
    moveSpeed = 1;
    scoreX = 20;
    scoreY = 30;
    flag.x = sticksNumber*40+600;
    
    sticks = [];
    for (var i = 0; i < sticksNumber; i++) {  
        sticks.push(new Stick(i * 40 + 500, random(20, 260)));
    }

    
    badsticks = [];
    
    if(lvl1 === true){
        levelBadSticks = 10;
        badSticksPlacement = 160;
    } else if (lvl2 === true){
        levelBadSticks = 15;
        badSticksPlacement = 106;
    } else if (lvl3 === true){
        levelBadSticks = 20;
        badSticksPlacement = 80;
    }
    
    for (var i = 0; i < levelBadSticks; i++) {  
        badsticks.push(new badStick(i * badSticksPlacement + 500, random(20, 260)));
        
    }
    
    walls = [];
    
    if(lvl1 === true){
        levelWalls = 1;
        wallsPlacement = 200;
    } else if (lvl2 === true){
        levelWalls = 1;
        wallsPlacement = 1200;
    } else if (lvl3 === true){
        levelWalls = 5;
        wallsPlacement = 300;
    }
    
    for (var i = 0; i < levelWalls; i++) { 
        if (lvl1 === true) {
            
            
        } else if (lvl2 === true) {
            
            walls.push(new Wall(wallsPlacement + 500, random(50, 230)));
            
        } else if (lvl3 === true) {
            
            walls.push(new Wall(i * wallsPlacement + 900, random(50, 230)));
            
        }

    }
    
    beaver.sticks = 0;
    Win = false;
    Lose = false;
    
    wallHit = false;
};


//Start screen ///////////////////////////////

var startScreen = function(){
    fill(130, 79, 43);
    rectMode(CORNER);
    rect(0, height*0.9, width, height*0.10);
    
    moveSpeed = 0;
    
    for (var i = 0; i < grassXs.length; i++) {
        image(getImage("cute/GrassBlock"), grassXs[i], height*0.85, 20, 20);
        grassXs[i] -= moveSpeed;
        if (grassXs[i] <= -20) {
            grassXs[i] = width;
        }
    }
    
    //Welcome text
    fill(95, 158, 207);
    textSize(15);
    textAlign(CENTER);
    text("Welcome to",200,30);
    fill(43, 9, 153);
    textSize(25);
    text("Dragons ADVENTURES!",200,70);

    //Start button
    textAlign(CENTER,CENTER);
    textSize(14);
    stroke(109, 149, 168);
    fill(168, 222, 224);
    rectMode(CORNER);
    rect(150,115,100,30,3);
    fill(56, 3, 3);
    text("Start the game",200,130);
    
    //Instructions
    
    textAlign(LEFT,UP);
    text("Instructions:",30,190);
    textSize(9);
    text("Use SPACE to make Dragon jump\n\nGather as many sticks as possible to get an increase of score(+1)\n\nAvoid red sticks (Score -1)\n\nGetting stuck behind a wall = Game over\n\nFlag = Finish",20,220);
    
    sticks = [];
    sticks.push(new Stick(230,235));
    sticks[0].draw();
    
    badsticks = [];
    badsticks.push(new badStick(240,255));
    badsticks[0].draw();
    
    flag = new Flag(200,340);
    flag.draw();
    
    walls = [];
    walls.push(new Wall(300,305));
    walls[0].draw();
    
    if (mouseIsPressed && mouseX>150 && mouseX<250 && mouseY>115 && mouseY<145){
       lvl1 = true;
       restart();
    }
    
   
};


//Level 1 ///////////////////////////////////

var levelOne = function(){
    fill(130, 79, 43);
    rectMode(CORNER);
    rect(0, height*0.9, width, height*0.10);
    
   
    
    flag.x -= moveSpeed;
    
    Target = 0.5;
    
    textSize(18);
    textAlign(LEFT,BASELINE);
    text("Level 1",330,20);
    
    for (var i = 0; i < grassXs.length; i++) {
        image(getImage("cute/GrassBlock"), grassXs[i], height*0.85, 20, 20);
        grassXs[i] -= moveSpeed;
        if (grassXs[i] <= -20) {
            grassXs[i] = width;
        }
    }
    for (var i = 0; i < sticks.length; i++) {
        sticks[i].draw();
        beaver.checkForStickGrab(sticks[i]);
        sticks[i].x -= moveSpeed;
    }
    for (var i = 0; i < badsticks.length; i++) {
        badsticks[i].draw();
        beaver.checkForBadStickGrab(badsticks[i]);
        badsticks[i].x -= moveSpeed;
    }
    for (var i = 0; i < walls.length; i++) {
        walls[i].draw();
        beaver.checkForWallHit(walls[i]);
        walls[i].x -= moveSpeed;
    }
    
    
    textSize(18);
    textAlign(LEFT,BASELINE);
    text("Score: " + beaver.sticks, scoreX, scoreY);
    text("Target: " + sticks.length*Target, scoreX, scoreY+30);
    
    
    if (beaver.x >= flag.x) {
        beaver.fall();
    } else if (beaver.x <= flag.x) {
        if (keyIsPressed && keyCode === 0) {
        //if (mouseIsPressed) {
            beaver.hop();
        } else {
            beaver.fall();
        }
    }
    
    if (beaver.x >= flag.x+100) {
        moveSpeed = 0;
        
    }
    
    if (wallHit === true) {
        moveSpeed = 0;
        beaver.fall();
        loseLevel();
        Lose = true;
    }
            
    if (mouseIsPressed && Win && mouseX>210 && mouseX<290 && mouseY>115 && mouseY<145){
        restart();
    }
    
    if (mouseIsPressed && Win && mouseX>110 && mouseX<280 && mouseY>115 && mouseY<145){
       lvl2 = true;
       lvl1 = false;
       restart();
    }
    
    if (mouseIsPressed && Lose && mouseX>160 && mouseX<240 && mouseY>115 && mouseY<145){
        restart();
    }
    
    
    if (beaver.x >= flag.x) {
        
        if(scoreX < 160){
            scoreX+=1; 
        }
        if(scoreY < 200){
            scoreY+=1; 
        }
    }
    //check if won or not
    if (scoreY === 200 && beaver.sticks >= sticks.length*Target) {
        
        winLevel();
        Win = true;
       
    } else if (scoreY === 200){
        loseLevel();
        Lose = true;
    }
    
    
    
    flag.draw();
    beaver.draw();
};


//Level 2 ///////////////////////////////////

var levelTwo = function(){
    fill(130, 79, 43);
    rectMode(CORNER);
    rect(0, height*0.9, width, height*0.10);
    
    flag.x -= moveSpeed;
    
    Target = 0.7;
    
    textSize(18);
    textAlign(LEFT,BASELINE);
    text("Level 2",330,20);
    
    for (var i = 0; i < grassXs.length; i++) {
        image(getImage("cute/GrassBlock"), grassXs[i], height*0.85, 20, 20);
        grassXs[i] -= moveSpeed;
        if (grassXs[i] <= -20) {
            grassXs[i] = width;
        }
    }
    for (var i = 0; i < sticks.length; i++) {
        sticks[i].draw();
        beaver.checkForStickGrab(sticks[i]);
        sticks[i].x -= moveSpeed;
    }
    for (var i = 0; i < badsticks.length; i++) {
        badsticks[i].draw();
        beaver.checkForBadStickGrab(badsticks[i]);
        badsticks[i].x -= moveSpeed;
    }
    for (var i = 0; i < walls.length; i++) {
        walls[i].draw();
        beaver.checkForWallHit(walls[i]);
        walls[i].x -= moveSpeed;
    }
    
    textSize(18);
    textAlign(LEFT,BASELINE);
    text("Score: " + beaver.sticks, scoreX, scoreY);
    text("Target: " + sticks.length*Target, scoreX, scoreY+30);
    
    
    if (beaver.x >= flag.x) {
        beaver.fall();
    } else if (beaver.x <= flag.x) {
        if (keyIsPressed && keyCode === 0) {
        //if (mouseIsPressed) {
            beaver.hop();
        } else {
            beaver.fall();
        }
    }
    
    if (beaver.x >= flag.x+100) {
        moveSpeed = 0;
        
    }
    
            
    if (mouseIsPressed && Win && mouseX>210 && mouseX<290 && mouseY>115 && mouseY<145){
        restart();
    }
    
    
    if (mouseIsPressed && Win && mouseX>110 && mouseX<280 && mouseY>115 && mouseY<145){
       lvl3 = true;
       lvl2 = false;
       restart();
    }
    
    if (mouseIsPressed && Lose && mouseX>160 && mouseX<240 && mouseY>115 && mouseY<145){
        restart();
    }
    
    
    if (beaver.x >= flag.x) {
        
        if(scoreX < 160){
            scoreX+=1; 
        }
        if(scoreY < 200){
            scoreY+=1; 
        }
    }
    //check if won or not
    if (scoreY === 200 && beaver.sticks >= sticks.length*Target) {
        winLevel();
        Win = true;
        
    } else if (scoreY === 200){
        loseLevel();
        Lose = true;
    }
    
    
    
    flag.draw();
    beaver.draw();
};

//Level 3 ///////////////////////////////////

var levelThree = function(){
    fill(130, 79, 43);
    rectMode(CORNER);
    rect(0, height*0.9, width, height*0.10);
    
    flag.x -= moveSpeed;
    
    Target = 0.875;
    
    textSize(18);
    textAlign(LEFT,BASELINE);
    text("Level 3",330,20);
    
    for (var i = 0; i < grassXs.length; i++) {
        image(getImage("cute/GrassBlock"), grassXs[i], height*0.85, 20, 20);
        grassXs[i] -= moveSpeed;
        if (grassXs[i] <= -20) {
            grassXs[i] = width;
        }
    }
    for (var i = 0; i < sticks.length; i++) {
        sticks[i].draw();
        beaver.checkForStickGrab(sticks[i]);
        sticks[i].x -= moveSpeed;
    }
    for (var i = 0; i < badsticks.length; i++) {
        badsticks[i].draw();
        beaver.checkForBadStickGrab(badsticks[i]);
        badsticks[i].x -= moveSpeed;
    }
    for (var i = 0; i < walls.length; i++) {
        walls[i].draw();
        beaver.checkForWallHit(walls[i]);
        walls[i].x -= moveSpeed;
    }
    
    textSize(18);
    textAlign(LEFT,BASELINE);
    text("Score: " + beaver.sticks, scoreX, scoreY);
    text("Target: " + sticks.length*Target, scoreX, scoreY+30);
    
    
    if (beaver.x >= flag.x) {
        beaver.fall();
    } else if (beaver.x <= flag.x) {
        if (keyIsPressed && keyCode === 0) {
        //if (mouseIsPressed) {
            beaver.hop();
        } else {
            beaver.fall();
        }
    }
    
    if (beaver.x >= flag.x+100) {
        moveSpeed = 0;
        
    }
    
            
    if (mouseIsPressed && Win && mouseX>210 && mouseX<290 && mouseY>115 && mouseY<145){
        restart();
    }
    
    
    if (mouseIsPressed && Win && mouseX>110 && mouseX<280 && mouseY>115 && mouseY<145){
       // next level;
    }
    
    if (mouseIsPressed && Lose && mouseX>160 && mouseX<240 && mouseY>115 && mouseY<145){
        restart();
    }
    
    
    if (beaver.x >= flag.x) {
        
        if(scoreX < 160){
            scoreX+=1; 
        }
        if(scoreY < 200){
            scoreY+=1; 
        }
    }
    //check if won or not
    if (scoreY === 200 && beaver.sticks >= sticks.length*Target) {
        finalWin();
        
    } else if (scoreY === 200){
        loseLevel();
        Lose = true;
    }
    
    
    
    flag.draw();
    beaver.draw();
};

var currentLevel = function() {
    if (lvl1 === false && lvl2 === false && lvl3 === false){
        //start screen
        startScreen();
    } else if (lvl1 === true) {
        levelOne();
    } else if (lvl2 === true) {
        levelTwo();
    } else if (lvl3 === true) {
        levelThree();
    }
};

//Draw function ///////////////////////////////////
draw = function() {
    
    // static
    background(227, 254, 255);
    currentLevel();
};








