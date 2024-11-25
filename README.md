Here's the `README.md` file based directly on your provided PHP code:

```markdown
# Library Management System API

This is a PHP-based API for managing a library system, including users, books, authors, and their relationships. It uses the Slim framework and Firebase JWT for authentication.

---

## Prerequisites
- PHP 7.x or higher
- Composer for dependency management
- Slim Framework
- Firebase JWT Library
- MySQL database

---

## Authentication

### JWT Authentication
The API uses JSON Web Tokens (JWT) for authentication. All secured endpoints require a valid JWT in the `Authorization` header.

Example:
```
Authorization: Bearer <token>
```

---

## Endpoints and Payloads

### User Endpoints

#### Register a User
- **Endpoint**: `POST /user/register`
- **Payload**:
  ```json
  {
    "username": "string",
    "password": "string"
  }
  ```
- **Response**:
  - `200`: User registered successfully.
  - `400`: Invalid input.

#### Login a User
- **Endpoint**: `POST /user/login`
- **Payload**:
  ```json
  {
    "username": "string",
    "password": "string"
  }
  ```
- **Response**:
  - `200`: JWT token returned on successful authentication.
  - `401`: Invalid credentials.

#### Display All Users
- **Endpoint**: `GET /user/display`
- **Headers**:
  ```
  Authorization: Bearer <token>
  ```
- **Response**:
  - `200`: Returns all users and a new token.
  - `401`: Unauthorized or invalid token.

#### Update a User
- **Endpoint**: `PUT /user/update`
- **Headers**:
  ```
  Authorization: Bearer <token>
  ```
- **Payload**:
  ```json
  {
    "username": "string",
    "password": "string"
  }
  ```
- **Response**:
  - `200`: User updated and a new token returned.
  - `401`: Unauthorized.

#### Delete a User
- **Endpoint**: `DELETE /user/delete`
- **Headers**:
  ```
  Authorization: Bearer <token>
  ```
- **Response**:
  - `200`: User deleted and a new token returned.
  - `401`: Unauthorized.

---

### Book Endpoints

#### Register a Book
- **Endpoint**: `POST /book/register`
- **Headers**:
  ```
  Authorization: Bearer <token>
  ```
- **Payload**:
  ```json
  {
    "title": "string",
    "authorids": ["int"]
  }
  ```
- **Response**:
  - `200`: Book registered successfully.
  - `400`: Invalid input or missing `authorids`.

#### Display All Books
- **Endpoint**: `GET /books/displaybooks`
- **Headers**:
  ```
  Authorization: Bearer <token>
  ```
- **Response**:
  - `200`: Returns all books.
  - `401`: Unauthorized.

#### Update a Book
- **Endpoint**: `PUT /book/update`
- **Headers**:
  ```
  Authorization: Bearer <token>
  ```
- **Payload**:
  ```json
  {
    "bookid": "int",
    "title": "string",
    "authorid": "int"
  }
  ```
- **Response**:
  - `200`: Book updated successfully.
  - `400`: Invalid input or missing fields.

#### Delete a Book
- **Endpoint**: `DELETE /book/delete`
- **Headers**:
  ```
  Authorization: Bearer <token>
  ```
- **Payload**:
  ```json
  {
    "bookid": "int"
  }
  ```
- **Response**:
  - `200`: Book deleted successfully.
  - `400`: Missing `bookid`.

---

### Author Endpoints

#### Register an Author
- **Endpoint**: `POST /author/register`
- **Headers**:
  ```
  Authorization: Bearer <token>
  ```
- **Payload**:
  ```json
  {
    "name": "string"
  }
  ```
- **Response**:
  - `200`: Author registered successfully.
  - `400`: Invalid input.

#### Display All Authors
- **Endpoint**: `GET /authors/display`
- **Headers**:
  ```
  Authorization: Bearer <token>
  ```
- **Response**:
  - `200`: Returns all authors.
  - `401`: Unauthorized.

#### Update an Author
- **Endpoint**: `PUT /author/update`
- **Headers**:
  ```
  Authorization: Bearer <token>
  ```
- **Payload**:
  ```json
  {
    "authorid": "int",
    "name": "string"
  }
  ```
- **Response**:
  - `200`: Author updated successfully.
  - `400`: Invalid input.

#### Delete an Author
- **Endpoint**: `DELETE /author/delete`
- **Headers**:
  ```
  Authorization: Bearer <token>
  ```
- **Payload**:
  ```json
  {
    "authorid": "int"
  }
  ```
- **Response**:
  - `200`: Author deleted successfully.
  - `400`: Missing `authorid`.

---

### Book-Author Relationship Endpoints

#### Create a Relationship
- **Endpoint**: `POST /book-authors/connect`
- **Headers**:
  ```
  Authorization: Bearer <token>
  ```
- **Payload**:
  ```json
  {
    "bookid": "int",
    "authorid": "int"
  }
  ```
- **Response**:
  - `200`: Relationship created successfully.
  - `400`: Invalid input or missing fields.

#### Display Relationships
- **Endpoint**: `GET /book-authors/display`
- **Headers**:
  ```
  Authorization: Bearer <token>
  ```
- **Response**:
  - `200`: Returns all relationships.
  - `401`: Unauthorized.

#### Update a Relationship
- **Endpoint**: `PUT /book-authors/update`
- **Headers**:
  ```
  Authorization: Bearer <token>
  ```
- **Payload**:
  ```json
  {
    "collectionid": "int",
    "bookid": "int",
    "authorid": "int"
  }
  ```
- **Response**:
  - `200`: Relationship updated successfully.
  - `400`: Invalid input or missing fields.

#### Delete a Relationship
- **Endpoint**: `DELETE /book-authors/delete`
- **Headers**:
  ```
  Authorization: Bearer <token>
  ```
- **Payload**:
  ```json
  {
    "collectionid": "int"
  }
  ```
- **Response**:
  - `200`: Relationship deleted successfully.
  - `400`: Missing `collectionid`.

---

## Database Schema

### Users Table
| Column    | Type   |
|-----------|--------|
| userid    | INT    |
| username  | STRING |
| password  | STRING |

### Books Table
| Column  | Type   |
|---------|--------|
| bookid  | INT    |
| title   | STRING |

### Authors Table
| Column    | Type   |
|-----------|--------|
| authorid  | INT    |
| name      | STRING |

### Book-Authors Table
| Column       | Type   |
|--------------|--------|
| collectionid | INT    |
| bookid       | INT    |
| authorid     | INT    |

---

## Security Notes
- Replace the `hack_me` secret key with a secure key in production.
- Use HTTPS to secure token transmissions.
