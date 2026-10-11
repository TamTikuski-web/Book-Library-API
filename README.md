
# Book Library API Documentation

Oct 11, 2026 · @Brisibe Wisdom Nemiye

The Book Library API lets you manage a library catalogue over HTTP: create an account, log in, then add, read, update and delete books. Each `##` section below is one page of the Docusaurus site.

## Introduction

The Book Library API is a REST API built with Node.js and Express. It returns JSON and uses token-based authentication.

| Item | Value |
| --- | --- |
| Base URL | `http://localhost:3000/api/v1` |
| Format | JSON (`Content-Type: application/json`) |
| Authentication | Bearer token (JWT) |
| Versioning | In the URL path (`/v1`) |

## Quickstart

You will register, log in, and add your first book in about five minutes.

**Prerequisites:** Node.js 18 or later, npm, and a terminal.

**1. Start the server**

```bash
git clone <your-repo-url>
cd book-library-api
npm install
npm start
```

The API now runs at `http://localhost:3000`.

**2. Register a user**

```bash
curl -X POST http://localhost:3000/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{"name": "Ada", "email": "ada@example.com", "password": "Str0ngPass!"}'
```

Expected response (`201 Created`):

```json
{
  "id": "u_101",
  "name": "Ada",
  "email": "ada@example.com"
}
```

**3. Log in to get a token**

```bash
curl -X POST http://localhost:3000/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email": "ada@example.com", "password": "Str0ngPass!"}'
```

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "expiresIn": 3600
}
```

Copy the `token` value. You need it for every request that follows.

**4. Add a book**

```bash
curl -X POST http://localhost:3000/api/v1/books \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"title": "Things Fall Apart", "author": "Chinua Achebe", "isbn": "9780385474542", "publishedYear": 1958, "genre": "Fiction"}'
```

A `201 Created` response with the new book means everything works. Next, read the Authentication and Endpoints pages.