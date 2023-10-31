---
toc: True
comments: True
layout: post
title: Student Lesson Python Libraries
description: To teach the class how to use public Python libraries around the internet
type: hacks
courses: {'csp': {'week': 10}}
---

### What is a Library?
Essentially a list of pre-written code that you can use to streamline and clean up your program.

Libraries can help simplify complex programs

APIS are specifications for how the procedures in a library behave, and how they can be used 

Documentations for an API/library is necessary in understanding the behaviors provided by the API/library and how to use them

Libraries that we will go over: Requests, Pillow, Pandas, Numpy, Scikit-Learn, TensorFlow, matplotlib.


### Required Installations
Please run the following commands in your vscode terminal in order to continue the lesson
- pip install numpy
- pip install matplotlib
- pip install scikit-learn
- pip install pillow
- pip install pandas
- pip install tensorflow
- pip install requests

### Images using requests and pillow libraries
'Requests' is focused on handling HTTP requests and web data while 'Pillow' is designed for data manipulation and analysis
It's common to see them used together in data-related assignments where data is fetched by HTTP requests using Requests and then processed and analyzed with Pandas.

Here's an example:


```python
import requests
from PIL import Image
from io import BytesIO

# Step 1: Download an image using Requests
image_url = "https://example.com/path/to/your/image.jpg"  # Replace with the actual URL of the image you want to download
response = requests.get(image_url)

if response.status_code == 200:
    # Step 2: Process the downloaded image using Pillow
    image_data = BytesIO(response.content)  # Create an in-memory binary stream from the response content
    img = Image.open(image_data)  # Open the image using Pillow

    # Perform image processing tasks here, like resizing or applying filters
    img = img.resize((x, y))  # Resize the image and replace x,y with desired amounts

    # Step 3: Save the processed image using Pillow
    img.save("processed_image.jpg")  # Save the processed image to a file

    print("Image downloaded, processed, and saved.")
else:
    print(f"Failed to download image. Status code: {response.status_code}")

```

    Failed to download image. Status code: 404


In this code, we use the Requests library to download an image from a URL and then if the download is successful the HTTP status code 200 will pop up, and from there we create an in-memory binary stream (BytesIO) from the response content. We then use the Pillow library to open the image, make any necessary changes, and save the processed image to a file.

Here's a step by step tutorial on how we wrote this code: 
1)We started by importing the necessary libraries, which were Requests, Pillow, and io.

2)Download the Image

3)Use the Requests library to send an HTTP GET request to the URL to download the image.
Check the response status code to make sure the download goes through(status code 200).

4)If the download is successful, create an in-memory binary stream (BytesIO) from the response content.
Process the Image:

5)Utilize the Pillow library to open the image from the binary stream.
Change photo to desired preference(ie: size)
Save the Processed Image:

6)Save the processed image to a file using Pillow. Choose a filename and file format for the saved image.




### Hack 1

Write a Python code that accomplishes the following tasks:

Downloads an image from a specified URL using the Requests library.
Processes the downloaded image (like resizing) using the Pillow library.
Save the processed image to a file.



```python
#Code here
import requests
from PIL import Image
from io import BytesIO

# Step 1: Download an image using Requests
image_url = "https://cdn.vox-cdn.com/thumbor/hhnSE8SDm8Bg92fG_gb3J9gTUjU=/0x0:6000x4000/1200x800/filters:focal(2958x758:3918x1718)/cdn.vox-cdn.com/uploads/chorus_image/image/72365465/1258245670.0.jpg"  # Replace with the actual URL of the image you want to download
response = requests.get(image_url)

if response.status_code == 200:
    # Step 2: Process the downloaded image using Pillow
    image_data = BytesIO(response.content)  # Create an in-memory binary stream from the response content
    img = Image.open(image_data)  # Open the image using Pillow

    # Perform image processing tasks here, like resizing or applying filters
    img = img.resize((670,490))  # Resize the image and replace x,y with desired amounts

    # Step 3: Save the processed image using Pillow
    img.save("processed_image.jpg")  # Save the processed image to a file

    print("Image downloaded, processed, and saved.")
else:
    print(f"Failed to download image. Status code: {response.status_code}")

```

    Image downloaded, processed, and saved.


### Math Operations With Python Libraries
Numpy(Numerical Python) is used for numerical and scientific computing. It provides tools for handling large sets of numbers, such as data tables and arrays. Numpy makes it easier and more efficient to do mathematical tasks. 

The Matplotlib library lets you create a visual representation of your data (graphs, charts, and etc.)

### Example Sine Graph
Uses numpy and matplotlib libaries


```python
import numpy as np
import matplotlib.pyplot as plt

# Generate sample data with NumPy
x = np.linspace(0, 2 * np.pi, 100) 
# Create an array of values from 0 to 2*pi
# 100 is included to have 100 points distributed between 0 and 2π to make graph smoother
y = np.sin(x)
# Compute the sine of each value

# Create a simple line plot using Matplotlib
plt.plot(x, y, label='Sine Function', color='blue', linestyle='-')  # Create the plot
plt.title('Sine Function')  # Set the title
plt.xlabel('x')  # Label for the x-axis
plt.ylabel('sin(x)')  # Label for the y-axis
plt.grid(True)  # Display a grid
plt.legend()  # Show the legend
plt.show()  # Display the plot

```


    
![png](output_10_0.png)
    


### Hack 2
Using the data from the numpy library, create a visual graph using different matplotlib functions.


```python
import numpy as np
import matplotlib.pyplot as plt

# Generate data for two lines
x = np.linspace(0, 10, 50)  # Create an array of values from 0 to 10
y1 = 2 * x + 1  # Set of data poits

# Create and display a plot using Matplotlib
# Create a simple line plot using Matplotlib
plt.plot(x, y1, label='Line', color='blue', linestyle='-')  # Create the plot
plt.title('Line')  # Set the title
plt.xlabel('x')  # Label for the x-axis
plt.ylabel('y')  # Label for the y-axis
plt.grid(True)  # Display a grid
plt.legend()  # Show the legend
plt.show()  # Display the plot
# your code here

```


    
![png](output_12_0.png)
    


Tensor Flow is used in deep learning and neural networks, while scikit-learn is used for typical machine learning tasks. When used together, they can tackle machine learning projects. In the code below, Tensor Flow is used for model creation and training. Scikit-learn is used for data-processing and model evaluation.

## Pip install tensorflow scikit-learn


```python

```


```python
import numpy as np
import tensorflow as tf
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error
from sklearn.preprocessing import StandardScaler
from tensorflow import keras
from tensorflow.keras import layers
# Generate synthetic data
np.random.seed(0)
X = np.random.rand(100, 1)  # Feature
y = 2 * X + 1 + 0.1 * np.random.randn(100, 1)  # Target variable with noise
# Split the data into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
# Standardize the features
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)
# Create a simple linear regression model using TensorFlow and Keras
model = keras.Sequential([
    layers.Input(shape=(1,)),
    layers.Dense(1)
])
# Compile the model
model.compile(optimizer='adam', loss='mean_squared_error')
# Train the model
model.fit(X_train, y_train, epochs=100, batch_size=32, verbose=2)
# Make predictions on the test set
y_pred = model.predict(X_test)
# Calculate the Mean Squared Error on the test set
mse = mean_squared_error(y_test, y_pred)
print(f"Mean Squared Error: {mse:.4f}")
```

    Epoch 1/100
    3/3 - 0s - loss: 6.3253 - 288ms/epoch - 96ms/step
    Epoch 2/100
    3/3 - 0s - loss: 6.3058 - 7ms/epoch - 2ms/step
    Epoch 3/100
    3/3 - 0s - loss: 6.2832 - 7ms/epoch - 2ms/step
    Epoch 4/100
    3/3 - 0s - loss: 6.2632 - 6ms/epoch - 2ms/step
    Epoch 5/100
    3/3 - 0s - loss: 6.2430 - 7ms/epoch - 2ms/step
    Epoch 6/100
    3/3 - 0s - loss: 6.2221 - 7ms/epoch - 2ms/step
    Epoch 7/100
    3/3 - 0s - loss: 6.2016 - 7ms/epoch - 2ms/step
    Epoch 8/100
    3/3 - 0s - loss: 6.1815 - 7ms/epoch - 2ms/step
    Epoch 9/100
    3/3 - 0s - loss: 6.1614 - 8ms/epoch - 3ms/step
    Epoch 10/100
    3/3 - 0s - loss: 6.1395 - 8ms/epoch - 3ms/step
    Epoch 11/100
    3/3 - 0s - loss: 6.1192 - 7ms/epoch - 2ms/step
    Epoch 12/100
    3/3 - 0s - loss: 6.0993 - 8ms/epoch - 3ms/step
    Epoch 13/100
    3/3 - 0s - loss: 6.0805 - 8ms/epoch - 3ms/step
    Epoch 14/100
    3/3 - 0s - loss: 6.0586 - 8ms/epoch - 3ms/step
    Epoch 15/100
    3/3 - 0s - loss: 6.0384 - 7ms/epoch - 2ms/step
    Epoch 16/100
    3/3 - 0s - loss: 6.0187 - 8ms/epoch - 3ms/step
    Epoch 17/100
    3/3 - 0s - loss: 5.9990 - 7ms/epoch - 2ms/step
    Epoch 18/100
    3/3 - 0s - loss: 5.9791 - 6ms/epoch - 2ms/step
    Epoch 19/100
    3/3 - 0s - loss: 5.9590 - 9ms/epoch - 3ms/step
    Epoch 20/100
    3/3 - 0s - loss: 5.9393 - 9ms/epoch - 3ms/step
    Epoch 21/100
    3/3 - 0s - loss: 5.9194 - 9ms/epoch - 3ms/step
    Epoch 22/100
    3/3 - 0s - loss: 5.9002 - 8ms/epoch - 3ms/step
    Epoch 23/100
    3/3 - 0s - loss: 5.8789 - 8ms/epoch - 3ms/step
    Epoch 24/100
    3/3 - 0s - loss: 5.8597 - 9ms/epoch - 3ms/step
    Epoch 25/100
    3/3 - 0s - loss: 5.8407 - 8ms/epoch - 3ms/step
    Epoch 26/100
    3/3 - 0s - loss: 5.8199 - 8ms/epoch - 3ms/step
    Epoch 27/100
    3/3 - 0s - loss: 5.8017 - 8ms/epoch - 3ms/step
    Epoch 28/100
    3/3 - 0s - loss: 5.7818 - 8ms/epoch - 3ms/step
    Epoch 29/100
    3/3 - 0s - loss: 5.7612 - 9ms/epoch - 3ms/step
    Epoch 30/100
    3/3 - 0s - loss: 5.7425 - 7ms/epoch - 2ms/step
    Epoch 31/100
    3/3 - 0s - loss: 5.7228 - 7ms/epoch - 2ms/step
    Epoch 32/100
    3/3 - 0s - loss: 5.7040 - 8ms/epoch - 3ms/step
    Epoch 33/100
    3/3 - 0s - loss: 5.6837 - 6ms/epoch - 2ms/step
    Epoch 34/100
    3/3 - 0s - loss: 5.6644 - 6ms/epoch - 2ms/step
    Epoch 35/100
    3/3 - 0s - loss: 5.6441 - 6ms/epoch - 2ms/step
    Epoch 36/100
    3/3 - 0s - loss: 5.6250 - 6ms/epoch - 2ms/step
    Epoch 37/100
    3/3 - 0s - loss: 5.6061 - 6ms/epoch - 2ms/step
    Epoch 38/100
    3/3 - 0s - loss: 5.5857 - 7ms/epoch - 2ms/step
    Epoch 39/100
    3/3 - 0s - loss: 5.5674 - 6ms/epoch - 2ms/step
    Epoch 40/100
    3/3 - 0s - loss: 5.5490 - 8ms/epoch - 3ms/step
    Epoch 41/100
    3/3 - 0s - loss: 5.5289 - 7ms/epoch - 2ms/step
    Epoch 42/100
    3/3 - 0s - loss: 5.5101 - 6ms/epoch - 2ms/step
    Epoch 43/100
    3/3 - 0s - loss: 5.4905 - 7ms/epoch - 2ms/step
    Epoch 44/100
    3/3 - 0s - loss: 5.4729 - 6ms/epoch - 2ms/step
    Epoch 45/100
    3/3 - 0s - loss: 5.4541 - 6ms/epoch - 2ms/step
    Epoch 46/100
    3/3 - 0s - loss: 5.4358 - 5ms/epoch - 2ms/step
    Epoch 47/100
    3/3 - 0s - loss: 5.4166 - 7ms/epoch - 2ms/step
    Epoch 48/100
    3/3 - 0s - loss: 5.3984 - 6ms/epoch - 2ms/step
    Epoch 49/100
    3/3 - 0s - loss: 5.3815 - 7ms/epoch - 2ms/step
    Epoch 50/100
    3/3 - 0s - loss: 5.3627 - 9ms/epoch - 3ms/step
    Epoch 51/100
    3/3 - 0s - loss: 5.3442 - 14ms/epoch - 5ms/step
    Epoch 52/100
    3/3 - 0s - loss: 5.3250 - 8ms/epoch - 3ms/step
    Epoch 53/100
    3/3 - 0s - loss: 5.3080 - 7ms/epoch - 2ms/step
    Epoch 54/100
    3/3 - 0s - loss: 5.2907 - 6ms/epoch - 2ms/step
    Epoch 55/100
    3/3 - 0s - loss: 5.2705 - 7ms/epoch - 2ms/step
    Epoch 56/100
    3/3 - 0s - loss: 5.2534 - 6ms/epoch - 2ms/step
    Epoch 57/100
    3/3 - 0s - loss: 5.2360 - 7ms/epoch - 2ms/step
    Epoch 58/100
    3/3 - 0s - loss: 5.2179 - 8ms/epoch - 3ms/step
    Epoch 59/100
    3/3 - 0s - loss: 5.2005 - 6ms/epoch - 2ms/step
    Epoch 60/100
    3/3 - 0s - loss: 5.1818 - 6ms/epoch - 2ms/step
    Epoch 61/100
    3/3 - 0s - loss: 5.1637 - 6ms/epoch - 2ms/step
    Epoch 62/100
    3/3 - 0s - loss: 5.1472 - 6ms/epoch - 2ms/step
    Epoch 63/100
    3/3 - 0s - loss: 5.1298 - 6ms/epoch - 2ms/step
    Epoch 64/100
    3/3 - 0s - loss: 5.1102 - 6ms/epoch - 2ms/step
    Epoch 65/100
    3/3 - 0s - loss: 5.0937 - 7ms/epoch - 2ms/step
    Epoch 66/100
    3/3 - 0s - loss: 5.0763 - 6ms/epoch - 2ms/step
    Epoch 67/100
    3/3 - 0s - loss: 5.0591 - 8ms/epoch - 3ms/step
    Epoch 68/100
    3/3 - 0s - loss: 5.0408 - 11ms/epoch - 4ms/step
    Epoch 69/100
    3/3 - 0s - loss: 5.0243 - 7ms/epoch - 2ms/step
    Epoch 70/100
    3/3 - 0s - loss: 5.0069 - 7ms/epoch - 2ms/step
    Epoch 71/100
    3/3 - 0s - loss: 4.9905 - 8ms/epoch - 3ms/step
    Epoch 72/100
    3/3 - 0s - loss: 4.9721 - 8ms/epoch - 3ms/step
    Epoch 73/100
    3/3 - 0s - loss: 4.9560 - 8ms/epoch - 3ms/step
    Epoch 74/100
    3/3 - 0s - loss: 4.9393 - 6ms/epoch - 2ms/step
    Epoch 75/100
    3/3 - 0s - loss: 4.9221 - 6ms/epoch - 2ms/step
    Epoch 76/100
    3/3 - 0s - loss: 4.9055 - 8ms/epoch - 3ms/step
    Epoch 77/100
    3/3 - 0s - loss: 4.8883 - 7ms/epoch - 2ms/step
    Epoch 78/100
    3/3 - 0s - loss: 4.8720 - 8ms/epoch - 3ms/step
    Epoch 79/100
    3/3 - 0s - loss: 4.8556 - 7ms/epoch - 2ms/step
    Epoch 80/100
    3/3 - 0s - loss: 4.8380 - 8ms/epoch - 3ms/step
    Epoch 81/100
    3/3 - 0s - loss: 4.8220 - 7ms/epoch - 2ms/step
    Epoch 82/100
    3/3 - 0s - loss: 4.8047 - 6ms/epoch - 2ms/step
    Epoch 83/100
    3/3 - 0s - loss: 4.7866 - 5ms/epoch - 2ms/step
    Epoch 84/100
    3/3 - 0s - loss: 4.7705 - 5ms/epoch - 2ms/step
    Epoch 85/100
    3/3 - 0s - loss: 4.7528 - 7ms/epoch - 2ms/step
    Epoch 86/100
    3/3 - 0s - loss: 4.7361 - 5ms/epoch - 2ms/step
    Epoch 87/100
    3/3 - 0s - loss: 4.7193 - 7ms/epoch - 2ms/step
    Epoch 88/100
    3/3 - 0s - loss: 4.7018 - 7ms/epoch - 2ms/step
    Epoch 89/100
    3/3 - 0s - loss: 4.6850 - 7ms/epoch - 2ms/step
    Epoch 90/100
    3/3 - 0s - loss: 4.6691 - 8ms/epoch - 3ms/step
    Epoch 91/100
    3/3 - 0s - loss: 4.6516 - 7ms/epoch - 2ms/step
    Epoch 92/100
    3/3 - 0s - loss: 4.6356 - 8ms/epoch - 3ms/step
    Epoch 93/100
    3/3 - 0s - loss: 4.6187 - 7ms/epoch - 2ms/step
    Epoch 94/100
    3/3 - 0s - loss: 4.6018 - 7ms/epoch - 2ms/step
    Epoch 95/100
    3/3 - 0s - loss: 4.5858 - 7ms/epoch - 2ms/step
    Epoch 96/100
    3/3 - 0s - loss: 4.5700 - 10ms/epoch - 3ms/step
    Epoch 97/100
    3/3 - 0s - loss: 4.5536 - 7ms/epoch - 2ms/step
    Epoch 98/100
    3/3 - 0s - loss: 4.5374 - 7ms/epoch - 2ms/step
    Epoch 99/100
    3/3 - 0s - loss: 4.5216 - 8ms/epoch - 3ms/step
    Epoch 100/100
    3/3 - 0s - loss: 4.5054 - 8ms/epoch - 3ms/step
    1/1 [==============================] - 0s 31ms/step
    Mean Squared Error: 4.9275


A decrease in loss and time metrics (ms/epoch and ms/step) shows the efficiency increases as the training epochs increases

## Hack
fill in the missing code to match the custom data set


```python
import numpy as np
import tensorflow as tf
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error
from sklearn.preprocessing import StandardScaler
from tensorflow import keras
from tensorflow.keras import layers

# Set a random seed for reproducibility
np.random.seed(0)

# Generate a synthetic dataset for house prices based on number of bedrooms and square footage
num_samples = 100
bedrooms = np.random.randint(1, 5, num_samples)
square_footage = np.random.randint(1000, 2500, num_samples)
house_prices = 100000 + 50000 * bedrooms + 100 * square_footage + 10000 * np.random.randn(num_samples)

# Combine features (bedrooms and square footage) into one array
features = np.column_stack((bedrooms, square_footage))
target = house_prices.reshape(-1, 1)

# Split the dataset into training and test sets
X_train, X_test, y_train, y_test = train_test_split(features, target, test_size=0.2, random_state=42)

# Standardize the features
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)

# Create a simple linear regression model using TensorFlow and Keras
model = keras.Sequential([
    layers.Input(shape=(2,)),  # Input shape matches the number of features (2)
    layers.Dense(1)  # Single output neuron for regression
])

# Compile the model
model.compile(optimizer='adam', loss='mean_squared_error')

# Train the model
model.fit(X_train, y_train, epochs=100, batch_size=32, verbose=2)

# Make predictions on the test set
y_pred = model.predict(X_test)

# Calculate the Mean Squared Error on the test set
mse = mean_squared_error(y_test, y_pred)
print(f"Mean Squared Error: {mse:.4f}")

```

    Epoch 1/100
    3/3 - 0s - loss: 171448008704.0000 - 306ms/epoch - 102ms/step
    Epoch 2/100
    3/3 - 0s - loss: 171448025088.0000 - 8ms/epoch - 3ms/step
    Epoch 3/100
    3/3 - 0s - loss: 171448025088.0000 - 7ms/epoch - 2ms/step
    Epoch 4/100
    3/3 - 0s - loss: 171447992320.0000 - 6ms/epoch - 2ms/step
    Epoch 5/100
    3/3 - 0s - loss: 171447992320.0000 - 8ms/epoch - 3ms/step
    Epoch 6/100
    3/3 - 0s - loss: 171447992320.0000 - 9ms/epoch - 3ms/step
    Epoch 7/100
    3/3 - 0s - loss: 171447975936.0000 - 9ms/epoch - 3ms/step
    Epoch 8/100
    3/3 - 0s - loss: 171447992320.0000 - 10ms/epoch - 3ms/step
    Epoch 9/100
    3/3 - 0s - loss: 171447992320.0000 - 14ms/epoch - 5ms/step
    Epoch 10/100
    3/3 - 0s - loss: 171447975936.0000 - 14ms/epoch - 5ms/step
    Epoch 11/100
    3/3 - 0s - loss: 171447975936.0000 - 10ms/epoch - 3ms/step
    Epoch 12/100
    3/3 - 0s - loss: 171447975936.0000 - 9ms/epoch - 3ms/step
    Epoch 13/100
    3/3 - 0s - loss: 171447975936.0000 - 10ms/epoch - 3ms/step
    Epoch 14/100
    3/3 - 0s - loss: 171447975936.0000 - 8ms/epoch - 3ms/step
    Epoch 15/100
    3/3 - 0s - loss: 171447975936.0000 - 8ms/epoch - 3ms/step
    Epoch 16/100
    3/3 - 0s - loss: 171447975936.0000 - 7ms/epoch - 2ms/step
    Epoch 17/100
    3/3 - 0s - loss: 171447975936.0000 - 6ms/epoch - 2ms/step
    Epoch 18/100
    3/3 - 0s - loss: 171447975936.0000 - 6ms/epoch - 2ms/step
    Epoch 19/100
    3/3 - 0s - loss: 171447975936.0000 - 7ms/epoch - 2ms/step
    Epoch 20/100
    3/3 - 0s - loss: 171447975936.0000 - 5ms/epoch - 2ms/step
    Epoch 21/100
    3/3 - 0s - loss: 171447943168.0000 - 6ms/epoch - 2ms/step
    Epoch 22/100
    3/3 - 0s - loss: 171447943168.0000 - 7ms/epoch - 2ms/step
    Epoch 23/100
    3/3 - 0s - loss: 171447943168.0000 - 7ms/epoch - 2ms/step
    Epoch 24/100
    3/3 - 0s - loss: 171447943168.0000 - 8ms/epoch - 3ms/step
    Epoch 25/100
    3/3 - 0s - loss: 171447943168.0000 - 6ms/epoch - 2ms/step
    Epoch 26/100
    3/3 - 0s - loss: 171447943168.0000 - 5ms/epoch - 2ms/step
    Epoch 27/100
    3/3 - 0s - loss: 171447926784.0000 - 6ms/epoch - 2ms/step
    Epoch 28/100
    3/3 - 0s - loss: 171447943168.0000 - 7ms/epoch - 2ms/step
    Epoch 29/100
    3/3 - 0s - loss: 171447926784.0000 - 5ms/epoch - 2ms/step
    Epoch 30/100
    3/3 - 0s - loss: 171447943168.0000 - 5ms/epoch - 2ms/step
    Epoch 31/100
    3/3 - 0s - loss: 171447910400.0000 - 6ms/epoch - 2ms/step
    Epoch 32/100
    3/3 - 0s - loss: 171447926784.0000 - 6ms/epoch - 2ms/step
    Epoch 33/100
    3/3 - 0s - loss: 171447926784.0000 - 6ms/epoch - 2ms/step
    Epoch 34/100
    3/3 - 0s - loss: 171447910400.0000 - 7ms/epoch - 2ms/step
    Epoch 35/100
    3/3 - 0s - loss: 171447910400.0000 - 5ms/epoch - 2ms/step
    Epoch 36/100
    3/3 - 0s - loss: 171447910400.0000 - 5ms/epoch - 2ms/step
    Epoch 37/100
    3/3 - 0s - loss: 171447910400.0000 - 7ms/epoch - 2ms/step
    Epoch 38/100
    3/3 - 0s - loss: 171447910400.0000 - 6ms/epoch - 2ms/step
    Epoch 39/100
    3/3 - 0s - loss: 171447910400.0000 - 7ms/epoch - 2ms/step
    Epoch 40/100
    3/3 - 0s - loss: 171447910400.0000 - 7ms/epoch - 2ms/step
    Epoch 41/100
    3/3 - 0s - loss: 171447894016.0000 - 7ms/epoch - 2ms/step
    Epoch 42/100
    3/3 - 0s - loss: 171447894016.0000 - 7ms/epoch - 2ms/step
    Epoch 43/100
    3/3 - 0s - loss: 171447910400.0000 - 7ms/epoch - 2ms/step
    Epoch 44/100
    3/3 - 0s - loss: 171447894016.0000 - 7ms/epoch - 2ms/step
    Epoch 45/100
    3/3 - 0s - loss: 171447894016.0000 - 8ms/epoch - 3ms/step
    Epoch 46/100
    3/3 - 0s - loss: 171447894016.0000 - 7ms/epoch - 2ms/step
    Epoch 47/100
    3/3 - 0s - loss: 171447877632.0000 - 7ms/epoch - 2ms/step
    Epoch 48/100
    3/3 - 0s - loss: 171447894016.0000 - 10ms/epoch - 3ms/step
    Epoch 49/100
    3/3 - 0s - loss: 171447861248.0000 - 8ms/epoch - 3ms/step
    Epoch 50/100
    3/3 - 0s - loss: 171447894016.0000 - 9ms/epoch - 3ms/step
    Epoch 51/100
    3/3 - 0s - loss: 171447861248.0000 - 8ms/epoch - 3ms/step
    Epoch 52/100
    3/3 - 0s - loss: 171447877632.0000 - 8ms/epoch - 3ms/step
    Epoch 53/100
    3/3 - 0s - loss: 171447861248.0000 - 6ms/epoch - 2ms/step
    Epoch 54/100
    3/3 - 0s - loss: 171447861248.0000 - 6ms/epoch - 2ms/step
    Epoch 55/100
    3/3 - 0s - loss: 171447844864.0000 - 6ms/epoch - 2ms/step
    Epoch 56/100
    3/3 - 0s - loss: 171447844864.0000 - 6ms/epoch - 2ms/step
    Epoch 57/100
    3/3 - 0s - loss: 171447844864.0000 - 7ms/epoch - 2ms/step
    Epoch 58/100
    3/3 - 0s - loss: 171447844864.0000 - 8ms/epoch - 3ms/step
    Epoch 59/100
    3/3 - 0s - loss: 171447844864.0000 - 8ms/epoch - 3ms/step
    Epoch 60/100
    3/3 - 0s - loss: 171447844864.0000 - 10ms/epoch - 3ms/step
    Epoch 61/100
    3/3 - 0s - loss: 171447844864.0000 - 9ms/epoch - 3ms/step
    Epoch 62/100
    3/3 - 0s - loss: 171447844864.0000 - 9ms/epoch - 3ms/step
    Epoch 63/100
    3/3 - 0s - loss: 171447844864.0000 - 7ms/epoch - 2ms/step
    Epoch 64/100
    3/3 - 0s - loss: 171447844864.0000 - 8ms/epoch - 3ms/step
    Epoch 65/100
    3/3 - 0s - loss: 171447844864.0000 - 9ms/epoch - 3ms/step
    Epoch 66/100
    3/3 - 0s - loss: 171447828480.0000 - 9ms/epoch - 3ms/step
    Epoch 67/100
    3/3 - 0s - loss: 171447812096.0000 - 7ms/epoch - 2ms/step
    Epoch 68/100
    3/3 - 0s - loss: 171447828480.0000 - 8ms/epoch - 3ms/step
    Epoch 69/100
    3/3 - 0s - loss: 171447828480.0000 - 7ms/epoch - 2ms/step
    Epoch 70/100
    3/3 - 0s - loss: 171447828480.0000 - 7ms/epoch - 2ms/step
    Epoch 71/100
    3/3 - 0s - loss: 171447812096.0000 - 7ms/epoch - 2ms/step
    Epoch 72/100
    3/3 - 0s - loss: 171447828480.0000 - 7ms/epoch - 2ms/step
    Epoch 73/100
    3/3 - 0s - loss: 171447812096.0000 - 8ms/epoch - 3ms/step
    Epoch 74/100
    3/3 - 0s - loss: 171447812096.0000 - 7ms/epoch - 2ms/step
    Epoch 75/100
    3/3 - 0s - loss: 171447812096.0000 - 6ms/epoch - 2ms/step
    Epoch 76/100
    3/3 - 0s - loss: 171447795712.0000 - 8ms/epoch - 3ms/step
    Epoch 77/100
    3/3 - 0s - loss: 171447795712.0000 - 7ms/epoch - 2ms/step
    Epoch 78/100
    3/3 - 0s - loss: 171447812096.0000 - 7ms/epoch - 2ms/step
    Epoch 79/100
    3/3 - 0s - loss: 171447779328.0000 - 7ms/epoch - 2ms/step
    Epoch 80/100
    3/3 - 0s - loss: 171447779328.0000 - 8ms/epoch - 3ms/step
    Epoch 81/100
    3/3 - 0s - loss: 171447779328.0000 - 8ms/epoch - 3ms/step
    Epoch 82/100
    3/3 - 0s - loss: 171447779328.0000 - 8ms/epoch - 3ms/step
    Epoch 83/100
    3/3 - 0s - loss: 171447779328.0000 - 8ms/epoch - 3ms/step
    Epoch 84/100
    3/3 - 0s - loss: 171447779328.0000 - 8ms/epoch - 3ms/step
    Epoch 85/100
    3/3 - 0s - loss: 171447779328.0000 - 8ms/epoch - 3ms/step
    Epoch 86/100
    3/3 - 0s - loss: 171447779328.0000 - 7ms/epoch - 2ms/step
    Epoch 87/100
    3/3 - 0s - loss: 171447779328.0000 - 8ms/epoch - 3ms/step
    Epoch 88/100
    3/3 - 0s - loss: 171447762944.0000 - 10ms/epoch - 3ms/step
    Epoch 89/100
    3/3 - 0s - loss: 171447779328.0000 - 8ms/epoch - 3ms/step
    Epoch 90/100
    3/3 - 0s - loss: 171447762944.0000 - 9ms/epoch - 3ms/step
    Epoch 91/100
    3/3 - 0s - loss: 171447762944.0000 - 6ms/epoch - 2ms/step
    Epoch 92/100
    3/3 - 0s - loss: 171447762944.0000 - 7ms/epoch - 2ms/step
    Epoch 93/100
    3/3 - 0s - loss: 171447762944.0000 - 9ms/epoch - 3ms/step
    Epoch 94/100
    3/3 - 0s - loss: 171447762944.0000 - 7ms/epoch - 2ms/step
    Epoch 95/100
    3/3 - 0s - loss: 171447762944.0000 - 7ms/epoch - 2ms/step
    Epoch 96/100
    3/3 - 0s - loss: 171447762944.0000 - 10ms/epoch - 3ms/step
    Epoch 97/100
    3/3 - 0s - loss: 171447762944.0000 - 7ms/epoch - 2ms/step
    Epoch 98/100
    3/3 - 0s - loss: 171447746560.0000 - 7ms/epoch - 2ms/step
    Epoch 99/100
    3/3 - 0s - loss: 171447762944.0000 - 8ms/epoch - 3ms/step
    Epoch 100/100
    3/3 - 0s - loss: 171447730176.0000 - 8ms/epoch - 3ms/step
    1/1 [==============================] - 0s 41ms/step
    Mean Squared Error: 158482082727.9915


## HOMEWORK 1

Create a GPA calculator using Pandas and Matplot libraries and make:
1) A dataframe
2) A specified dictionary
3) and a print function that outputs the final GPA

Extra points can be earned with creativity.


```python
import pandas as pd
import matplotlib.pyplot as plt

# Create a dictionary to represent courses and grades
data = {
    'Course': ['Math', 'Science', 'History', 'English', 'Art'],
    'Grade': [3.7, 4.0, 3.3, 3.0, 3.5]  # Replace with your actual grades
}

# Create a DataFrame from the dictionary
df = pd.DataFrame(data)

# Create a dictionary to map grades to GPA scale
grade_to_gpa = {
    'A+': 4.0,
    'A': 4.0,
    'A-': 3.7,
    'B+': 3.3,
    'B': 3.0,
    'B-': 2.7,
    'C+': 2.3,
    'C': 2.0,
    'C-': 1.7,
    'D+': 1.3,
    'D': 1.0,
    'F': 0.0
}

# Remove rows with missing grades (NaN)
df = df.dropna(subset=['Grade'])

# Calculate GPA
def calculate_gpa(grades):
    total_points = sum(grade_to_gpa.get(grade, 0) for grade in grades)
    gpa = total_points / len(grades)
    return gpa

# Map grades to GPA
df['Grade'] = df['Grade'].map({v: k for k, v in grade_to_gpa.items()})

# Print function to calculate and output the final GPA
def print_final_gpa(dataframe):
    grades = [grade for grade in dataframe['Grade']]
    gpa = calculate_gpa(grades)
    print("Course Grades:")
    print(dataframe)
    print(f"Final GPA: {gpa:.2f}")

# Print the final GPA
print_final_gpa(df)

# Extra: Visualize GPA with a bar chart
plt.bar(df['Course'], df['Grade'].map(grade_to_gpa))
plt.title("Course GPA")
plt.xlabel("Courses")
plt.ylabel("GPA")
plt.ylim(0, 4.0)
plt.show()

```

    Course Grades:
        Course Grade
    0     Math    A-
    1  Science     A
    2  History    B+
    3  English     B
    4      Art   NaN
    Final GPA: 2.80



    
![png](output_21_1.png)
    


## HOMEWORK 2

Import and use the "random" library to generate 50 different points from the range 0-100, then display the randomized data using a scatter plot.

Extra points can be earned with creativity.


```python
import random
import matplotlib.pyplot as plt

# Generate 50 random points in the range 0-100
x = [random.uniform(0, 100) for _ in range(50)]
y = [random.uniform(0, 100) for _ in range(50)]

# Create a scatter plot with custom styling
plt.figure(figsize=(8, 6))  # Adjust the figure size
plt.scatter(x, y, c='skyblue', s=75, alpha=0.7, edgecolors='b', marker='o', label='Random Points')
plt.xlabel('X-Axis', fontsize=14)  # Adjust label font size
plt.ylabel('Y-Axis', fontsize=14)
plt.title('Random Scatter Plot', fontsize=16)
plt.legend(loc='best', fontsize=12)  # Adjust legend font size

# Add a grid
plt.grid(True, linestyle='--', alpha=0.5)

# Add a color bar to indicate point density
cb = plt.colorbar()
cb.set_label('Point Density', fontsize=12)

# Add a title and labels
plt.text(60, 90, 'Generated Data', fontsize=14, color='red')
plt.annotate('Outlier', xy=(x[0], y[0]), xytext=(20, 40),
             arrowprops=dict(facecolor='black', shrink=0.05))

# Display the plot
plt.show()

```


    
![png](output_23_0.png)
    

