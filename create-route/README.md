<h1>
  <span class="headline">FastAPI MVC CRUD Build</span>
  <span class="subhead">Create Route</span>
</h1>

**Learning objective:** By the end of this lesson, you will be able to **implement** the HTTP POST method to create new "tea" resources in a FastAPI project.

## Introduction

The HTTP `POST` method is commonly used to send data to a server to create a new resource. In this lesson, you'll use `POST` to add new "tea" items to your mock database in the FastAPI app.

## Implement the `POST` method in FastAPI

Now, let's implement the `POST` method in our `controllers/teas.py` file to allow us to add new tea resources.

1. Open the `controllers/teas.py` file.

2. Add the following code to implement the `POST` method:

```python
# teas.py

@router.post("/teas")
def create_tea(tea: dict):
    # Create a new tea
    teas_db["teas"].append(tea)
    return tea
```

### what is happening on this code?

- **`@router.post("/teas")`**: This decorator creates a new `POST` route at `/teas`. It allows you to send tea data to this endpoint and add it to the `teas_db`.

- **`tea: dict`**: This indicates that the data sent in the `POST` request must be a Python dictionary (in JSON format).

- **`teas_db["teas"].append(tea)`**: This line appends the new tea to the mock database (`teas_db`).

## Using FastAPI's interactive documentation

FastAPI provides a built-in developer sandbox to test your API endpoints. You can use it to quickly try out your `POST` method without writing any client-side code.

1. Start your FastAPI server if it's not already running:

```bash
pipenv run uvicorn main:app --reload
```

2. Open your browser and navigate to [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs).

   This is FastAPI’s interactive API documentation. You'll see a list of all available endpoints, including the `POST /api/teas` route.

3. Click on **POST /api/teas** to expand it.

4. Click the **Try it out** button. You'll see a text box where you can input JSON data to create a new tea.

5. Paste the following JSON data into the **Request body** field:

```json
{
  "id": 4,
  "name": "sumatra",
  "in_stock": true,
  "rating": 5
}
```

6. Click the **Execute** button. This sends the `POST` request to create a new tea.

   - You should see a response with the `200 OK` status, indicating the new tea was successfully added.

## Verifying the new tea

1. After executing the POST request, navigate to [http://127.0.0.1:8000/api/teas](http://127.0.0.1:8000/api/teas) in your browser.

   - You should now see the newly added tea in the list, like this:

```json
{
  "teas": [
    { "id": 1, "name": "chai", "in_stock": true, "rating": 4.2 },
    { "id": 2, "name": "lemongrass", "in_stock": true, "rating": 3.8 },
    { "id": 3, "name": "matcha", "in_stock": false, "rating": 4.4 },
    { "id": 4, "name": "sumatra", "in_stock": true, "rating": 5 }
  ]
}
```

You’ve successfully implemented the `POST` method to create a new tea! Now, let's continue building the CRUD routes for a complete FastAPI app!
