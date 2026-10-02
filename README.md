# Assignment 4 : Missing Cat Reporter - The React App
### Prepared for COMP10300 by Dr Nicholas Moore

In this assignment, you will work alone or in pairs to create a React application which communicates with a Node.js server backend to present a minimally functional lost cat reporting application.

## Group Work
For this assignment, you are allowed to work individually or in pairs.  If you choose to work in a group, you will be evaluated on your contribution to the group.  **You must choose a different partner than you had for Assignment 3**.

Your instructor will examine git commit logs and other activity on GitHub to determine your level of involvement in the assignment.  There is an evaluation category where the instructor will deduct marks for unequal participation. There will be deductions both for students who minimally participate, or get a "free ride" up to 100% of the grade for this assignment.

If it is found that a student does all or nearly all of the project without planning for the inclusion of the other student, or "hogging all the work", there will be a suitable deduction for this type of behaviour as well. Somewhere you should document who had what responsibilities. The best way to do this is the built-in issue tracker, and by assigning people to issues.

It is the general expectation that students will use the collaboration tools provided by GitHub in order to complete the assignment.  If it's not in the git log it didn't happen.

Group work is an important skill.  In industry, nearly all work is group work. If you are having extraordinary trouble with this, please email your instructor.

## Artificial Intelligence Usage
For this assignment, use of generative AI for content creation is strictly forbidden. You *may* use AI for bug analysis and error checking.  Use of AI for content generation on this assignment may result in a formal charge of academic integrity violation. Please see Mohawk College's academic integrity policy

The best way to demonstrate that this assignment is your own work is to commit and push your work frequently. If your entire solution is committed in one go, this will be taken as an indicator that an academic integrity violation may have occurred, and your work will be investigated for other signs of violation.

## Special Instructions
As with all assignments in this class, your application is expected to compile and run without compiler errors, and that you have tested your application to ensure it meets the requirements.

This assignment requires you to use the fetch API to communicate with a Node.js server which has been provided in this repository. Because Node.js servers are not the subject of this course (They will be covered extensively in COMP10302), some special instructions are required.

Please note that an understanding of the internal operation of the Node.js server is not necessary to complete this assignment, but you need to know how to turn one on.

### General Setup
This assignment in fact contains two servers, a Vite server running the React process and a Node.js server that provides the web API your React app will need to hook into. In order for your application to work, *both servers will need to be running*.

#### Running the Node.js server
In order to run the Node.js server, navigate to the file `back-end/index.js`, and press the play button in WebStorm.  You should get a message in the terminal window that the server is now running on port 3000.

You are not to make changes to the Node.js server, so you can just leave it running, regardless what you're doing with the front-end. If you're having trouble with this assignment, the back-end folder will generally not be the place to look.

#### Running the Vite server
1. Open any file within the `front-end` folder, such as `index.html`.
2. Open the terminal by clicking the button that looks like this: \[>_\], or using Alt+F12.
3. Type the command `npm run dev`

If done correctly, the terminal output will contain a hyperlink such as "http://localhost:5173/". Clicking this link will load your React application in your default browser.

A nice feature of Vite is that your application will be automatically recompiled any time you save changes to one of the source code files. The changes will also be reflected in the browser, but depending on the nature of the recompilation things sometimes break (particularly if you have a syntax error). Occasionally you'll be given a fresh reload, and sometimes you'll want to trigger one yourself.

## Program Description
The purpose of this web application is to use a simple database to help the owners of lost cats connect to people who may have seen them.

Our web application will have two main features.
1. A "report a cat" feature
    - The user must enter their name, and time and location the lost cat was spotted.
    - The website must present the user with all of the cats currently missing.  The user must select one in order to submit the sighting.
2. A "view cat sightings" feature.
    - The user must be prompted to provide an email address and phone number.  These will be compared against the emails and phone numbers in the database to select the right owner.
        - This is an early (and very bad) version of user authentication, a topic we will explore in more detail in COMP 10302.
    - Once the user has entered valid "login credentials", they will be given a read out of the sighting data for every cat they own in the database.

The following features are obvious, but implementing them is *not a requirement*:
3. The ability to add new owners to the database
4. The ability to add missing cats to the database.

Any group which implements these features, which are, again, not required, may be eligible for bonus points on this assignment, at the discretion of the instructor.

### Data Files
The database for this web application is a series of JSON files, stored in 'back-end/data'. In a "real" version of this web app, these JSON files would certainly be replaced with an SQL server, but a concious decision was made to provide the data in a format that you, the student, could read, assuming no prior SQL knowledge. This section details how these files are laid out.  Managing these files is the job of the Node server (and not your responsibility), but understanding the structure of the data will help you work with it once that data hits the browser.

The three files are:
- `cats.json` - data on the missing cats.
- `owners.json` - data on the owners of the missing cats.
- `sightings.json` - records of times and places people have seen the missing cats.

All three JSON structures are lists of objects.

#### The Cat Object
A cat object has the following properties:
- `cat_id` - A unique identifier for each cat.
- `owner_id` - The ID of the owner of the cat, cross referencing the Owner object list.
- All other fields are the identifying attributes of the cat.

#### The Owner Object
An owner object has the following properties:
- `owner_id` - A unique identifier for each cat. Note that an owner may own any number of cats.
- `email` - Used as a pseudo-user name during the view cat sightings login procedure
- `phone` - Used as a password during the view cat sightings login procedure.
- All other fields are the identifying attributes of the person.

#### The Sighting Object
A Sighting object records the date, time and location that a missing cat was seen, and who it was seen by.
- `cat_id` - The unique identifyer of the cat that was sighted.
- `reported_by` - The name of the person who sighted the cat (distinct from owner names).
- `datetime` - A timestamp string, the time at which the cat was spotted.
- `location` - A string describing where and how the cat was spotted.

### The Node Server's API Specification
The node server provided in this repository provides the following API.
| Method | Endpoint | Description | Example |
|--------|----------|-------------|---------|
| GET    | /api/hello | Returns a Hello World string, for testing purpose only. |  |
| POST | /api/reset | Restores data files to the the state stored in `data_backup` | |
| GET | /api/cats | Returns a JSON containing the contents of `cats.json` | |
| POST | /api/report/:id | Returns all sightings for cats owned by the specified owner (id). | /api/report/3 |
| | | | |
| | | | |

## Requirements

### The Whole Thing Must Be React
You are not permitted to add any HTML files to the project, or any HTML code which is not a React component. All JavaScript must be contained within your JSX files, and using traditional DOM manipulation is strictly forbidden.

You are, however, permitted to use external CSS.

## Evaluation

### Group Work

### Grading Breakdown

