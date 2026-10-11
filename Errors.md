## Errors

Every error uses the same JSON shape, so your code can handle all failures in one place.

```json
{
  "error": {
    "code": "BOOK_NOT_FOUND",
    "message": "No book exists with id b_99."
  }
}
```

| Status | Code | What it means | How to fix it |
| --- | --- | --- | --- |
| 400 | `VALIDATION_ERROR` | A required field is missing or has the wrong type | Check the request body against the book object table |
| 401 | `UNAUTHORIZED` | The token is missing or invalid | Add the header `Authorization: Bearer <token>` |
| 401 | `TOKEN_EXPIRED` | The token is older than 1 hour | Log in again to get a new token |
| 403 | `FORBIDDEN` | Your account cannot perform this action | Use an account with the required permission |
| 404 | `BOOK_NOT_FOUND` | No book matches the id | Check the id with `GET /books` |
| 409 | `DUPLICATE_ISBN` | A book with this ISBN already exists | Update the existing book instead of creating a new one |
| 429 | `RATE_LIMITED` | Too many requests in a short time | Wait a few seconds, then retry |
| 500 | `INTERNAL_ERROR` | Something failed on the server | Retry once; if it persists, report it with the time of the request |