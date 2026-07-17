📘 Library Management System API
A RESTful API built with Node.js, Express.js, and Sequelize ORM for managing Authors and Books with a one‑to‑many relationship and cascade deletion.

📂 Project Structure
Code
library-api/
  src/
    models/
      index.js
      author.js
      book.js
    routes/
      authors.js
      books.js
    app.js
  package.json
  package-lock.json
  node_modules/
  .env
  .env.example
  README.md
⚙️ Technologies Used
Node.js

Express.js

Sequelize ORM

MySQL (or Postgres if configured)

dotenv

🔧 Setup Instructions
1. Clone the repository
Code
git clone <your-repo-url>
cd library-api
2. Install dependencies
Code
npm install
3. Create a database
Create a MySQL database (or Postgres if you changed dialect):

Code
CREATE DATABASE library_db;
4. Configure environment variables
Copy .env.example → .env

Code
DB_NAME=library_db
DB_USER=root
DB_PASSWORD=yourpassword
DB_HOST=localhost
DB_DIALECT=mysql
PORT=3000
5. Start the server
Code
npm start
Server runs at:

Code
http://localhost:3000
🗄️ Sequelize Models
Author Model
Field	Type	Rules
id	Integer	PK, auto-increment
name	String	required, max 100
email	String	required, unique, valid email
bio	Text	optional
birthYear	Integer	optional, 1900–2024


Book Model
Field	Type	Rules
id	Integer	PK, auto-increment
title	String	required, max 200
isbn	String	required, unique, exactly 13 chars
publishedYear	Integer	optional
authorId	Integer	FK → Author, cascade delete


Relationship
One Author has many Books

One Book belongs to one Author

Cascade delete enabled → deleting an author deletes all their books

📡 API Endpoints
🔹 Author Endpoints
Method	Endpoint	Description
GET	/api/authors	Get all authors (supports sortBy=name)
GET	/api/authors/:id	Get single author with all their books
POST	/api/authors	Create author (validates email + uniqueness)
PUT	/api/authors/:id	Update author
DELETE	/api/authors/:id	Delete author + cascade delete books
GET	/api/authors/:authorId/books	Get all books for an author
POST	/api/authors/:authorId/books	Create book under an author


🔹 Book Endpoints
Method	Endpoint	Description
GET	/api/books	Get all books (includes author info)
GET	/api/books/:id	Get single book with author details
POST	/api/books	Create book (validates authorId exists)


🔍 Query / Filter Features
Books:
/api/books?year=2020  
Filter books by published year

/api/books?author=Smith  
Search books by author name

Authors:
/api/authors?sortBy=name  
Sort authors alphabetically

🧪 Testing Examples
1. Create an author
Code
POST /api/authors
Body:
{
  "name": "J.K. Rowling",
  "email": "jk@email.com",
  "birthYear": 1965
}
2. Create a book for an author
Code
POST /api/authors/1/books
Body:
{
  "title": "Harry Potter",
  "isbn": "9780439708180",
  "publishedYear": 1997
}
3. Get author with books
Code
GET /api/authors/1
4. Delete author (cascade delete books)
Code
DELETE /api/authors/1
Expected: 204 No Content