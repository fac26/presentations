# Authentication Project 

### Iman, Konstantina, Laura, Natalia, Niete 
<style>
.reveal {
    font-size: 24px;
}
</style>

---

## Website intro

A website named "Corporategirl" where you can read secrets about companies - inspired by gossipgirl, fishbowl and glassdoor. 

---

# Teamwork

- Worked individually on separate pieces of code, but then came together in pairs or groups to go through it and understand the coders motivation behind the code.
- While working separately we would go into groups where we were working in the same file e.g if multiple people were working on routes they would work in a group

---

## Role Reflections

- Scrum ( Niete )
- QA ( Laura )
- Dev Ops ( Natalia  )
- UX Lead ( Konstantina )
- Iman helped out with all roles in some capacity

---

## Criteria

- [x] Forms for users to sign up and log in
- [x] A form for users to submit data only accessible to logged in users
- [x] A page showing all the data
- [ ] A way for logged in users to delete their own data
- [x] Semantic form elements with correctly associated labels
- [x] A SQLite database
- [x] Hidden environment variables (i.e. not on GitHub)

---

## KSBs (Niete)

---

### Knowledge

- K1 - All stages of the software development life-cycle (what each stage contains, including the inputs and outputs)
- K2 - Roles and responsibilities within the software development lifecycle (who is responsible for what)
- K6 - How teams work effectively to produce software and how to contribute appropriately
- K7 - Software design approaches and patterns, to identify reusable solutions to commonly occurring problems
- K10 - Principles and uses of relational and non-relational databases

---

### Skills

- S1 - Create logical and maintainable code
- S3 - Link code to data sets
- S8 - Create simple software designs to effectively communicate understanding of the program
- S10 - Build, manage and deploy code into the relevant environment

---

### Behaviours

- B1 - Works independently and takes responsibility. For example, has a disciplined and responsible approach to risk and stays motivated and committed when facing challenges
- B2 - Applies logical thinking. For example, uses clear and valid reasoning when making decisions related to undertaking work instructions
- B3 - Maintains a productive, professional and secure working environment
- B4 - Works collaboratively with a wide range of people in different roles, internally and externally, with a positive attitude to inclusion & diversity
- B6 - Shows initiative and takes responsibility for solving problems within their own remit, being resourceful when faced with a problem to solve.
- B9 - Committed to continued professional development.

---
## KSBs ( Konstantina)

- K7 - Software design approaches and patterns, to identify reusable solutions to commonly occurring problems
- S3 - Link code to data sets
- S8 - Create simple software designs to effectively communicate understanding of the program
- S10 - Build, manage and deploy code into the relevant environment
- B1 - Works independently and takes responsibility. For example, has a disciplined and responsible approach to risk and stays motivated and committed when facing challenges


## Separation of Concerns

![](https://i.imgur.com/jClujYI.png)

---

## Schema (Konstantina)

```sql
BEGIN;

CREATE TABLE IF NOT EXISTS users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  email TEXT UNIQUE,
  hash TEXT,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE IF NOT EXISTS sessions (
  id TEXT PRIMARY KEY,
  user_id INTEGER REFERENCES users(id),
  expires_at DATETIME NOT NULL,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE IF NOT EXISTS secrets (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  title TEXT,
  content TEXT,
  user_id INTEGER REFERENCES users(id),
  company_id INTEGER REFERENCES companies(id),
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE IF NOT EXISTS companies(
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL
);

COMMIT
```

---

## How sign-up works (Natalia)

```js
function postSignUp(req, res) {
    let { email, password } = req.body;
    if (!email || !password) {
        return res.status(400).send('Bad input');
    }
    bcrypt
        .hash(password, 12)
        .then((hash) => {
            email = sanitize(email);
            const user = createUser(email, hash);
            const session_id = createSession(user.id); //returns session id
            res.cookie('group2-sid', session_id, {
                signed: true,
                maxAge: 1000 * 60 * 60 * 24 * 3, // 3 days
                sameSite: 'lax',
                httpOnly: true,
            });
            res.status(200).redirect('/');
        })
        .catch((err) =>
            console.log('Error from hashing the password, something went wrong with brypt.hash', err)
        );}
```

---

## How the add-secrets works (Iman)

```js
function handleAddSecret(req, res) {
    let { title, companies, secret } = req.body;

    const errors = {};
    if (!title) {
        errors.title = 'please add title';
    }
    if (!companies) {
        errors.companies = 'please add company';
    }
    if (!secret) {
        errors.secret = 'please add secret';
    }
    if (Object.keys(errors).length > 0) {
        console.log(errors);
        const title = 'Add your secret!';
        const content = addSecretsForm(errors); //addSecretsForm.formhtml
        const nav = navBar(req.session);
        const body = html(title, nav, content); //sort this line out
        res.send(body);
    } else {
        
        const companyId = addCompanyToDB(companies); //{id}
        const DBsession = getSession(req.session.id); //{ id: '5ON/HTpizT2wyYzDxt5elJHv', user_id: 7,expires_at: '2023-02-08'}
        //console.log(DBsession, 'add-secret.js, getSession() returns');

        createSecret(
            title,
            secret,
            DBsession.user_id,
            companyId.id
        );
        // console.log(secretCreated);
        res.redirect(`/`);
    }
}

```

---

## Protected Routes (Laura)

```js
server.get('/sign-up', confirmLogin, getSignUp);
server.get('/sign-in', confirmLogin, getSignin);
server.get('/add-secret', confirmLoggedOut, addSecretform); 

function confirmLogin(req, res, next) {
    const isLoggedIn = req.session;
    if (isLoggedIn) {
        return res.redirect('/');
    }
    next();
}

function confirmLoggedOut(req, res, next) {
    const isLoggedIn = req.session;
    if (!isLoggedIn) {
        res.redirect('/');
    }
    next();
}

```

---

## Project Board: 

https://github.com/orgs/fac26/projects/13/views/1

---

## Challenges

---

## Questions?
