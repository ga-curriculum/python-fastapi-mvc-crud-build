<h1>
  <span class="headline">FastAPI MVC CRUD Build</span>
  <span class="subhead">Create the Server</span>
</h1>

**Learning Objective:** By the end of this lesson, you will be able to set up a FastAPI server and create the basic structure for a FastAPI MVC CRUD application, including controller and model files.

## Introduction

In this lesson, you’ll build your first FastAPI application using the **Model-View-Controller (MVC)** design pattern. This means you’ll organize your code into:

- **Models**: Define and structure your data.
- **Views**: Send responses to the client (in APIs, this is typically JSON).
- **Controllers**: Handle requests, interact with models, and return responses.

Let’s start by setting up your project and ensuring your FastAPI server is running correctly.

## Review your installation

Before you begin, let’s confirm what the following command does:

```bash
pipenv install fastapi uvicorn
```

### What we installed:

- **Installs FastAPI**: The core library to build your application.
- **Installs Uvicorn**: A server that runs your FastAPI app.
- **Sets up a virtual environment**: A contained environment for your project with dependencies listed in Pipfile and Pipfile.lock.

> Tip: If you clone a FastAPI project, running pipenv install will install all necessary dependencies automatically.

If you need a refresher, check out the [pipenv guide](https://pipenv.pypa.io/en/latest/).

## Create the FastAPI entry point

1. Create a new file called `main.py`:

```sh
touch main.py
```

2. Add the follwoing code :

```python
# main.py

from fastapi import FastAPI

app = FastAPI()


@app.get('/')
def home():
    # Hello world function
    return {'message': 'Hello World!'}
```

## Testing the Application

1. Start the server:

```sh
 pipenv run uvicorn main:app --reload
```

2. Open your browser and go to: [`http://127.0.0.1:8000`](http://127.0.0.1:8000)

You should see:

```json
{
  "message": "Hello World!"
}
```

Make sure you see the `Hello World!` message before proceeding.

## Prepare the MVC directory structure

To build an MVC application, you need to organize your code into folders for **models** and **controllers**.

Open a new terminal window while keeping the server running.

1. Navigate to your project folder:

```bash
cd ~/development/lessons/practice-fastapi-crud-app
```

2. Create directories for models and controllers:

```bash
mkdir models controllers
```

3. Create placeholder files for your models and controllers:

```bash
touch models/tea_data.py controllers/teas.py
```

- `models/tea_data.py`: This file will define the data structure for your app.
- `controllers/teas.py`: This file will handle requests and manage logic for the app.

With our Project structure in place, next we will build out our models and controllers.
