```
let table;

function preload() {
table = loadTable('assets/Andbrain_DataSet.csv', 'csv', 'header');
}

function setup() {
  //counts the columns
  print(table.getRowCount() + ' total rows in table');
  print(table.getColumnCount() + ' total columns in table');
  
  //names of the columns
  //print(table.getColumn('name'));
  
  //cycle through the table
  for (let r = 0; r < table.getRowCount(); r++){
    let word = table.getString(r, 0);
    let scores = {
      "disgust": parseFloat(table.getString(r, 1)),
      "suprise": parseFloat(table.getString(r, 2)),
      "neutral": parseFloat(table.getString(r, 3)),
      "anger": parseFloat(table.getString(r, 4)),
      "sad": parseFloat(table.getString(r, 5)),
      "happy": parseFloat(table.getString(r, 6)),
      "fear": parseFloat(table. getString(r, 7))
    };
    
    let largest = Object.keys(scores).reduce(function(a, b){ return scores[a] > scores[b] ? a : b });
    //runs through dictionary to get largest value
    console.log(largest);
  }
}
```
---------------------------------------------------------------------------------------------------------

This is the code I've experimented with using mostly things I found off of the internet. 
I've gotten help from people who have more knowledge in code than me to explain each of the components. 
It was difficult to wrap my head around the process as it was my first time coding. I don't believe 
that I'd be able to get to this point without the help of friends and the internet, so there's still
a lot of basic knowledge I need to grasp. 

But at this stage, the data has been loaded into P5js. The highest value of a word and the emotion the value
is identified. 
