---
layout: post
title: 1.4 Correcting errors
description: Practice with identifying and correcting code blocks
type: ccc
author: Safin Singh and Rohan Juneja
permalink: /basics/js-debug
hide: True
---

{% include nav_basics.html %}

[College Board Big Idea 1](https://apclassroom.collegeboard.org/103/home?unit=1)

## Identifying and Correcting Errors (Unit 1.4)

> Become familiar with types of errors and strategies for fixing them

- Review CollegeBoard videos and take notes on blog
- Complete assigned MCQ questions if applicable

# Code Segments

Practice fixing the following code segments!

## Segment 1: Alphabet List

Intended behavior: create a list of characters from the string contained in the variable `alphabet`

### Code:


```python
%%js

var alphabet = "abcdefghijklmnopqrstuvwxyz";
var alphabetList = [];

for (var i = 0; i < alphabet.length; i++) {
    alphabetList.push(alphabet[i]);
}

console.log(alphabetList);
```


    <IPython.core.display.Javascript object>


### What I Changed

I pushed(alphabet[i]) instead of just (i)

## Segment 2: Numbered Alphabet

Intended behavior: print the number of a given alphabet letter within the alphabet. For example:
```
"_" is letter number _ in the alphabet
```

Where the underscores (_) are replaced with the letter and the position of that letter within the alphabet (e.g. a=1, b=2, etc.)

### Code:


```python
%%js

// Copy your previous code to built alphabetList here

var alphabet = "abcdefghijklmnopqrstuvwxyz";
var alphabetList = [];

for (var i = 0; i < alphabet.length; i++) {
    alphabetList.push(alphabet[i]);
}


let letterNumber = 5

for (var i = 0; i < alphabetList; i++) {
	console.log(alphabetList[i] + '=' + i+1)
	
}

// Should output:
// "e" is letter number 5 in the alphabet
```


    <IPython.core.display.Javascript object>


### What I Changed

I simply added a list of characters for the letters, used those letters and print them induvidually with a for loop, added the index number for each letter

## Segment 3: Odd Numbers

Intended behavior: print a list of all the odd numbers below 10

### Code:


```python
%%js

let odds = [];
let i = 1; // Start with 1 to generate odd numbers

while (i <= 10) {
  odds.push(i);
  i += 2; // Increment by 2 to get the next odd number
}

console.log(odds);
```


    <IPython.core.display.Javascript object>


### What I Changed

I changed the offset to start at one, so every number -1 then divisible by two would have a denominator of zero.

# BELOW NOT EDITED

The intended outcome is printing a number between 1 and 100 once, if it is a multiple of 2 or 5 
- What values are outputted incorrectly. Why?, there are multiple loops, while does not fit this criteria.
- Make changes to get the intended outcome. The index is siplified in a for loop, and there is an or statement in the for loop to tell if a nuber is even or a multiple of five


```python
%%js

var numbers = [];
var newNumbers = [];

for (var i = 1; i <= 100; i++) {
    if (i % 2 === 0 || i % 5 === 0) {
        newNumbers.push(i);
    }
}

console.log(newNumbers);


```


    <IPython.core.display.Javascript object>


# Challenge

This code segment is at a very early stage of implementation.
- What are some ways to (user) error proof this code?
- The code should be able to calculate the cost of the meal of the user

Hint:
- write a “single” test describing an expectation of the program of the program
- test - input burger, expect output of burger price
- run the test, which should fail because the program lacks that feature
- write “just enough” code, the simplest possible, to make the test pass

Then repeat this process until you get program working like you want it to work.


```python
%%js

var menu =  {"burger": 3.99,
         "fries": 1.99,
         "drink": 0.99}
var total = 0

//shows the user the menu and prompts them to select an item
console.log("Menu")
for (var item in menu) {
    console.log(item + "  $" + menu[item].toFixed(2)) //why is toFixed used?
}
//ideally the code should support mutliple items
var item = "burger"

//code should add the price of the menu items selected by the user 
console.log(total)
```


    <IPython.core.display.Javascript object>


## Hacks
- Fix the errors in the first three segments in this notebook and say what you changed in the code cell under "What I Changed" (Challenge is optional)
