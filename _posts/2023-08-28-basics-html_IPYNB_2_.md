---
layout: post
hide: True
title: Basics of HTML Guide
description: An introduction to basic HTML, and resources to learn more.
type: ccc
permalink: /basics/html
author: Rohan Juneja
---

{% include nav_basics.html %}


# How does HTML work?
Similar function to Markdown, syntax defines how stuff should be displayed
- HTML is based on beginning and closing tags `<tagname>content</tagname>`
  - Note the "/" on the ending or closing tag of the pair

## Compare markdown to html below
This below example shows comparison of a [heading](https://www.w3schools.com/html/html_headings.asp) and [paragraph](https://www.w3schools.com/html/html_paragraphs.asp).  Click on links to see many more HTML examples.


```python
%%markdown

### Markdown: This is a Heading

This is a paragraph

```



### Markdown: This is a Heading

This is a paragraph




```python
%%html

<h3>HTML: This is a Heading</h3>
<p>This is a paragraph.</p>
```



<h3>HTML: This is a Heading</h3>
<p>This is a paragraph.</p>



# Attributes
- Learn about [attributes](https://www.w3schools.com/html/html_attributes.asp) 
- Tags can have additional info in the form of attributes
- Attributes usually come in name/value pairs like: name="value"

```html
<tagname attribute_name="attribute_value" another_attribute="another_value">inner html text</tagname>
```

- href example with attribute for web link and inner html to describe link

```html
<a href="https://www.w3schools.com/html/default.asp">Visit W3Schools HTML Page</a>
```

## Sample Markdown vs HTML Tags
Image Tag - Markdown

```md
![describe image](link to image)
```

Image Tag - HTML

```html
<!-- no content so no end tag, width/height is optional (in pixels) -->
<img alt="describe image" src="link to image" width="100" height="200">
```

Link Tag - Markdown

```md
[link text](link)
```

Link Tag - HTML

```html
<a href="link">link text</a>
```

Bolded Text - Markdown

```md
**Bolded Text**
```

Bolded Text - HTML

```md
<strong>Bolded Text</strong>
```

Italic Text - Markdown

```md
*Italic Text*
```

Italic Text - HTML

```md
<i>Italic Text</i>
```

# More tags (not really in markdown)
P tag (just represeants a paragraph/normal text)

```html
<p>This is a paragraph</p>
```

Button

```html
<button>some button text</button>
```

Div (groups together related content)

```html
<!-- first information -->
<div>
    <!-- notice how tags can be put INSIDE eachother -->
    <p>This is the first paragarph of section 1</p>
    <p>This is the second paragraph of section 1</p>
</div>

<!-- second information -->
<div>
    <!-- notice how tags can be put INSIDE eachother -->
    <p>This is the first paragarph of section 2</p>
    <p>This is the second paragraph of section 2</p>
</div>
```



# Resources
- https://www.w3schools.com/html/default.asp
- I will show a demo of how to find information on this website

# HTML Hacks
- Below is a wireframe for an HTML element you will create. A wireframe is a rough visual representation of HTML elements on a page and isn't necessarily to scale or have the exact styling that the final HTML will have. Using the syntax above, try to create an HTML snippet that corresponds to the below wireframe.
- The "a tags" can contain any links that you want

![wireframe for html hacks]({{ site.baseurl }}/images/wireframe.png)


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



<!-- put your HTML code in this cell, Make sure to press the Run button to see your results below -->


