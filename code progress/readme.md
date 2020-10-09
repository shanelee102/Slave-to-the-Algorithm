```
let lang = navigator.language || 'en-US';

let table;

let speechRec = new p5.SpeechRec(lang, onResult);
let continuous = true;
let interim = true;
var runningText;

let img;
var imageDrawWidth = 500;
var imageDrawHeight = 500;
let checkingSpeech = false;
let currWord = false;
let splitted = [];

//let myFont;
//function preload() {
//  myFont = loadFont('data/Verdana-BoldItalic-48.vlw');
//}

function preload() {
  table = loadTable('assets/Andbrain_DataSet.csv', 'csv', 'header');
}

function setup() {
  
  background(0);
  createCanvas(windowWidth, windowHeight);
  
  img = loadImage ('assets/japan_lantern.jpg');
 
  speechRec.start(continuous, interim);
  
}

function draw() {
  background(0);
  image(
    img, 
    windowWidth/2-imageDrawWidth/2, 
    windowHeight/2-imageDrawHeight/2, 
    imageDrawWidth, 
    imageDrawHeight
  ); 
  
  if (currWord) {
     textSize(48);
     fill(255);
     textFont('helvetica');
     text(currWord, 300, height/2);
  }
}
//function drawText(font) {
//  fill(255);
//  textFont(font, 36);
//  text('p5*js', 10, 50);
//}

function onResult() {
  
  // When speech to text finds a said sentence
  // and currently not checking other sentence
  // start checking this one
  if (speechRec.resultValue && !checkingSpeech) {
    checkingSpeech = true;
    
    splitted = speechRec.resultString.split(" ");
    processWord();
  }
}

function processWord() {
  if (splitted.length > 0) {
    
    // Get the next word in sentence array
    currWord = splitted.shift();
    
    // Find the emotion and apply the
    // filter for this word
    let emotion = evaluateEmotion(currWord);
       applyEmotion(emotion);
    // Calls for to process the next
    // word in the sentence array
    setTimeout(processWord, 1000);
  }
  else {
    checkingSpeech = false;
    currWord = false;
  }
}

function evaluateEmotion(givenWord) {
  
  // Cycle through the table
  for (let r = 0; r < table.getRowCount(); r++){
    let word = table.getString(r, 0);
    word = word.substring(0, word.length - 1)
    console.log(word)
    
    if (word == givenWord) {
      let scores = {
        "disgust": parseFloat(table.getString(r, 1)),
        "surprise": parseFloat(table.getString(r, 2)),
        "neutral": parseFloat(table.getString(r, 3)),
        "anger": parseFloat(table.getString(r, 4)),
        "sad": parseFloat(table.getString(r, 5)),
        "happy": parseFloat(table.getString(r, 6)),
        "fear": parseFloat(table. getString(r, 7))
      };
      
      // Runs through dictionary to get largest value
      let largest = Object.keys(scores).reduce(function(a, b){ return scores[a] > scores[b] ? a : b });
      return largest;
    }
    //console.log(evaluateEmotion(givenWord));
  }
  return false;
}
function applyEmotion(emotion){
 
 if (emotion == "disgust"){
 disgustFilter();
 }
 else if (emotion == "surprise"){
 surpriseFilter();
 }
 else if (emotion == "neutral"){
 neutralFilter();
 }
 else if (emotion == "anger"){
 angerFilter();
 }
 else if (emotion == "sad"){
 sadFilter(); 
 }
 else if (emotion == "happy"){
 happyFilter();
 }
 else if (emotion == "fear"){
 fearFilter();
 }
 //console.log(emotion);
}
function disgustFilter(){
 //filter(DILATE); 
   image(
    img, 
    windowWidth/2-imageDrawWidth/2, 
    windowHeight/2-imageDrawHeight/2, 
    imageDrawWidth, 
    imageDrawHeight
    );
 tint (0, 255, 103, 126); 
}
function surpriseFilter(){
  image(
    img, 
    windowWidth/2-imageDrawWidth/2, 
    windowHeight/2-imageDrawHeight/2, 
    imageDrawWidth, 
    imageDrawHeight
    );
 tint (255, 20, 146, 126); 
}
function neutralFilter(){
  image(
    img, 
    windowWidth/2-imageDrawWidth/2, 
    windowHeight/2-imageDrawHeight/2, 
    imageDrawWidth, 
    imageDrawHeight
    );
 tint (136, 136, 136, 126);
}
function angerFilter(){
 //filter(POSTERIZE, 3); 
 image(
    img, 
    windowWidth/2-imageDrawWidth/2, 
    windowHeight/2-imageDrawHeight/2, 
    imageDrawWidth, 
    imageDrawHeight
    );
 tint (255, 0, 0, 126);
}
function sadFilter(){
 //filter (BLUR, 3); 
 image(
    img, 
    windowWidth/2-imageDrawWidth/2, 
    windowHeight/2-imageDrawHeight/2, 
    imageDrawWidth, 
    imageDrawHeight
    );
 tint (0, 255, 255, 126);
}
function happyFilter(){
  image(
  img, 
    windowWidth/2-imageDrawWidth/2, 
    windowHeight/2-imageDrawHeight/2, 
    imageDrawWidth, 
    imageDrawHeight
    );
 tint (255, 213, 0, 126);
}
function fearFilter(){
//filter (ERODE);
image(
    img, 
    windowWidth/2-imageDrawWidth/2, 
    windowHeight/2-imageDrawHeight/2, 
    imageDrawWidth, 
    imageDrawHeight
    );
 tint (125, 0, 255, 126);
}
```


