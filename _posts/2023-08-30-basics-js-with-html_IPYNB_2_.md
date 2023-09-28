---
title: Using Javascript with HTML DOM
hide: True
description: A Tech Talk on how javascript can interact with HTML DOM
type: ccc
permalink: /basics/dom
author: Rohan Juneja
---

{% include nav_basics.html %}


# Following along
Remember to "git pull" on teacher repository to update to lates.
- Run this notebook in VSCode
- Activate Help-Toogel Developer Tools to add console outputs to runtime experience

# Referencing HTML elements using javascript
- To get an HTML element, use ``document.getElementById("idTag")``
- You will use the ID that you set in your HTML
- if you `console.log` the resulting variable you will get some information about the element


```python
%%html
<!-- the ID must be specified within the element -->
<h1 id="domTitleID">My Title</h1>

<!-- javascript goes here -->
<script>
var titleElement = document.getElementById("domTitleID")
<!-- outputs h1 tag -->
console.log("Example #1, show element in DOM")
console.log(titleElement)
</script>
```


<!-- the ID must be specified within the element -->
<h1 id="domTitleID">My Title</h1>

<!-- javascript goes here -->
<script>
var titleElement = document.getElementById("domTitleID")
<!-- outputs h1 tag -->
console.log("Example #1, show element in DOM")
console.log(titleElement)
</script>



# Getting the data within the HTML element
- The variable titleElement stores the "object"
- Basically think of this as the group of data enclosed in HTML tag
- To access a certain type of data from an "object" we use "." notation
  - .innerHTML gets data within center of tag


```python
%%html
<!-- the ID must be specified within the element -->
<h1 id="domTitleIDget">My Title</h1>

<!-- javascript goes here -->
<script>
var titleElement = document.getElementById("domTitleIDget")
<!-- outputs h1 innerHTML from h1 tag -->
console.log("Example #2, show innerHTML")
console.log(titleElement.innerHTML)
</script>
```


<!-- the ID must be specified within the element -->
<h1 id="domTitleIDget">My Title</h1>

<!-- javascript goes here -->
<script>
var titleElement = document.getElementById("domTitleIDget")
<!-- outputs h1 innerHTML from h1 tag -->
console.log("Example #2, show innerHTML")
console.log(titleElement.innerHTML)
</script>



# Setting the data within the HTML Element
- The innerHTML data in this "object" can be set like a variable
  - Change the value of the innerHTML using the "=" (assignment) operator


```python
%%html
<!-- the ID must be specified on the element -->
<h1 id="domTitleIDset">My Title</h1>

<!-- javascript goes here -->
<script>
var titleElement = document.getElementById("domTitleIDset")
titleElement.innerHTML = "Set and Update My Title"
<!-- outputs h1 innerHTML after h1 tag has been updated -->
console.log("Example #3, update innerHTML")
console.log(titleElement.innerHTML)
</script>
```


<!-- the ID must be specified on the element -->
<h1 id="domTitleIDset">My Title</h1>

<!-- javascript goes here -->
<script>
var titleElement = document.getElementById("domTitleIDset")
titleElement.innerHTML = "Set and Update My Title"
<!-- outputs h1 innerHTML after h1 tag has been updated -->
console.log("Example #3, update innerHTML")
console.log(titleElement.innerHTML)
</script>



# Creating elements
- Create a new element with the document.createElement function -> takes in the type of element
- Set properties in the element just like the "h1" example


```python
%%html
<!-- the ID must be specified on the element -->
<div id="divContainerID">
    <h1 id="h1ElementID">My Title</h1>
</div>

<!-- javascript goes here -->
<script>
   // creates a new element
   var pElement = document.createElement("p")
   pElement.innerHTML = "Starting a paragraph of text."
   
   // outputs p tag after it has been created
   console.log("Example #4, create a p tag within JS")
   console.log(pElement)
</script>
```


<!-- the ID must be specified on the element -->
<div id="divContainerID">
    <h1 id="h1ElementID">My Title</h1>
</div>

<!-- javascript goes here -->
<script>
   // creates a new element
   var pElement = document.createElement("p")
   pElement.innerHTML = "Starting a paragraph of text."

   // outputs p tag after it has been created
   console.log("Example #4, create a p tag within JS")
   console.log(pElement)
</script>



# Issue! How to Create element that appears in HTML?
- Here is a visualization of what is happening => the "p" is not placed inside the HRML page!
![visual on p tag floating]({{ site.baseurl }}/images/dom-visual-1.png)


# Solution
- Correct by placeing the element somewhere in the page
- For example, we could add the element within the div
   - For this, use the appendChild function on the div object (the parameter would be the p element we created)
   - Remember, use the getELementById to get the object for something in the html (the div!)
- Updated Diagram
![visual on p tag in div]({{ site.baseurl }}/images/dom-visual-2.png)


```python
%%html
<!-- the ID must be specified on the element -->
<div id="divContainerIDset">
    <h1 id="h1ElementIDset">My Title</h1>
</div>

<!-- javascript goes here -->
<script>
   // creates a new element
   var pElement = document.createElement("p")
   pElement.innerHTML = "Starting a paragraph of text."
   
   // outputs p tag after it has been created
   console.log("Example #5, add p tag to HTML")
   console.log(pElement)
   
   // place the p element inside the HTML page
   var div = document.getElementById("divContainerIDset")
   div.appendChild(pElement)
</script>
```


<!-- the ID must be specified on the element -->
<div id="divContainerIDset">
    <h1 id="h1ElementIDset">My Title</h1>
</div>

<!-- javascript goes here -->
<script>
   // creates a new element
   var pElement = document.createElement("p")
   pElement.innerHTML = "Starting a paragraph of text."

   // outputs p tag after it has been created
   console.log("Example #5, add p tag to HTML")
   console.log(pElement)

   // place the p element inside the HTML page
   var div = document.getElementById("divContainerIDset")
   div.appendChild(pElement)
</script>



# Functions in JavaScript, using with DOM
- Functions allow you to "do something"
  - ex. "eat food" in a Snake Game
- Functions were used in previous examples
  - console.log = "print something"
  - document.getElementById = "find an element with id"
- Functions take in parameters, what to do (inside the parenthesis)
  - the parameter tells console.log what to print
  - the parameter in document.getElementById tells the id of the element
- Functions can be used with DOM as well, thes will be shown below

# Creeating functions
- document functions functions were used to create a lot of functionality, but how can a developer create their own?
- function are useful to avoid writing the same code over and over again
- function can contain parameters for input (they effectively become variables)
- function can contain a return, the are the "output" of the function


```python
%%html
<!-- the ID must be specified on the element -->
<div id="divContainerIDfunction">
    <h1 id="h1ElementIDfunction">My Title</h1>
</div>

<!-- javascript goew here -->
<script>
    // define a function => takes parameter text, returns a new p tab
    function createPTag(text) {
        // creates a new element
        var pElement = document.createElement("p")

        // using the parameter like a variable
        pElement.innerHTML = text
        
        // outputs p tag after it has been created
        console.log("Example #6, add p tag using a function")
        console.log(pElement)

        return pElement;
    }

    // using a function to create p tag
    var pTag = createPTag("Starting a paragraph with cooler text than before.")

    // place the p element in the webpage
    var div = document.getElementById("divContainerIDfunction")
    div.appendChild(pTag)
</script>
```


<!-- the ID must be specified on the element -->
<div id="divContainerIDfunction">
    <h1 id="h1ElementIDfunction">My Title</h1>
</div>

<!-- javascript goew here -->
<script>
    // define a function => takes parameter text, returns a new p tab
    function createPTag(text) {
        // creates a new element
        var pElement = document.createElement("p")

        // using the parameter like a variable
        pElement.innerHTML = text

        // outputs p tag after it has been created
        console.log("Example #6, add p tag using a function")
        console.log(pElement)

        return pElement;
    }

    // using a function to create p tag
    var pTag = createPTag("Starting a paragraph with cooler text than before.")

    // place the p element in the webpage
    var div = document.getElementById("divContainerIDfunction")
    div.appendChild(pTag)
</script>



# OnClick Event
- Run a function when an event occurs
   - In this case, the p tag is created when the button is clicked


```python
%%html
<!-- the ID must be specified on the elements -->
<button id="buttonID">Click here!</button>

<div id="divContainerIDbutton">
    <h1 id="h1ElementIDbutton">My Title</h1>
</div>

<!-- our javascript goe here -->
<script>
    // define a function => takes parameter text, returns a new p tab
    function createPTag(text) {
        // creates a new element
        var pElement = document.createElement("p")

        // using the parameter like a variable
        pElement.innerHTML = text
        
        // outputs p tag after it has been created
        console.log("Example #7.1, add p tag using a function")
        console.log(pElement)

        return pElement;
    }

    // create a function that sets specific text and adds to div
    function addPTagOnButton() {
        // using our new function
        var pTag = createPTag("Starting a paragraph with text created on button press.")

        // place the p element in the webpage
        var div = document.getElementById("divContainerIDbutton")

        // add p tag to the div
        div.appendChild(pTag)
        
        // outputs p tag after it has been created
        console.log("Example #7.2, update container adding a 'p' tag")
        console.log(div)
    }

    // add the P tag when our button is clicked
    var myButton = document.getElementById("buttonID")
    myButton.onclick = addPTagOnButton
    
</script>
```


<!-- the ID must be specified on the elements -->
<button id="buttonID">Click here!</button>

<div id="divContainerIDbutton">
    <h1 id="h1ElementIDbutton">My Title</h1>
</div>

<!-- our javascript goe here -->
<script>
    // define a function => takes parameter text, returns a new p tab
    function createPTag(text) {
        // creates a new element
        var pElement = document.createElement("p")

        // using the parameter like a variable
        pElement.innerHTML = text

        // outputs p tag after it has been created
        console.log("Example #7.1, add p tag using a function")
        console.log(pElement)

        return pElement;
    }

    // create a function that sets specific text and adds to div
    function addPTagOnButton() {
        // using our new function
        var pTag = createPTag("Starting a paragraph with text created on button press.")

        // place the p element in the webpage
        var div = document.getElementById("divContainerIDbutton")

        // add p tag to the div
        div.appendChild(pTag)

        // outputs p tag after it has been created
        console.log("Example #7.2, update container adding a 'p' tag")
        console.log(div)
    }

    // add the P tag when our button is clicked
    var myButton = document.getElementById("buttonID")
    myButton.onclick = addPTagOnButton

</script>



# Hacks
- Copy your HTML code from the HTML hacks. Write a Javascript snippet to switch the links of the two a tags when a button is pressed. Once they are switched, change the inner HTML of the top p tag to the word "switched!"


```python
%%html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vibrant Webpage Example</title>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;700&display=swap">
    <style>
        /* Reset some default styles */
        body {
            margin: 0;
            padding: 0;
            font-family: 'Open Sans', sans-serif;
        }

        /* Style for the navbar */
        .navbar {
            background-color: #333;
            overflow: hidden;
        }

        /* Style for navbar links */
        .navbar a {
            float: left;
            display: block;
            color: white;
            text-align: center;
            padding: 14px 16px;
            text-decoration: none;
            transition: background-color 0.3s ease, color 0.3s ease;
        }

        /* Hover effect for navbar links */
        .navbar a:hover {
            background-color: #555;
            color: white;
            transform: scale(1.1); /* Scale effect on hover */
        }

        /* Style for navbar buttons */
        .navbar .btn {
            background-color: #4CAF50;
            border: none;
            color: white;
            padding: 10px 20px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 16px;
            margin: 4px 2px;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.3s ease;
        }

        /* Hover effect for navbar buttons */
        .navbar .btn:hover {
            background-color: #45a049;
            transform: scale(1.1) rotate(10deg); /* Scale and rotate effect on hover */
        }

        /* Style for dropdown menu */
        .dropdown {
            float: left;
            overflow: hidden;
        }

        /* Style for dropdown button */
        .dropdown .dropbtn {
            font-size: 16px;
            border: none;
            outline: none;
            color: white;
            background-color: inherit;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.3s ease;
            padding: 14px 16px;
        }

        /* Hover effect for dropdown button */
        .dropdown .dropbtn:hover {
            background-color: #555;
            color: white;
            transform: scale(1.1); /* Scale effect on hover */
        }

        /* Style for dropdown content */
        .dropdown-content {
            display: none;
            position: absolute;
            background-color: #f9f9f9;
            min-width: 160px;
            box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
            z-index: 1;
            transition: opacity 0.3s ease, visibility 0.3s ease;
            opacity: 0;
            visibility: hidden;
        }

        /* Style for dropdown links */
        .dropdown-content a {
            float: none;
            color: black;
            padding: 12px 16px;
            text-decoration: none;
            display: block;
            text-align: left;
            transition: background-color 0.3s ease, color 0.3s ease;
        }

        /* Hover effect for dropdown links */
        .dropdown-content a:hover {
            background-color: #ddd;
            color: black;
            transform: rotate(-5deg); /* Rotate effect on hover */
        }

        /* Show the dropdown menu on hover */
        .dropdown:hover .dropdown-content {
            display: block;
            opacity: 1;
            visibility: visible;
        }

        /* Style for the paragraph */
        .content {
            margin-top: 20px;
            padding: 20px;
            border: 1px solid #ddd;
            background-color: white; /* White background for content */
        }

        /* Additional links and buttons */
        .additional-content {
            text-align: center;
            padding: 20px;
        }

        .additional-content a {
            display: inline-block;
            margin: 10px;
            padding: 10px 20px;
            background-color: #3498db; /* Vibrant button color */
            color: white;
            text-decoration: none;
            border-radius: 5px;
            transition: background-color 0.3s ease, transform 0.3s ease;
        }

        /* Hover effect for additional links */
        .additional-content a:hover {
            background-color: #2980b9; /* Darker button color on hover */
            transform: scale(1.2) rotate(15deg); /* Scale and rotate effect on hover */
        }
        
    </style>
</head>
<body>
    <!-- Navbar -->
    <div class="navbar">
        <a href="https://www.microsoft.com">Microsoft</a>
        <a href="https://www.apple.com">Apple</a>
        <div class="dropdown">
            <button class="dropbtn">Services</button>
            <div class="dropdown-content">
                <a href="https://www.amazon.com">Amazon</a>
                <a href="https://www.grammarly.com">Grammarly</a>
                <a href="#">Service 3</a>
            </div>
        </div>
        <div class="dropdown">
            <button class="dropbtn">More</button>
            <div class="dropdown-content">
                <a href="https://www.youtube.com">YouTube</a>
                <a href="https://www.google.com">Google</a>
                <a href="https://www.openai.com">OpenAI</a>
            </div>
        </div>
        <a href="https://www.python.org">Python</a>
        <a href="https://www.java.com">Java</a>
        <button class="btn" onclick="shuffleLinksAndButtons()">Shuffle</button>
    </div>

    <!-- Content -->
    <div class="content">
        <p>This is some content below the navbar.</p>
    </div>

    <!-- Additional Links and Buttons -->
    <div class="additional-content">
        <a href="#">Link 1</a>
        <a href="#">Link 2</a>
        <button onclick="showAlert()" class="btn">Button 1</button>
        <button onclick="showAlert()" class="btn">Button 2</button>
    </div>

    <script>
        // Function to shuffle the links and buttons randomly
        function shuffleLinksAndButtons() {
            // Get all the links and buttons
            const linksAndButtons = document.querySelectorAll('.navbar a, .dropdown-content a, .additional-content a, .navbar .btn, .additional-content .btn');

            // Convert NodeList to an array
            const linksAndButtonsArray = Array.from(linksAndButtons);

            // Shuffle the array randomly
            shuffleArray(linksAndButtonsArray);

            // Update the DOM with the shuffled links and buttons
            linksAndButtonsArray.forEach((element, index) => {
                // Replace the content of the original elements with shuffled elements
                linksAndButtons[index].textContent = element.textContent;
                linksAndButtons[index].setAttribute('href', element.getAttribute('href'));
            });
        }

        // Function to show an alert when a button is clicked
        function showAlert() {
            alert("Button clicked!");
        }

        // Fisher-Yates shuffle algorithm
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
        }
    </script>
</body>
```


<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vibrant Webpage Example</title>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;700&display=swap">
    <style>
        /* Reset some default styles */
        body {
            margin: 0;
            padding: 0;
            font-family: 'Open Sans', sans-serif;
        }

        /* Style for the navbar */
        .navbar {
            background-color: #333;
            overflow: hidden;
        }

        /* Style for navbar links */
        .navbar a {
            float: left;
            display: block;
            color: white;
            text-align: center;
            padding: 14px 16px;
            text-decoration: none;
            transition: background-color 0.3s ease, color 0.3s ease;
        }

        /* Hover effect for navbar links */
        .navbar a:hover {
            background-color: #555;
            color: white;
            transform: scale(1.1); /* Scale effect on hover */
        }

        /* Style for navbar buttons */
        .navbar .btn {
            background-color: #4CAF50;
            border: none;
            color: white;
            padding: 10px 20px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 16px;
            margin: 4px 2px;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.3s ease;
        }

        /* Hover effect for navbar buttons */
        .navbar .btn:hover {
            background-color: #45a049;
            transform: scale(1.1) rotate(10deg); /* Scale and rotate effect on hover */
        }

        /* Style for dropdown menu */
        .dropdown {
            float: left;
            overflow: hidden;
        }

        /* Style for dropdown button */
        .dropdown .dropbtn {
            font-size: 16px;
            border: none;
            outline: none;
            color: white;
            background-color: inherit;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.3s ease;
            padding: 14px 16px;
        }

        /* Hover effect for dropdown button */
        .dropdown .dropbtn:hover {
            background-color: #555;
            color: white;
            transform: scale(1.1); /* Scale effect on hover */
        }

        /* Style for dropdown content */
        .dropdown-content {
            display: none;
            position: absolute;
            background-color: #f9f9f9;
            min-width: 160px;
            box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
            z-index: 1;
            transition: opacity 0.3s ease, visibility 0.3s ease;
            opacity: 0;
            visibility: hidden;
        }

        /* Style for dropdown links */
        .dropdown-content a {
            float: none;
            color: black;
            padding: 12px 16px;
            text-decoration: none;
            display: block;
            text-align: left;
            transition: background-color 0.3s ease, color 0.3s ease;
        }

        /* Hover effect for dropdown links */
        .dropdown-content a:hover {
            background-color: #ddd;
            color: black;
            transform: rotate(-5deg); /* Rotate effect on hover */
        }

        /* Show the dropdown menu on hover */
        .dropdown:hover .dropdown-content {
            display: block;
            opacity: 1;
            visibility: visible;
        }

        /* Style for the paragraph */
        .content {
            margin-top: 20px;
            padding: 20px;
            border: 1px solid #ddd;
            background-color: white; /* White background for content */
        }

        /* Additional links and buttons */
        .additional-content {
            text-align: center;
            padding: 20px;
        }

        .additional-content a {
            display: inline-block;
            margin: 10px;
            padding: 10px 20px;
            background-color: #3498db; /* Vibrant button color */
            color: white;
            text-decoration: none;
            border-radius: 5px;
            transition: background-color 0.3s ease, transform 0.3s ease;
        }

        /* Hover effect for additional links */
        .additional-content a:hover {
            background-color: #2980b9; /* Darker button color on hover */
            transform: scale(1.2) rotate(15deg); /* Scale and rotate effect on hover */
        }

    </style>
</head>
<body>
    <!-- Navbar -->
    <div class="navbar">
        <a href="https://www.microsoft.com">Microsoft</a>
        <a href="https://www.apple.com">Apple</a>
        <div class="dropdown">
            <button class="dropbtn">Services</button>
            <div class="dropdown-content">
                <a href="https://www.amazon.com">Amazon</a>
                <a href="https://www.grammarly.com">Grammarly</a>
                <a href="#">Service 3</a>
            </div>
        </div>
        <div class="dropdown">
            <button class="dropbtn">More</button>
            <div class="dropdown-content">
                <a href="https://www.youtube.com">YouTube</a>
                <a href="https://www.google.com">Google</a>
                <a href="https://www.openai.com">OpenAI</a>
            </div>
        </div>
        <a href="https://www.python.org">Python</a>
        <a href="https://www.java.com">Java</a>
        <button class="btn" onclick="shuffleLinksAndButtons()">Shuffle</button>
    </div>

    <!-- Content -->
    <div class="content">
        <p>This is some content below the navbar.</p>
    </div>

    <!-- Additional Links and Buttons -->
    <div class="additional-content">
        <a href="#">Link 1</a>
        <a href="#">Link 2</a>
        <button onclick="showAlert()" class="btn">Button 1</button>
        <button onclick="showAlert()" class="btn">Button 2</button>
    </div>

    <script>
        // Function to shuffle the links and buttons randomly
        function shuffleLinksAndButtons() {
            // Get all the links and buttons
            const linksAndButtons = document.querySelectorAll('.navbar a, .dropdown-content a, .additional-content a, .navbar .btn, .additional-content .btn');

            // Convert NodeList to an array
            const linksAndButtonsArray = Array.from(linksAndButtons);

            // Shuffle the array randomly
            shuffleArray(linksAndButtonsArray);

            // Update the DOM with the shuffled links and buttons
            linksAndButtonsArray.forEach((element, index) => {
                // Replace the content of the original elements with shuffled elements
                linksAndButtons[index].textContent = element.textContent;
                linksAndButtons[index].setAttribute('href', element.getAttribute('href'));
            });
        }

        // Function to show an alert when a button is clicked
        function showAlert() {
            alert("Button clicked!");
        }

        // Fisher-Yates shuffle algorithm
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
        }
    </script>
</body>


