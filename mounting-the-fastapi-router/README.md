<h1>
  <span class="headline">FastAPI MVC CRUD Build</span>
  <span class="subhead">Mounting the FastAPI Router</span>
</h1>

**Learning Objective:** By the end of this lesson, you will be able to mount routers in a FastAPI project to organize and manage API endpoints efficiently, and test your FastAPI app by making API requests.

## Organizing the application with routers

In FastAPI, routers allow us to organize and manage our API endpoints. Instead of having all your endpoints in the `main.py` file, you can split them into separate modules. This helps keep the code clean and maintainable.

### Import the router controller module

We’ve already created the `teas` controller, which defines the `/teas` route for retrieving the tea data. Now, we need to include this router into our main application.

Open the `main.py` file and add the following code:

```python
# main.py

from fastapi import FastAPI
from controllers.teas import router as TeasRouter  # Import the teas router

app = FastAPI()

# Include the teas router with a prefix '/api'
app.include_router(TeasRouter, prefix="/api")

@app.get('/')
def home():
    # Hello world function
    return {'message': 'Hello World!'}
```

In this code, the line `app.include_router(TeasRouter, prefix="/api")` does two important things:

1. **Mounts the `TeasRouter`**: This makes all the routes defined in the `teas` controller available to the application.

2. **Adds a prefix `/api`**: This means that all routes from the `TeasRouter` will now be available at paths like `/api/teas` instead of just `/teas`.

## Testing the API

Now that we’ve organized our code, it’s time to test it!

1. Start the FastAPI server by running the following command in your terminal:

```bash
pipenv run uvicorn main:app --reload
```

2. Open your browser and navigate to [`http://127.0.0.1:8000/api/teas`](http://127.0.0.1:8000/api/teas).

   - This will trigger the `GET /api/teas` route from the `teas` controller.

If everything is set up correctly, you should see the following JSON response with the mock tea data:

```json
{
  "teas": [
    { "id": 1, "name": "chai", "in_stock": true, "rating": 4.2 },
    { "id": 2, "name": "lemongrass", "in_stock": true, "rating": 3.8 },
    { "id": 3, "name": "matcha", "in_stock": false, "rating": 4.4 }
  ]
}
```

## Add more routes

Now that your basic setup is complete, it’s time to expand the functionality by adding more routes to your API.

### Add a route for a single tea

Let’s say we want to retrieve a specific tea by its `id`. To do this, we’ll add a new `GET` route to the `teas` controller.

1. Open `controllers/teas.py` and add the following code:

```python
# teas.py

from fastapi import APIRouter
from models.tea_data import teas_db

router = APIRouter()

@router.get("/teas")
def get_teas():
    # Get all teas
    return teas_db

@router.get("/teas/{tea_id}")
def get_single_tea(tea_id: int):
    # Get tea by ID
    for tea in teas_db['teas']:
        if tea['id'] == tea_id:
            return tea
    # If tea with the given ID is not found
    raise HTTPException(status_code=404, detail="Tea not found")
```

- **`@router.get("/teas/{tea_id}")`**: This is a route to handle `GET` requests for a specific tea by `id`. The `{tea_id}` part in the URL is a **path parameter** that captures the ID of the tea.
- **`get_tea(tea_id: int)`**: This function looks up the tea by its `id` from the `teas_db` mock data. If no tea is found with that ID, it returns a "Tea not found" message.

### Testing the new route

1. Start your FastAPI server again if it’s not running:

```bash
pipenv run uvicorn main:app --reload
```

2. Now, navigate to [`http://127.0.0.1:8000/api/teas/1`](http://127.0.0.1:8000/api/teas/1) in your browser, replacing `1` with the ID of the tea you want to retrieve.

   - You should see the specific tea's data returned in the same JSON format.

```json
{
  "id": 1,
  "name": "chai",
  "in_stock": true,
  "rating": 4.2
}
```

In the next steps, you can continue expanding your FastAPI app by adding more routes to handle creating, updating, and deleting teas!
