<h1>
  <span class="headline">FastAPI MVC CRUD Build</span>
  <span class="subhead">Delete Route</span>
</h1>

**Learning objective:** By the end of this lesson, you will be able to **implement** the HTTP DELETE method to remove existing "tea" resources from a FastAPI project.

## Introduction

The HTTP `DELETE` method is used to remove a resource from the server. In this lesson, you'll use `DELETE` to remove a tea from your mock database in the FastAPI app.

## Implement the `DELETE` method in FastAPI

Now, let's implement the `DELETE` method in our `controllers/teas.py` file to allow us to delete a tea resource.

1. Open the `controllers/teas.py` file.

2. Add the following code to implement the `DELETE` method:

```python
# teas.py

@router.delete("/teas/{tea_id}")
def delete_tea(tea_id: int):
    # Delete a tea by ID
    for tea in teas_db['teas']:
        if tea['id'] == tea_id:
            teas_db['teas'].remove(tea)  # Remove the tea from the database
            return {"message": f"Tea with ID {tea_id} has been deleted."}

    # If tea was not found, raise an error
    raise HTTPException(status_code=404, detail="Tea not found")
```

### What is happening in this code?

- **`@router.delete("/teas/{tea_id}")`**: This decorator creates a new `DELETE` route at `/teas/{tea_id}`. The `{tea_id}` part is a URL parameter that identifies which tea to delete.

- **`tea_id: int`**: This part indicates that the URL parameter `tea_id` should be an integer, representing the ID of the tea to delete.

- **`teas_db['teas'].remove(tea)`**: This line removes the tea from the mock database (`teas_db`) by identifying the tea and calling `remove()` to delete it.

## Testing the `DELETE` method using FastAPI's interactive documentation

FastAPI provides a built-in developer sandbox to test your API endpoints. You can use it to quickly try out your `DELETE` method without writing any client-side code.

1. Start your FastAPI server if it's not already running:

```bash
pipenv run uvicorn main:app --reload
```

2. Open your browser and navigate to [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs).

   This is FastAPI’s interactive API documentation. You'll see a list of all available endpoints, including the `DELETE /api/teas/{tea_id}` route.

3. Click on **DELETE /api/teas/{tea_id}** to expand it.

4. Click the **Try it out** button. You'll see a field where you can input the `tea_id` to specify which tea you want to delete.

5. In the **`tea_id`** field, enter the ID of the tea you want to delete (ex: `1`).

6. Click the **Execute** button. This sends the `DELETE` request to remove the tea with the specified ID.

   - You should see a response confirming the deletion, with a message like this:

```json
{
  "message": "Tea with ID 1 has been deleted."
}
```

## Verifying the deletion

1. After executing the `DELETE` request, navigate to [http://127.0.0.1:8000/api/teas](http://127.0.0.1:8000/api/teas) in your browser.

   - You should see that the tea with the specified `tea_id` is no longer in the list. For example, if you deleted tea with ID `1`, the list should look like this:

```json
{
  "teas": [
    { "id": 2, "name": "lemongrass", "in_stock": true, "rating": 3.8 },
    { "id": 3, "name": "matcha", "in_stock": false, "rating": 4.4 }
  ]
}
```

## What’s Next?

You’ve successfully implemented the `DELETE` method to remove a tea. This completes the basic CRUD operations (Create, Read, Update, Delete) for managing tea resources in FastAPI.

Now that you've learned the full CRUD cycle, you can start using these skills to build more complex applications or improve your existing FastAPI projects.
