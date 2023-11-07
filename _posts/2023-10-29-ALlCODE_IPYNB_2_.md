---
toc: True
comments: True
layout: post
title: ALL CODE
type: tangibles
courses: {'csp': {'week': 10}}
---

# This is the final code for everything to do with API

## API Blueprint and API file


```python
from flask import Blueprint, jsonify
from flask_restful import Api, Resource, reqparse
from __init__ import db
from model.cookies import Cookie  # Import the Cookie model

# Create a Blueprint for the Cookie API
Cookie_api = Blueprint('Cookie_api', __name__, url_prefix='/api/Cookie')

# Create the API instance
api = Api(Cookie_api)

class CookieAPI(Resource):
    def get(self):
        # Retrieve all cookies from the database
        cookies = Cookie.query.all()

        # Prepare the data in JSON format
        json_ready = [cookie.to_dict() for cookie in cookies]

        # Return the JSON response
        return jsonify(json_ready)

    def post(self):
        parser = reqparse.RequestParser()
        parser.add_argument("cookie_name", required=True, type=str)
        parser.add_argument("image", required=True, type=str)
        parser.add_argument("stock", required=True, type=int)
        parser.add_argument("price", required=True, type=float)
        args = parser.parse_args()

        new_cookie = Cookie(args["cookie_name"], args["image"], args["stock"], args["price"])  # Use a different name here

        try:
            db.session.add(new_cookie)
            db.session.commit()
            return new_cookie.to_dict(), 201
        except Exception as exception:
            db.session.rollback()
            return {"message": f"Error: {exception}"}, 500

    def put(self):
        parser = reqparse.RequestParser()
        parser.add_argument("id", required=True, type=int)
        parser.add_argument("cookie_name", type=str)
        parser.add_argument("image", type=str)
        parser.add_argument("stock", type=int)
        parser.add_argument("price", type=float)  # Change type to float for price
        args = parser.parse_args()

        try:
            cookie = db.session.query(Cookie).get(args["id"])
            if cookie:
                if args["cookie_name"] is not None:
                    cookie.cookie_name = args["cookie_name"]
                if args["image"] is not None:
                    cookie.image = args["image"]
                if args["stock"] is not None:
                    cookie.stock = args["stock"] 
                if args["price"] is not None:
                    cookie.price = args["price"]  # Fix the attribute name here
                db.session.commit()
                return cookie.to_dict(), 200
            else:
                return {"message": "Cookie not found"}, 404
        except Exception as exception:
            db.session.rollback()
            return {"message": f"Error: {exception}"}, 500


    def delete(self):
        parser = reqparse.RequestParser()
        parser.add_argument("id", required=True, type=int)
        args = parser.parse_args()

        try:
            cookie = db.session.query(Cookie).get(args["id"])
            if cookie:
                db.session.delete(cookie)
                db.session.commit()
                return cookie.to_dict()
            else:
                return {"message": "Cookie not found"}, 404
        except Exception as exception:
            db.session.rollback()
            return {"message": f"Error: {exception}"}, 500

# Add the CookieAPI resource to the /api/Cookie/<int:id> endpoint
api.add_resource(CookieAPI, "/")

class CookieListAPI(Resource):
    def get(self):
        # Retrieve all cookies from the database
        cookies = Cookie.query.all()

        # Prepare the data in JSON format
        json_ready = [cookie.to_dict() for cookie in cookies]

        # Return the JSON response
        return jsonify(json_ready)
    
# Add the CookieListAPI resource to the /api/Cookie endpoint
api.add_resource(CookieListAPI, "/")
```

## The Model itself


```python
from __init__ import db

class Cookie(db.Model):
    __tablename__ = "Cookie"
    id = db.Column(db.Integer, primary_key=True)  #  Define a primary key column
    Cookie_name = db.Column(db.String, nullable=False)
    image = db.Column(db.String, nullable=False)
    stock = db.Column(db.String, nullable=False)
    price = db.Column(db.String, nullable=False)

    def __init__(self, Cookie_name, image, stock, price):
        self.Cookie_name = Cookie_name
        self.image = image
        self.stock = stock
        self.price = price

    def to_dict(self):
        return {"id": self.id,"Cookie_name": self.Cookie_name, "image": self.image, "stock": self.stock, "price": self.price}

def init_cookies():
    # You can keep the rest of your code as is
    Cookie1 = Cookie(Cookie_name="Blueberry Delight", image="blueberry_cookie.jpg", stock="75", price="2.50")
    Cookie2 = Cookie(Cookie_name="Chocolate Chip", image="chocolate_chip_cookie.jpg", stock="90", price="1.99")
    Cookie3 = Cookie(Cookie_name="Oatmeal Raisin", image="oatmeal_raisin_cookie.jpg", stock="80", price="2.25")
    Cookie4 = Cookie(Cookie_name="Double Chocolate", image="double_chocolate_cookie.jpg", stock="85", price="2.75")
    Cookie5 = Cookie(Cookie_name="Peanut Butter", image="peanut_butter_cookie.jpg", stock="70", price="2.20")
    Cookie6 = Cookie(Cookie_name="Coconut Macaroon", image="coconut_macaroon_cookie.jpg", stock="95", price="2.10")
    Cookie7 = Cookie(Cookie_name="sugar", image="sugar_cookie.jpg", stock="95", price="2.10")
    Cookie8 = Cookie(Cookie_name="Snickerdoodle", image="snickerdoodle_cookie.jpg", stock="80", price="2.25")

    db.session.add(Cookie1)
    db.session.add(Cookie2)
    db.session.add(Cookie3)
    db.session.add(Cookie4)
    db.session.add(Cookie5)
    db.session.add(Cookie6)
    db.session.add(Cookie7)
    db.session.add(Cookie8)

    db.session.commit()

# Ensure you have imported the necessary modules and configured your database connection before running this code.


# from __init__ import db

# class Song(db.Model):
#     __tablename__ = "Song"
#     id = db.Column(db.Integer, primary_key=True)  # Define a primary key column
#     character = db.Column(db.String, nullable=False)
#     song_name = db.Column(db.String, nullable=False)
#     artist = db.Column(db.String, nullable=False)
#     genre = db.Column(db.String, nullable=False)
#     def __init__(self, character, song_name, artist, genre):
#         self.character = character
#         self.song_name = song_name
#         self.artist = artist
#         self.genre = genre
#     def to_dict(self):
#         return {"character": self.character, "song_name": self.song_name, "artist": self.artist, "genre": self.genre}
# def initSongs():
#     # You can keep the rest of your code as is
#     song1 = Song(character="Walter White", song_name="Changes", artist="David Bowie", genre="Art Pop"); db.session.add(song1)#replace with real data
#     song2 = Song(character="Walter White", song_name="Back in Black", artist="AC/DC", genre="Hard Rock"); db.session.add(song2)
#     song3 = Song(character="Walter White", song_name="Baby Blue", artist="Badfinger", genre="Rock"); db.session.add(song3)
#     song4 = Song(character="Walter White", song_name="A Horse with No Name", artist="America", genre="Soft Rock"); db.session.add(song4)
#     db.session.commit()
```

## The main.py updated with the api



```python
import threading

# import "packages" from flask
from flask import render_template  # import render_template from "public" flask libraries

# import "packages" from "this" project
from __init__ import app,db  # Definitions initialization
from model.jokes import initJokes
from model.users import initUsers
from model.players import initPlayers
from model.cookies import init_cookies

# setup APIs
from api.covid import covid_api # Blueprint import api definition
from api.joke import joke_api # Blueprint import api definition
from api.user import user_api # Blueprint import api definition
from api.player import player_api
from api.cookie import Cookie_api


# setup App pages
from projects.projects import app_projects # Blueprint directory import projects definition


# Initialize the SQLAlchemy object to work with the Flask app instance
db.init_app(app)

# register URIs
app.register_blueprint(joke_api) # register api routes
app.register_blueprint(covid_api) # register api routes
app.register_blueprint(user_api) # register api routes
app.register_blueprint(player_api)
app.register_blueprint(Cookie_api)
app.register_blueprint(app_projects) # register app pages

@app.errorhandler(404)  # catch for URL not found
def page_not_found(e):
    # note that we set the 404 status explicitly
    return render_template('404.html'), 404

@app.route('/')  # connects default URL to index() function
def index():
    return render_template("index.html")

@app.route('/table/')  # connects /stub/ URL to stub() function
def table():
    return render_template("table.html")

@app.before_first_request
def activate_job():  # activate these items 
    initJokes()
    initUsers()
    initPlayers()
    init_cookies()

# this runs the application on the development server
if __name__ == "__main__":
    # change name for testing
    from flask_cors import CORS
    CORS(app)
    app.run(debug=True, host="0.0.0.0", port="8911")
```
