# task3
/book-api
├── index.js
├── package.json
└── README.md
const express = require('express');
const app = express();
const PORT = 3000;

app.use(express.json());

let books = [
  { id: 1, title: 'The Great Gatsby', author: 'F. Scott Fitzgerald' },
  { id: 2, title: '1984', author: 'George Orwell' },
];

// Get all books
app.get('/books', (req, res) => {
  res.json(books);
});

// Add a new book
app.post('/books', (req, res) => {
  const { title, author } = req.body;
  const newBook = {
    id: books.length + 1,
    title,
    author
  };
  books.push(newBook);
  res.status(201).json(newBook);
});

// Update a book by ID
app.put('/books/:id', (req, res) => {
  const bookId = parseInt(req.params.id);
  const { title, author } = req.body;
  const book = books.find(b => b.id === bookId);

  if (!book) return res.status(404).json({ message: 'Book not found' });

  book.title = title || book.title;
  book.author = author || book.author;

  res.json(book);
});

// Delete a book by ID
app.delete('/books/:id', (req, res) => {
  const bookId = parseInt(req.params.id);
  const index = books.findIndex(b => b.id === bookId);

  if (index === -1) return res.status(404).json({ message: 'Book not found' });

  books.splice(index, 1);
  res.status(204).send();
});

app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
npm init -y
npm install express
{
  "name": "book-api",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "express": "^4.18.0"
  }
}
# 📚 Book API – Node.js + Express

A simple REST API to manage a list of books. Supports CRUD operations using Express with data stored in-memory (no database).

---

## 🚀 Features

- GET `/books` – Retrieve all books
- POST `/books` – Add a new book
- PUT `/books/:id` – Update a book by ID
- DELETE `/books/:id` – Delete a book by ID

---

## 🛠️ Tools Used

- [Node.js](https://nodejs.org)
- [Express](https://expressjs.com)
- [Postman](https://www.postman.com/) – for API testing

---

## 📂 Setup Instructions

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/book-api.git
cd book-api
npm install
npm start
{
  "title": "Clean Code",
  "author": "Robert C. Martin"
}
[
  {
    "id": 1,
    "title": "The Great Gatsby",
    "author": "F. Scott Fitzgerald"
  },
  {
    "id": 2,
    "title": "1984",
    "author": "George Orwell"
  }
]
`bash
git init
git add .
git commit -m "Initial commit - Book API with Express"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/book-api.git
git push -u origin main
