---

---

```python
<!-- HTML table layout for the page. The table is populated by the JavaScript code below. -->
<table>
    <thead>
    <tr>
      <th>Name</th>
      <th>ID</th>
      <th>Age</th>
    </tr>
    </thead>
    <tbody id="result">
      <!-- javascript generated data -->
    </tbody>
  </table>
  
  <!-- 
  The JavaScript code below fetches user data from an API and displays it in the table. i
  It uses the Fetch API to make a GET request to the '/api/users/' endpoint. 
  The 'uri' variable and 'options' object are imported from the 'config.js' file.
  
  The script executes sequentially when the page is loaded.
  -->
  <script type="module">
    // Import 'uri' variable and 'options' object from 'config.js'
    import { uri, options } from '/teacher_portfolio/assets/js/api/config.js';
  
    // Set the URL to the 'users' endpoint
    const url = uri + '/api/users/';
  
    // Get the HTML element where the results will be displayed
    const resultContainer = document.getElementById("result");
  
    // Make a GET request to the API
    fetch(url, options)
      // response is a RESTful "promise" on any successful fetch
      .then(response => {
        // If the response status is not 200, display an error message
        if (response.status !== 200) {
            const errorMsg = 'Database response error: ' + response.status;
            console.log(errorMsg);
            const tr = document.createElement("tr");
            const td = document.createElement("td");
            td.innerHTML = errorMsg;
            tr.appendChild(td);
            resultContainer.appendChild(tr);
            return;
        }
        // valid response will contain JSON data
        response.json().then(data => {
            console.log(data);
            for (const row of data) {
              // Create a new table row and cells for each piece of data
              // tr and td build out for each row
              const tr = document.createElement("tr");
              const name = document.createElement("td");
              const id = document.createElement("td");
              const age = document.createElement("td");
              // data is specific to the API
              name.innerHTML = row.name; 
              id.innerHTML = row.uid; 
              age.innerHTML = row.age; 
              // this builds td's into tr
              tr.appendChild(name);
              tr.appendChild(id);
              tr.appendChild(age);
              // Append the row to the table
              resultContainer.appendChild(tr);
            }
        })
    })
    // If the fetch request fails (e.g., due to network issues), display an error message
    .catch(err => {
      console.error(err);
      const tr = document.createElement("tr");
      const td = document.createElement("td");
      td.innerHTML = err + ": " + url;
      tr.appendChild(td);
      resultContainer.appendChild(tr);
    });
  </script>
```

## Accessing Data (Backend)

The following code snippets demonstrate a guarded GET method using `@token_required` as the guard.

### Guarded GET Method
- The method is protected by `@token_required`.
- Potential failures result in 'Unauthorized' or 'Forbidden' responses.

### token_required Function
- Handles failure possibilities.
- Upon success, returns a user object from the database based on the user ID in the token.

### GET Method Logic
- Enables logged-in users to query all users from the database.
- Returns protected user list from the database as a result of authenticated access.



```python
# from user.py file
# ... more import and blueprint code
class UserAPI:        
    class _CRUD(Resource):
        # ... more resource code omitted
        # The @token_required decorator ensures that the user is authenticated before they can access the data.
        @token_required()
        # The get method retrieves all users from the database.
        # The underscore (_) indicates that the current_user is not used in this method.
        def get(self, _): 
            users = User.query.all()    # Query all users from the database
            json_ready = [user.read() for user in users]  # Prepare the data for JSON output
            return jsonify(json_ready)  # Convert the data to a JSON response

    # Add the _CRUD resource to the API at the root endpoint ('/')
    api.add_resource(_CRUD, '/')


# from auth_middlewares.py file
# ... more import code
# The token_required function is a decorator that checks if the user is authenticated.
# If roles are provided, it also checks if the user has the required role.
def token_required(roles=None):
    def decorator(f):
        @wraps(f)
        def decorated(*args, **kwargs):
            token = request.cookies.get("jwt")  # Get the JWT token from the cookies
            # If the token is missing, return an error message
            if not token:
                return {
                    "message": "Authentication Token is missing!",
                    "data": None,
                    "error": "Unauthorized"
                }, 401
            try:
                # Decode the token and get the user's data
                data = jwt.decode(token, current_app.config["SECRET_KEY"], algorithms=["HS256"])
                current_user = User.query.filter_by(_uid=data["_uid"]).first()
                # If the user doesn't exist or doesn't have the required role, return an error message
                if current_user is None:
                    return {
                        "message": "Invalid Authentication token!",
                        "data": None,
                        "error": "Unauthorized"
                    }, 401

                # If the doesn't have the required role, return an error message
                if roles and current_user.role not in roles:
                    return {
                        "message": "Insufficient permissions. Required roles: {}".format(roles),
                        "data": None,
                        "error": "Forbidden"
                    }, 403

            # If there's an error (likely with the token), return an error message
            except Exception as e:
                return {
                    "message": "Something went wrong, likely with the token!",
                    "data": None,
                    "error": str(e)
                }, 500

            # If the user is authenticated and has the required role (if applicable), call the decorated function
            return f(current_user, *args, **kwargs)

        return decorated

    return decorator


```

## Deployment Process Overview

### AWS Setup
- **Launch EC2 Instance**: Choose Ubuntu AMI, create key pair for SSH access, configure security group for SSH, HTTP, and HTTPS.
- **Allocate Elastic IP**: Recommended for consistent IP address after instance reboot.
- **Set Up Route 53**: Create domain or subdomain for mapping Nginx configuration.

### Configuration Files
- **GitHub for Version Control**: Store configuration files for Docker, Nginx, and Python in GitHub.

### Docker
- **Dockerfile and docker-compose.yml**: Build Python application, mount persistent volumes for database and uploads, expose application port.

### Nginx
- **Nginx Configuration**: Listen for DNS requests, reverse proxy to Docker-exposed port, manage CORS policies and HTTP methods.

### Python
- **init.py Configuration**: Manage settings, specify database and uploads location outside Docker container.



# Sample Docker file



```python
 Use the official Python 3.10 image from Docker Hub as the base image
FROM docker.io/python:3.10

# Set the working directory to the root of the Docker container
WORKDIR /

# Update the system packages and install Python3, pip, and git
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y python3 python3-pip git

# Copy the local files into the Docker container
COPY . /

# Install the Python dependencies specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Install gunicorn, a WSGI HTTP server for Python web applications
RUN pip install gunicorn

# Set the command line arguments for gunicorn
# --workers=1: Use 1 worker process
# --bind=0.0.0.0:8086: Bind the server to all available network interfaces and use port 8086
ENV GUNICORN_CMD_ARGS="--workers=1 --bind=0.0.0.0:8086"

# Expose port 8086 to the host machine, allowing external access to the application
EXPOSE 8086

# Start the gunicorn server when the container is run, using the application defined in main.py
CMD [ "gunicorn", "main:app" ]
```

# Sample docker-compose.yml


```python
# Specify the Docker Compose file version
version: '3'

# Define the services that make up your app
services:
    # The 'web' service is your Flask application
    web:
        # Name of the Docker image to be built for the 'web' service
        image: flask_portfolio_v1
        # Build the Dockerfile in the current directory
        build: .
        # Map port 8286 on the host to port 8086 in the container
        ports:
                - "8286:8086"
        # Mount the 'instance' directory from the host to '/instance' in the container
        # This allows the container to access the data in the 'instance' directory
        volumes:
                - ./instance:/instance
        # Automatically restart the container if it crashes, unless it was manually stopped
        restart: unless-stopped
```

# Sample Nginx configuration file


```python
# This block defines a server that listens on port 80
server {
    # Listen for incoming connections on port 80 for both IPv4 and IPv6
    listen 80;
    listen [::]:80;

    # DNS. The server_name directive 
    server_name flask2.nighthawkcodingsociety.com;

    # This block defines how to respond to requests for the root location ("/")
    location / {
        # Port. The proxy_pass directive sets the protocol and address of the proxied server
        proxy_pass http://localhost:8286;

        # This block handles preflighted requests (HTTP OPTIONS method)
        if ($request_method = OPTIONS) {
            # Cookies. This allows the browser to include credentials in the request
            add_header "Access-Control-Allow-Credentials" "true" always;

            # CORS. This specifies the cross origin that is allowed to access the resource
            add_header "Access-Control-Allow-Origin"  "https://nighthawkcoders.github.io" always;

            # Methods. This specifies the methods that are allowed when accessing the resource
            add_header "Access-Control-Allow-Methods" "GET, POST, PUT, OPTIONS, HEAD" always;

            # This specifies how long the results of a preflight request can be cached
            add_header "Access-Control-Allow-MaxAge" 600 always;

            # This specifies the headers that are allowed in the actual request
            add_header "Access-Control-Allow-Headers" "Authorization, Origin, X-Requested-With, Content-Type, Accept" always;

            # This indicates that the server has successfully fulfilled the request and there is no additional content to send in the response payload body
            return 204;
        }

    }
}
```

# Sample init.py file


```python
from flask import Flask
from flask_cors import CORS
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate
import os

"""
These object can be used throughout project.
1.) Objects from this file can be included in many blueprints
2.) Isolating these object definitions avoids duplication and circular dependencies
"""

# Setup of key Flask object (app)
app = Flask(__name__)
# Allowed servers for cross-origin resource sharing (CORS)
cors = CORS(app, supports_credentials=True, origins=['http://localhost:4100', 'http://127.0.0.1:4100', 'http://127.0.0.1:8086', 'https://nighthawkcoders.github.io'])

# Secret key for session handling and CSRF protection
SECRET_KEY = os.environ.get('SECRET_KEY') or 'SECRET_KEY'
app.config['SECRET_KEY'] = SECRET_KEY

# Setup SQLAlchemy object and properties for the database (db)
# Local SQLite database within the instance folder
dbURI = 'sqlite:///volumes/sqlite.db'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
app.config['SQLALCHEMY_DATABASE_URI'] = dbURI
db = SQLAlchemy()
Migrate(app, db)

# Images storage settings and location
app.config['MAX_CONTENT_LENGTH'] = 5 * 1024 * 1024  # maximum size of uploaded content
app.config['UPLOAD_EXTENSIONS'] = ['.jpg', '.png', '.gif']  # supported file types
app.config['UPLOAD_FOLDER'] = os.path.join(app.instance_path, 'uploads')
os.makedirs(app.config['UPLOAD_FOLDER'], exist_ok=True)
```

## Relationship of Full Stack and Deployment to College Board Questions

### Sending and Receiving Information
- Full Stack applications constantly exchange information between client and server for actions like logging in or retrieving data.

### Facilitating Data Transfer
- Computer systems and networks facilitate data transfer in Full Stack applications by handling requests and responses between frontend and backend.

### JavaScript Fetch, URI, Credentials, and Cookie
- JavaScript Fetch API sends requests, configures URI, manages credentials, and handles cookies for communication between frontend and backend.

### Nginx, Credentials, Cookies, CORS, and HTTP Methods
- Nginx manages inbound requests, sets CORS policies, handles cookies, and specifies allowed HTTP methods, facilitating communication between client and server.

### Transmitting Information on the Internet
- Full Stack applications deploy to servers accessible via the Internet, allowing users to send requests and receive responses over the Internet.

### Python, CORS, Instance Data, CSRF
- Python backend manages CORS policies, instance data persistence, and CSRF protection, enhancing security and data management.

### Purpose of Internet Protocols
- Internet protocols like HTTP and HTTPS standardize request/response formatting and transmission, ensuring secure and efficient communication.

### Certbot, HTTPS, SSL/TLS Certificates
- Certbot automates SSL/TLS certificate installation, enhancing security for HTTPS communication over the Internet.

### Fault Tolerance and Data Persistence
- Cloud services like AWS provide fault tolerance through redundancy and data persistence outside Docker containers, ensuring data integrity and availability.

### Parallel and Distributed Computing
- Full Stack applications leverage parallel processing to handle multiple requests simultaneously, improving efficiency and response times.

### Ability of Parallel Solution to Improve Efficiency
- Parallel processing in Full Stack applications optimizes server performance, enabling faster response times under heavy load.

### Difference Between Running in Parallel or Sequence
- Handling requests in parallel allows tasks to run simultaneously, providing faster response times compared to sequential processing.

