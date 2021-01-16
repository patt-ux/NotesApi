# NotesApi
## About this App
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
    * Download the Postman app https://www.postman.com/downloads
    * Launch the app and sign up/sign in.
3. Clone or Download this repo from Github
    * To CLONE - you will need GIT
        1. Install GIT (https://git-scm.com/downloads)
        2. Once Git is installed, open a Command Prompt (Windows) or Terminal (MacOS)
            * To open a Command Prompt on Windows, search for "CMD"
            * To open a Terminal on MacOS, search for "Terminal"
        3. In the Command Prompt/Terminal window, navigate to the folder you want to install this repo into
        4. Clone the repo:
        ```
        git clone https://github.com/patt-ux/NotesApi.git
        ```
    * To Download, simply download the ZIP file for this repo and unzip it into the directory where you want it installed.
4. Install node modules:
    * In the Command Prompt/Terminal window, navigate to where the app was cloned/unzipped to
    * Run `npm install`
6. Run the Server:
    * In the Command Prompt/Terminal window, to run the node server, type `node server.js`
    * Windows machines may show a modal to ask for permission for the server to access the network - click 'Allow Access'
    * If all goes well you should see `Listening on port 5000`

## Test the API
### PART 1: Create a Note
1. In the Postman App, open a new tab.
2. The default method is `GET` - change this to `POST`
3. For the request url, enter `localhost:5000/api/notes`
4. Select the Body tab
5. Click the "raw" radio button for type
6. To the far right of all the radio buttons (next to GraphQL) is a dropdown, ensure JSON is selected
7. Enter new note data in the Body text box as follows:
```
{
    "title": "A new note",
    "body": "This is a wonderful note"
}
```
8. Click "Send"
9. You should see the following in the response:
```
{
    "title": "A new note",
    "body": "This is a wonderful note",
    "id": 1
}
```
10. You have successfully added a note. Add a few more notes by following PART 1 again and changing the title and body data.

### PART 2: Getting a specific note
1. Now that we've created a note, let's retrieve it.
    * You can retrieve specific notes by id through the route `/api/notes/{id}`
2. We know the id of the note we created in PART 1 is 1, so we'll look at `/api/notes/1` to get our note.
3. Since this is just a GET request, you can do this through the browser or the Postman app.
    * BROWSER:
        1. In a browser type `http://localhost:5000/api/notes/1`
        2. Depending on the browser, the result should be something like:
        ```
        {"title":"A new note","body":"This is a wonderful note","id":1}
        ```
    * Postman:
        * In the Postman App, open a new tab.
        * Set the method to `GET`
        * For the request url, enter `localhost:5000/api/notes/1`
        * Click "Send"
        * You should see the following in the response:
        ```
        {
            "title": "A fresh new Note",
            "body": "Testing 2 - id 5",
            "id": 1
        }
        ```

### PART 3: Getting all Notes
1. You can retreive all notes in the database through the route `/api/notes`
2. Since this is just a GET request, you can do this through the browser or the Postman app.
    * BROWSER:
        1. In a browser type `http://localhost:5000/api/notes`
        2. Depending on the browser the result should be:
        ```
        [{"title":"A new note","body":"This is a wonderful note","id":1}]
        ```
    * Postman:
        * In the Postman App, open a new tab.
        * Set the method to `GET`
        * For the request url, enter `localhost:5000/api/notes`
        * Click "Send"
        * You should see the following in the response:
        ```
        [{
        "title": "A fresh new Note",
        "body": "Testing 2 - id 5",
        "id": 1
        }]
        ```
3. If you see more entries, that just means you had fun making notes in step 1.

### PART 4: Updating a note
Let's update our note from PART 1:
1. In the Postman App, open a new tab.
2. The default method is `GET` - change this to `PUT`
3. For the request url, enter `localhost:5000/api/notes/1` - we want to update note ID 1
4. Select the Body tab
5. Click the "raw" radio button for type
6. To the far right of all the radio buttons (next to GraphQL) is a dropdown, ensure JSON is selected
7. Enter new note data in the Body text box as follows:
```
{
    "title": "An updated note",
    "body": "This wonderful note is now updated"
}
```
7. Click "Send"
8. You should see the following in the response:
```
{
    "title": "An updated note",
    "body": "This wonderful note is now updated",
    "id": 1
}
```

### PART 5: Deleting a note
We can delete specific notes through the DELETE route `/api/notes/{id}`. Let's delete the note from PART 1.
1. In the Postman App, open a new tab.
2. Set the method to `DELETE`
3. For the url, enter `localhost:5000/api/notes/1` - we want to delete note id 1.
4. Click "Send"
5. You should see `note deleted` in the response

### PART 6: Deleting all notes
You can delete all notes through the DELETE route `/api/notes`.
1. In the Postman App, open a new tab.
2. Set the method to `DELETE`
3. For the url, enter `localhost:5000/api/notes` - we want to delete all notes.
4. Click "Send"
5. You should see `[]` in the response indicating the database is empty

## Stopping the Server
* While developing, you may need to stop the server.
* WINDOWS USERS:
    * In COMMAND PROMPT windows press the CTRL and C keys at the same time.
* MAC USERS:
    * In a Terminal Window press the Apple CMD and C keys at the same time. 
* Press the keys again if necessary to stop all processes on the terminal.
* You may also attempt to close/kill the terminal application to stop the process.

## Conclusion
We've walked through how to set up the server, stop the server and all the available CRUD operations. You can now hook this up to a handsome front end application for some serious note taking. Although I would advise swapping out lowdb for something more robust like MongoDB or an RDBMS like MySQL.