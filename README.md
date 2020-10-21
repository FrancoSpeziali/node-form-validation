# Node.js Backend Form Validation

In this assignment you will be expected to write a backend system which validates the data which you receive from the client.

This folder includes backend and frontend files.

## Getting started

Please run `npm install` before starting

## Running

`package.json` scripts have been prepared for you

To run the backend:
```shell script
npm run nodemon
```

To run the frontend:
```shell script
npm run live-server
```

> 🤯 IMPORTANT! You must run both of these commands in separate terminals

## What you will be doing

This project will teach you:

- Server side data validation
- FormData API

This project assumes you've already had experience with:

- JavaScript
- Frontend
- Fetch API
- Tools for testing APIs, such as Postman or Insomnia

## Assignments

For the backend part of this assignment, you are expected to write your code in the file `server.js`

For the frontend part of this assignment, you can write your code in the file `index.html`. Here you must use vanilla JavaScript. If you wish you can use React, but you will need to set up your own project.

## Assignment 1 - Prepare your frontend

Examine the JavaScript inside the `index.html` file. It is not complete.

We will use the FormData API to access the values inside the form.

We will then send those values as part of a POST request (this code has already been prepared for you).

> Note: For the next steps - if you prefer, you can create a new project and complete this assignment with React

Research:
[FormData API (en)](https://developer.mozilla.org/en-US/docs/Web/API/FormData)

[FormData API (de)](https://developer.mozilla.org/de/docs/Web/API/FormData)

1. Run the `preventDefault()` function on the submit `event` object to prevent the default behaviour.

2. Create a new variable `formData`

3. Assign to this variable the `new FormData()` constructor, passing into the constructor the `target` property of the `event` object.

4. Inside the `formFields` object, create the property `username`, and assign to this the username value from the form using the following code `formData.get('userName')` 

5. Do the same for the rest of the form fields.

## Assignment 2 - Prepare your backend (server)

1. Run the following command in the root folder:

    ```shell script
    npm install express
    ```

2. Import them into `server.js` using `require`

    > Hint: We are not using ES6 imports here, we are using the CommonJS `require` function

3. Create your `app` variable by running `express()`

4. At the end of your file, add the following code:

    ```javascript
    app.listen(3001);
    ```

## Assignment 3 - Installing express-validator

```shell script
npm install express-validator
```

We will import it later

## Assignment 4 - Setting up your POST route

1. Use `app.post()` to create a route to the path `/registerUser`

2. Add a callback inside your `app.post()` route which accepts the `request` and `response` arguments.

3. Use `console.log()` on the `request.body` property

4. Run your server using the `npm run nodemon` command and make a POST request to your API with an API testing tool such as POSTMAN / Insomnia. Watch the `console` for the output.

    > Hint: You will need to send some JSON in the request body to see a result

What is the result?

## Assignment 5 - Setting up our middleware - express.json()

You may have noticed that when you tried testing your API, your `console.log()` command output an empty object `{}` even if you posted some valid JSON. Why is this?

We need to use some middleware to make the `body` property accessible to us. Luckily for us, express.js comes with some built-in middleware to take care of this for us.

1. Add the following line of code to `server.js`. It should be called before any routes. 

    ```javascript
    app.use(express.json());
    ```

## Assignment 6 - Connect your frontend to your backend

1. Use `fetch` (or another library such as axios) to make a request to the backend server from the frontend.

2. Use the URL `http://localhost:3001/registerUser`

3. Make this a POST request

4. Use the following values in the `headers`

    ```text
       'Content-Type': 'application/json'
    ```
   
5. Send your data as part of the `BODY`

## Assignment 7 - Setting up our middleware - cors()

You may have noticed that when you tried testing your API, from the website, you got a CORS error. Why is this?

Right now, our server is preventing any CORS requests by default. We must allow CORS requests. The simplest way to do this is to use the CORS middleware.

1. Install the following package

    ```shell script
    npm install cors
    ```

2. Add the following line of code to `server.js`. It should be called before any routes. 

    ```javascript
    app.use(cors());
    ```

## Assignment 8 - Setting up our middleware - express-validator - Part 1

express-validator is not part of express.js. We must install it before we can use it.

1. Install the following package

    ```shell script
    npm install express-validator
    ```

Now we've installed the express-validator package, we can begin to use it.

2. Import the **named** body object from 'express-validator';

    > Hint: We are not using ES6 imports here, we are using the CommonJS `require` function

## Assignment 9 - Setting up our middleware - express-validator - Part 2

The JSON object which comes from the client when they make a POST request, is available to us via the `body` object.

We will add validators for the `body` object, because we want to validate these `body` properties which comes from the client.

We need to reference the same properties which we send with our POST request.

We should be sending the following properties with the POST request from our client:

```
username
password
firstName
lastName
dateOfBirth
email
telephone
gender
```

Before we start, we should modify our `app.post()` function call to accept the middleware we will use from express-validator.

Currently we are passing in 2 values into the `app.post()` function:

    1. The route '/registerUser'
    2. The callback
    
We must add another value for the middleware. This will be in between the route and the callback. Since we will use multiple calls to the middleware, this extra value will be an array.

1. Add an array `[]` to the values we pass into the `app.post()` function call.

    Your code should look something like this:
    ```
    app.post('/registerUser', [], (reqest, response) => {
    ```
   
## Assignment 10 - Add our first validator

Let's create our first middleware. We want to check that the `username` property which comes from the `body` is alphanumeric (contains only letters and numbers).

1. Inside the middleware array `[]`, create a function call for `body('username').isAlphanumeric(),`

## Assignment 11 - Understanding the express-validator middleware

Let's take a moment to break apart the middleware we just used.

1. We called the `body()` function

2. We pass into this function the property we want to validate `username`

3. We run a method onto this function call `isAlphanumeric()`

## Assignment 12 - More validators

Now we understand how express-validator middleware works, we can add more validation calls.

We will add more function calls into this array to perform more validation.

Following the example from the previous assignment:

1. Add the `isLength({ min: 8 })` validator on the `password` property

2. Add the `isAlpha()` validator on the `firstname` & `lastname` properties

    > Hint: If you need to send multiple values into the function call (with express-validator), instead of passing in a single string `'hello'`, you can pass in an array of strings `['hello', 'goodbye']`

3. Add the `isDate()` validator on the `dateOfBirth` property

4. Add the `isEmail()` validator on the `email` property

5. Add the `isNumeric()` validator on the `telephone` property

6. Add the `isIn(['Male', 'Female', 'N/A'])` validator on the `gender` property

## Assignment 13 - Add sanitisers

Following the same examples from above:

1. Add the `trim()` sanitiser on the following properties:

```
username
password
firstname
lastname
email
telephone
```

> Hint: If you need to send multiple values into the function call (with express-validator), instead of passing in a single string `'hello'`, you can pass in an array of strings `['hello', 'goodbye']`

2. Add the `normalizeEmail()` sanitiser on the `email` property

## Assignment 14 - Return a 400 error, if the validation fails

To check if the validation fails, we must import another **named value**  from express-validator

1. Import the `validationResult` from express-validator

2. In our callback inside `app.post`, call the `validationResult` function, passing into it the `request` object. For example, if your `request` object is `req`, your code should look like this:

    ```javascript
    validationResult(req);
    ```

3. Assign this to a variable called `errors`

```javascript
const errors = validationResult(req);
```

What is happening here?

We are looking for the errors reported by the validator. Our variable `errors` will be an array of values. If the array is empty, it means we had no errors.

4. With this information, if we have any errors here, return an error code of 400 to the user, passing in the errors.

## Assignment 15 (optional) - Inform the user of any errors

If the server gives us an error, we should inform the user.

Adapt the frontend part of this assignment to listen for a 400 error, and inform the user which fields did not meet the validation.