---
toc: True
comments: True
layout: post
title: CSP plans
type: tangibles
courses: {'csp': {'week': 8}}
---

# ISSUES

LINKS
[Issue 1, IMG links in Meta](https://github.com/KinetekEnergy/ByteBuffoons-Pages/issues/11) All of the links that are in the meta model of backend need to be real cookies (low priority)

[Issue 2, Add post request](https://github.com/KinetekEnergy/ByteBuffoons-Pages/issues/21) use post requests to add votable cookies (Pending)

[Issue 3, we need data](https://github.com/KinetekEnergy/ByteBuffoons-Pages/issues/15) Intergration, get function, made parseable cards (done)

[Issue 4, decrese API value ](https://github.com/KinetekEnergy/ByteBuffoons-Pages/issues/9) Update stock, exremely important for an ecomerce website (done)

# WEEK 8

Started to experiment with Blueprint and then I tried to copy the jokes API and make it as my API by changing a few things.



```python

import random

cookie_data = {
    "cookies": [],
    "list": [
        "Chocolate Chip", "Oatmeal Raisin", "Snickerdoodle", "Peanut Butter", "Sugar Cookie"
    ]
}

# Initialize cookies
def initCookies():
    # Setup cookies into a dictionary with type, ingredients, price, and stock
    for item_type in cookie_data["list"]:
        cookie_data["cookies"].append({"type": item_type, "ingredients": [], "price": 0, "stock": 0})
    # Prime some stock levels
    for i in range(len(cookie_data["list"])):
        cookie_data["cookies"][i]["stock"] = random.randint(50, 100)

# Return all cookies from cookie_data
def getCookies():
    return cookie_data["cookies"]

# Cookie getter
def getCookie(cookie_type):
    for cookie in cookie_data["cookies"]:
        if cookie['type'] == cookie_type:
            return cookie

# Return random cookie from cookie_data
def getRandomCookie():
    return random.choice(cookie_data["cookies"])

# Buy a cookie and update stock
def buyCookie(cookie_type):
    cookie = getCookie(cookie_type)
    if cookie and cookie['stock'] > 0:
        cookie['stock'] -= 1
        return {"message": f"Purchased one {cookie_type} cookie."}
    elif cookie:
        return {"message": f"Sorry, {cookie_type} cookies are out of stock."}, 400
    else:
        return {"message": "Cookie type not found."}, 404

# Pretty Print cookie
def printCookie(cookie):
    print("Type:", cookie['type'])
    print("Ingredients:", ', '.join(cookie['ingredients']))
    print("Price:", cookie['price'])
    print("Stock:", cookie['stock'])

# Number of cookies
def countCookies():
    return len(cookie_data["cookies"])

# Test Cookie Model
if __name__ == "__main__":
    initCookies()  # initialize cookies

    # Random cookie
    random_cookie = getRandomCookie()
    print("Random cookie:")
    printCookie(random_cookie)

    # Buy a cookie
    cookie_type = "Chocolate Chip"  # Change to the type you want to buy
    buy_result = buyCookie(cookie_type)
    print(buy_result)

    # Count of Cookies
    print("Cookies Count:", countCookies())
```

then once this inevitablly failed, I tested extensively on postman untill I decided to try and change my Meta data model into a database system. This had many issues though, I had to initiate my meta data not in main, rather than the model file. I also learned a valuable lesson in namng files as All of my files were named Cookie, therfore it was hard to tell what i was calling in my main.

Updated code for model and main 
[https://github.com/Harkirat47/ByteBuFOOOns/commit/c83eee0b248b9574a093035b6e421872e77ed277 ](https://github.com/Harkirat47/ByteBuFOOOns/commit/c83eee0b248b9574a093035b6e421872e77ed277 )

Port Changes
[https://github.com/Harkirat47/ByteBuFOOOns/commit/eeca1cefea7abd23d74b4c3bf22209d68453a306](https://github.com/Harkirat47/ByteBuFOOOns/commit/eeca1cefea7abd23d74b4c3bf22209d68453a306)


Fixing Ports
[https://github.com/Harkirat47/ByteBuFOOOns/commit/1bfc7a87d04d31845d14e11444860e56815a99cc](https://github.com/Harkirat47/ByteBuFOOOns/commit/1bfc7a87d04d31845d14e11444860e56815a99cc)

This is current edition with Jokes intergration
[https://github.com/Harkirat47/ByteBuFOOOns/commit/5534790ed61c52f470e144f15dcd6526fded21f2](https://github.com/Harkirat47/ByteBuFOOOns/commit/5534790ed61c52f470e144f15dcd6526fded21f2)

# WEEK 9

THINGS GO TERRIBLY WRONG

One of my teamates thought they were helping and somehow moved all of the files from their paths, this took me over 3 hours to fix until i finnally figured out the damage
This was partly due to my lack of teaching my teamates backend, and expecting them to know how to do things

It's time to get GET and POST to actually work. Last week was mainly about running the Docker and getting the model running. One problem, however, was that my API would only work on my localhost provided I ran the following in a terminal code cell:

python
Copy code
python main.py
CORS was a huge issue this week as well. Luckily, in this commit, link this commit, basically, all I really had to do was read the docs for this one and copy the CORS code from there.

Another thing I did this week was deploy to the AWS server for the first time. Not set up, rather actually used docker-compose up --d build on the Nighthawk server.

## UPDATE: EVERYTHING BROKE due to read-write permissions.

Baisically, my meta data would just apend onto my previos data when i restarted the server. One way to fix this was to Drop the sqlite table all-together. this plan did not work due to read write permissions wich I cannot Change, Work on this later, get post to work Right now

### POST WORKS

- due to URL problems prevelent in the Cookie.py in API folder

- as you can see, cookies 1 - 8 are meta data, many of this is test and post data, but you can see how they keep repeting

![Another Image]({{site.baseurl}}/images/CookieMMMMM.png)

### Code for post 
```python
 def post(self):
        parser = reqparse.RequestParser()
        parser.add_argument("Cookie_name", required=True, type=str)
        parser.add_argument("image", required=True, type=str)
        parser.add_argument("stock", required=True, type=str)  # Adjust the type to int
        parser.add_argument("price", required=True, type=str)  # Adjust the type to float
        args = parser.parse_args()
        cookie = Cookie(args["Cookie_name"], args["image"], args["stock"], args["price"])

```
Baisically I did not know how to parse anything, this is something that I learned through lots of google after CHATGPT failed

### Commits for this week

Post request intergration with main
[https://github.com/Harkirat47/ByteBuFOOOns/commit/a7dea271cc6355b45c09456db627d3ce47bd997e ](https://github.com/Harkirat47/ByteBuFOOOns/commit/a7dea271cc6355b45c09456db627d3ce47bd997e )


Teamate Mishap 
[https://github.com/Harkirat47/ByteBuFOOOns/commit/5a534389c04e6a5dda3663d8a9a3bd683c203c38](https://github.com/Harkirat47/ByteBuFOOOns/commit/5a534389c04e6a5dda3663d8a9a3bd683c203c38)

CSV Fixing(this was an expiriment that I tried to do but inevitably did not do as it was uneeded)
[Issue 2, Add post request](https://github.com/Harkirat47/ByteBuFOOOns/commit/40dcd38afe9109d0da2eec8939290c306fca312e)

Post Request fixing finnaly done with minor issues
[https://github.com/Harkirat47/ByteBuFOOOns/commit/79ecdee301c50f949f264834112f280496cf13d0](https://github.com/Harkirat47/ByteBuFOOOns/commit/79ecdee301c50f949f264834112f280496cf13d0)

Formatting and also final Post fixes
[https://github.com/Harkirat47/ByteBuFOOOns/commit/604322d11a39629aeb784758ff91a5c4ecf2949b](https://github.com/Harkirat47/ByteBuFOOOns/commit/604322d11a39629aeb784758ff91a5c4ecf2949b)


# WEEK 10

#### Intergration Week

 ##### Things to Acheive this week

 - GET METHOD FETCHED

 - HELP FRONTEND WITH DYNAMIC CARDS
 

Update, Huge issue, the data cannot be called, yet the api is on the AWS server, figure out how to fetch

### SIDE QUEST

SSH to the AWS server 

FIX THE NGINX BECAUSE PPL KEEP TURNING OFF THE SERVER Credit:WILLIAM CHENG, I figured out how to get to the SSH, William figured out how to fix NGINx

![Another Image]({{site.baseurl}}/images/LESGOOOOO.png)

### Back to the main parts

UPDATE: CHATGPT has helped fixing our fetch code


```python
fetch(apiUrl)
.then(response => response.json()) // Parse the JSON response
.then(data => {
    // Organize the data into a dictionary
    const organizedData = {
        Cookie_api: {
            url_prefix: '/api/Cookie',
            CookieAPI: {
                get: {
                    description: 'Retrieve all cookies from the database',
                    url: '/api/Cookie',
                    method: 'GET',
                    data: data, // Include the retrieved data here
                },
            },
        },
        CookieListAPI: {
            CookieListAPI: {
                get: {
                    description: 'Retrieve all cookies from the database',
                    url: '/api/Cookie',
                    method: 'GET',
                    data: data, // Include the retrieved data here
                },
            },
        },
        };

// Now, you have the organized data in the "organizedData" dictionary
})
.catch(error => {
console.error('Error fetching data:', error);
});
```

### now we make dynamic cards

first we have to get the data

next we have to append it to some cards

More testing,


```python
console.log(organizedData); //data[id].Cookie_name, image whatever u may need,
```

![Another Image]({{site.baseurl}}/images/data.png)

so the path is therfore .Cookie_api.CookieAPI.get.data

Update this works, now to sudo code the parser for adding custom cards

For each item in Data
    Create a new card element
    Set the card's class to "card"

    Create a new image element
    Set the image's source (src) to the item's image property
    Set the image's alt text to "cookie"

    Create a new cardContent element
    Set the cardContent's class to "card-content"

    Create a new title element
    Set the title's class to "title"
    Set the title's text content to "item.Cookie_name - $item.price"

    Create a new whitespace1 element
    Set whitespace1's class to "title"
    Set whitespace1's text content to an empty string

    Create a new chip element
    Set the chip's class to "chip"
    Set the chip's text content to "Add to Cart"
    Add a click event listener to the chip

    Create a new whitespace2 element
    Set whitespace2's class to "title"
    Set whitespace2's text content to an empty string

    Append the title to cardContent
    Append whitespace1 to cardContent
    Append chip to cardContent
    Append whitespace2 to cardContent

    Append the image to the card
    Append cardContent to the card

    Append the card to the catalogGrid


### This is the working code 


```python
Data.forEach((item) => {
    const card = document.createElement("div")
    card.className = "card";

    const image = document.createElement("img");
    image.src = item.image;
    image.alt = "cookie";

    const cardContent = document.createElement("div")
    cardContent.className = "card-content";

    const title = document.createElement("p");
    title.className = "title";
    title.textContent = `${item.Cookie_name} - $${item.price}`


    // new line
    const whitespace1 = document.createElement("p");
    whitespace1.className = "title";
    whitespace1.textContent = ``

    const chip = document.createElement("a");
    chip.className = "chip";
    chip.textContent = "Add to Cart";
    chip.addEventListener("click", () => {
        // <a href="#" class="chip snipcart-add-item" data-item-id="Chocolate Chip" data-item-price="3.99"
        //     data-item-image="https://www.cookingclassy.com/wp-content/uploads/2014/06/chocolate-chip-cookie-16.jpg"
        //     data-item-name="Chocolate Chip">Add to cart
        // </a>
    });

    // new line
    const whitespace2 = document.createElement("p");
    whitespace2.className = "title";
    whitespace2.textContent = ``


    cardContent.appendChild(title);
    cardContent.appendChild(whitespace1)
    cardContent.appendChild(chip);
    cardContent.appendChild(whitespace2)

    card.appendChild(image);
    card.appendChild(cardContent);

    catalogGrid.appendChild(card);
```

Commits for this Week That are Important

Testing data paths
[https://github.com/KinetekEnergy/ByteBuffoons-Pages/commit/8fb375d9533ea06ec224720c09799e66e8a8d9aa](https://github.com/KinetekEnergy/ByteBuffoons-Pages/commit/8fb375d9533ea06ec224720c09799e66e8a8d9aa)

Starting the fetch system
[https://github.com/KinetekEnergy/ByteBuffoons-Pages/commit/3ed77be45fedbebafb99a813cf6dde5348c3d274](https://github.com/KinetekEnergy/ByteBuffoons-Pages/commit/3ed77be45fedbebafb99a813cf6dde5348c3d274)


Apending new cards to the code
[https://github.com/KinetekEnergy/ByteBuffoons-Pages/commit/4aa939a7fbfe37318687ec05586536aa1f9b89c1](https://github.com/KinetekEnergy/ByteBuffoons-Pages/commit/4aa939a7fbfe37318687ec05586536aa1f9b89c1)



Honerable mentions:

Fixing exposed Data ports
[https://github.com/Harkirat47/ByteBuFOOOns/commit/dc4f9bdb07be7bd055e09af8d14303e0d10e52fa](https://github.com/Harkirat47/ByteBuFOOOns/commit/dc4f9bdb07be7bd055e09af8d14303e0d10e52fa)


# Week 11

MCQ Revisions

- Queston 1, Replacing a variable in psudo code with temporary variable is extremely weird,


## temp <= first
## first <= seccond
## seccond <= first

Queston 3

- Encryption for a bank, recipients private key is more important than sender.
- Calling the phone number given in the e-mail and providing the personal information over the phone BAD

Queston 14

- when index is different, the correct answer is: This option is incorrect. The programs display different values.
### output <= [1,2,3,4,5,6,7,8]
### output <= [0,1,2,3,4,5,6,7]
### DIFFERENT VALUES

Queston 23

- This option is incorrect. There are multiple paths from P to S (for example, P to S and P to Q to S).
- This is a path queston, the answer is B as thre is only one path to P

Queston 26

- The code I selected does nothing,
- SIMPLE MISTAKE, always call move right, and if the output does not work, move forward

Queston 30

- what does the coe really mean, it calls every time in the index

Queston 35

- This option is correct. Creative Commons licenses can be used by creators of digital music to specify how the samples can be used by others. A no-rights-reserved license allows others to freely make use of the samples.

Queston 50

-  It implements a linear search. Bianary search is not sequential, it takes mean and recusres it over and over again.

Queston 52 

- Also a linear search
- First keep palindromes, then shorten, then sort

Queston 55

- The procedure returns false no matter what the input value is.

Queston 58

- I. The Internet can provide crowdsourcing participants access to useful tools, information, and professional knowledge. II. The speed and reach of the Internet can lower geographic barriers, allowing individuals from different locations to contribute to projects.

Queston 65

- remember what an or function is

Queston 66 

- The list will not run with low index at 10 starting





# REFLECTION


Certainly, here's some additional advice for improving my performance on AP CSP multiple-choice questions:

Regular Practice: I should consistently practice solving various types of multiple-choice questions to get a better feel for the format and the types of questions that may appear on the AP CSP exam. This practice helps me become more familiar with common patterns and concepts tested in these questions.

Review the Course Material: Going through the course material, notes, and textbooks is essential. Sometimes, the answers to MCQs can be found within the course content. A thorough understanding of the curriculum is crucial.

Analyze Mistakes: After taking practice exams or mock quizzes, I should carefully review any mistakes I made. Understanding why I got a particular question wrong and learning from those mistakes is crucial for improvement.

Understand the AP CSP Exam Format: Familiarizing myself with the structure of the AP CSP exam, including the number of questions, time constraints, and scoring, will help me better plan and manage my time during the test.

Use Resources: There are numerous resources available, such as review books, online courses, and sample questions provided by the College Board. These can be incredibly helpful in preparing for the exam.

Consider Group Study: Sometimes, discussing and solving problems with peers can provide new perspectives and insights. Collaborative study sessions can be very beneficial.

Stay Calm and Focused: During the actual exam, it's important to remain calm and focused. If I encounter a challenging question, it's better to temporarily skip it and return later. Panicking can negatively impact my performance.

Simulate Real Exam Conditions: When practicing, I should simulate the actual exam conditions as closely as possible, including timing myself to get a sense of what the real test experience will be like.

By following these strategies and consistently working on improving my understanding of the subject matter, my problem-solving skills, and my test-taking abilities, I can increase my chances of success on the AP CSP multiple-choice questions.

# Collaberation

I was backend in my group and I did most of the work on it while my friends were doing the frontent

## Things to do better next time

    Assign more work for other people to do backend

    Have the work more outsourced

Admitting mistakes is a crucial part of the Agile methodology, and it's a step towards improvement. Recognizing that you took on too much work within the Agile framework is a valuable realization. In Agile, collaboration and delegation are key principles, ensuring that responsibilities are shared and distributed among the team members. To improve, you can refocus on the core principles of Agile, such as transparency, communication, and teamwork. Learn from your experience and strive to involve your team more effectively, allowing for shared ownership and responsibilities in future projects. This adjustment can lead to a more balanced workload and better outcomes in the spirit of Agile's iterative and collaborative approach.
