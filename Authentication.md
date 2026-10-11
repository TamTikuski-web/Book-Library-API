## Authentication

The API uses JSON Web Tokens (JWT). Log in once, then send the token in the `Authorization` header of every protected request.

```text
Authorization: Bearer <token>
```

| Endpoint | Method | Auth required | Purpose |
| --- | --- | --- | --- |
| `/auth/register` | POST | No | Create an account |
| `/auth/login` | POST | No | Exchange credentials for a token |

Tokens expire after 3600 seconds (1 hour). When a token expires, the API returns `401` with the code `TOKEN_EXPIRED`. Log in again to get a new one.

**Using the token in JavaScript**

```javascript
const login = await fetch('http://localhost:3000/api/v1/auth/login', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ email: 'ada@example.com', password: 'Str0ngPass!' }),
});
const { token } = await login.json();

const books = await fetch('http://localhost:3000/api/v1/books', {
  headers: { Authorization: `Bearer ${token}` },
});
console.log(await books.json());
```

Keep tokens secret. Never commit them to Git or expose them in client-side code.
