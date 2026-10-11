## Endpoints

All book endpoints require authentication.

| Method | Path | Description |
| --- | --- | --- |
| GET | `/books` | List books |
| GET | `/books/:id` | Get one book |
| POST | `/books` | Create a book |
| PUT | `/books/:id` | Update a book |
| DELETE | `/books/:id` | Delete a book |

### The book object

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `id` | string | Auto | Unique identifier, set by the server |
| `title` | string | Yes | Book title |
| `author` | string | Yes | Author's full name |
| `isbn` | string | Yes | 13-digit ISBN, unique per book |
| `publishedYear` | integer | No | Year of first publication |
| `genre` | string | No | Category, for example `Fiction` |

### List books

`GET /books`

Returns a paginated list of books.

| Query parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `page` | integer | 1 | Page number |
| `limit` | integer | 10 | Items per page (maximum 50) |
| `author` | string | None | Filter by author name |
| `genre` | string | None | Filter by genre |

**curl**

```bash
curl "http://localhost:3000/api/v1/books?genre=Fiction&limit=2" \
  -H "Authorization: Bearer YOUR_TOKEN"
```

**JavaScript**

```javascript
const res = await fetch('http://localhost:3000/api/v1/books?genre=Fiction&limit=2', {
  headers: { Authorization: `Bearer ${token}` },
});
const data = await res.json();
```

**Response (`200 OK`)**

```json
{
  "page": 1,
  "limit": 2,
  "total": 14,
  "data": [
    {
      "id": "b_1",
      "title": "Things Fall Apart",
      "author": "Chinua Achebe",
      "isbn": "9780385474542",
      "publishedYear": 1958,
      "genre": "Fiction"
    }
  ]
}
```

### Get a book

`GET /books/:id`

```bash
curl http://localhost:3000/api/v1/books/b_1 \
  -H "Authorization: Bearer YOUR_TOKEN"
```

```javascript
const res = await fetch('http://localhost:3000/api/v1/books/b_1', {
  headers: { Authorization: `Bearer ${token}` },
});
const book = await res.json();
```

Returns `200 OK` with a single book object, or `404 Not Found` with the code `BOOK_NOT_FOUND`.

### Create a book

`POST /books`

**JavaScript**

```javascript
const res = await fetch('http://localhost:3000/api/v1/books', {
  method: 'POST',
  headers: {
    Authorization: `Bearer ${token}`,
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    title: 'Half of a Yellow Sun',
    author: 'Chimamanda Ngozi Adichie',
    isbn: '9780007200283',
    publishedYear: 2006,
    genre: 'Fiction',
  }),
});
const book = await res.json();
```

**Response (`201 Created`)**

```json
{
  "id": "b_2",
  "title": "Half of a Yellow Sun",
  "author": "Chimamanda Ngozi Adichie",
  "isbn": "9780007200283",
  "publishedYear": 2006,
  "genre": "Fiction"
}
```

The request fails with `400` if a required field is missing and `409` if the ISBN already exists.

### Update a book

`PUT /books/:id`

Send the fields you want to change. Returns `200 OK` with the updated book.

```bash
curl -X PUT http://localhost:3000/api/v1/books/b_2 \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"genre": "Historical Fiction"}'
```

### Delete a book

`DELETE /books/:id`

Returns `204 No Content` with an empty body when the book is deleted.

```bash
curl -X DELETE http://localhost:3000/api/v1/books/b_2 \
  -H "Authorization: Bearer YOUR_TOKEN"
```