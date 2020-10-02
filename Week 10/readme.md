```
let lang = navigator.language || 'en-US';

let table;

let speechRec = new p5.SpeechRec(lang);
let continuous = true;
let interim = true;
var runningText;

let img;
var imageDrawWidth = 500;
var imageDrawHeight = 500;
let checkingSpeech = false;
let currWord = false;
let splitted = [];

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
  
  // When speech to text finds a said sentence
  // and currently not checking other sentence
  // start checking this one
  if (speechRec.resultValue && !checkingSpeech) {
    checkingSpeech = true;
    splitted = speechRec.resultString.split(" ");
    processWord();
  }
  
  if (currWord) {
     textSize(32);
     fill(255);
     text(currWord, 200, height/2);
  }
}

function processWord() {
  if (splitted.length) {
    
    // Get the next word in sentence array
    currWord = splitted.shift();
    
    // Find the emotion and apply the
    // filter for this word
    let emotion = evaluateEmotion(currWord);
    
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
  }
  return false;
}
function evaluate(){
 let emotion = evaluateEmotion(givenWord);
 
 if (emotion == "disgust"){
 disgustFilter();
 }
 if (emotion == "surprise"){
 surpriseFilter();
 }
 if (emotion == "neutral"){
 neutralFilter();
 }
 if (emotion == "anger"){
 angerFilter();
 }
 if (emotion == "sad"){
 sadFilter(); 
 }
 if (emotion == "happy"){
 happyFilter();
 }
 if (emotion == "fear"){
 fearFilter();
}
function disgustFilter(){
 filter(DILATE); 
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
 filter(POSTERIZE, 3); 
}
function sadFilter(){
 filter (BLUR, 3); 
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
filter (ERODE);
}
```
--------------------------------------------------------------------------------------------------
This is my current progress with the code. Although I've adding filters, I still have not been able to see these filters appearing on screen. 







