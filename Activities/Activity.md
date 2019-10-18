## Acrivity 25: Render To-Dos  ##

*  This activity is to create a function that will render our todos into a list in the browser.

 ```javascript
 	  function renderTodos(){
   //Initially set the text content of the todoList to an empty string.
    todoList.textContent="";
   //todoCountSpan should show the total count of todos on the page.
    todoCountSpan.innerHTML=count;
   // Inside of your render function you will also need a for loop. 
    for (var i=0;i<todos.length;i++){
   //It should loop over the `todos` array creating an `li` element for each index of the array.   
      var liEl=document.createElement("li");
   // It should set the content of the created `li` element to the value of the current array index.   
      liEl.textContent=todos[i];
   //Finally the new `li` should be appended to the `ul` provided   
      todoList.append(liEl); 
    }
  }
  renderTodos();//function call
```
---
## Activity 26: Add Todo's##
* In this activity, we continued to build on our Todo activity. This time, we added the `add` functionality

```javascript

 	// Add an event listener so that when a user hits enter, the value from the todo input field is pushed to our todo array.

  todoForm.addEventListener("submit",addInput);

  function addInput(event){
    event.preventDefault();
    var input=todoInput.value.trim();
  //Make sure that empty values are not pushed to the array.
    if(input===""){
      return;
    }  
    todos.push(input);
 
 //Once the value has been added to the array, clear the input field and re-render the todo list. 
   todoInput.value="";
   renderTodos();
  }
 		   
```
---
## Activity 27: Complete Todos ##

* In this activity, we created a "complete" button that successfully removes a todo item from the list when clicked.

```javascript
function renderTodos() {
  // Clear todoList element and update todoCountSpan
  todoList.innerHTML = "";
  todoCountSpan.textContent = todos.length;

  // Render a new li for each todo
  for (var i = 0; i < todos.length; i++) {
    var todo = todos[i];

    var li = document.createElement("li");
    li.textContent = todo;
  // When a new todo is created, add a `data-index` for each `li`  
    li.setAttribute("data-index",i);
  // Create a complete button  
    var button=document.createElement("button");
    button.textContent="complete";
  //append the button to the li element
    li.append(button);
  //append the li element to unordered list  
    todoList.appendChild(li);
    
  }
}

//Add an event listener so that when a user clicks the Complete button, it accesses the `data-index` value and removes that todo element from the list.
todoList.addEventListener("click",removeTodo);
function removeTodo(event){
   event.preventDefault();
  if (event.target.matches("button")){ //if the clicked element is a button, find which element to remove from list by accessing parent's data-index
// use `setAttribute` for `data-index` 
    var dIndex=event.target.parentElement.getAttribute("data-index");
// use  `splice` to remove the selected todo from the list    
    todos.splice(dIndex,1);
//render Todos again    
    renderTodos();
 }
 ```
---

## Activity 28: Local Storage ToDos:  

* In this activity, we worked on storing our todos in `localStorage`. 

```javascript

function init() {
  // Write code here to check if there are todos in localStorage
  // If so, parse the value from localStorage and assign it to the todos variable
  //Set a variable called `storedTodos` that retrieves the todos from `localStorage` and parses the JSON string to an object.
  var storedToDos=localStorage.getItem("todos");
 // Check if the todos were retrieved from `localStorage` and if so, set a `todos` variable with the `storedTodos`.
  if (storedToDos!=null){
      todos=JSON.parse(storedToDos);
  }
  renderTodos(); //render todo's 
}

function storeTodos() {
  // Add code here to stringify the todos array and save it to the "todos" key in localStorage
  // Stringify and set the "todos" key in `localStorage` to the `todos` array.
  
  localStorage.setItem("todos",JSON.stringify(todos));
}

 ```
--- 
## Third Party APIS   ##
## Activity 2: JSDrinklist:

* This activity is about dynamically generating HTML content that displays all of the drink options. Bonus is instead of using a `for` loop, using the `.forEach` method. So for-loop is commented out.


```javascript

  // 1. Create code that "grabs" the div with the matching id (#drink-options);
    // ...
       var divEl=document.getElementById("drink-options");

    // ...


    // 2. Create a for loop that creates HTML content of all the drinks using JavaScript.
    // HINT: You will need to use each of the following methods: createElement, textContent, appendChild
    // ...
       /* for (var i=0;i<drinkList.length;i++){
          var dEl=document.createElement("p");
          p.textContent=drinkList[i];
          divEl.appendChild(dEl);
        }*/
    // Instead of using a `for` loop, use the `.forEach` method.

        drinkList.forEach(function(drink){
          var dEl=document.createElement("p");
          dEl.textContent=drink;
          divEl.appendChild(dEl);
        });

 
```
---
## Activity 4: JQuery Drink List ##

* In this activity we Re-factor our previous drinkList code from Activity 2, but this time use jQuery to complete all of the same tasks.


```javascript

// Using JavaScript programmatically append each drinkList item to the "drink-options" div
    // HINT: you will need a for loop to go over each element in the list
    var divEl= $("#drink-options");
  /*  for (var i=0;i<drinkList.length;i++){
         var pEl=$("<p>"+drinkList[i]+"</p>");//create a paragraph that holds a drink
         divEl.append(pEl); //append the paragraph to the div.
    }*/

    //Instead of using a `for` loop, try searching about the use of the jQuery `.each` method.
     $.each(drinkList,function(index,drink)
     {
      var pEl=$("<p>"+drink+"</p>");
      divEl.append(pEl);
     }
     );

```
---

## Activity 6: Sandwich Click ##

* In this activity, we add in the missing code such that clicking any of the sandwiches causes…

  1. An alert message to popup saying something snarky about the sandwich type.

  2. A second alert message that displays to the user how many of that specific sandwich they've eaten.

  3. Also the picture of the relative sandwiches is added to the bottom when the sandwich is clicked.

```javascript
$(document).ready(function() {

      // VARIABLES
      // ====================================================================
      // Here we create variables for tracking the number of sandwiches eaten
         var countPbj=0;
         var countGrilledCheese=0;
         var countRoastBeef=0;


      // ...

      // FUNCTIONS
      // ====================================================================
      // Here we create various on "click" functions which capture the clicks
      // Inside each click event is the code to create an alert, update the counter, then show the updated count.
      // ...
            var  divEl=$("#image-div");
           $("#pbj").on("click", function(){
            alert("OK!! Peanut Butter Jelly!!");
            countPbj++;
             alert("You ate "+countPbj+ " Peanut Butter Jelly Sandwiches");
          // BONUS-Add a picture of clicked sandwich at the bottom
          $("#image-div").html("<img src='https://i1.wp.com/snotapwi.com/wp-content/uploads/2017/03/PBJ-Sandwiches.jpg?resize=590%2C368&ssl=1' />");

           })

           $("#grilledcheese").on("click", function(){
            alert("OK!! Grilled Cheese!!");
             countGrilledCheese++;
             alert("You ate "+countGrilledCheese+ " Grilled Cheese Sandwiches");
              // BONUS
             $("#image-div").html("<img src='http://cdn.funcheap.com/wp-content/uploads/2014/04/The-Perfect-Grilled-Cheese-Sandwich-800-158111.jpg' />");
             
           })

           $("#roastbeef").on("click", function(){
            alert("OK!! Roast Beef!!");
            countRoastBeef++;
             alert("You ate "+countRoastBeef+ " Roast Beef Sandwiches");
             // BONUS
        $("#image-div").html("<img src='https://www.cscassets.com/recipes/wide_cknew/wide_25336.jpg' />");
           });

```
---
## Activity 7: Trigger Random
* In this activity, clicking the blue button generates and displays a random number between 1 and 1000

```javascript

  $("#random-button").on("click",function(event){
              event.preventDefault();
        //Create random numberr between 1 and 1000      
              var random=Math.floor((Math.random()*1000)+1);
        //Show the random number on the page
              $("#random-number").text(random);
   });

```
---

## Activity 8:Lottery Generator ##

* In this activity, using the code from activity 7 random number generator as a starting point,  we created a lottery generator.

```javascript

 $(document).ready(function() {

      $("#random-button").on("click", function() {

        // Create a string which will hold the lottery number
        var str= "";

        // Then initiate a loop to generate 9 separate numbers
        for (var i = 0; i < 9; i++) {

          // For each iteration, generate a new random number between 0 and 9.
          var random = Math.floor(Math.random() * 10);

          // Take this number and then add it to the rest of the string.
          // In essence, we are iteratively building a string of numbers. (e.g. First: 1, Second: 13, Third: 135, etc.)
          str = str+random ;
           
        }
       
        // ... and then dump the random number into our random-number div.
        $("#random-number").prepend(str+"<br><hr>");

      });

    });
```    
-- 
## Activity 9:Number Checker ##

* In this activity, we created a number guessing game.

```javascript
$(document).ready(function() {

            // Here we create the on click event that gets the user's pick
            $(".btn-choice").on("click", function() {
              
              // computer picks a random number between 1 and 4.
               var random=Math.floor((Math.random()*4)+1);
              // Then determine which button was clicked
               var choice=$(this).val();
                // Compare the computer and user guess
                if(random===parseInt(choice)){
                //If the user’s number matches the computer’s number, display text informing them that they've won in the "Result" Card
                $("#result").text("You guessed it right!!");
                //reveal computer's choice
                $("#computer-pick").text(random);
                }
                else{ 
               // Otherwise, display text informing them that they've lost.
               $("#result").text("You guessed it wrong!!");
               //reveal computer's choice
                $("#computer-pick").text(random);
              }
              
              

            });
          });

```

## Activity 10 : Captain Planet Game ##
* In this activity, I created a copy button which clones Captain Planet

[clone]("copy-captain.png");

```javascript
$(".copy-button").on("click", function() {
      
      
      x=captainPlanet.clone(true).appendTo(".col-lg-6");
      x.animate({left:"+=2000"},10000);
      
});

 ```
---

## Activity 11: Fridge Game ##

* In this activity, we created a game as follows

  1. JavaScript dynamically generates buttons for each of the letters on the screen.

  2. Clicking any of the buttons leads the SAME letter to be displayed on the fridge.

  3. Hitting the clear button erases all of the letters from the fridge.

```javascript

 $(document).ready(function() {

      // Here we are provided an initial array of letters.
      // Use this array to dynamically create buttons on the screen.
      var letters = ["A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z", "_"];


      // MAJOR TASK #1: DYNAMICALLY CREATE BUTTONS
      // =================================================================================

      //1. Create a for-loop to iterate through the letters array.
         for(var i=0;i<letters.length;i++){
       //2. Create a variable named "letterBtn" equal to $("<button>");    
           var letterBtn=$("<button>");
      //3. Then give each "letterBtn" the following classes: "letter-button" "letter" "letter-button-color".      
           letterBtn.addClass("letter-button");
           letterBtn.addClass("letter");
           letterBtn.addClass("letter-button-color");
      //4. Then give each "letterBtn" an attribute called "data-letter", with a value eqaual to "letters[i]"      
           letterBtn.attr("data-letter",letters[i]);
      //5. Then give each "letterBtn" a text equal to "letters[i]".      
           letterBtn.text(letters[i]);
      // 6. Finally, append each "letterBtn" to the "#buttons" div (provided).     
           $("#buttons").append(letterBtn);
         }

      // Be sure to test that your code works for this major task, before proceeding to the next one!

      // MAJOR TASK #2: ATTACH ON-CLICK EVENTS TO "LETTER" BUTTONS
      // =================================================================================

      // 7. Create an "on-click" event attached to the ".letter-button" class.
      // Inside the on-click event...
         $(".letter-button").on("click",function(){
      // 8. Create a variable called "fridgeMagnet" and set the variable equal to a new div.
             var fridgeMagnet=$("<div>");
     // 9. Give each "fridgeMagnet" the following classes: "letter fridge-color".         
             fridgeMagnet.addClass("letter")
             fridgeMagnet.addClass("fridge-color");
     // 10. Then chain the following code onto the "fridgeMagnet" variable: .text($(this).attr("data-letter"))        
             fridgeMagnet.text($(this).attr("data-letter"));
     // 11. Lastly append the fridgeMagnet variable to the "#display" div (provided);        
             $("#display").append(fridgeMagnet);
            
         } )


      // Be sure to test that your code works for this major task, before proceeding to the next one!

      // MAJOR TASK #3: ATTACH ON-CLICK EVENTS TO "CLEAR" BUTTON
      // =================================================================================

      // 12. Create an "on-click" event attached to the "#clear" button id.
      // Inside the on-click event..
        $("#clear").on("click",function(){
     // 13. Use the jQuery "empty()" method to clear the contents of the "#display" div.   
          $("#display").empty();
        })
 

    });
```
---
## Activity 13 : Scope Activity 1 ##
* In this activity, we answer scope questions of code.

```javascript

function outside() {
      // what is the scope of this variable?
      var x = 1; // the scope of x is outside()

      // what is the scope of this function and the scope of y?
      function inside(y) {//scope of the function is outside(), scope pf y is inside()

        console.log(x + y); 
      }

      return inside;
    }

    // what is happening here?
    var insideOut = outside();//calling outside returns inside which is assaigned to insideOut.

    // What does this return?
    insideOut(2); //returns 3

    // Uncaught ReferenceError: x is not defined.
    // How does insideOut have access to x?
    console.log("The value of 'x' outside 'outside()' is: " + x);//x is visible inside()
    //and outside returns inside() and assigns it to insideOut, so insideOut has access to x.
    // a closure is created this way since x is not accessible globally.

 ```
---
## Activity 15 : Scope Activity 3 ##
* In this activity, we answer scope questions of code.

```javascript


    // Example One: Global Scope
    // -------------------------------------------
    var a = 1;
    function one() {
      alert("One: " + a);
    }

    // What will get alerted?
    one();//One:1

    // Example Two: Local Scope
    // -------------------------------------------
    function twotop() {

      function two(a) {
        alert("Two: " + a);
      }

      two(a);
    }

    // What will get alerted?
    twotop(); //Two:1

    // Example Three: Local Scope
    // -------------------------------------------
    var a = 5;
    function three() {

      var a = 3;
      alert("Three: " + a);
    }

    // What will get alerted?
    three(); //Three:3

    // Example Four: Local Scope
    // -------------------------------------------
    function first() {
      var a = 5;

      function second() {
        var a = 3;

        function third() {
          alert("Four: " + a);
        }

        third();
      }

      second();

      alert("Five: " + a);
    }

    // What will get alerted?
    first();//Four:3

 ```
 --   
 ## Activity 18 : This Example ##
* In this activity, we answer different questions involving "this" keyword

```javascript


    // EXAMPLE ONE:
    // --------------------------------------------------
    // What is "this" going to print?

    console.log(this); //This refers to the calling object, here no calling object.
                      //This refers to most global object which is "window"


    // EXAMPLE TWO:
    // --------------------------------------------------
    // What is "this" going to print?

    function myFunction() {
      console.log(this);//WINDOW
    }
    myFunction();

    // EXAMPLE THREE (IMPORTANT):
    // --------------------------------------------------
    // What is "someObj.say()" going to print?

    var someObj = {
      name: "Red Hat",
      say: function() {
        console.log(this.name); //"Red Hat"
      }
    };
    someObj.say();


    // EXAMPLE FOUR (BONUS, TRICKY!):
    // --------------------------------------------------
    // What is "myObj.yell()" going to print? Why?

    var myObj = {
      name: "",
      yell: function() {
        this.name = "Star Powerup";

        var changeName = function(newName) {
          this.name = newName;
        };
        changeName("Blue Shell");
        console.log(this);
      }
    };
    myObj.yell(); //OBJECT with name star power up


    // EXAMPLE FIVE (BONUS, TRICKY!):
    // --------------------------------------------------
    // What is "myObj.yell()" going to print? Why?

    var myObj = {
      name: "",
      yell: function() {

        // This line is important!
        var thisObject = this;

        this.name = "Star Powerup";
        var changeName = function(newName) {
          thisObject.name = newName;
        };
        changeName("Blue Shell");
        console.log(thisObject); //OBJECT with name  blue shell. Solves the problem in previous example.
      }
    };
    myObj.yell();


 ```
 --   
  ## Activity 19 : Cobweb ##
* In this activity, we try to find objects in objects with fields: item, items(array) and other nested objects.

```javascript
   
  // Here we are given a cob-web of items. Let's dig in and grab the items we need.
  var theCobWeb = {
    biggestWeb: {
      item: "comb",
      biggerWeb: {
        items: ["glasses", "paperclip", "bubblegum"],
        smallerWeb: {
          item: "toothbrush",
          tinyWeb: {
            items: ["toenails", "lint", "wrapper", "homework"]
          }
        }
      },
      otherBigWeb: {
        item: "headphones"
      }
    }
  };

// Create the code necessary to print each of the following lines using the object above:
// "I found my glasses!"
    console.log("I found my "+theCobWeb.biggestWeb.biggerWeb.items[0]);
// "I found my toothbrush!"
    console.log("I found my "+theCobWeb.biggestWeb.biggerWeb.smallerWeb.item);
// "I found my headphones!"
    console.log("I found my "+theCobWeb.biggestWeb.otherBigWeb.item);
// "I found my homework!"

    console.log("I found my "+theCobWeb.biggestWeb.biggerWeb.smallerWeb.tinyWeb.items[3]);
// Bonus (Extra Hard): It's impossible to complete this in the allotted time. Take this home as a challenge and bring it back to your TA/Instructor for the solution.
// Create a function using JavaScript (NOT jQuery) for which you can pass the name of an item and theCobWeb
// and the function returns the smallest web it was found inside of.
// Your code should work if someone were to modify theCobWeb.  
//  for example if you gave your program 
//    comb it should give back biggestWeb
//    toenails it should give back tinyWeb
//    headphones it should give back otherBigWeb
// HINT: you should use recursion
function isObject(o) {
    return typeof o == "object"; //looks if o is an object type
}

  function findInObj(obj, itemName, webName) {
    for (key in obj) { 
      if (key == "item") { //if there is an item field in the obj
        if (obj[key] == itemName) { //look if item matches the sought item
          console.log(webName);  //if so return the name of the obj
        }
      }else if(key == "items") { //if there is an items array in the obj, return the index of the item in the array, if it's not found it'll retirn -1;
        if (obj[key].indexOf(itemName) > -1) {
          console.log(webName); //if it's found it'll return the index. So we can output the name of the obj.
        }
      }else{
        if (isObject(obj[key])) { //if the field is an object , do more exploration recursively.
          findInObj(obj[key], itemName, key); // recursion
        }
      }
    }
  }
  
  // tests

  // should console log biggestWeb
  findInObj(theCobWeb, "comb", "theCobWeb");

  // should console log tinyWeb
  findInObj(theCobWeb, "toenails", "theCobWeb");

  // should console log otherBigWeb  
  findInObj(theCobWeb, "headphones", "theCobWeb");

  console.log("should have returned biggestWeb, tinyWeb, otherBigWeb");

console.log(rec("comb",theCobWeb));   

 ```
 --   
 ## Activity 20 : JQuery Calvulator  ##
* In this activity, we build a jquery calculator that do addition,multiplication,subtraction, division, power operation and shows them all
on the screen

```javascript
  $(document).ready(function() {

// Your code here...
/*nstructions:
Create the JavaScript logic necessary to add functionality to the jQuery Calculator.
Your calculator should be able to handle basic mathematical operations like addition, subtraction, multiplication, etc.
You should be making use of the existing buttons.
You should be making use of the existing placeholders for entering content (i.e. “firstNumber”, “operator”, “secondNumber”, “result”).
You should have fun and push yourselves! This is a challenge activity—which means, if you get it done, you are a King of jQuery. If you don’t, no sweat. The important thing is that you learned at least a FEW things along the way.*/

//DOM MANIPULATION
  
 //if 0 to 9 is pressed , it'll show on the text field
  
 //add event listeners
   
   var result=$("#result"); //this is the result field for the answer to be shown
   $("#first-number").text("");
   $("#second-number").text("");
  

  $(".btn").on("click",function(){ //when you click a button
     var key=$(this).attr("value"); //you get the value of the clicked button.
     if (!isNaN(key)){ //if the key is a number so it will be 0 to 9
     
        if($("#operator").text()===""){    
          
         $("#first-number").text($("#first-number").text()+key); //if first number is empty, assign first number
        } 
       else{
        $("#second-number").text($("#second-number").text()+key); //if first not empty but second empty, assign second number
       }   
     }
     else{
            switch (key){

              case  "plus":  
                             $("#operator").text("+");   //output the operators       
                             break;
              case  "minus": 
                             $("#operator").text("-");
                             break;
              case "times":  
                             $("#operator").text("*");          
                             break;
              case "divide": 
                             $("#operator").text("/");              
                             break;
              case "power":  
                             $("#operator").text("^");                    
                             break;
              case  "equals": 
                              switch(($("#operator").text())){ //if it's = operator, output the operation
                                case "+": result.text(parseInt($("#first-number").text())+parseInt($("#second-number").text()));break;
                                case "-": result.text(parseInt($("#first-number").text())-parseInt($("#second-number").text()));break;
                                case "*": result.text(parseInt($("#first-number").text())*parseInt($("#second-number").text()));break;
                                case "/": result.text(parseInt($("#first-number").text())/parseInt($("#second-number").text()));break;
                                case "^": result.text(Math.pow(parseInt($("#first-number").text()),parseInt($("#second-number").text())));break;
                               }  
                            break;
            
            }

           
          }  
          
     });    
  });
  function clear(){
      $("#first-number").text("");
      $("#second-number").text("");
      $("#operator").text("");
      $("#result").text("");
  }
  $("#button-clear").on("click",clear);//clears everything 
  
 ```
 --   

