<h1>
  <span class="headline">FastAPI MVC CRUD Build</span>
  <span class="subhead">Update Route</span>
</h1>

**Learning objective:** By the end of this lesson, you will be able to **implement** the HTTP PUT method to update existing "tea" resources in a FastAPI project.

## Introduction

The HTTP `PUT` method is commonly used to update existing resources on a server. In this lesson, you'll use `PUT` to update the details of an existing tea in your mock database in the FastAPI app.

## Implement the `PUT` method in FastAPI

Now, let's implement the `PUT` method in our `controllers/teas.py` file to allow us to update existing tea resources.

1. Open the `controllers/teas.py` file.

2. Add the following code to implement the `PUT` method:

```python
# teas.py

@router.put("/teas/{tea_id}")
def update_tea(tea_id: int, tea: dict):

    # Find the tea to update
    for existing_tea in teas_db['teas']:
        if existing_tea['id'] == tea_id:
            existing_tea.update(tea)  # Update the existing tea's data
            return existing_tea

    # If tea was not found, raise an error
    raise HTTPException(status_code=404, detail="Tea not found")
```

### What is happening in this code?

- **`@router.put("/teas/{tea_id}")`**: This decorator creates a new `PUT` route at `/teas/{tea_id}`. The `{tea_id}` part is a URL parameter that identifies the specific tea to update.

- **`tea_id: int`**: This part indicates that the URL parameter `tea_id` should be an integer, representing the ID of the tea to update.

- **`tea: dict`**: This part indicates that the data sent in the `PUT` request must be a dictionary (in JSON format) with the updated values for the tea.

- **`existing_tea.update(tea)`**: This updates the tea’s data with the new values passed in the request.

## Testing the `PUT` method using FastAPI's interactive documentation

FastAPI provides a built-in developer sandbox to test your API endpoints. You can use it to quickly try out your `PUT` method without writing any client-side code.

1. Start your FastAPI server if it's not already running:

```bash
pipenv run uvicorn main:app --reload
```

2. Open your browser and navigate to [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs).

   This is FastAPI’s interactive API documentation. You'll see a list of all available endpoints, including the `PUT /api/teas/{tea_id}` route.

3. Click on **PUT /api/teas/{tea_id}** to expand it.

4. Click the **Try it out** button. You'll see fields where you can input the `tea_id` and the updated data for the tea.

5. In the **`tea_id`** field, enter the ID of the tea you want to update (ex: `1`).

6. In the **Request body** field, paste the following JSON data to update the tea:

```json
{
  "name": "chai latte",
  "in_stock": true,
  "rating": 4.8
}
```

7. Click the **Execute** button. This sends the `PUT` request to update the tea with the specified ID.

   - You should see a response with the `200 OK` status, indicating the tea was successfully updated.

## Verifying the updated tea

1. After executing the `PUT` request, navigate to [http://127.0.0.1:8000/api/teas](http://127.0.0.1:8000/api/teas) in your browser.

   - You should see the updated tea in the list, like this:

```json
{
  "teas": [
    { "id": 1, "name": "chai latte", "in_stock": true, "rating": 4.8 },
    { "id": 2, "name": "lemongrass", "in_stock": true, "rating": 3.8 },
    { "id": 3, "name": "matcha", "in_stock": false, "rating": 4.4 }
  ]
}
```

You’ve successfully implemented the `PUT` method to update an existing tea. Now, let's continue building the CRUD routes for a complete FastAPI app! In the upcoming lessons, we'll focus on implementing the `DELETE` operation to remove teas from the database.
