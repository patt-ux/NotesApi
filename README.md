# NotesAppApi
* A no-frills, node based api for managing notes.
* Built with Node, Express, LowDB to handle persisting and CRUD operations.
    * Each note has the properties id (integer), title (string), body (string):
        * `{"id":0, "title":"A Title", "body": "A Body"}`
        * Note id field is incremented based on last note in DB. This is to prevent duplicates. Ids for notes start at 1.
        * title requires at least 3 characters for note creation or update
        * body can be blank - sometimes you just need a placeholder note
    * GET `/api/notes` returns all notes
    * GET `/api/notes/{id}` returns a specific note
    * POST `/api/notes` creates a new note
    * PUT `/api/notes/{id}` updates a specific note
    * DELETE `/api/notes` deletes all notes
    * DELETE `/api/notes/{id}` deletes a specific note


## Getting Started
1. You will Need to have Node installed.
    * You can download node from https://nodejs.org/en/ - this app is built on version 14.15.4
2. To test the API, you will need an application capable of making POST, PUT and DELETE requests. If you already have something, use that. We will be using Postman to test the API in the following "Test the API" section.
    * Sign up for PostMan at https://www.postman.com/
    * Download the Postman app and sign in.
3. Clone or Download this repo from Github
4. Install node modules:
    * In a terminal or command prompt window, navigate to the root of this repo (e.g. C:/NotesApi)
    * Run `npm install`
6. Run the Server:
    * In the terminal or command prompt window (see step 2), run the node server `node server.js`
    * If all goes well you should see `Listening on port 5000`


## Test the API
1. Create a Note
    * In the Postman App, open a new tab.
    * Set the method to `POST`
    * For the url, enter `localhost:5000/api/notes`
    * Select the Body tab
    * Click the "raw" radio button for type
    * Ensure JSON is selected as the content type in the dropdown
    * Enter new note data in the Body text box as follows:
    `{
        "title": "A new note",
        "body": "This is a wonderful note"
    }`
    * Click "Send"
    * You should see the following in the response:
    `{
    "title": "A fresh new Note",
    "body": "Testing 2 - id 5",
    "id": 1
    }`
    * Add a few more notes by changing the title and body data.
2. Getting a specific note
    * Now that we've created a note, let's retrieve it. You can retrieve specific notes by id through the route `/api/notes/{id}`
    * We know the id of the note we created in step 1 is 1, so we'll look at `/api/notes/1` to get our note.
    * Since this is just a GET request, you can do this through the browser or the Postman app.
    * BROWSER:
        * In a browser type `http://localhost:5000/api/notes/1`
        * Depending on the browser, the result should be:
        `{"title":"A fresh new Note","body":"Testing 2 - id 5","id":1}`
    * Postman:
        * In the Postman App, open a new tab.
        * Set the method to `GET`
        * For the url, enter `localhost:5000/api/notes/1`
        * Click "Send"
        * You should see the following in the response:
        `{
        "title": "A fresh new Note",
        "body": "Testing 2 - id 5",
        "id": 1
        }`
3. Getting all Notes
    * You can retreive all notes in the database through the route `/api/notes`
    * Since this is just a GET request, you can do this through the browser or the Postman app.
    * BROWSER:
        * In a browser type `http://localhost:5000/api/notes`
        * Depending on the browser the result should be:
        `[{"title":"A fresh new Note","body":"Testing 2 - id 5","id":1}]`
        * If you see more entries, that just means you had fun making notes in step 1.
    * Postman:
        * In the Postman App, open a new tab.
        * Set the method to `GET`
        * For the url, enter `localhost:5000/api/notes`
        * Click "Send"
        * You should see the following in the response:
        `[{
        "title": "A fresh new Note",
        "body": "Testing 2 - id 5",
        "id": 1
        }]`
        * If you see more entries, that just means you had fun making notes in step 1.
4. Updating a note
    * Let's update our note from step 1:
        * In the Postman App, open a new tab.
        * Set the method to `PUT`
        * For the url, enter `localhost:5000/api/notes/1` - we want to update note id 1.
        * Select the Body tab 
        * Click the "raw" radio button for type
        * Ensure JSON is selected as the content type in the dropdown
        * Enter new note data in the Body text box as follows:
        `{
            "title": "An updated note",
            "body": "This wonderful note is now updated"
        }`
        * Click "Send"
        * You should see the following in the response:
        `{
        "title": "An updated note",
        "body": "This wonderful note is now updated",
        "id": 1
        }`
5. Deleting a note
    * We've decided to delete our note. We can do so through the DELETE route `/api/notes/{id}`
    * In the Postman App, open a new tab.
        * Set the method to `DELETE`
        * For the url, enter `localhost:5000/api/notes/1` - we want to delete note id 1.
        * Click "Send"
        * You should see `note deleted` in the response
6. Deleting all notes
    * You may find it necessary to wipe out the database and start clean. You can do so through the DELETE route `/api/notes`
    * In the Postman App, open a new tab.
        * Set the method to `DELETE`
        * For the url, enter `localhost:5000/api/notes` - we want to delete all notes.
        * Click "Send"
        * You should see `[]` the newly cleaned database, in the response

## Stopping the Server
* In both the server app terminal press the CTRL and C keys at the same time (or CMD and C for Mac). Press again if necessary to stop all processes on the terminal. You may also attempt to close/kill the terminal application to stop the process.