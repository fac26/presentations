#  :lock: Authentification :lock:

<style>
.reveal {
    font-size: 24px;
}
</style>

---

## Bikes, bikes, bikes! :bike:

A site where users can make an account, log in and out and post comments about bikes.

---

## Post example

```js
function post(request, response) {
    const { username, password } = request.body;
    const user = getUserByUsername(username);
    if (!username || !password || !user) {
        response.status(400).send('<h1>Login Failed</h1>');
    }
    bcrypt.compare(password, user.hash).then((result) => {
        if (!result) {
            return response.status(400).send('<h1>Login Failed</h1>');
        } else {
            const session_id = createSession(user.id);
            response.cookie('sid', session_id, {
                signed: true,
                httpOnly: true,
                maxAge: 1000 * 60 * 60 * 24 * 7,
                sameSite: 'lax',
            });
            response.redirect('/');
        }
    });
}
```

---

# Teamwork

<img src="https://media4.giphy.com/media/3oEjHV0z8S7WM4MwnK/giphy.gif?cid=ecf05e47718mbvd2msia6av3mqwnlrm3rhzye3bxk1q3wfte&rid=giphy.gif&ct=g" />

---

## Criteria

- [x] As a user, I want to: submit information to your site for anyone to see
- [x] As a user, I want to: come back to your site later and see what I posted is still there
- [ ] As a user, I want to: be the only person allowed to delete my stuff
- [x] Forms for users to sign-up and sign-in
- [x] Form to submit data only accessible to logged in users
- [x] Page showing all the data
- [ ] Way for logged in users to delete their own data
- [x] Semantic HTML
- [x] Database
- [x] Hidden env variables
- [ ] Tests for all routes
- [x] User page showing all posts from single user
- [ ] Github action to run tests on push

---

## KSBs Gal

K7
Software design approaches and patterns, to identify reusable solutions to commonly occurring problems

S7
apply structured techniques to problem solving, debug code and understand the structure of programmes in order to identify and resolve issues

---

## Scrum Facilitator :rugby_football: 
- Regular breaks
- Team check ins/outs
- Regular pair switching 

---

## UX Lead

- Created a style guide
- Lead on project documentation by regularly updating the `README.md` file

---

## QA | G 🧪

- set up `/test` folder and files

```js
test("createSession can create and insert a new session", async () => {
  reset();
  const user = createUser("MrTest", "abc");
  const sid = createSession(user.id);
  assert.ok(
    ...
  );
});
```

---

## QA | G 🧹

- monitored code to keep it tidy and legible

---

## QA | G | KSBs 💾

K6: How teams work effectively to produce software and how to contribute appropriately

S7: Apply structured techniques to problem solving, debug code and understand the structure of programmes in order to identify and resolve issues

---

## Schema (Georgia and Gal)

```sql
BEGIN;

CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    username TEXT UNIQUE,
    hash TEXT,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE IF NOT EXISTS sessions (
    id TEXT PRIMARY KEY,
    user_id INTEGER REFERENCES users(id),
    expires_at DATETIME NOT NULL,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE IF NOT EXISTS posts (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    content TEXT,
    user_id INTEGER REFERENCES users(id),
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

COMMIT;
```

---

## Tables and how they're connected

users DB:

| id | username | hash | created_at |
|:--:|:--------:|:----:|:----------:|
| <span style="color:green">1</span>  |          |  | <span style="color: blue">1</span> |
| <span style="color:green">2</span>  |          |  | <span style="color: blue">2</span> |
| <span style="color:green">3</span>  |          |  | <span style="color: blue">3</span> |
| <span style="color:green">4</span>  |          |  | <span style="color: blue">4</span> |
| <span style="color:green">5</span>  |          |  | <span style="color: blue">5</span>
| <span style="color:green">6</span>  |          |  | <span style="color: blue">6</span> |

sessions DB:

| id | user_id | expires_at | created_at |
|:--:|:-------:|:---------- |:---------: |
| 1  | <span style="color: red">1</span> | | <span style="color: blue">1</span> |                          |   |          |
| 2  | <span style="color: red">2</span> | | <span style="color: blue">2</span>          |
| 3  | <span style="color: red">3</span> | | <span style="color: blue">3</span> |  |          | 
| 4  | <span style="color: red">4</span> | | <span style="color: blue">4</span>         |
| 5  | <span style="color: red">5</span> |            | <span style="color: blue">5</span>   |         |
| 6  | <span style="color: red">6</span>       |              | <span style="color: blue">6</span>  |             |   |        |
| 7  | <span style="color: red">7</span> |     | <span style="color: blue">7</span>  |          | 

posts DB:

| id | content | user_id | created_at |
|:--:|:-------:|:-------:|:-----------| 
| 1  |    | <span style="color: red">1</span>  | <span style="color: blue">1</span> |
| 2  |    | <span style="color: red">2</span>  | <span style="color: blue">2</span> |
| 3  |    | <span style="color: red">3</span>  | <span style="color: blue">3</span> |
| 4  |    | <span style="color: red">4</span>  | <span style="color: blue">4</span> |
| 5  |    | <span style="color: red">5</span>  | <span style="color: blue">5</span> | 


sqlite_sequence DB:

| name     | seq        | 
|:--:      |:---------: |                                                                            
| name  |           | 
| seq   |           | 

---


## Kanban Board: 

![](https://i.imgur.com/sGCIqvr.png)

---

# Design

![](https://i.imgur.com/gIVquOm.png)
![](https://i.imgur.com/HYfs9pu.png)

---

## DevOps (Dominic)

- [x] Got deployment to Fly.io and volume

---

## Questions?
