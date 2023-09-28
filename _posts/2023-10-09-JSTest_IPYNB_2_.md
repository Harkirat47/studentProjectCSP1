---
layout: post
title: Web Programming Basics hacks list
description: An introduction to key topics in Web Programming
courses: {'csse': {'week': 6}, 'csp': {'week': 6}}
type: plans
permalink: /basics/home
---

{% include nav_basics.html %}

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
        <a href="#">Home</a>
        <a href="#">About</a>
        <div class="dropdown">
            <button class="dropbtn">Services</button>
            <div class="dropdown-content">
                <a href="#">Service 1</a>
                <a href="#">Service 2</a>
                <a href="#">Service 3</a>
            </div>
        </div>
        <div class="dropdown">
            <button class="dropbtn">More</button>
            <div class="dropdown-content">
                <a href="#">Portfolio</a>
                <a href="#">Testimonials</a>
                <a href="#">Blog</a>
            </div>
        </div>
        <a href="#">Contact</a>
        <button class="btn" onclick="showAlert()">Sign Up</button>
    </div>

    <!-- Content -->
    <div class="content">
        <p>This is some content below the navbar.</p>
    </div>

    <!-- Additional Links and Buttons -->
    <div class="additional-content">
        <a href="#">Link 1</a>
        <a href="#">Link 2</a>
        <button onclick="alert('button is clicked')" class="btn" href = "amazon.com"> Button 1</button>
        <button onclick="showAlert()" class="btn"  href = "#"> button 2 </button>
    </div>

    <script>
        // Function to show an alert when a button is clicked
        function showAlert() {
            alert("Button clicked!");
        }
        function switchButtons() {
            var button1 = document.querySelector('.additional-content button:nth-child(3)');
            var button2 = document.querySelector('.additional-content button:nth-child(4)');
            
            // Clone Button 1 and Button 2
            var button1Clone = button1.cloneNode(true);
            var button2Clone = button2.cloneNode(true);

            // Replace Button 1 with Button 2
            button1.parentNode.replaceChild(button2Clone, button1);
            // Replace Button 2 with Button 1
            button2.parentNode.replaceChild(button1Clone, button2);}

        showAlert();
        switchButtons();
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
        <a href="#">Home</a>
        <a href="#">About</a>
        <div class="dropdown">
            <button class="dropbtn">Services</button>
            <div class="dropdown-content">
                <a href="#">Service 1</a>
                <a href="#">Service 2</a>
                <a href="#">Service 3</a>
            </div>
        </div>
        <div class="dropdown">
            <button class="dropbtn">More</button>
            <div class="dropdown-content">
                <a href="#">Portfolio</a>
                <a href="#">Testimonials</a>
                <a href="#">Blog</a>
            </div>
        </div>
        <a href="#">Contact</a>
        <button class="btn" onclick="showAlert()">Sign Up</button>
    </div>

    <!-- Content -->
    <div class="content">
        <p>This is some content below the navbar.</p>
    </div>

    <!-- Additional Links and Buttons -->
    <div class="additional-content">
        <a href="#">Link 1</a>
        <a href="#">Link 2</a>
        <button onclick="alert('button is clicked')" class="btn" href = "amazon.com"> Button 1</button>
        <button onclick="showAlert()" class="btn"  href = "#"> button 2 </button>
    </div>

    <script>
        // Function to show an alert when a button is clicked
        function showAlert() {
            alert("Button clicked!");
        }
        function switchButtons() {
            var button1 = document.querySelector('.additional-content button:nth-child(3)');
            var button2 = document.querySelector('.additional-content button:nth-child(4)');

            // Clone Button 1 and Button 2
            var button1Clone = button1.cloneNode(true);
            var button2Clone = button2.cloneNode(true);

            // Replace Button 1 with Button 2
            button1.parentNode.replaceChild(button2Clone, button1);
            // Replace Button 2 with Button 1
            button2.parentNode.replaceChild(button1Clone, button2);}

        showAlert();
        switchButtons();
    </script>
</body>






```python
%%js
   // Create an object representing yourself
const person = {
    name: "Harkirat",
    age: 15,
    currentClasses: ["Calculus", "Computer Science"],
    interests: ["Coding", "Hiking", "Music"],
    favoriteBooks: [
        { title: "The Great Gatsby", author: "F. Scott Fitzgerald" },
        { title: "To Kill a Mockingbird", author: "Harper Lee" }
    ],
    currentLocation: {
        city: "San Diego",
        country: "USA"
    }
};

// Print the entire object
console.log("Original Object:");
console.log(person);

// Manipulate the arrays within the object
person.age += 1; // Increment age
person.currentClasses.push("Data Science"); // Add a new class
person.interests.pop(); // Remove the last interest

// Print the entire object after manipulation
console.log("\nObject after Manipulation:");
console.log(person);

// Perform mathematical operations on fields
const ageInFiveYears = person.age + 5;
const halfAge = person.age / 2;
const moduloAge = person.age % 2;

console.log("\nMathematical Operations:");
console.log(`In five years, I'll be ${ageInFiveYears} years old.`);
console.log(`Half of my age is ${halfAge}.`);
console.log(`My age modulo 2 is ${moduloAge}.`);

// Use typeof to determine the types of fields
const ageType = typeof person.age;
const interestsType = typeof person.interests;
const locationType = typeof person.currentLocation;

console.log("\nData Types:");
console.log(`The data type of 'age' is ${ageType}.`);
console.log(`The data type of 'interests' is ${interestsType}.`);
console.log(`The data type of 'currentLocation' is ${locationType}.`);

// Access a nested object property
const cityName = person.currentLocation.city;
console.log(`\nCurrent city: ${cityName}`);

// Modify a nested object property
person.currentLocation.city = "San Francisco";

// Print the object with the modified nested property
console.log("\nObject after Modifying Nested Property:");
console.log(person);


```


    <IPython.core.display.Javascript object>



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




```python
%%js

// Define the values of variables a and b
    const a = 5;
    const b = 7;

// Compare the values of a and b
    if (a > b) {
        console.log("a is greater");
} else if (b > a) {
        console.log("b is greater");
} else {
        console.log("both are equal");
}
```


    <IPython.core.display.Javascript object>

