---
toc: True
comments: False
layout: post
title: Homework problems Data Abstractions
type: hacks
courses: {'csp': {'week': 4}}
---

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


```python
import random

class IceCreamShop:
    def __init__(self, name):
        self.name = "your code here" # name is a variable in the function
        self.rating = random.uniform("your code here", "your code here")  # Randomly generate a rating between 3.0 and 5.0
        self.price_per_scoop = random.uniform("your code here", "your code here")  # Randomly generate a price per scoop between 1.0 and 3.0
        self.distance = random.uniform("your code here", "your code here")  # Randomly generate a distance between 0.1 and 10.0 miles from the client
    
    def calculate_score(self):
        # Calculate a score based on a weighted combination of rating, price, and distance
        rating_weight = 0.4
        price_weight = 0.3
        distance_weight = 0.3
        score = " your code here"
        return score
    
def select_contract_winner(shops):
    # Select the ice cream shop with the highest score as the contract winner
    winner = max(shops, key=lambda shop: shop.calculate_score())
    return winner

if __name__ == "__main__":
    # Create a list of 10 ice cream shops
    ice_cream_shops = [IceCreamShop(f"Shop {i+1}") for i in range(10)]

    #hint, try putting something inside the brackets before this for loop, it is worth an extra point[ for i in range(10)]

    # Select the contract winner
    contract_winner = select_contract_winner(ice_cream_shops)

    print(f"The contract is awarded to {contract_winner.name}")
    print(f"Rating: {contract_winner.rating}")
    print(f"Price per scoop: ${contract_winner.price_per_scoop:.2f}")
    print(f"Distance from client: {contract_winner.distance:.2f} miles")

```


```python
# Define a class representing a Bank Account
class BankAccount:
    def __init__(self, account_holder, balance=0):
        self.account_holder = account_holder
        self.balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            print(f"Deposited ${amount}. New balance: ${self.balance}")
        else:
            print("Invalid deposit amount.")

    def withdraw(self, amount):
        if 0 < amount <= self.balance:
            self.balance -= amount
            print(f"Withdrew ${amount}. New balance: ${self.balance}")
        else:
            print("Invalid withdrawal amount or insufficient funds.")

    def get_balance(self):
        return self.balance

    def __str__(self):
        return f"Account holder: {self.account_holder}, Balance: ${self.balance}"


# Create two bank accounts
account1 = BankAccount("Alice", 1000)
account2 = BankAccount("Bob", 500)

# Perform some transactions
account1.deposit(500)
account1.withdraw(200)
account2.deposit(1000)
account2.withdraw(800)

# Display account information
print("Account 1:", account1)
print("Account 2:", account2)

```


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
