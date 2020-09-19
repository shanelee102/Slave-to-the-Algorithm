This week I began looking for ways to apply filters to images. I found a lot of interesting ways to manipulate an image through this site : https://medium.com/@delightful_Kdub/image-manipulation-with-processing3-c52ec08bbf27 

But as I am currently trying to work with P5.js, I began scouring for something similar for P5. 

I did a little experimenting on the P5.js web editor with the help of this site: https://codeburst.io/instagram-filters-with-javascript-p5-js-83f28c9f7fda
, experimenting with adding filters to video capture.

![capture_filter_ellipse](https://user-images.githubusercontent.com/68723452/93660950-53228b80-fa97-11ea-9779-e39776e3fba0.JPG)

var capture;

function setup() {
  createCanvas(400, 400);
  capture = createCapture (VIDEO)
  capture.size (400, 300);
  noStroke();
}

function draw() {
  background(0);
  capture.loadPixels();
  var stepSize = 5
  for (var x = 0; x < capture.width; x += stepSize){
  for (var y = 0; y < capture.height; y += stepSize){ 
    var index = ((y*capture.width) + x) * 4;
    var redVal = capture.pixels[index];
    var greenVal = capture.pixels[index + 1];
    var blueVal = capture.pixels[index + 2];
    fill(redVal,greenVal,blueVal);
    ellipse (x,y, stepSize, stepSize);
    }
  }
}

![capture_filter_rect](https://user-images.githubusercontent.com/68723452/93660955-587fd600-fa97-11ea-9369-8ee750618eb4.JPG)

var capture;

function setup() {
  createCanvas(400, 400);
  capture = createCapture (VIDEO)
  capture.size (400, 300);
  noStroke();
}

function draw() {
  background(0);
  capture.loadPixels();
  var stepSize = 5
  for (var x = 0; x < capture.width; x += stepSize){
  for (var y = 0; y < capture.height; y += stepSize){ 
    var index = ((y*capture.width) + x) * 4;
    var redVal = capture.pixels[index];
    var greenVal = capture.pixels[index + 1];
    var blueVal = capture.pixels[index + 2];
    fill(redVal,greenVal,blueVal);
    rect (x,y, stepSize, stepSize);
    }
  }
}

![capture_filter_rect_8](https://user-images.githubusercontent.com/68723452/93661024-d9d76880-fa97-11ea-8e19-9602129d8be9.JPG)

var capture;

function setup() {
  createCanvas(400, 400);
  capture = createCapture (VIDEO)
  capture.size (400, 300);
  noStroke();
}

function draw() {
  background(0);
  capture.loadPixels();
  var stepSize = 8
  for (var x = 0; x < capture.width; x += stepSize){
  for (var y = 0; y < capture.height; y += stepSize){ 
    var index = ((y*capture.width) + x) * 4;
    var redVal = capture.pixels[index];
    var greenVal = capture.pixels[index + 1];
    var blueVal = capture.pixels[index + 2];
    fill(redVal,greenVal,blueVal);
    rect (x,y, stepSize, stepSize);
    }
  }
}

I started by changing the shapes of the pixels and their size. Then I moved on to experimenting with the colours. 
