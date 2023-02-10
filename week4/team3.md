# Server Side App Project

### Niete, Gal, Karol
<style>
.reveal {
    font-size: 24px;
}
</style>

---

## Website intro (N)

I :heart: Food is an app that allows you to add beautiful looking dishes for others to see and rate, with the goal of providing users with inspiration for their next dish.

---

## Teamwork (K)

- Solo coding on issues.
- Pair programming on blockers.

---

## Project Board: (K)

![](https://i.imgur.com/vWQGBJr.png)

---

## Role Reflections

- Scrum ( Karol )
- QA ( Gal )
- Dev Ops ( Niete )
- UX Lead, everyone was supposed to help out with but didn't get round to finishing.

---

## Criteria (G)

- [x] Authentication
- [x] Express Server
- [x] Well-organised modular codebase
- [x] SQLite database
- [x] Hosted on Fly.io
- [ ] File uploads :cry: :weary: 
- [x] Validate user-submitted data on the server (maybe)
- [ ] Handle errors and inform the user
- [ ] Styled appropriately

---

## Learnings (G)

- [ ] Build a stable, professional app
- [x] Handle errors without our server crashing
- [x] Communicate problems to the user
- [x] Research and implement complex new features on our own :hourglass: 

---

## KSBs

---

### Karol

K6: How teams work effectively to produce software and how to contribute appropriately

S14: follow company, team or client approaches to continuous integration, version and source control

B3: Maintains a productive, professional and secure working environment

---

### Gal

B2: Applies logical thinking. For example, uses clear and valid reasoning when making decisions related to undertaking work instructions

S3: link code to data sets

K3: the roles and responsibilities of the project life-cycle within your organisation, and your role

---

### Niete

K6: How teams work effectively to produce software and how to contribute appropriately.

S8: Create simple software designs to effectively communicate understanding of the program

B9: Committed to continued professional development.

---

## SCHEMA (Niete)

```sql
BEGIN;

CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    username TEXT UNIQUE,
    email TEXT UNIQUE,
    hash TEXT,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE IF NOT EXISTS sessions (
    id TEXT PRIMARY KEY,
    user_id INTEGER REFERENCES users(id),
    expires_at DATETIME,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE IF NOT EXISTS foods (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    dish_name TEXT,
    food_desc TEXT,
    user_id INTEGER REFERENCES uses(id),
    rating INTEGER,
    image_path TEXT,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

COMMIT;
```

---

## Challenges

- Couldn't get MULTER and file uploads to work :clock1: 
- Things kept crashing or not working :angry: 
- Having to adjust work style because one team member was sick

---


## Questions?
