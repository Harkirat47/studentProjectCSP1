---
toc: True
comments: False
layout: post
title: Homework problems Data Abstractions
type: hacks
courses: {'csp': {'week': 4}}
---

### Problem 1
- Two airplanes are in a race, your job is to make a plane name list, append the name value to the participents  then make a variable that pulls the distance covered for each plane. in the end, in the curly brackets print the name of the plane, add more variables with curly brackets. 


```python
# Define a list of airplane race participants
participants = [
    {"name": "Billium Bang", "plane": "Red Rocket", "distance_covered": 1200},
    {"name": "Bushawn Bal", "plane": "The Biggest Bird", "distance_covered": 1500}
]

# Calculate the total distance covered by each pilot during the race
for participant in participants:
    
    #your code here

    print(f" what happens, print here, use {null} to insert variables")

# Determine the winner
winner = max(participants, key=lambda x: x["distance_covered"])
print(f"The winner of the airplane race is {winner['name']} in the '{winner['plane']}' with a distance of {winner['distance_covered']} miles!")

```

### Problem 2
- Add more participants , in the loop, add a tricks variable that gets data from participants list
    score = tricks * 10  # Each trick is worth 10 points
    add a score and add it to a score in the list ex list[score] = score


```python
# Define a list of dog show participants
participants = [
    {"name": "Fido", "breed": "Golden Retriever", "tricks": 4},
    # Add more dog participants here
]

# Calculate the scores for each dog based on the number of tricks they can perform
for participant in participants:
    #your code here
    score = tricks * 10  # Each trick is worth 10 points
    #your code here

# Determine the winning dog
winner = max(participants, key=lambda x: x["score"])

# Display the dog show results
print("Dog Show Results:")
for participant in participants:
    print(f"{null} your code here!")

print(f"The winner of the dog show is {winner['name']} points!")
```

this problem, were making a bank account, you just have to know what to do to add all of the functions to change the variables


```python
# Define a class representing a Bank Account
class BankAccount:
    def __init__(self, account_holder, balance=0):
        self.account_holder = account_holder
        self.balance = balance

    def deposit(self, amount):
        if amount > 0:
            #your code
            print(f"Deposited ${amount}. New balance: ${self.balance}")
        else:
            print("Invalid deposit amount.")

    def withdraw(self, amount):
        if 0 < amount <= self.balance:
            # your code
            print (f" what happens, print here, use {null} to insert variables")
        else:
            print(f" what happens, print here, use {null} to insert variables")
                
    def get_balance(self):
        return "your Code..."

    def __str__(self):
        return "your code..."


# Create two bank accounts Alex with 1000$ initially, and Noah with 5$ initially:
alexAccount = BankAccount("Alex", 1000)
noahAccount = null

# Perform some transactions, withdraw all money of Alex , and give it all to Noah. now that noah has a lot of money, he goes on a spending spree, he must withdraw all of his money
# EX!!!! account1.deposit(500)
#
#your code !
#
#
#  Display account information

print("Alex Account", alexAccount)
print("Noah Account", noahAccount)

```

### add more regions



```python
import random

# Define a list of regions, each represented as a dictionary
regions = [
    {
        "name": "Region A",
        "GDP_growth": random.uniform(0.5, 3.0),  # Random GDP growth rate between 0.5% and 3.0%
        "unemployment_rate": random.uniform(3.0, 10.0),  # Random unemployment rate between 3.0% and 10.0%
        "investment_score": random.uniform(50, 100),  # Random investment score between 50 and 100
        "education_index": random.uniform(0.5, 1.0),  # Random education index between 0.5 and 1.0
        "infrastructure_quality": random.uniform(3.0, 8.0)  # Random infrastructure quality between 3.0 and 8.0 (scale of 1-10)
    },
    # Define more regions
]

# Define weights for each economic indicator
weights = {
    "GDP_growth": 0.4,
    "unemployment_rate": -0.2,
    "investment_score": 0.3,
    "education_index": 0.1,
    "infrastructure_quality": 0.2
}

# Function to calculate a score for each region based on economic indicators and weights
def calculate_score(region):
    score = 0
    for indicator, weight in weights.items():
        score += region[indicator] * weight
    return score

# Find the region with the highest economic growth potential
best_region = max(regions, key=calculate_score)

# Display information about the winning region
print(f"The region with the highest economic growth potential is {best_region['name']}:")
print(f"- GDP Growth Rate: {best_region['GDP_growth']:.2f}%")
print(f"- Unemployment Rate: {best_region['unemployment_rate']:.2f}%")
print(f"- Investment Score: {best_region['investment_score']:.2f}")
print(f"- Education Index: {best_region['education_index']:.2f}")
print(f"- Infrastructure Quality: {best_region['infrastructure_quality']:.2f}")

```

### problem final

- make an empty list and dictionary
- add data in all of the given simple loops, so that this problem runs its print functions without error
- this one is hard, try very hard, a heartfelt atempt, like all of the code done with minor issues is still full credit

try to understand this problem, it has lots of data abstractions

data is given on the bottem and a function is calling it IMPORTANT!!!



```python
def simulate_data_structure(data):
    # Dictionary to store city data must be blank
     # List to store city statistics also blank

    for person in data:
        name = person[]
        age = person[]
        city = person[]

        # 1. Create a dictionary of city data
        if city not in city_data:
            city_data[city] = {"names": [], "total_age": 0, "total_people": 0} # reduces err

        city_data[city]["names"]# Add the name to the city's list
        city_data[city]["total_age"] # Add the age to the city's total age hint , use +=
        city_data[city]["total_people"]  # Increment the total people count hint , use +=

    for city, city_info in city_data.items():
        # 2. Calculate the average age for each city
        average_age = city_info["what goes in here?"] / city_info["what goes in here?"]
        city_info["average_age"] = round(average_age, 2)  # Round to 2 decimal places

        # 3. Create a dictionary for city statistics
        city_stats. #your code after the dot, what happens here, how do u apend a dictionary???

    # Add the city statistics under the "Statistics" key
    city_data["Statistics"] = city_stats

    return city_data


# Example data
data = [
    {"name": "Alice", "age": 25, "city": "New York"},
    {"name": "Bob", "age": 30, "city": "Los Angeles"},
    {"name": "Charlie", "age": 22, "city": "New York"},
    {"name": "David", "age": 35, "city": "Los Angeles"},
    {"name": "Eve", "age": 28, "city": "Chicago"},
]

result = simulate_data_structure(data)
print(result)

```


```python
ingredients = ["butter", "white sugar", "light brown sugar", "vanilla extract", "eggs", "flour", "chocolate chips", "baking soda", "salt", "baking powder"]
# Print this list

# << CODE >>


# Create a list called bowl
# Your list must include:
# "flour"
# "baking soda"
# "salt"
# "baking powder"
# When creating this list, make sure to remove these items from the "ingredients" list!
# Print your list

# << CODE >>

# Create a list called cream
# Include:
# "butter"
# "white sugar"
# "light brown sugar"
# "vanilla extract"
# "eggs"
# When creating this list, make sure to remove these items from the "ingredients" list!
# Print your list

# << CODE >>

# Create a list called "dough"
# Combine the bowl list and cream list together
# Print your list

# << CODE >>

# Append chocolate chips to the dough list and remove it from the ingredients list
# Print the list

# << CODE >>

# Create a string that says "Now roll the dough into balls and place them on cookie sheets!"
# Print it

# << CODE >>

# Create an int called temperature and set it to 375
# Print "Place in a <<your integer goes here>> F oven for 8-10 minutes and remove just before they start to turn brown."

# << CODE >>

# Create an int called "cool down" using pascal case and set it to 2
# Print "Let them sit on the baking pan for <<your integer goes here>> minutes before removing to cooling rack."

# << CODE >>

# Create 5 string (use whatever casing you feel)
# First string should be "Enjoy"
# Second string should be "your"
# Third string should be "CHOCOLATE"
# Fourth string should be "CHIP"
# Fifth string should be "COOKIES!!!"
# Using ONE print statement, print ALL of these variables (with a space between each)

# << CODE >>

# JSON CHALLENGE
# can your do the whole project by using a JSON list?
# can you convert it to a python dictionary and do all these steps?

# Yes this is a real cookie recipe. You can find it below if you wanna make them! :)
# https://joyfoodsunshine.com/the-most-amazing-chocolate-chip-cookies/

```
