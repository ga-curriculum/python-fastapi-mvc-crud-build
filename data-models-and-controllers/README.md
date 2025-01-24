<h1>
  <span class="headline">FastAPI MVC CRUD Build</span>
  <span class="subhead">Data Models and Controllers</span>
</h1>

**Learning Objective:** By the end of this lesson, you will be able to create mock data models for a FastAPI application and build a basic controller to serve that data through an API.

## Introduction

In this lesson, you’ll learn how to define **mock data models** and create the **controller** that will handle API requests in your FastAPI app. We'll be building a simple app that mimics the functionality of an inventory system for teas. While we’re not working with a real database, this approach will let us focus on the fundamental concepts of building a FastAPI CRUD app.

In the context of MVC (Model-View-Controller) architecture:

- **Model**: The data structure that represents the tea information.
- **View**: The API responses sent to the user (we’ll return the data in JSON format).
- **Controller**: The logic that handles requests and interacts with the models (data).

By creating and structuring your app this way, you’ll be able to scale and replace the mock data with a real database later on without disrupting the flow of your application.

## Define your mock data model

Before we build the controller, we’ll start by defining some mock data to simulate what we would typically store in a database. In the `models/tea_data.py` file, we will create a Python dictionary that holds a list of tea objects.

### Why use mock data?

We'll use mock data for the following reasons:

- **Simplified Development**: You don’t need a full database setup yet, so you can start building your app right away.
- **Testing & Debugging**: With mock data, it’s easy to test your endpoints and ensure everything works before introducing the complexity of a database.
- **Focusing on Core Functionality**: By using mock data, you can focus on learning how to build routes, handle requests, and structure your FastAPI app.

Here’s what your `models/tea_data.py` file should look like:

```python
# tea_data.py

teas_db = {
    "teas": [
        {"id": 1, "name": "chai", "in_stock": True, "rating": 4.2},
        {"id": 2, "name": "lemongrass", "in_stock": True, "rating": 3.8},
        {"id": 3, "name": "matcha", "in_stock": False, "rating": 4.4},
    ]
}
```

This mock data will represent our "database," and it contains a list of tea objects. Each tea object has:

- `id`: The unique identifier for the tea.
- `name`: The name of the tea.
- `in_stock`: A boolean indicating whether the tea is available in stock.
- `rating`: A rating value for the tea.

## Create the controller

Next, we’ll create a controller in the `controllers/teas.py` file. The controller is responsible for handling requests, interacting with the model (in this case, `tea_data.py`), and returning the appropriate responses.

In FastAPI, the controller is implemented using `routers`. A router groups related endpoints together.

Open `controllers/teas.py` in your editor and add the following code:

```py
# teas.py

from fastapi import APIRouter
from models.tea_data import teas_db

router = APIRouter()

@router.get("/teas")
def get_teas():
    # Retrieve all teas
    return teas_db
```

### Let's review this code together:

1. We first create an instance of `APIRouter` and assign it to the `router` variable. This is where we will define our API endpoints related to teas.

```py
router = APIRouter()
```

2. The `@router.get("/teas")` line tells FastAPI that we want to define a `GET` endpoint for `/teas`. This means that when a user sends a `GET` request to `/teas`, the `get_teas` function will be called.

```py
@router.get("/teas")
def get_teas():
    # Retrieve all teas
    return teas_db
```

3. The get_teas function will return the data from `teas_db`, which contains all the mock tea data. Since FastAPI automatically converts the data to `JSON` format, this will be returned as a JSON response to the client.
