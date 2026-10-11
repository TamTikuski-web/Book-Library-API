## Postman collection

Use the collection to try every endpoint without writing code.

1. Download `book-library-api.postman_collection.json` from the repository.
2. In Postman, select **Import** and choose the file.
3. Create an environment with two variables: `baseUrl` set to `http://localhost:3000/api/v1`, and `token` left empty.
4. Run **Auth > Login**. Its test script saves the token for you:

```javascript
pm.environment.set('token', pm.response.json().token);
```

5. Run any request in the **Books** folder. Each one sends `Authorization: Bearer {{token}}` automatically.