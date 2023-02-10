 Server Side App 

### Iman, Dominic, Laura
<style>
.reveal {
    font-size: 24px;
}
</style>

---

## Film Image Sharing App 	:film_projector:

A website where users can share their favourite movie stills and discover more film stills.

---

## Teamwork 

- Planned the project together in the beginning, then split off to tackle issues.
- Came together in pairs or groups to go through sticking points.

---

## Role Reflections 

- Scrum ( Laura ) 
- QA ( Dominic )
- Dev Ops ( Iman )
- UX Lead ( Group effort )

---

## Criteria

- [x] Express server
- [x] Well-organised modular codebase
- [x] SQLite database
- [ ] Hosted on Fly.io
- [x] One of the spike topics
- [x] Validate user-submitted data on the server
- [x] Handle errors and inform the user
- [x] Styled appropriately

---

## KSBs (Iman)

---

## KSBs (Dominic)

- K1 - All stages of the software development life-cycle (what each stage contains, including the inputs and outputs): Our inputs included taking sign-up information and storing the details, for which they would used as log-in and log-out details
- K3 - The roles and responsibilities of the project life-cycle within your organisation, and your role: As the QA, I ensured that the file structure was consistent from the start. 

---

- K10: Principles and uses of relational and non-relational databases: We used relational databases in SQLite, with primary keys matching to foreign keys. As QA, I set up the schema, and seeded the database. 
- S4 & S6: Test code and analyse results to correct errors found using unit testing / Identify and create test scenarios: I set up a Test folder, linked to a helper file
- B1: Works independently and takes responsibility. For example, has a disciplined and responsible approach to risk and stays motivated and committed when facing challenges: I kept committed to addressing problems in the code like my test failing and how to handle email addresses that already exist


---

## KSBs (Laura)

- K6 - How teams work effectively to produce software and how to contribute appropriately
- S1 - Create logical and maintainable code 
- B1 - Works independently and takes responsibility. For example, has a disciplined and responsible approach to risk and stays motivated and committed when facing challenges

---

## Separation of Concerns

![](https://i.imgur.com/iSekU64.png)

---

## Schema 

- Films DB:

| id | name                                         | year          | director        | genre_id  |
|:--:|:----------------------------------------:    |:-------------:|:---------------:|:---------:|                                                                     
| 1  | Star Wars                                    | 1977          | George Lucas    | 1         |
| 2  | Jaws                                         | 1973          | Steven Spielberg| 2         |
| 3  | Schindler's List                             | 1993          | Steven Spielberg| 3         |                             
| 4  | The Lord of the Rings: The Return of the King| 2003          | Peter Jackson   | 4         |                   
| 5  | JFK                                          | 1991          | Oliver Stone    | 5         |

---

- Genres DB

| id | name                                         | 
|:--:|:----------------------------------------:    |                                                                    
| 1  | Science Fiction                              |
| 2  | Horror                                       |
| 3  | Drama                                        |
| 4  | Fantasy                                      |
| 5  | Politics                                     |

---

- Users DB

| id | email                                       | hash          | created_at          | 
|:--:|:----------------------------------------:   |:-------------:|:--------------: |                                                                     
| 1  | a@example.com                               | ....          | date            |
| 2  | a@example.com                               | ....          | date            |

---

- Sessions DB

| id | user_id                                       | expires_at          | created_at          | 
|:--:|:----------------------------------------:   |:-------------:|:--------------: |                                                                     
| 1  | 1                               | date            | date
| 2  | 2                               | date          | date          |

---

## Code run through

In server.js: 
```js
const multer = require("multer");
const upload = multer({ dest: "public/uploads" });

server.post("/add-film", bodyParser, upload.single("image"), postAddFilmForm);
```

Allowing image uploads in the form:

```js
  <form method="POST" action="/add-film" enctype="multipart/form-data"> // need to declare enctype
  <div>
  <label for="image">Upload image</label>
  <input name="image" id="image" type="file">  //name to match upload.single("image") and type="file"
</div>
  <button class="Button" type="Submit">Add &plus;</button>
  </form>
  `;
    return formhtml;
}
```

---

## Code run through

```js
function filmCardTemplate(film, session = {}) {
    const filmTemplate = /*html*/ `
        <li class="film">
        <h4>${film.name}</h4>
        <p>${film.year}</p>   
        <p>${film.director}</p> 
    `;
    if (!checkCurrentUser(film, session)) {
        return /*html*/ `
      ${filmTemplate}
  </li>
      `;
    } else {
        return /*html*/ `
    ${filmTemplate}
    ${deleteButton(film)}`;
    }
```

---

## Project Board: 

https://github.com/orgs/fac26/projects/15


---

## Challenges

---

## Questions?
