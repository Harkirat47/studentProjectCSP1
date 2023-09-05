---
layout: post
title: Python quiz
description: These examples show the basic language structures and constructs of Python using input and output (print) commands.
courses: {'csp': {'week': 1, 'categories': ['1.A', '3.A', '4.B']}}
categories: ['C4.0']
type: hacks
---

### Me and Anthoy's quiz

    this uses imports and other things to test wether you are smart


```python
# Define a list of questions, answer choices, and correct answers
questions = [
    {
        "question": "What is an if function",
        "choices": ["A) a queston", "B) I cant code :(", "C) a condition", "D) trick queston"],
        "correct_answer": "C"
    },
    {
        "question": "What does i mean in a loop",
        "choices": ["A) Inception ", "B) Index", "C) just an uneeded variable", "D) Undefined"],
        "correct_answer": "B"
    },
    {
        "question": "what is the meaning of life",
        "choices": ["A) CSP", "B) Code Code Code", "C) Nothingness ", "D) Death "],
        "correct_answer": "B"
    }
]

# Initialize a variable to keep track of the score
score = 0

# Iterate through the questions
for i, question in enumerate(questions, 1):
    print(f"Question {i}: {question['question']}")
    for choice in question['choices']:
        print(choice)
    
    # Get the user's answer
    user_answer = input("Enter your answer (A/B/C/D): ").upper()

    # Check if the user's answer is correct
    if user_answer == question['correct_answer']:
        print("Correct!\n")
        score += 1
    else:
        print(f"Wrong. The correct answer is {question['correct_answer']}.\n")

# Display the final score
print(f"You got {score} out of {len(questions)} questions correct.")

```

    Question 1: What is the capital of France?
    A) London
    B) Berlin
    C) Paris
    D) Madrid
    Wrong. The correct answer is C.
    
    Question 2: Which planet is known as the Red Planet?
    A) Earth
    B) Mars
    C) Venus
    D) Jupiter
    Wrong. The correct answer is B.
    
    Question 3: What is the largest mammal on Earth?
    A) African Elephant
    B) Blue Whale
    C) Giraffe
    D) Hippopotamus

