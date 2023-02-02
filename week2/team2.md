# FAC26 | Week 2 | Database Project

## Film Database | Team 2

You can view the project [here](https://week2-database-ggkl.fly.dev/).

### Contributors:

[Gal](https://github.com/GalKJ), [Georgia](https://github.com/rockyrelay), [Konstantina](https://github.com/konstantinakatmada), [Laura](https://github.com/LauraK0) 

---

## About

We created a community film database, allowing users to input a film via name, year, director, and a selection of genres. An id is created for each entry.

The database has the following structure:



| id  | name | year | director         | genre_id |
| --- | ---- | ---- | ---------------- | -------- |
| 1   |Jaws  |1975  |Steven Spielberg  |  1       |
| 2   | Star Wars     |  1977    |George Lucas | 2 |
| 3   | The Empire Strikes Back | 1980 | Ivan Kershner | 2       |




---

## Setup

Make sure you have Git and Node (v18) installed.

1. Clone this repo and cd into the directory
1. Run `npm install` to install all the dependencies
1. Run `npm run dev` to start the server.

### Repo Structure

![](https://i.imgur.com/qeC4z5X.png)


---



## Testing

To run tests, ensure setup steps are followed and run `npm run test` << ENSURE CORRECT

---

## User Stories

### Core
 
* As a user, I want to: submit information to your site for anyone to see
* As a user, I want to: come back to your site later and see what I posted is still there

### Project-specific

* I want to submit a film to the database
* I want to find films within the database
* I want to explore films in the database

### Acceptance Criteria

- [ ] A form for users to submit data
- [x] A page showing all the data
- [ ] Semantic form elements with correctly associated labels
- [x] A SQLite database
- [ ] A schema describing your database in your README
- [ ] Tests for server routes and database access
- [ ] Not process user input as SQL commands
- [ ] Hidden environment variables (i.e. not on GitHub)

### Stretch criteria 

- [ ] A way to view filtered/sorted data, instead of just all of it
- [ ] GitHub Actions CI setup to run your tests when you push
