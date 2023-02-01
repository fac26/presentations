# Week 1 Server Project - Dirty Little Secret 
---

![](https://i.imgur.com/dfnc8tu.png)

---

## WHAT, WHY and HOW?

For this project we were tasked with using our learnings from the server workshop to create a simple app that allowed users to post inputs and read inputs. 

Keeping this in mind we decided to create an app that allowed users to share their secrets while remaining anonymous using the POST request on a server. Users would also be be able to read any posted secrets using a GET route request.

---
## Team roles

We split the roles between us, practicing Pair Programming in two teams of two, the members of which swapped on Day 2.
At our Sprint Planning you can see the tickets of the tasks completed each day from each team. Each member also had another role (QA, DevOps,UX lead,Scum facilitating) which will be explained in further detail below.

---

## QA // Niete

- I was responsible for writing tests to ensure functions, database queries and routes worked as intended.
- I also helped Dom by creating a mock-up design of what the app could look like.

___

## DevOps // Georgia

My responsibilities included: 

 - setting up our team repo on GitHub and organising the file structure
     > https://github.com/fac26/week1-server-dominic-georgia-konstantina-niete

    > ![](https://i.imgur.com/SLifoVo.png)     
    > Files separated into appropriate folders

 - deploying the server to fly.io and take ongoing responsibility for versions deployed
  > ![](https://i.imgur.com/rDCJdRr.png)
    > currently on. v4
 - make sure separation of concerns is considered throughout the structure and set up environment variables for local and remote databases
  > We took on the issues created via our peers' code reviews and implemented a better separation of concerns by adding a `template.js` file to move our interpolated html away from `/GET`

>`const express = require("express");
const { html } = require("./template.js");
const server = express();`
    
 - A few issues with the server and git merge 


---


## UX // Dominic

We created some initial mock-ups on Photoshop first, and quickly came up with the concept of a black background and an input in the middle, with accompanying text inviting the user to submit their secrets anonymously. The secrets would then be displayed underneath the text field and submit button. We also sourced a transparent PNG logo from The Noun Project website,  as well as a rubbish icon for deleting posts (due to time contraints, we didn't implement the latter in the end).

For the CSS, we created media queries so that the site scales responsively. We also took into account mentor Maria Paz's suggesion to abandon px measurements and use rems instead as a unit of measure, as these scale better when taking into account responsiveness.


![](https://i.imgur.com/5ij9VPQ.jpg)

![](https://i.imgur.com/xjyahzU.jpg)


---



## SF // Konstantina

As a Scrum facilitator, I kicked off day 1 by creating our Kanban board at our Github repo Projects, where I tracked the progress of our work. I was also responsible for our Github Issues, which helped us a lot in our planning and user stories. Leading standups and clearing the blockers we encountered where also two responsibilies of mine, in which I can not say I succeeded.
One Scrum task that I am very proud of is our Sprint planning slides, where you can see tickets of the work we completed each day (daily rundown was one of the SCRUM tasks).

---



## Live Project DEMO

Deployed on fly.io: [Dirty Little Secret](https://https://w1-server-dgkn.fly.dev/)

---

# The Code

---

## What we're proud of

The fact that we managed to get a server app working 

--- 

## Things we learnt

### This week we focused on learning servers via Node and Express. 

- [ ] Create a web server that responds to http requests
- [ ] Conditionally set ports for our server based on the runtime environment
- [ ] Read secrets from a .env file
- [ ] Prevent sensitive data from being pushed to GitHub
- [ ] Route requests to the correct handler function(s)
- [ ] Serve different types of files to the client
- [ ] Read information sent in a URL query string
- [ ] Request bodies 
- [ ] Handle data received from a POST request
- [ ] Handle streams of data sent from the client that don’t arrive all at once
- [ ] Give descriptive names to HTML form input fields so that it is easy to access data in the request
- [ ] Parse data sent via a default HTML form submission
---
### Core modules 

#### Use core Node modules
- [ ] read files synchronously and asynchronously using Node’s fs module
Design 

#### Design a website that is easy to use and to navigate
- [ ] Identify common design patterns that aid usability
- [ ] Build website navigation that demonstrates good usability
- [ ] Make HTML elements look different on hover and focus to indicate their state to the user
Testing 

#### Test our code with a third party library
- [ ] Install libraries from npm as dev dependencies
- [ ] Create package.json scripts that run our tests
---
## Things we can do better next time.

- We understand the importance of Separation of Concerns now, and are going to be better at it onwards.
- We can have a sanitize and validate function, as we have understood the importance of including it. The lack of a latter function ensures that the user can click the 'Tell Me' submit button and prevent an empty string from being posted.
- We can have a delete function that allows the user to remove their posts.
- We can refactor the code so that new posts appear at the top of the UL instead of the bottom.
- We also understand the importance of files such at .gitignore and the dependecies within package.json 
