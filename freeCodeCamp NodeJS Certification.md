# Basic Node and Express

## 1. Meet the Node console
Working on these challenges will involve you writing your code using one of the following methods:

-   Clone [this GitHub repo](https://github.com/freeCodeCamp/boilerplate-express/) and complete these challenges locally.
-   Use [our Replit starter project](https://replit.com/github/freeCodeCamp/boilerplate-express) to complete these challenges.
-   Use a site builder of your choice to complete the project. Be sure to incorporate all the files from our GitHub repo.

If you use Replit, follow these steps to set up the project:

-   Start by importing the project on Replit.
-   Next, you will see a `.replit` window.
-   Select `Use run command` and click the `Done` button.

When you are done, make sure a working demo of your project is hosted somewhere public. Then submit the URL to it in the `Solution Link` field.
During the development process, it is important to be able to check what’s going on in your code.

Node is just a JavaScript environment. Like client side JavaScript, you can use the console to display useful debug information. On your local machine, you would see console output in a terminal. On Replit, a terminal is open in the right pane by default.

We recommend to keep the terminal open while working at these challenges. By reading the output in the terminal, you can see any errors that may occur.

---

Modify the `myApp.js` file to log "Hello World" to the console.

### Solution
```js
console.log("Hello World")
```

## 2. Start a Working Express Server
In the first two lines of the file `myApp.js`, you can see how easy it is to create an Express app object. This object has several methods, and you will learn many of them in these challenges. One fundamental method is `app.listen(port)`. It tells your server to listen on a given port, putting it in running state. For testing reasons, we need the app to be running in the background so we added this method in the `server.js` file for you.

Let’s serve our first string! In Express, routes takes the following structure: `app.METHOD(PATH, HANDLER)`. METHOD is an http method in lowercase. PATH is a relative path on the server (it can be a string, or even a regular expression). HANDLER is a function that Express calls when the route is matched. Handlers take the form `function(req, res) {...}`, where req is the request object, and res is the response object. For example, the handler
```js
function(req, res) {
  res.send('Response String');
}
```
will serve the string 'Response String'.

---

Use the `app.get()` method to serve the string "Hello Express" to GET requests matching the `/` (root) path. Be sure that your code works by looking at the logs, then see the results in the preview if you are using Replit.

**Note:** All the code for these lessons should be added in between the few lines of code we have started you off with.

### Solution:
```js
app.get('/', (req, res) => {
  console.log("Hello Express");
})
```

## 3. Serve an HTML File
You can respond to requests with a file using the `res.sendFile(path)` method. You can put it inside the `app.get('/', ...)` route handler. Behind the scenes, this method will set the appropriate headers to instruct your browser on how to handle the file you want to send, according to its type. Then it will read and send the file. This method needs an absolute file path. We recommend you to use the Node global variable `__dirname` to calculate the path like this:

```js
absolutePath = __dirname + relativePath/file.ext
```

---

Send the `/views/index.html` file as a response to GET requests to the `/` path. If you view your live app, you should see a big HTML heading (and a form that we will use later…), with no style applied.

**Note:** You can edit the solution of the previous challenge or create a new one. If you create a new solution, keep in mind that Express evaluates routes from top to bottom, and executes the handler for the first match. You have to comment out the preceding solution, or the server will keep responding with a string.

### Solution:
```js
app.get('/', (req, res) => {
  res.sendFile(__dirname + "/views/index.html");
});
```

## 4. Serve Static Assets
An HTML server usually has one or more directories that are accessible by the user. You can place there the static assets needed by your application (stylesheets, scripts, images).

In Express, you can put in place this functionality using the middleware `express.static(path)`, where the `path` parameter is the absolute path of the folder containing the assets.

If you don’t know what middleware is... don’t worry, we will discuss in detail later. Basically, middleware are functions that intercept route handlers, adding some kind of information. A middleware needs to be mounted using the method `app.use(path, middlewareFunction)`. The first `path` argument is optional. If you don’t pass it, the middleware will be executed for all requests.

---

Mount the `express.static()` middleware to the path `/public` with `app.use()`. The absolute path to the assets folder is `__dirname + /public`.

Now your app should be able to serve a CSS stylesheet. Note that the `/public/style.css` file is referenced in the `/views/index.html` in the project boilerplate. Your front-page should look a little better now!

### Solution:
```js
app.use("/public", express.static(__dirname + "/public"));
```

## 5. Serve JSON on a Specific Route
While an HTML server serves HTML, an API serves data. A REST (REpresentational State Transfer) API allows data exchange in a simple way, without the need for clients to know any detail about the server. The client only needs to know where the resource is (the URL), and the action it wants to perform on it (the verb). The GET verb is used when you are fetching some information, without modifying anything. These days, the preferred data format for moving information around the web is JSON. Simply put, JSON is a convenient way to represent a JavaScript object as a string, so it can be easily transmitted.

Let's create a simple API by creating a route that responds with JSON at the path `/json`. You can do it as usual, with the `app.get()` method. Inside the route handler, use the method `res.json()`, passing in an object as an argument. This method closes the request-response loop, returning the data. Behind the scenes, it converts a valid JavaScript object into a string, then sets the appropriate headers to tell your browser that you are serving JSON, and sends the data back. A valid object has the usual structure `{key: data}`. `data` can be a number, a string, a nested object or an array. `data` can also be a variable or the result of a function call, in which case it will be evaluated before being converted into a string.

---

Serve the object `{"message": "Hello json"}` as a response, in JSON format, to GET requests to the `/json` route. Then point your browser to `your-app-url/json`, you should see the message on the screen.

### Solution:
```js
app.get("/json", (req, res, next) => {
  var message = "Hello json"
  res.json({"message": message});
})
```

## 6. Use the .env File
The `.env` file is a hidden file that is used to pass environment variables to your application. This file is secret, no one but you can access it, and it can be used to store data that you want to keep private or hidden. For example, you can store API keys from external services or your database URI. You can also use it to store configuration options. By setting configuration options, you can change the behavior of your application, without the need to rewrite some code.

The environment variables are accessible from the app as `process.env.VAR_NAME`. The `process.env` object is a global Node object, and variables are passed as strings. By convention, the variable names are all uppercase, with words separated by an underscore. The `.env` is a shell file, so you don’t need to wrap names or values in quotes. It is also important to note that there cannot be space around the equals sign when you are assigning values to your variables, e.g. `VAR_NAME=value`. Usually, you will put each variable definition on a separate line.

---

Let's add an environment variable as a configuration option.

Create a `.env` file in the root of your project directory, and store the variable `MESSAGE_STYLE=uppercase` in it.

Then, in the `/json` GET route handler you created in the last challenge access `process.env.MESSAGE_STYLE` and transform the response object's `message` to uppercase if the variable equals `uppercase`. The response object should either be `{"message": "Hello json"}` or `{"message": "HELLO JSON"}`, depending on the `MESSAGE_STYLE` value.

**Note:** If you are using Replit, you cannot create a `.env` file. Instead, use the built-in SECRETS tab to add the variable.

If you are working locally, you will need the `dotenv` package. It loads environment variables from your `.env` file into `process.env`. The `dotenv` package has already been installed, and is in your project's `package.json` file. At the top of your `myApp.js` file, import and load the variables with `require('dotenv').config()`.

### Solution:
```js
app.get("/json", (req, res, next) => {
  var message = "Hello json"
  
  if (process.env.MESSAGE_STYLE === "uppercase")
    message = message.toUpperCase()
  
  res.json({"message": message});
})
```

## 7. Implement a Root-Level Request Logger Middleware
Earlier, you were introduced to the `express.static()` middleware function. Now it’s time to see what middleware is, in more detail. Middleware functions are functions that take 3 arguments: the request object, the response object, and the next function in the application’s request-response cycle. These functions execute some code that can have side effects on the app, and usually add information to the request or response objects. They can also end the cycle by sending a response when some condition is met. If they don’t send the response when they are done, they start the execution of the next function in the stack. This triggers calling the 3rd argument, `next()`.

Look at the following example:

```js
function(req, res, next) {
  console.log("I'm a middleware...");
  next();
}
```

Let’s suppose you mounted this function on a route. When a request matches the route, it displays the string “I’m a middleware…”, then it executes the next function in the stack. In this exercise, you are going to build root-level middleware. As you have seen in challenge 4, to mount a middleware function at root level, you can use the `app.use(<mware-function>)` method. In this case, the function will be executed for all the requests, but you can also set more specific conditions. For example, if you want a function to be executed only for POST requests, you could use `app.post(<mware-function>)`. Analogous methods exist for all the HTTP verbs (GET, DELETE, PUT, …).

---

Build a simple logger. For every request, it should log to the console a string taking the following format: `method path - ip`. An example would look like this: `GET /json - ::ffff:127.0.0.1`. Note that there is a space between `method` and `path` and that the dash separating `path` and `ip` is surrounded by a space on both sides. You can get the request method (http verb), the relative route path, and the caller’s ip from the request object using `req.method`, `req.path` and `req.ip`. Remember to call `next()` when you are done, or your server will be stuck forever. Be sure to have the ‘Logs’ opened, and see what happens when some request arrives.

**Note:** Express evaluates functions in the order they appear in the code. This is true for middleware too. If you want it to work for all the routes, it should be mounted before them.

### Solution:
```js
app.use((req, res, next) => {
  console.log(req.method + " " + req.path + " - " + req.ip)
  next()
})
```

## 8. Chain Middleware to Create a Time Server
Middleware can be mounted at a specific route using `app.METHOD(path, middlewareFunction)`. Middleware can also be chained within a route definition.

Look at the following example:

```js
app.get('/user', function(req, res, next) {
  req.user = getTheUserSync();  // Hypothetical synchronous operation
  next();
}, function(req, res) {
  res.send(req.user);
});
```

This approach is useful to split the server operations into smaller units. That leads to a better app structure, and the possibility to reuse code in different places. This approach can also be used to perform some validation on the data. At each point of the middleware stack you can block the execution of the current chain and pass control to functions specifically designed to handle errors. Or you can pass control to the next matching route, to handle special cases. We will see how in the advanced Express section.

---

In the route `app.get('/now', ...)` chain a middleware function and the final handler. In the middleware function you should add the current time to the request object in the `req.time` key. You can use `new Date().toString()`. In the handler, respond with a JSON object, taking the structure `{time: req.time}`.

**Note:** The test will not pass if you don’t chain the middleware. If you mount the function somewhere else, the test will fail, even if the output result is correct.

### Solution:
```js
app.get('/now', (req, res, next) => {
  req.time = new Date().toString()
  next()
}, (req, res) => {
  res.json({time: req.time});
})
```

## 9. Get Route Parameter Input from the Client
When building an API, we have to allow users to communicate to us what they want to get from our service. For example, if the client is requesting information about a user stored in the database, they need a way to let us know which user they're interested in. One possible way to achieve this result is by using route parameters. Route parameters are named segments of the URL, delimited by slashes (/). Each segment captures the value of the part of the URL which matches its position. The captured values can be found in the `req.params` object.

> route_path: '/user/:userId/book/:bookId'  
> actual_request_URL: '/user/546/book/6754'  
> req.params: {userId: '546', bookId: '6754'}

---

Build an echo server, mounted at the route `GET /:word/echo`. Respond with a JSON object, taking the structure `{echo: word}`. You can find the word to be repeated at `req.params.word`. You can test your route from your browser's address bar, visiting some matching routes, e.g. `your-app-rootpath/freecodecamp/echo`.

### Solution:
```js
app.get('/:word/echo', (req, res) => {
  res.json({echo: req.params.word})
})
```

## 10. Get Query Parameter Input from the Client
Another common way to get input from the client is by encoding the data after the route path, using a query string. The query string is delimited by a question mark (?), and includes field=value couples. Each couple is separated by an ampersand (&). Express can parse the data from the query string, and populate the object `req.query`. Some characters, like the percent (%), cannot be in URLs and have to be encoded in a different format before you can send them. If you use the API from JavaScript, you can use specific methods to encode/decode these characters.

> route_path: '/library'  
> actual_request_URL: '/library?userId=546&bookId=6754'  
> req.query: {userId: '546', bookId: '6754'}

---

Build an API endpoint, mounted at `GET /name`. Respond with a JSON document, taking the structure `{ name: 'firstname lastname'}`. The first and last name parameters should be encoded in a query string e.g. `?first=firstname&last=lastname`.

**Note:** In the following exercise you are going to receive data from a POST request, at the same `/name` route path. If you want, you can use the method `app.route(path).get(handler).post(handler)`. This syntax allows you to chain different verb handlers on the same path route. You can save a bit of typing, and have cleaner code.

### Solution:
```js
app.get('/name', (req, res) => {
  var {first: firstName, last: lastName} = req.query;
  res.json({name: `${firstName} ${lastName}`})
})
```

## 11. Use body-parser to Parse POST Requests
Besides GET, there is another common HTTP verb, it is POST. POST is the default method used to send client data with HTML forms. In REST convention, POST is used to send data to create new items in the database (a new user, or a new blog post). You don’t have a database in this project, but you are going to learn how to handle POST requests anyway.

In these kind of requests, the data doesn’t appear in the URL, it is hidden in the request body. The body is a part of the HTTP request, also called the payload. Even though the data is not visible in the URL, this does not mean that it is private. To see why, look at the raw content of an HTTP POST request:
```
http
POST /path/subpath HTTP/1.0
From: john@example.com
User-Agent: someBrowser/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 20

name=John+Doe&age=25
```
As you can see, the body is encoded like the query string. This is the default format used by HTML forms. With Ajax, you can also use JSON to handle data having a more complex structure. There is also another type of encoding: multipart/form-data. This one is used to upload binary files. In this exercise, you will use a URL encoded body. To parse the data coming from POST requests, you must use the `body-parser` package. This package allows you to use a series of middleware, which can decode data in different formats.<br>
<hr>
<br>`body-parser` has already been installed and is in your project's `package.json` file. `require` it at the top of the `myApp.js` file and store it in a variable named `bodyParser`. The middleware to handle URL encoded data is returned by `bodyParser.urlencoded({extended: false})`. Pass the function returned by the previous method call to `app.use()`. As usual, the middleware must be mounted before all the routes that depend on it.

**Note:** `extended` is a configuration option that tells `body-parser` which parsing needs to be used. When `extended=false` it uses the classic encoding `querystring` library. When `extended=true` it uses `qs` library for parsing.

When using `extended=false`, values can be only strings or arrays. The object returned when using `querystring` does not prototypically inherit from the default JavaScript `Object`, which means functions like `hasOwnProperty`, `toString` will not be available. The extended version allows more data flexibility, but it is outmatched by JSON.

### Solution:
```js
app.use(bodyParser.urlencoded({extended: false}))
```

## 12. Get Data from POST Requests
Mount a POST handler at the path `/name`. It’s the same path as before. We have prepared a form in the html frontpage. It will submit the same data of exercise 10 (Query string). If the body-parser is configured correctly, you should find the parameters in the object `req.body`. Have a look at the usual library example:

```
route: POST '/library'  
urlencoded_body: userId=546&bookId=6754  
req.body: {userId: '546', bookId: '6754'}
```

Respond with the same JSON object as before: `{name: 'firstname lastname'}`. Test if your endpoint works using the html form we provided in the app frontpage.

Tip: There are several other http methods other than GET and POST. And by convention there is a correspondence between the http verb, and the operation you are going to execute on the server. The conventional mapping is:

POST (sometimes PUT) - Create a new resource using the information sent with the request,

GET - Read an existing resource without modifying it,

PUT or PATCH (sometimes POST) - Update a resource using the data sent,

DELETE => Delete a resource.

There are also a couple of other methods which are used to negotiate a connection with the server. Except from GET, all the other methods listed above can have a payload (i.e. the data into the request body). The body-parser middleware works with these methods as well.

### Solution:
```js
app.post('/name', (req, res) => {
  var {first: firstName, last: lastName} = req.body;
  res.json({name: `${firstName} ${lastName}`})
})
```

### Final Code After this Section:
```js
let express = require('express');
let app = express();
let bodyParser = require('body-parser')
/*
Root level middleware
*/
app.use((req, res, next) => {
  console.log(req.method + " " + req.path + " - " + req.ip)
  next()
})
app.use(bodyParser.urlencoded({extended: false}))
/*
The '/' is the root page, and index.htmlpage willbe served in this address
*/
app.get('/', (req, res) => {
  // res.send("Hello Express");
  res.sendFile(__dirname + "/views/index.html");
});

// The /public directory is being served and can be used 
// by html file now
app.use("/public", express.static(__dirname + "/public"));

app.get("/json", (req, res, next) => {
  var message = "Hello json"
  
  if (process.env.MESSAGE_STYLE === "uppercase")
    message = message.toUpperCase()
  
  res.json({"message": message});
})

app.get('/now', (req, res, next) => {
  req.time = new Date().toString()
  next()
}, (req, res) => {
  res.json({time: req.time});
})

app.get('/:word/echo', (req, res) => {
  res.json({echo: req.params.word})
})

// app.get('/name', (req, res) => {
//   var {first: firstName, last: lastName} = req.query;
  
//   res.json({name: `${firstName} ${lastName}`})
// })

app.post('/name', (req, res) => {
  var {first: firstName, last: lastName} = req.body;
  res.json({name: `${firstName} ${lastName}`})
})

module.exports = app;
```

<hr>



# MongoDB and Mongoose

## 1. Install and Set Up Mongoose
Working on these challenges will involve you writing your code using one of the following methods:

-   Clone [this GitHub repo](https://github.com/freeCodeCamp/boilerplate-mongomongoose/) and complete these challenges locally.
-   Use [our Replit starter project](https://replit.com/github/freeCodeCamp/boilerplate-mongomongoose) to complete these challenges.
-   Use a site builder of your choice to complete the project. Be sure to incorporate all the files from our GitHub repo.

If you use Replit, follow these steps to set up the project:

-   Start by importing the project on Replit.
-   Next, you will see a `.replit` window.
-   Select `Use run command` and click the `Done` button.

When you are done, make sure a working demo of your project is hosted somewhere public. Then submit the URL to it in the `Solution Link` field.

In this challenge, you will set up a MongoDB Atlas database and import the required packages to connect to it.

Follow [this tutorial](https://www.freecodecamp.org/news/get-started-with-mongodb-atlas/) to set up a hosted database on MongoDB Atlas.

---

`mongoose@^5.11.15` has been added to your project’s `package.json` file. First, require mongoose as `mongoose` in `myApp.js`. Next, create a `.env` file and add a `MONGO_URI` variable to it. Its value should be your MongoDB Atlas database URI. Be sure to surround the URI with single or double quotes, and remember that you can't use spaces around the `=` in environment variables. For example, `MONGO_URI='VALUE'`.

**Note:** If you are using Replit, you cannot create a `.env` file. Instead, use the built-in SECRETS tab to add the variable. _Do not_ surround the values with quotes when using the _SECRETS_ tab.

When you are done, connect to the database using the following syntax:

```js
mongoose.connect(<Your URI>, { useNewUrlParser: true, useUnifiedTopology: true });
```

### Solution:
```js
const MONGO_URI = process.env.MONGO_URI;

mongoose.connect(MONGO_URI, { 
  useNewUrlParser: true, 
  useUnifiedTopology: true
})
```

## 2. Create a Model
**CRUD Part I - CREATE**

First of all, we need a Schema. Each schema maps to a MongoDB collection. It defines the shape of the documents within that collection. Schemas are building blocks for Models. They can be nested to create complex models, but in this case, we'll keep things simple. A model allows you to create instances of your objects, called documents.

Replit is a real server, and in real servers, the interactions with the database happen in handler functions. These functions are executed when some event happens (e.g. someone hits an endpoint on your API). We’ll follow the same approach in these exercises. The `done()` function is a callback that tells us that we can proceed after completing an asynchronous operation such as inserting, searching, updating, or deleting. It's following the Node convention, and should be called as `done(null, data)` on success, or `done(err)` on error.

Warning - When interacting with remote services, errors may occur!

```js
/* Example */

const someFunc = function(done) {
  //... do something (risky) ...
  if (error) return done(error);
  done(null, result);
};
```

Create a person schema called `personSchema` having this prototype:

```markup
- Person Prototype -
--------------------
name : string [required]
age :  number
favoriteFoods : array of strings (*)
```

Use the Mongoose basic schema types. If you want you can also add more fields, use simple validators like required or unique, and set default values. See our [Mongoose article](https://www.freecodecamp.org/news/introduction-to-mongoose-for-mongodb-d2a7aa593c57/).

Now, create a model called `Person` from the `personSchema`.

### Solution:
```js
const {Schema} = mongoose;

let personSchema = new Schema({
  name: {type: String, required: true},
  age: String,
  favoriteFoods: [String]
})

let Person = mongoose.model("Person", personSchema);
```

## 3. Create and Save a Record of a Model
In this challenge you will have to create and save a record of a model.

Within the `createAndSavePerson` function, create a document instance using the `Person` model constructor you built before. Pass to the constructor an object having the fields `name`, `age`, and `favoriteFoods`. Their types must conform to the ones in the `personSchema`. Then, call the method `document.save()` on the returned document instance. Pass to it a callback using the Node convention. This is a common pattern; all the following CRUD methods take a callback function like this as the last argument.

```js
/* Example */

// ...
person.save(function(err, data) {
  //   ...do your stuff here...
});
```

### Solution:
```js
const createAndSavePerson = (done) => {
  var person = new Person({
    name: "Subhadeep Mandal",
    age: 21,
    favoriteFoods: ["a", "b", "c"]
  });
  
  person.save((err, data) => {
    if (err)
      return console.error(err);
    done(null, data);
  })
};
```

## 4. Create Many Records with model.create()
Sometimes you need to create many instances of your models, e.g. when seeding a database with initial data. `Model.create()` takes an array of objects like `[{name: 'John', ...}, {...}, ...]` as the first argument, and saves them all in the db.

Modify the `createManyPeople` function to create many people using `Model.create()` with the argument `arrayOfPeople`.

**Note:** You can reuse the model you instantiated in the previous exercise.

### Solution
```js
const createManyPeople = (arrayOfPeople, done) => {
  Person.create(arrayOfPeople, (err, data) => {
    if (err)
      return console.error(err)
    done(null, data);
  })
};
```

## 5. Use model.find() to Search Your Database
In its simplest usage, `Model.find()` accepts a query document (a JSON object) as the first argument, then a callback. It returns an array of matches. It supports an extremely wide range of search options. Read more in the docs.

Modify the `findPeopleByName` function to find all the people having a given name, using `Model.find() -> [Person]`

Use the function argument `personName` as the search key.

### Solution
```js
const findPeopleByName = (personName, done) => {
  Person.find({name: personName}, (err, data) => {
    if (err)
      return console.error(err)
    done(null, data);
  })

  // console.log(result)
};
```

## 6. Use model.findOne() to Return a Single Matching Document from Your Database
`Model.findOne()` behaves like `Model.find()`, but it returns only one document (not an array), even if there are multiple items. It is especially useful when searching by properties that you have declared as unique.

Modify the `findOneByFood` function to find just one person which has a certain food in the person's favorites, using `Model.findOne() -> Person`. Use the function argument `food` as search key.

### Solution:
```js
const findOneByFood = (food, done) => {
  Person.findOne({favoriteFoods: food}, (err, data) => {
    if (err)
      return console.error(err);
    done(null, data);
  })
};
```

## 7. Use model.findById() to Search Your Database By **__id**
When saving a document, MongoDB automatically adds the field `_id`, and set it to a unique alphanumeric key. Searching by `_id` is an extremely frequent operation, so Mongoose provides a dedicated method for it.

Modify the `findPersonById` to find the only person having a given `_id`, using `Model.findById() -> Person`. Use the function argument `personId` as the search key.

### Solution
```js
const findPersonById = (personId, done) => {
  Person.findById(personId, (err, data) => {
    if (err)
      return console.error(err);
    done(null, data);
  })
};
```

## 8. Perform Classic Updates by Running Find, Edit, then Save
In the good old days, this was what you needed to do if you wanted to edit a document, and be able to use it somehow (e.g. sending it back in a server response). Mongoose has a dedicated updating method: `Model.update()`. It is bound to the low-level mongo driver. It can bulk-edit many documents matching certain criteria, but it doesn’t send back the updated document, only a 'status' message. Furthermore, it makes model validations difficult, because it just directly calls the mongo driver.

Modify the `findEditThenSave` function to find a person by `_id` (use any of the above methods) with the parameter `personId` as search key. Add `"hamburger"` to the list of the person's `favoriteFoods` (you can use `Array.push()`). Then - inside the find callback - `save()` the updated `Person`.

**Note:** This may be tricky, if in your Schema, you declared `favoriteFoods` as an Array, without specifying the type (i.e. `[String]`). In that case, `favoriteFoods` defaults to Mixed type, and you have to manually mark it as edited using `document.markModified('edited-field')`. See our [Mongoose article](https://www.freecodecamp.org/news/introduction-to-mongoose-for-mongodb-d2a7aa593c57/).

### Solution
```js
const findEditThenSave = (personId, done) => {
  const foodToAdd = "hamburger";
  Person.findById(personId, (err, person) => {
    if (err)
      return console.error(err);
    person.favoriteFoods.push(foodToAdd);
    person.save(person, (err, updatedPerson) => {
      if (err)
        return console.error(err);
      done(null, updatedPerson);
    })
  })
};
```

## 9. Perform New Updates on a Document Using model.findOneAndUpdate()
Recent versions of Mongoose have methods to simplify documents updating. Some more advanced features (i.e. pre/post hooks, validation) behave differently with this approach, so the classic method is still useful in many situations. `findByIdAndUpdate()` can be used when searching by id.

Modify the `findAndUpdate` function to find a person by `Name` and set the person's age to `20`. Use the function parameter `personName` as the search key.

**Note:** You should return the updated document. To do that, you need to pass the options document `{ new: true }` as the 3rd argument to `findOneAndUpdate()`. By default, these methods return the unmodified object.

### Solution
```js
const findAndUpdate = (personName, done) => {
  const ageToSet = 20;
  Person.findOne({name: personName}, (err, person) => {
    if (err)
        return console.error(err);
    person.age = ageToSet;
    person.save(person, (err, updatedPerson) => {
      if (err)
        return console.error(err);
      done(null, updatedPerson);
    })
  })
};
```
**or**
```js
const findAndUpdate = (personName, done) => {
  const ageToSet = 20; 
  Person.findOneAndUpdate({name: personName}, {age: ageToSet}, {new: true}, (err, updatedDoc) => { 
    if(err) 
      return console.log(err); 
    done(null, updatedDoc); 
  }) 
};
```

## 10. Delete One Document Using model.findByIdAndRemove
`findByIdAndRemove` and `findOneAndRemove` are like the previous update methods. They pass the removed document to the db. As usual, use the function argument `personId` as the search key.

Modify the `removeById` function to delete one person by the person's `_id`. You should use one of the methods `findByIdAndRemove()` or `findOneAndRemove()`.

### Solution:
```js
const removeById = (personId, done) => {
  Person.findByIdAndRemove(personId, (err, person) => {
    if (err)
      return console.error(err);
    done(null, person);
  })
};
```

## 11. Delete Many Documents with model.remove()
`Model.remove()` is useful to delete all the documents matching given criteria.

Modify the `removeManyPeople` function to delete all the people whose name is within the variable `nameToRemove`, using `Model.remove()`. Pass it to a query document with the `name` field set, and a callback.

**Note:** The `Model.remove()` doesn’t return the deleted document, but a JSON object containing the outcome of the operation, and the number of items affected. Don’t forget to pass it to the `done()` callback, since we use it in tests.

### Solution:
```js
const removeManyPeople = (done) => {
  const nameToRemove = "Mary";
  Person.remove({name: nameToRemove}, (err, person) => {
    if (err)
      return console.error(err);
    done(null, person);
  })
};
```

## 12. Chain Search Query Helpers to Narrow Search Results
If you don’t pass the callback as the last argument to `Model.find()` (or to the other search methods), the query is not executed. You can store the query in a variable for later use. This kind of object enables you to build up a query using chaining syntax. The actual db search is executed when you finally chain the method `.exec()`. You always need to pass your callback to this last method. There are many query helpers, here we'll use the most commonly used.

Modify the `queryChain` function to find people who like the food specified by the variable named `foodToSearch`. Sort them by `name`, limit the results to two documents, and hide their age. Chain `.find()`, `.sort()`, `.limit()`, `.select()`, and then `.exec()`. Pass the `done(err, data)` callback to `exec()`.

### Solution:
```js
const queryChain = (done) => {
  const foodToSearch = "burrito";
  Person.find({favoriteFoods: foodToSearch}).sort({name: 1}).limit(2).select({age: 0}).exec((err, data) => {
    if (err)
      return console.error(err);
    done(null, data);
  })
};
```

### Final Code after all solutions
```js
require('dotenv').config();
let mongoose = require("mongoose");

const MONGO_URI = process.env.MONGO_URI;

mongoose.connect(MONGO_URI, { 
  useNewUrlParser: true, 
  useUnifiedTopology: true
})

// Get the Schema class from mongoose
const {Schema} = mongoose;

// creating personSchema
let personSchema = new Schema({
  name: {type: String, required: true},
  age: Number,
  favoriteFoods: [String]
})

// Creating Person object using personSchema
var Person = mongoose.model("Person", personSchema);

const createAndSavePerson = (done) => {
  var person = new Person({
    name: "Subhadeep Mandal",
    age: 21,
    favoriteFoods: ["a", "b", "c"]
  });
  
  person.save((err, data) => {
    if (err)
      return console.error(err);
    done(null, data);
  })
};

const createManyPeople = (arrayOfPeople, done) => {
  Person.create(arrayOfPeople, (err, data) => {
    if (err)
      return console.error(err)
    done(null, data);
  })
};

const findPeopleByName = (personName, done) => {
  Person.find({name: personName}, (err, data) => {
    if (err)
      return console.error(err)
    done(null, data);
  })

  // console.log(result)
};

const findOneByFood = (food, done) => {
  Person.findOne({favoriteFoods: food}, (err, data) => {
    if (err)
      return console.error(err);
    done(null, data);
  })
};

const findPersonById = (personId, done) => {
  Person.findById(personId, (err, data) => {
    if (err)
      return console.error(err);
    done(null, data);
  })
};

const findEditThenSave = (personId, done) => {
  const foodToAdd = "hamburger";
  Person.findById(personId, (err, person) => {
    if (err)
      return console.error(err);
    person.favoriteFoods.push(foodToAdd);
    person.save(person, (err, updatedPerson) => {
      if (err)
        return console.error(err);
      done(null, updatedPerson);
    })
  })
};

const findAndUpdate = (personName, done) => {
  const ageToSet = 20;
  Person.findOne({name: personName}, (err, person) => {
    if (err)
        return console.error(err);
    person.age = ageToSet;
    person.save(person, (err, updatedPerson) => {
      if (err)
        return console.error(err);
      done(null, updatedPerson);
    })
  })
};

const removeById = (personId, done) => {
  Person.findByIdAndRemove(personId, (err, person) => {
    if (err)
      return console.error(err);
    done(null, person);
  })
};

const removeManyPeople = (done) => {
  const nameToRemove = "Mary";
  Person.remove({name: nameToRemove}, (err, person) => {
    if (err)
      return console.error(err);
    done(null, person);
  })
};

const queryChain = (done) => {
  const foodToSearch = "burrito";
  Person.find({favoriteFoods: foodToSearch}).sort({name: 1}).limit(2).select({age: 0}).exec((err, data) => {
    if (err)
      return console.error(err);
    done(null, data);
  })
};
```


# Back End Development and APIs Projects

## 1. Timestamp Microservice
Build a full stack JavaScript app that is functionally similar to this: [https://timestamp-microservice.freecodecamp.rocks](https://timestamp-microservice.freecodecamp.rocks/). Working on this project will involve you writing your code using one of the following methods:

-   Clone [this GitHub repo](https://github.com/freeCodeCamp/boilerplate-project-timestamp/) and complete your project locally.
-   Use [our Replit starter project](https://replit.com/github/freeCodeCamp/boilerplate-project-timestamp) to complete your project.
-   Use a site builder of your choice to complete the project. Be sure to incorporate all the files from our GitHub repo.

If you use Replit, follow these steps to set up the project:

-   Start by importing the project on Replit.
-   Next, you will see a `.replit` window.
-   Select `Use run command` and click the `Done` button.

When you are done, make sure a working demo of your project is hosted somewhere public. Then submit the URL to it in the `Solution Link` field. Optionally, also submit a link to your project's source code in the `GitHub Link` field.

**Note:** Time zones conversion is not a purpose of this project, so assume all sent valid dates will be parsed with `new Date()` as GMT dates.

### Solution:
```js
var express = require('express');
var app = express();

var cors = require('cors');
app.use(cors({optionsSuccessStatus: 200}));

app.get('/api/', (req, res) => {
  const date = new Date();
  res.json({
    "unix": date.getTime(),
    "utc": `${date}`
  })
})

app.get('/api/:date?', (req, res) => {
  var inputDate = req.params.date;
  inputDate = isNaN(inputDate) ? inputDate : parseInt(inputDate);
  const date = new Date(inputDate);
  if (date == "Invalid Date")
    res.json({"error": `${date}`})
  else
    res.json({
      "unix": date.getTime(),
      "utc": date.toUTCString()
    })
})

// listen for requests :)
var listener = app.listen(process.env.PORT, function () {
  console.log('Your app is listening on port ' + listener.address().port);
});

```

## 2. Request Header Parser Microservice
Build a full stack JavaScript app that is functionally similar to this: [https://request-header-parser-microservice.freecodecamp.rocks/](https://request-header-parser-microservice.freecodecamp.rocks/). Working on this project will involve you writing your code using one of the following methods:

-   Clone [this GitHub repo](https://github.com/freeCodeCamp/boilerplate-project-headerparser/) and complete your project locally.
-   Use [our Replit starter project](https://replit.com/github/freeCodeCamp/boilerplate-project-headerparser) to complete your project.
-   Use a site builder of your choice to complete the project. Be sure to incorporate all the files from our GitHub repo.

If you use Replit, follow these steps to set up the project:

-   Start by importing the project on Replit.
-   Next, you will see a `.replit` window.
-   Select `Use run command` and click the `Done` button.

When you are done, make sure a working demo of your project is hosted somewhere public. Then submit the URL to it in the `Solution Link` field. Optionally, also submit a link to your project's source code in the `GitHub Link` field.

### Solution:
```js
require('dotenv').config();
var express = require('express');
var app = express();

var cors = require('cors');
app.use(cors({ optionsSuccessStatus: 200 })); 

app.use(express.static('public'));

app.get('/', function (req, res) {
  res.sendFile(__dirname + '/views/index.html');
});

app.get('/api/whoami', (req, res) => {
  var rawHeaders = req.rawHeaders;
  var ip = req.connection.remoteAddress
  var lang = rawHeaders[9]
  var software = rawHeaders[3]
  res.json({
    "ipaddress": ip,
    "language": lang,
    "software": software
  })
})

// listen for requests :)
var listener = app.listen(process.env.PORT || 3000, function () {
  console.log('Your app is listening on port ' + listener.address().port);
});

```

## 3. URL Shortener Microservice
Build a full stack JavaScript app that is functionally similar to this: [https://url-shortener-microservice.freecodecamp.rocks](https://url-shortener-microservice.freecodecamp.rocks/). Working on this project will involve you writing your code using one of the following methods:

-   Clone [this GitHub repo](https://github.com/freeCodeCamp/boilerplate-project-urlshortener/) and complete your project locally.
-   Use [our Replit starter project](https://replit.com/github/freeCodeCamp/boilerplate-project-urlshortener) to complete your project.
-   Use a site builder of your choice to complete the project. Be sure to incorporate all the files from our GitHub repo.

If you use Replit, follow these steps to set up the project:

-   Start by importing the project on Replit.
-   Next, you will see a `.replit` window.
-   Select `Use run command` and click the `Done` button.

When you are done, make sure a working demo of your project is hosted somewhere public. Then submit the URL to it in the `Solution Link` field. Optionally, also submit a link to your project's source code in the `GitHub Link` field.

**HINT:** Do not forget to use a body parsing middleware to handle the POST requests. Also, you can use the function `dns.lookup(host, cb)` from the `dns` core module to verify a submitted URL.

### Solution:
```js
require('dotenv').config();
const express = require('express');
const cors = require('cors');
const app = express();
const bodyParser = require('body-parser')
const dns = require('dns')

// Basic Configuration
const port = process.env.PORT || 3000;

app.use(bodyParser.urlencoded({ extended: false }));
app.use(bodyParser.json());

app.use(cors());

app.use('/public', express.static(`${process.cwd()}/public`));

app.get('/', function(req, res) {
  res.sendFile(process.cwd() + '/views/index.html');
});

// Your first API endpoint
app.get('/api/hello', function(req, res) {
  res.json({ greeting: 'hello API' });
});

const urlList = [];

app.post('/api/shorturl', (req, res) => {
  let url = new URL(req.body.url);
  console.log(url);
  dns.lookup(url.hostname, (err, address, family) => {
    if (err) {
      res.json({ error: 'invalid url' })
    }
    else {
      if (!urlList.includes(url.href)) {
        urlList.push(url.href);
      }
      res.json({
        original_url: url,
        short_url: urlList.indexOf(url.href) + 1
      });
    }
  });
})

app.get('/api/shorturl/:id', (req, res) => {
  var id = req.params.id
  // console.log("redirect: " + urlList[id - 1])
  res.redirect(urlList[id - 1].toString())
})

app.listen(port, function() {
  console.log(`Listening on port ${port}`);
});
```

## 4. Exercise Tracker
Build a full stack JavaScript app that is functionally similar to this: [https://exercise-tracker.freecodecamp.rocks](https://exercise-tracker.freecodecamp.rocks/). Working on this project will involve you writing your code using one of the following methods:

-   Clone [this GitHub repo](https://github.com/freeCodeCamp/boilerplate-project-exercisetracker/) and complete your project locally.
-   Use [our Replit starter project](https://replit.com/github/freeCodeCamp/boilerplate-project-exercisetracker) to complete your project.
-   Use a site builder of your choice to complete the project. Be sure to incorporate all the files from our GitHub repo.

If you use Replit, follow these steps to set up the project:

-   Start by importing the project on Replit.
-   Next, you will see a `.replit` window.
-   Select `Use run command` and click the `Done` button.

When you are done, make sure a working demo of your project is hosted somewhere public. Then submit the URL to it in the `Solution Link` field. Optionally, also submit a link to your project's source code in the `GitHub Link` field.

Your responses should have the following structures.

Exercise:

```js
{
  username: "fcc_test",
  description: "test",
  duration: 60,
  date: "Mon Jan 01 1990",
  _id: "5fb5853f734231456ccb3b05"
}
```

User:

```js
{
  username: "fcc_test",
  _id: "5fb5853f734231456ccb3b05"
}
```

Log:

```js
{
  username: "fcc_test",
  count: 1,
  _id: "5fb5853f734231456ccb3b05",
  log: [{
    description: "test",
    duration: 60,
    date: "Mon Jan 01 1990",
  }]
}
```

**Hint:** For the `date` property, the `toDateString` method of the `Date` API can be used to achieve the expected output.

### Solution:

###### 1. Import `body-parser` and `mongoose` packages.
```js
const mongoose = require('mongoose')
const bodyParser = require('body-parser');

app.use(bodyParser.urlencoded({ extended: false }))
```

###### 2. Access MongoDB connection URI, and connect to mongoDb. 
```js
const MONGO_URI = process.env.MONGO_URI

mongoose.connect(MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true });

const dbConnection = mongoose.connection;
dbConnection.on("error", () => {
  console.error.bind(console, "MongoDB connection has an error!");
});
dbConnection.once("open", () => {
  console.log("MongoDB Connected Successfully!");
})
```

###### 3. Create the `User` and `Log` models.
```js
const User = mongoose.model(
  "User", 
  new mongoose.Schema({
    username: String,
  })
);

const Log = mongoose.model(
  "Log", 
  new mongoose.Schema({
    userid: String,
    username: String,
    description: String,
    duration: Number,
    date: {type: Date, default: Date.now},
  })
);
```

###### 4. Implement the POST method for new user.
```js
app.post('/api/users', async (req, res) => {
  if (req.body.username === '')
    res.json({"message": "username field cannot be empty."})
  
  const userExists = await User.findOne(
    {username: req.body.username});

  if (!userExists) {
    let newUser = new User({
      username: req.body.username,
    });
    await newUser.save();
    res.json({
      username: newUser.username,
      _id: newUser._id
    })
  }
  else {
    res.json({
      username: userExists.username,
      _id: userExists._id
    })
  }
});
```

###### 5. Implement the get all users method.
```js
app.get('/api/users', async (req, res) => {
  try {
    let allUsers = await User.find({});
    res.json(allUsers);
  } catch(err) {
    res.json({
      error: err.message
    });
  }
});
```

###### 6. Implement POST method of exercise
```js
app.post('/api/users/:_id/exercises', async (req, res) => {
  const _id = req.params._id
  const description = req.body.description
  const duration = req.body.duration
  const date = (req.body.date === undefined) ? new Date() : new Date(req.body.date);

  if (!description || !duration) {
    res.json({
      "message": "description and duration are required."
    })
  }
  if (isNaN(duration)) {
    res.json({
      "message": "Duration must be a number."
    })
  }
  if (date.toString() === "Invalid Date") {
    res.json({
      "message": "Date is not valid."
    })
  }
  const user = await User.findById(_id);
  if (!user) {
    res.json({"error": "User don't exist."})
  }
  
  const newLog = new Log({
    userid: _id,
    description,
    duration,
    date
  });

  await newLog.save();

  res.json({
    userid: user._id,
    username: user.username,
    description: newLog.description,
    duration: newLog.duration,
    date: newLog.date.toDateString(),
  })
})
```
###### 7. Implement GET method for all exercises of an user
```js
app.get('/api/users/:_id/logs', async (req, res) => {
  const _id = req.params._id;
  let {from, to, limit} = req.query;

  const fetchUser = await User.findById(_id);
  if (!fetchUser) {
    res.json({
      "message": "User not found."
    });
  }
  var filter = {userid: _id}

  if (from && to){
    if (from.toString() === "Invalid Date" || to.toString() === "Invalid Date")
      res.json({
        "message": "Invalid date format."
      })
    filter = {
      userid: _id,
      date: {
        $gte: from,
        $lte: to
      },
    }
  }
  else if (from) {
    if (from.toString() === "Invalid Date")
      res.json({
        "message": "Invalid date format."
      })
    filter = {
      userid: _id,
      date: {
        $gte: from,
      },
    }
  }
  else if (to) {
    if (to.toString() === "Invalid Date")
      res.json({
        "message": "Invalid date format."
      })
    filter = {
      userid: _id,
      date: {
        $lte: to
      },
    }
  }

  if (limit) {
    limit = parseInt(limit)
    if (isNaN(limit)) {
      res.json({
        "message": "Limit must be a number."
      })
    }
  }
  else {
    limit = 0
  }

  let filteredLogs = await Log.find(filter).limit(limit);

  filteredLogs = filteredLogs.map(log => {
    return {
      description: log.description,
      duration: log.duration,
      date: log.date.toDateString()
    };
  });

  res.json({
    username: fetchUser.username,
    count: filteredLogs.length,
    _id: fetchUser._id,
    log: filteredLogs
  });
})
```

#### Final Code:
```js
const express = require('express')
const app = express()
const cors = require('cors')
const mongoose = require('mongoose')
const bodyParser = require('body-parser');
require('dotenv').config()

const MONGO_URI = process.env.MONGO_URI

mongoose.connect(MONGO_URI, 
                 { useNewUrlParser: true, 
                  useUnifiedTopology: true 
                 });

const dbConnection = mongoose.connection;
dbConnection.on("error", () => {
  console.error.bind(console, "MongoDB connection has an error!");
});
dbConnection.once("open", () => {
  console.log("MongoDB Connected Successfully!");
})

app.use(cors())
app.use(express.static('public'))
app.use(bodyParser.urlencoded({ extended: false }))

app.get('/', (req, res) => {
  res.sendFile(__dirname + '/views/index.html')
});

const User = mongoose.model(
  "User", 
  new mongoose.Schema({
    username: String,
  })
);

const Log = mongoose.model(
  "Log", 
  new mongoose.Schema({
    userid: String,
    username: String,
    description: String,
    duration: Number,
    date: {type: Date, default: Date.now},
  })
);


// Adding new User
app.post('/api/users', async (req, res) => {
  if (req.body.username === '')
    res.json({"message": "username field cannot be empty."})
  
  const userExists = await User.findOne(
    {username: req.body.username});

  if (!userExists) {
    let newUser = new User({
      username: req.body.username,
    });
    await newUser.save();
    res.json({
      username: newUser.username,
      _id: newUser._id
    })
  }
  else {
    res.json({
      username: userExists.username,
      _id: userExists._id
    })
  }
});

// Get all users
app.get('/api/users', async (req, res) => {
  try {
    let allUsers = await User.find({});
    res.json(allUsers);
  } catch(err) {
    res.json({
      error: err.message
    });
  }
});

app.post('/api/users/:_id/exercises', async (req, res) => {
  const _id = req.params._id
  const description = req.body.description
  const duration = req.body.duration
  const date = (req.body.date === undefined) ? new Date() : new Date(req.body.date);

  if (!description || !duration) {
    res.json({
      "message": "description and duration are required."
    })
  }
  if (isNaN(duration)) {
    res.json({
      "message": "Duration must be a number."
    })
  }
  if (date.toString() === "Invalid Date") {
    res.json({
      "message": "Date is not valid."
    })
  }
  const user = await User.findById(_id);
  if (!user) {
    res.json({"error": "User don't exist."})
  }
  
  const newLog = new Log({
    userid: _id,
    description,
    duration,
    date
  });

  await newLog.save();

  res.json({
    username: user.username,
    description: newLog.description,
    duration: newLog.duration,
    date: newLog.date.toDateString(),
    _id: user._id,
  })
})

app.get('/api/users/:_id/logs', async (req, res) => {
  const _id = req.params._id;
  let {from, to, limit} = req.query;

  const fetchUser = await User.findById(_id);
  if (!fetchUser) {
    res.json({
      "message": "User not found."
    });
  }
  var filter = {userid: _id}

  if (from && to){
    if (from.toString() === "Invalid Date" || to.toString() === "Invalid Date")
      res.json({
        "message": "Invalid date format."
      })
    filter = {
      userid: _id,
      date: {
        $gte: from,
        $lte: to
      },
    }
  }
  else if (from) {
    if (from.toString() === "Invalid Date")
      res.json({
        "message": "Invalid date format."
      })
    filter = {
      userid: _id,
      date: {
        $gte: from,
      },
    }
  }
  else if (to) {
    if (to.toString() === "Invalid Date")
      res.json({
        "message": "Invalid date format."
      })
    filter = {
      userid: _id,
      date: {
        $lte: to
      },
    }
  }

  if (limit) {
    limit = parseInt(limit)
    if (isNaN(limit)) {
      res.json({
        "message": "Limit must be a number."
      })
    }
  }
  else {
    limit = 0
  }

  let filteredLogs = await Log.find(filter).limit(limit);

  filteredLogs = filteredLogs.map(log => {
    return {
      description: log.description,
      duration: log.duration,
      date: log.date.toDateString()
    };
  });

  res.json({
    username: fetchUser.username,
    count: filteredLogs.length,
    _id: fetchUser._id,
    log: filteredLogs
  });
})

const listener = app.listen(process.env.PORT || 3000, () => {
  console.log('Your app is listening on port ' + listener.address().port)
})

```

## 5. File Metadata Microservice
Build a full stack JavaScript app that is functionally similar to this: [https://file-metadata-microservice.freecodecamp.rocks](https://file-metadata-microservice.freecodecamp.rocks/). Working on this project will involve you writing your code using one of the following methods:

-   Clone [this GitHub repo](https://github.com/freeCodeCamp/boilerplate-project-filemetadata/) and complete your project locally.
-   Use [our Replit starter project](https://replit.com/github/freeCodeCamp/boilerplate-project-filemetadata) to complete your project.
-   Use a site builder of your choice to complete the project. Be sure to incorporate all the files from our GitHub repo.

If you use Replit, follow these steps to set up the project:

-   Start by importing the project on Replit.
-   Next, you will see a `.replit` window.
-   Select `Use run command` and click the `Done` button.

When you are done, make sure a working demo of your project is hosted somewhere public. Then submit the URL to it in the `Solution Link` field. Optionally, also submit a link to your project's source code in the `GitHub Link` field.

**HINT:** You can use the `multer` npm package to handle file uploading.

### Solution:
```js
var express = require('express');
var cors = require('cors');
const multer = require("multer");
require('dotenv').config()

var app = express();

app.use(cors());
app.use('/public', express.static(process.cwd() + '/public'));

const storage = multer.memoryStorage();
const upload = multer({
  storage: storage
});

app.get('/', function (req, res) {
  res.sendFile(process.cwd() + '/views/index.html');
});

app.post('/api/fileanalyse', upload.single("upfile"), (req, res) => {
  res.json({
    "name": req.file.originalname,
    "type": req.file.mimetype,
    "size": req.file.size
  });
});

const port = process.env.PORT || 3000;
app.listen(port, function () {
  console.log('Your app is listening on port ' + port)
});

```



# Frontend Masters NodeJS Tutorials

## Connecting to Database using Prisma
Install the required packages:
```shell
npm install typescript ts-node @types/node prisma --save-dev
```

The project tree so far:
```
project
├── node_modules
├── src
│   ├── home.js
├── app.js
├── package.json
└── package-lock.json
```

The code so far:
`src/home.js`
```js
const express = require("express");
  
const app = express();
  
app.get("/", (req, res) => {
	res.json({
		message: "Welcome to nodejs server!",
	});
});

module.exports = app;
```

`app.js`
```js
const app = require("./src/home");
const PORT = 3000;
  
app.listen(PORT, () => {
	console.log(`Server is running on port: ${PORT}`);
});
```

Create a `tsconfig.json` file
```json
{
	"compilerOptions": {
		"sourceMap": true,
		"outDir": "dist",
		"lib": ["ESNext"],
		"esModuleInterop": true
	}
}
```

Initialize Prisma:
```shell
npx prisma init
```

Set the database URL in `.env` file. Convert the `.js` files to `.ts` files.

`src/home.js`:
```ts
import express from "express";
  
const app = express();
  
app.get("/", (req, res) => {
	res.json({
		message: "Welcome to nodejs server!",
	});
});
  
export default app;
```

`app.ts`
```ts
import app from "./src/home";
  
const PORT = 3000;

app.listen(PORT, () => {
	console.log(`Server is running on port: ${PORT}`);
});
```

In the `package.json` file, add the line in `script` section:
`"dev": "ts-node app.js"`

### First Prisma Schema

User schema. Add this in `prisma/schema.prisma`
```
model User {
	id String @id @default(uuid())
	username String @unique
	password String
	createdAt DateTime @default(now())
}
```

Add a product Schema. It will be using the User schema:
```
model User {
	id String @id @default(uuid())
	username String @unique
	password String
	createdAt DateTime @default(now())
	  
	product Product[]
}
  
model Product {
	id String @id @default(uuid())
	createdAt DateTime @default(now())
	  
	name String @db.VarChar(255)
	belongsToId String
	belongsTo User @relation(fields: [belongsToId], references: [id])
}
```

