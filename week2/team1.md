# Database

<style>
.reveal {
    font-size: 24px;
}
</style>

---

## Website intro

A library app where you can add in your favourite books as recommendations for others.



---

## Code examples

```js
const { readFileSync } = require("node:fs");
const { join } = require("node:path");
const db = require("./database.js");

const seedPath = join("database", "seed.sql");
const seed = readFileSync(seedPath, "utf-8");
db.exec(seed);

console.log("DB seeded with example data");
```

---

# Teamwork

- Worked together as a group
- Later split into pairs to work on individual issues

---

## Role Reflections

- Scrum ( Natalia )
- QA ( Dominic )
- Dev Ops ( Karol )
- UX Lead ( Niete & Iman )

---

## Criteria

- [x] A form for users to submit data
- [x] A page showing all the data
- [x] Semantic form elements with correctly associated labels
- [x] A SQLite database
- [x] A schema describing your database in your README
- [ ] Tests for server routes and database access
- [ ] Not process user input as SQL commands
- [x] Hidden environment variables (i.e. not on GitHub)


---

## KSBs (Niete)

### Knowledge

- K2 - Roles and responsibilities within the software development lifecycle (who is responsible for what)
- K6 - How teams work effectively to produce software and how to contribute appropriately
- K7 - Software design approaches and patterns, to identify reusable solutions to commonly occurring problems
- K10 - Principles and uses of relational and non-relational databases

### Skills

- S1 - Create logical and maintainable code
- S2 - Develop effective user interfaces
- S3 - Link code to data sets
- S8 - Create simple software designs to effectively communicate understanding of the program
- S10 - Build, manage and deploy code into the relevant environment

### Behaviours

- B1 - Works independently and takes responsibility. For example, has a disciplined and responsible approach to risk and stays motivated and committed when facing challenges
- B2 - Applies logical thinking. For example, uses clear and valid reasoning when making decisions related to undertaking work instructions
- B3 - Maintains a productive, professional and secure working environment
- B4 - Works collaboratively with a wide range of people in different roles, internally and externally, with a positive attitude to inclusion & diversity
- B6 - Shows initiative and takes responsibility for solving problems within their own remit, being resourceful when faced with a problem to solve.
- B9 - Committed to continued professional development.


---

## UX Lead

- Created a style guide
- Worked with Iman to create the look of the APP
- Lead on project documentation by regularly updating the `README.md` file

---

## Separation of Concerns

![](https://i.imgur.com/GBgupVC.png)

---

## Schema (Dominic)

```sql
BEGIN;

CREATE TABLE IF NOT EXISTS genres (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL
);

CREATE TABLE IF NOT EXISTS books (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL,
  author_id INTEGER REFERENCES authors(id),
  year INTEGER, 
  genres_id INTEGER REFERENCES genres(id)
);

CREATE TABLE IF NOT EXISTS authors (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL
);

CREATE INDEX IF NOT EXISTS book_names ON books(name);


COMMIT
```


---

## Tables and how they're connected

genres DB:

| id | name             | 
|:--:|:---------:       |                                                                            
| <span style="color:blue">1</span>  | Fantasy          | 
| <span style="color:blue">2</span>  | Horror           |
| <span style="color:blue">3</span>  | Science Fiction  |    
| <span style="color:blue">4</span>  | Drama            |
| <span style="color:blue">5</span>  | Politics         | 

books DB:

| id | name                         | author_id     | year   | genres_id |
|:--:|:---------:                   |:-------------:|:------:|:---------:|
| 1  | The Lord of the Rings        | <span style="color:red">1</span>                         | 1955   | <span style="color: blue">1</span>         |
| 2  | The Hobbit                   | <span style="color: red">1</span>             | 1937   | <span style="color: blue">1</span>         |
| 3  | It                           | <span style="color: red">2</span>             | 1986   | <span style="color: blue">2</span>         | 
| 4  | The Stand                    | <span style="color: red">2</span>             | 1978   | <span style="color: blue">2</span>         |
| 5  | 2001: A Space Oddysey        | <span style="color: red">3</span>           | 1968   | <span style="color: blue">3</span>         |
| 6  | Rendezvous With Rama         | <span style="color: red">3</span>             | 1973   | <span style="color: blue">3</span>         |
| 7  | 1984                         | <span style="color: red">4</span>             | 1948   | <span style="color: blue">4</span>         |
| 8  | Homage to Catalonia          | <span style="color: red">4</span>             | 1938   | <span style="color: blue">5</span>         |           

authors DB:

| id | name             | 
|:--:|:---------:       |                                                                            
| <span style="color: red">1</span>  | J.R.R. Tolkien   | 
| <span style="color: red">2</span>  | Stephen King     |  
| <span style="color: red">3</span>  | Arthur C. Clarke |                            
| <span style="color: red">4</span>  | George Orwell    |                   
| <span style="color: red">5</span>  | Unknown          | 


sqlite_sequence DB:

| name     | seq        | 
|:--:      |:---------: |                                                                            
| authors  | 5          | 
| genres   | 5          |  
| books    | 8          |    

---

## List all books (Niete)

```js
const db = require('../database/database.js')

const select_all_books = db.prepare(/*sql*/ `
    SELECT 
    books.id, 
    books.name,
    books.year,
    genres.name AS genres_name,
    authors.name AS author_name
    FROM books
    JOIN genres ON books.genres_id = genres.id
    JOIN authors ON books.author_id = authors.id
`);
console.log('books')
function listBooks(){
    return select_all_books.all()
}

console.log(listBooks())

module.exports={listBooks}
```

---

## How we added a new book to the database (Iman)

```js
const insert_book = db.prepare(/*sql*/ `
  INSERT INTO books(name, author_id, year, genres_id)
  VALUES(
    $name,
    $author_id,
    $year,
    $genres_id
  )
  RETURNING id
`);

function addBookToDB(book) {
  return insert_book.get(book);
}
```

---

## Handle POST request (Karol)

```js

function handleAddBook(request, response) {
  let { name, author, year, genres_id } = request.body;
    
  if (Object.keys(errors).length > 0) {
  
    const body = htmlTemplate(
      "Add book",
      forms.addbookform(genres.listGenres(), errors),
      "All books",
      "/"
    );
    
    response.send(body);
    
  } else {
    name = sanitize(name);
    author = sanitize(author);
    year = sanitize(year);
    let author_id =  getAuthorId(author)?.id || inserteAuthorToDB({ name: author }).id;

    const new_book = { name, author_id, year, genres_id };

    addBookToDB(new_book);
    response.redirect("/");
  }
}

```

---

## Project Board: https://github.com/orgs/fac26/projects/9

---

# Design

---

![](https://i.imgur.com/sL0zjdy.png)

---

![](https://i.imgur.com/M25216f.png)

---

## Challenges

---

## Questions?
