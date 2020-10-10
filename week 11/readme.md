Testing the filters:
--------------
```
 let emotion = evaluateEmotion(currWord);
       applyEmotion(emotion);
```
```
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
 ```
 At first it didn't work and I spent a lot of time asking friends and trying to identify what the problem might be. Turns out that the dataset itself has spaces in front of the words which caused the code not to recognise the word. To address the problem we searched up how to remove the last character from a string. 
 ```
  word = word.substring(0, word.length - 1)
    console.log(word)
 ```
Using console.log was really helpful in checking this. 

-------------------------------------------------

After fixing that part of the code, I started seeing the changes, but only for the few words that have tints. Somehow the filters like filter(DILATE); wasn't showing. I've also tried drawing the image behind the filter within the function with no results. 

I decided to assign each emotion to a colour instead for now until I could figure out how to get them working. The colours ended up working really well. 
Some words weren't as accurate as I'd hoped and not a lot of common words are on the dataset but some of them were fairly accurate for example "stress" results in red for anger, "virus" gives purple for fear, "achievement" gives yellow for happy, "empty" results in blue for sad and "waste" gives green for disgust. Some other words were'nt as accurate however as "hello" results in blue for sad. All in all I was glad to get it working and it was a gratifying moment to see the colours change as I spoke. 



