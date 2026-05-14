<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Pixel Life</title>

<style>

body{
margin:0;
overflow:hidden;
background:black;
font-family:monospace;
}

canvas{
display:block;
margin:auto;
background:#111;
border:3px solid white;
}

</style>

</head>

<body>

<canvas id="game" width="1000" height="650"></canvas>

<script>

const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

let state = "menu";

let player = {
x:450,
y:300,
size:40,
speed:5
};

let playerName = "";
let playerGender = "";

let currentMessage = "";

let interacted = {};

let diaryOpen = false;

let score = 0;

let bullets = [];

let enemies = [];

let teacherTimer = 0;

const keys = {};



// OBJECTS

const objects = [

{
emoji:"🪑",
name:"table",
x:120,
y:180,
message:"Remember the table? Everything was done in that table. From tests to eat food to play games"
},

{
emoji:"✏️",
name:"pencil",
x:320,
y:100,
message:"the unnecessary tool which I always told not to use and use pen instead"
},

{
emoji:"📚",
name:"book",
x:500,
y:220,
message:"Atleast you read the book so nothing to make fun of"
},

{
emoji:"⭐",
name:"golden star sticker",
x:720,
y:160,
message:"the main stickers that you wished to get in the beginning of class"
},

{
emoji:"🍗",
name:"nuggets",
x:200,
y:450,
message:"always the main treat is either nuggets or burger or fries"
},

{
emoji:"🍕",
name:"pizza",
x:450,
y:470,
message:"the first ever party with pizza, remember?"
},

{
emoji:"🧸",
name:"tiny supermarket toy",
x:700,
y:420,
message:"remember going to supermarket and always calculating the price and you always make mistakes in bills"
}

];



// NEGATIVE COMMENTS

const comments = [

"You can't do this",
"This is too hard",
"You will fail",
"You are not good enough",
"Why even try?",
"Give up already"

];



// CREATE ENEMIES

for(let i=0;i<6;i++){

enemies.push({

x:120+i*120,
y:180,
text:comments[i]

});

}



// KEY EVENTS

document.addEventListener("keydown",(e)=>{

keys[e.key]=true;



// MENU

if(state==="menu" && e.key==="Enter"){

state="gender";

}



// GENDER

else if(state==="gender"){

if(e.key==="f"){

playerGender="female";
playerName="Gau-shi";
state="forest";

}

if(e.key==="m"){

playerGender="male";
playerName="Ewa-shi";
state="forest";

}

}



// SHOOTING

else if(state==="classroom" && e.key===" "){

bullets.push({

x:player.x+20,
y:player.y+10

});

}



// DIARY

else if(state==="bedroom" && e.key==="e"){

diaryOpen=true;

}

});



document.addEventListener("keyup",(e)=>{

keys[e.key]=false;

});



// DRAW TEXT

function drawText(text,x,y,color="white",size=20){

ctx.fillStyle=color;
ctx.font=size+"px monospace";
ctx.fillText(text,x,y);

}



// PLAYER MOVEMENT

function updatePlayer(){

if(keys["w"]) player.y-=player.speed;
if(keys["s"]) player.y+=player.speed;
if(keys["a"]) player.x-=player.speed;
if(keys["d"]) player.x+=player.speed;

}



// MENU

function drawMenu(){

ctx.fillStyle="black";
ctx.fillRect(0,0,1000,650);



// STARS

for(let i=0;i<100;i++){

ctx.fillStyle="white";
ctx.fillRect(Math.random()*1000,Math.random()*650,2,2);

}



drawText("PIXEL LIFE",390,200,"white",40);

drawText("Press ENTER to Start",320,300);

}



// GENDER SELECT

function drawGender(){

ctx.fillStyle="#222";
ctx.fillRect(0,0,1000,650);

drawText("Choose Character",350,150,"white",35);



// FEMALE

ctx.fillStyle="pink";
ctx.fillRect(180,220,250,250);

drawText("👧",270,340,"black",80);

drawText("Press F",250,420,"black",30);

drawText("Gau-shi",230,460,"black",30);



// MALE

ctx.fillStyle="lightblue";
ctx.fillRect(570,220,250,250);

drawText("👦",660,340,"black",80);

drawText("Press M",640,420,"black",30);

drawText("Ewa-shi",620,460,"black",30);

}



// FOREST

function drawForest(){

ctx.fillStyle="#102010";
ctx.fillRect(0,0,1000,650);



// STARS

for(let i=0;i<80;i++){

ctx.fillStyle="white";
ctx.fillRect(Math.random()*1000,Math.random()*650,1,1);

}



// TREES

for(let i=0;i<10;i++){

drawText("🌲",i*100,120,"white",80);

}



// PLAYER

if(playerGender==="female"){

drawText("👧",player.x,player.y,"white",40);

}else{

drawText("👦",player.x,player.y,"white",40);

}



drawText(playerName,player.x-10,player.y-10);



// OBJECTS

objects.forEach(obj=>{

drawText(obj.emoji,obj.x,obj.y,"white",35);



if(

Math.abs(player.x-obj.x)<40 &&
Math.abs(player.y-obj.y)<40

){

drawText(obj.name,obj.x,obj.y-20);

drawText("Press E to interact",340,610);



if(keys["e"]){

currentMessage=obj.message;
interacted[obj.name]=true;

}

}

});



drawText(currentMessage,30,40,"white",18);

drawText(

"Objects Found: "+Object.keys(interacted).length+"/7",
20,
80

);



// TELEPORT

if(Object.keys(interacted).length===7){

state="classroom";

player.x=450;
player.y=520;

}

}



// CLASSROOM

function drawClassroom(){

ctx.fillStyle="#b7d7ff";
ctx.fillRect(0,0,1000,650);



// FLOOR

ctx.fillStyle="#805030";
ctx.fillRect(0,540,1000,110);



// PLAYER

if(playerGender==="female"){

drawText("👧",player.x,player.y,"white",40);

}else{

drawText("👦",player.x,player.y,"white",40);

}



// TITLE

drawText(
"Destroy Negative Thoughts",
280,
50,
"black",
35
);



// ENEMIES

enemies.forEach(enemy=>{

ctx.fillStyle="white";
ctx.fillRect(enemy.x,enemy.y,100,60);

ctx.strokeStyle="red";
ctx.strokeRect(enemy.x,enemy.y,100,60);

drawText(enemy.text,enemy.x+5,enemy.y+35,"black",12);

});



// BULLETS

bullets.forEach((bullet,bIndex)=>{

bullet.x+=10;

ctx.fillStyle="yellow";
ctx.fillRect(bullet.x,bullet.y,10,5);



enemies.forEach((enemy,eIndex)=>{

if(

bullet.x<enemy.x+100 &&
bullet.x+10>enemy.x &&
bullet.y<enemy.y+60 &&
bullet.y+5>enemy.y

){

enemies.splice(eIndex,1);

bullets.splice(bIndex,1);

score++;

}

});

});



drawText(

"Negativity Removed: "+score+"/6",
20,
30,
"black"

);



// TEACHER

if(score>=6){

drawText(

"👩‍🏫 Good job in learning and avoiding negativity.",
170,
120,
"black",
25

);



teacherTimer++;



if(teacherTimer>180){

state="bedroom";

player.x=450;
player.y=500;

}

}

}



// BEDROOM

function drawBedroom(){

ctx.fillStyle="#ffddee";
ctx.fillRect(0,0,1000,650);



// BED

ctx.fillStyle="#ff99bb";
ctx.fillRect(650,350,250,180);



// WINDOW

ctx.fillStyle="#aaddff";
ctx.fillRect(100,100,180,120);



// PLAYER

if(playerGender==="female"){

drawText("👧",player.x,player.y,"white",40);

}else{

drawText("👦",player.x,player.y,"white",40);

}



// DIARY

drawText("📘",520,340,"white",50);

drawText("Diary",510,320,"black");



// INTERACT

if(

Math.abs(player.x-520)<50 &&
Math.abs(player.y-340)<50

){

drawText("Press E to read diary",330,600,"black");

}



// DIARY OPEN

if(diaryOpen){

ctx.fillStyle="black";
ctx.fillRect(40,40,920,560);



const lines = [

"Hope you enjoyed the game.",
"",
"It is a very small version.",
"",
"The forest represents memories.",
"Education shapes your future.",
"Your thoughts and decisions matter.",
"",
"Childhood is precious.",
"Enjoy life while you can.",
"",
"Choose a path you won't regret.",
"",
"Enjoy life and be happy.",
"",
"xoxoxo"

];



lines.forEach((line,index)=>{

drawText(

line,
70,
80+(index*30),
"white",
18

);

});

}

}



// GAME LOOP

function gameLoop(){

updatePlayer();



// STATES

if(state==="menu"){

drawMenu();

}

else if(state==="gender"){

drawGender();

}

else if(state==="forest"){

drawForest();

}

else if(state==="classroom"){

drawClassroom();

}

else if(state==="bedroom"){

drawBedroom();

}



requestAnimationFrame(gameLoop);

}



gameLoop();

</script>

</body>
</html>
