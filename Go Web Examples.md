# 1. Hello World

## Introduction

Go is a battery included programming language and has a webserver already built in. The `net/http` package from the standard library contains all functionalities about the HTTP protocol. This includes (am
ong many other things) an HTTP client and an HTTP server. In this example you will figure out how simple it is, to create a webserver that you can view in your browser.

## Registering a Request Handler

First, create a Handler which receives all incomming HTTP connections from browsers, HTTP clients or API requests. A handler in Go is a function with this signature:

```go
func (w http.ResponseWriter, r *http.Request)
```

The function receives two parameters:

1.  An `http.ResponseWriter` which is where you write your text/html response to.
2.  An `http.Request` which contains all information about this HTTP request including things like the URL or header fields.

Registering a request handler to the default HTTP Server is as simple as this:

```go
http.HandleFunc("/", func (w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello, you've requested: %s\n", r.URL.Path)
})
```

## Listen for HTTP Connections

The request handler alone can not accept any HTTP connections from the outside. An HTTP server has to listen on a port to pass connections on to the request handler. Because port 80 is in most cases the default port for HTTP traffic, this server will also listen on it.

The following code will start Go’s default HTTP server and listen for connections on port 80. You can navigate your browser to `http://localhost/` and see your server handing your request.

```go
http.ListenAndServe(":80", nil)
```

## The Code (for copy/paste)

This is the complete code that you can use to try out the things you’ve learned in this example.

```go
package main

import (
    "fmt"
    "net/http"
)

func main() {
    http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
        fmt.Fprintf(w, "Hello, you've requested: %s\n", r.URL.Path)
    })

    http.ListenAndServe(":80", nil)
}
```

# 2. HTTP Server

## Introduction

In this example you will learn how to create a basic HTTP server in Go. First, let’s talk about what our HTTP server should be capable of. A basic HTTP server has a few key jobs to take care of.

-   _Process dynamic requests:_ Process incoming requests from users who browse the website, log into their accounts or post images.
-   _Serve static assets:_ Serve JavaScript, CSS and images to browsers to create a dynamic experience for the user.
-   _Accept connections:_ The HTTP Server must listen on a specific port to be able to accept connections from the internet.

## Process dynamic requests

The `net/http` package contains all utilities needed to accept requests and handle them dynamically. We can register a new handler with the `http.HandleFunc` function. It’s first parameter takes a path to match and a function to execute as a second. In this example: When someone browses your websites (`http://example.com/`), he or she will be greeted with a nice message.

```go
http.HandleFunc("/", func (w http.ResponseWriter, r *http.Request) {
    fmt.Fprint(w, "Welcome to my website!")
})
```

For the dynamic aspect, the `http.Request` contains all information about the request and it’s parameters. You can read GET parameters with `r.URL.Query().Get("token")` or POST parameters (fields from an HTML form) with `r.FormValue("email")`.

## Serving static assets

To serve static assets like JavaScript, CSS and images, we use the inbuilt `http.FileServer` and point it to a url path. For the file server to work properly it needs to know, where to serve files from. We can do this like so:

```go
fs := http.FileServer(http.Dir("static/"))
```

Once our file server is in place, we just need to point a url path at it, just like we did with the dynamic requests. One thing to note: In order to serve files correctly, we need to strip away a part of the url path. Usually this is the name of the directory our files live in.

```go
http.Handle("/static/", http.StripPrefix("/static/", fs))
```

## Accept connections

The last thing to finish off our basic HTTP server is, to listen on a port to accept connections from the internet. As you can guess, Go has also an inbuilt HTTP server, we can start faily quickly. Once started, you can view your HTTP server in your [browser.](http://localhost/)

```go
http.ListenAndServe(":80", nil)
```

## The Code (for copy/paste)

This is the complete code that you can use to try out the things you’ve learned in this example.

```go
package main

import (
    "fmt"
    "net/http"
)

func main() {
    http.HandleFunc("/", func (w http.ResponseWriter, r *http.Request) {
        fmt.Fprintf(w, "Welcome to my website!")
    })

    fs := http.FileServer(http.Dir("static/"))
    http.Handle("/static/", http.StripPrefix("/static/", fs))

    http.ListenAndServe(":80", nil)
}
```

# 3. Routing (using gorilla/mux)

## Introduction

Go’s `net/http` package provides a lot of functionalities for the HTTP protocol. One thing it doesn’t do very well is complex request routing like segmenting a request url into single parameters. Fortunately there is a very popular package for this, which is well known for the good code quality in the Go community. In this example you will see how to use the `gorilla/mux` package to create routes with named parameters, GET/POST handlers and domain restrictions.

## Installing the `gorilla/mux` package

`gorilla/mux` is a package which adapts to Go’s default HTTP router. It comes with a lot of features to increase the productivity when writing web applications. It is also compliant to Go’s default request handler signature `func (w http.ResponseWriter, r *http.Request)`, so the package can be mixed and machted with other HTTP libraries like middleware or exisiting applications. Use the `go get` command to install the package from GitHub like so:

```sh
go get -u github.com/gorilla/mux
```

## Creating a new Router

First create a new request router. The router is the main router for your web application and will later be passed as parameter to the server. It will receive all HTTP connections and pass it on to the request handlers you will register on it. You can create a new router like so:

```go
r := mux.NewRouter()
```

## Registering a Request Handler

Once you have a new router you can register request handlers like usual. The only difference is, that instead of calling `http.HandleFunc(...)`, you call `HandleFunc` on your router like this: `r.HandleFunc(...)`.

## URL Parameters

The biggest strength of the `gorilla/mux` Router is the ability to extract segments from the request URL. As an example, this is a URL in your application:

```sh
/books/go-programming-blueprint/page/10
```

This URL has two dynamic segments:

1.  Book title slug (go-programming-blueprint)
2.  Page (10)

To have a request handler match the URL mentioned above you replace the dynamic segments of with placeholders in your URL pattern like so:

```go
r.HandleFunc("/books/{title}/page/{page}", func(w http.ResponseWriter, r *http.Request) {
    // get the book
    // navigate to the page
})
```

The last thing is to get the data from these segments. The package comes with the function `mux.Vars(r)` which takes the `http.Request` as parameter and returns a map of the segments.

```go
func(w http.ResponseWriter, r *http.Request) {
    vars := mux.Vars(r)
    vars["title"] // the book title slug
    vars["page"] // the page
}
```

## Setting the HTTP server’s router

Ever wondered what the `nil` in `http.ListenAndServe(":80", nil)` ment? It is the parameter for the main router of the HTTP server. By default it’s `nil`, which means to use the default router of the `net/http` package. To make use of your own router, replace the `nil` with the variable of your router `r`.

```go
http.ListenAndServe(":80", r)
```

## The Code (for copy/paste)

This is the complete code that you can use to try out the things you’ve learned in this example.

```go
package main

import (
    "fmt"
    "net/http"

    "github.com/gorilla/mux"
)

func main() {
    r := mux.NewRouter()

    r.HandleFunc("/books/{title}/page/{page}", func(w http.ResponseWriter, r *http.Request) {
        vars := mux.Vars(r)
        title := vars["title"]
        page := vars["page"]

        fmt.Fprintf(w, "You've requested the book: %s on page %s\n", title, page)
    })

    http.ListenAndServe(":80", r)
}
```

## Features of the `gorilla/mux` Router

## Methods

Restrict the request handler to specific HTTP methods.

```go
r.HandleFunc("/books/{title}", CreateBook).Methods("POST")
r.HandleFunc("/books/{title}", ReadBook).Methods("GET")
r.HandleFunc("/books/{title}", UpdateBook).Methods("PUT")
r.HandleFunc("/books/{title}", DeleteBook).Methods("DELETE")
```

## Hostnames & Subdomains

Restrict the request handler to specific hostnames or subdomains.

```go
r.HandleFunc("/books/{title}", BookHandler).Host("www.mybookstore.com")
```

## Schemes

Restrict the request handler to http/https.

```go
r.HandleFunc("/secure", SecureHandler).Schemes("https")
r.HandleFunc("/insecure", InsecureHandler).Schemes("http")
```

## Path Prefixes & Subrouters

Restrict the request handler to specific path prefixes.

```go
bookrouter := r.PathPrefix("/books").Subrouter()
bookrouter.HandleFunc("/", AllBooks)
bookrouter.HandleFunc("/{title}", GetBook)
```

# 4. MySQL Database

## Introduction

At some point in time, you want your web application to store and retrieve data from a database. This is almost always the case when you're dealing with dynamic content, serving up forms for users to enter data or storing login and password credentials for your users to authenticate them. For this purpose, we have databases.

Databases come in all forms and shapes. One commonly used database across all of the web is the MySQL database. It has been around for ages and has proven its position and stability more times than you can count.

In this example, we will dive into the fundamentals of database access in Go, create database tables, store data and retrieve it back again.

## Installing the `go-sql-driver/mysql` package

The Go programming language comes with a handy package called `database/sql` to query all sorts of SQL databases. This is useful as it abstracts all common SQL features into a single API for you to use. What Go does not include is are database drivers. In Go, database driver is a package which implements the low level details of a specific database (in our case MySQL). As you might have already guessed, this is useful to stay forward compatible. Since, at the time of creating all Go packages, the authors cannot foresee every single database coming to live in the future and supporting every possible database out there would be a large amount of maintenance work.

To install the MySQL database driver, go to your terminal of choice and run:

```sh
go get -u github.com/go-sql-driver/mysql
```

## Connecting to a MySQL database

The first thing we need to check after installing all necessary packages is, if we can connect to our MySQL database successfully. If you don’t have a MySQL database server already running, you can start a new instance with Docker easily. Here are the official docs for the Docker MySQL image: [](https://hub.docker.com/_/mysql)[https://hub.docker.com/_/mysql](https://hub.docker.com/_/mysql)

To check if we can connect to our database, import the `database/sql` and the `go-sql-driver/mysql` package and open up a connection like so:

```go
import "database/sql"
import _ "go-sql-driver/mysql"

// Configure the database connection (always check errors)
db, err := sql.Open("mysql", "username:password@(127.0.0.1:3306)/dbname?parseTime=true")

```

## Creating our first database table

Every data entry in our database is stored in a specific table. A database table consists of columns and rows. The columns give each data entry a label and specify the type of it. The rows are the inserted data values. In our first example we want to create a table like this:

id

username

password

created_at

1

johndoe

secret

2019-08-10 12:30:00

Translated to SQL, the command for creating the table will look like this:

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT,
    username TEXT NOT NULL,
    password TEXT NOT NULL,
    created_at DATETIME,
    PRIMARY KEY (id)
);
```

Now that we have our SQL command, we can use the `database/sql` package to create the table in our MySQL database:

```go
query := `
    CREATE TABLE users (
        id INT AUTO_INCREMENT,
        username TEXT NOT NULL,
        password TEXT NOT NULL,
        created_at DATETIME,
        PRIMARY KEY (id)
    );`

// Executes the SQL query in our database. Check err to ensure there was no error.
_, err := db.Exec(query)
```

## Inserting our first user

If you are familiar with SQL inserting new data to our table is as easy as creating our table. One thing to notice is: By default Go uses prepared statements for inserting dynamic data into our SQL queries, which is a way to securely pass user supplied data to our database without the risk of any damage. In the early days of web programming, programmers passed the data directly with the query to the database which caused massive vulnerabilities and could break an entire web application. Please do not do that. It’s easy to get it right.

To insert our first user into our database table, we create a SQL query like the following. As you can see, we omit the id column, as it gets automatically set by MySQL. The questionmark tells the SQL driver, that they are placeholders for actual data. This is the where you can see the prepared statements we talked about.

```sql
INSERT INTO users (username, password, created_at) VALUES (?, ?, ?)
```

We can now use this SQL query in Go and insert a new row into our table:

```go
import "time"

username := "johndoe"
password := "secret"
createdAt := time.Now()

// Inserts our data into the users table and returns with the result and a possible error.
// The result contains information about the last inserted id (which was auto-generated for us) and the count of rows this query affected.
result, err := db.Exec(`INSERT INTO users (username, password, created_at) VALUES (?, ?, ?)`, username, password, createdAt)
```

To grab the newly created id for your user simply get it like this:

```go
userID, err := result.LastInsertId()
```

## Querying our users table

Now that we have a user in our table, we want to query it and get back all of its information. In Go we have two possibilities to query our tables. There is `db.Query` which can query multiple rows, for us to iterate over and there is `db.QueryRow` in case we only want to query a specific row.

Querying a specific row works basically like every other SQL command we’ve covered before.  
Our SQL command to query one single user by its ID looks like this:

```sql
SELECT id, username, password, created_at FROM users WHERE id = ?
```

In Go we first declare some variables to store our data in and then query a single database row like so:

```go
var (
    id        int
    username  string
    password  string
    createdAt time.Time
)

// Query the database and scan the values into out variables. Don't forget to check for errors.
query := `SELECT id, username, password, created_at FROM users WHERE id = ?`
err := db.QueryRow(query, 1).Scan(&id, &username, &password, &createdAt)
```

## Querying all users

In the section before we’ve covered how to query a single user row. Many applications have use cases where you want to query all existing users. This works similar to the example above, but with a bit more coding involved.

We can use the SQL command from the example above and trim off the `WHERE` clause. This way, we query all existing users.

```sql
SELECT id, username, password, created_at FROM users
```

In Go we first declare some variables to store our data in and then query a single database row like so:

```go
type user struct {
    id        int
    username  string
    password  string
    createdAt time.Time
}

rows, err := db.Query(`SELECT id, username, password, created_at FROM users`) // check err
defer rows.Close()

var users []user
for rows.Next() {
    var u user
    err := rows.Scan(&u.id, &u.username, &u.password, &u.createdAt) // check err
    users = append(users, u)
}
err := rows.Err() // check err
```

The users slice now might contain something like this:

```go
users {
    user {
        id:        1,
        username:  "johndoe",
        password:  "secret",
        createdAt: time.Time{wall: 0x0, ext: 63701044325, loc: (*time.Location)(nil)},
    },
    user {
        id:        2,
        username:  "alice",
        password:  "bob",
        createdAt: time.Time{wall: 0x0, ext: 63701044622, loc: (*time.Location)(nil)},
    },
}
```

## Deleting a user from our table

Finally, deleting a user from our table is as straight forward as the `.Exec` from the sections above:

```go
_, err := db.Exec(`DELETE FROM users WHERE id = ?`, 1) // check err
```

## The Code (for copy/paste)

This is the complete code that you can use to try out the things you’ve learned from this example.

```go
package main

import (
    "database/sql"
    "fmt"
    "log"
    "time"

    _ "github.com/go-sql-driver/mysql"
)

func main() {
    db, err := sql.Open("mysql", "root:root@(127.0.0.1:3306)/root?parseTime=true")
    if err != nil {
        log.Fatal(err)
    }
    if err := db.Ping(); err != nil {
        log.Fatal(err)
    }

    { // Create a new table
        query := `
            CREATE TABLE users (
                id INT AUTO_INCREMENT,
                username TEXT NOT NULL,
                password TEXT NOT NULL,
                created_at DATETIME,
                PRIMARY KEY (id)
            );`

        if _, err := db.Exec(query); err != nil {
            log.Fatal(err)
        }
    }

    { // Insert a new user
        username := "johndoe"
        password := "secret"
        createdAt := time.Now()

        result, err := db.Exec(`INSERT INTO users (username, password, created_at) VALUES (?, ?, ?)`, username, password, createdAt)
        if err != nil {
            log.Fatal(err)
        }

        id, err := result.LastInsertId()
        fmt.Println(id)
    }

    { // Query a single user
        var (
            id        int
            username  string
            password  string
            createdAt time.Time
        )

        query := "SELECT id, username, password, created_at FROM users WHERE id = ?"
        if err := db.QueryRow(query, 1).Scan(&id, &username, &password, &createdAt); err != nil {
            log.Fatal(err)
        }

        fmt.Println(id, username, password, createdAt)
    }

    { // Query all users
        type user struct {
            id        int
            username  string
            password  string
            createdAt time.Time
        }

        rows, err := db.Query(`SELECT id, username, password, created_at FROM users`)
        if err != nil {
            log.Fatal(err)
        }
        defer rows.Close()

        var users []user
        for rows.Next() {
            var u user

            err := rows.Scan(&u.id, &u.username, &u.password, &u.createdAt)
            if err != nil {
                log.Fatal(err)
            }
            users = append(users, u)
        }
        if err := rows.Err(); err != nil {
            log.Fatal(err)
        }

        fmt.Printf("%#v", users)
    }

    {
        _, err := db.Exec(`DELETE FROM users WHERE id = ?`, 1)
        if err != nil {
            log.Fatal(err)
        }
    }
}
```

# 5. Templates

## Introduction

Go’s `html/template` package provides a rich templating language for HTML templates. It is mostly used in web applications to display data in a structured way in a client’s browser. One great benefit of Go’s templating language is the automatic escaping of data. There is no need to worry about XSS attacks as Go parses the HTML template and escapes all inputs before displaying it to the browser.

## First Template

Writing a template in Go is very simple. This example shows a TODO list, written as an unordered list (ul) in HTML. When rendering templates, the data passed in can be any kind of Go’s data structures. It may be a simple string or a number, it can even be nested data structure as in the example below. To access the data in a template the top most variable is access by `{{.}}`. The dot inside the curly braces is called the pipeline and the root element of the data.

```go
data := TodoPageData{
    PageTitle: "My TODO list",
    Todos: []Todo{
        {Title: "Task 1", Done: false},
        {Title: "Task 2", Done: true},
        {Title: "Task 3", Done: true},
    },
}
```

```html
<h1>{{.PageTitle}}</h1>
<ul>
    {{range .Todos}}
        {{if .Done}}
            <li class="done">{{.Title}}</li>
        {{else}}
            <li>{{.Title}}</li>
        {{end}}
    {{end}}
</ul>
```

## Control Structures

The templating language contains a rich set of control structures to render your HTML. Here you will get an overview of the most commonly used ones. To get a detailed list of all possible structures visit: [text/template](https://golang.org/pkg/text/template/#hdr-Actions)

Control Structure

Definition

`{{/* a comment */}}`

Defines a comment

`{{.}}`

Renders the root element

`{{.Title}}`

Renders the “Title”-field in a nested element

`{{if .Done}} {{else}} {{end}}`

Defines an if-Statement

`{{range .Todos}} {{.}} {{end}}`

Loops over all “Todos” and renders each using `{{.}}`

`{{block "content" .}} {{end}}`

Defines a block with the name “content”

## Parsing Templates from Files

Template can either be parsed from a string or a file on disk. As it is usually the case, that templates are pares from disk, this example shows how to do so. In this example there is a template file in the same directory as the Go program called `layout.html`.

```go
tmpl, err := template.ParseFiles("layout.html")
// or
tmpl := template.Must(template.ParseFiles("layout.html"))
```

## Execute a Template in a Request Handler

Once the template is parsed from disk it’s ready to be used in the request handler. The `Execute` function accepts an `io.Writer` for writing out the template and an `interface{}` to pass data into the template. When the function is called on an `http.ResponseWriter` the Content-Type is header is automatically set in the HTTP response to `Content-Type: text/html; charset=utf-8`.

```go
func(w http.ResponseWriter, r *http.Request) {
    tmpl.Execute(w, "data goes here")
}
```

## The Code (for copy/paste)

This is the complete code that you can use to try out the things you’ve learned in this example.

```go
package main

import (
    "html/template"
    "net/http"
)

type Todo struct {
    Title string
    Done  bool
}

type TodoPageData struct {
    PageTitle string
    Todos     []Todo
}

```

```html
<h1>{{.PageTitle}}</h1>
<ul>
    {{range .Todos}}
        {{if .Done}}
            <li class="done">{{.Title}}</li>
        {{else}}
            <li>{{.Title}}</li>
        {{end}}
    {{end}}
</ul>
```

# 6. Assets and Files

## Assets and Files

This example will show how to serve static files like CSS, JavaScript or images from a specific directory.

```go
// static-files.go
package main

import "net/http"

func main() {
    fs := http.FileServer(http.Dir("assets/"))
    http.Handle("/static/", http.StripPrefix("/static/", fs))

    http.ListenAndServe(":8080", nil)
}
```

```sh
$ tree assets/
assets/
└── css
    └── styles.css
```

```sh
$ go run static-files.go

$ curl -s http://localhost:8080/static/css/styles.css
body {
    background-color: black;
}
```

# 7. Forms

## Forms

This example will show how to simulate a contact form and parse the message into a struct.

```go
// forms.go
package main

import (
    "html/template"
    "net/http"
)

type ContactDetails struct {
    Email   string
    Subject string
    Message string
}

func main() {
    tmpl := template.Must(template.ParseFiles("forms.html"))

    http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
        if r.Method != http.MethodPost {
            tmpl.Execute(w, nil)
            return
        }

        details := ContactDetails{
            Email:   r.FormValue("email"),
            Subject: r.FormValue("subject"),
            Message: r.FormValue("message"),
        }

        // do something with details
        _ = details

        tmpl.Execute(w, struct{ Success bool }{true})
    })

    http.ListenAndServe(":8080", nil)
}
```

```html
<!-- forms.html -->
{{if .Success}}
    <h1>Thanks for your message!</h1>
{{else}}
    <h1>Contact</h1>
    <form method="POST">
        <label>Email:</label><br />
        <input type="text" name="email"><br />
        <label>Subject:</label><br />
        <input type="text" name="subject"><br />
        <label>Message:</label><br />
        <textarea name="message"></textarea><br />
        <input type="submit">
    </form>
{{end}}
```

```console
$ go run forms.go
```

# 8. Middleware (Basic)

## Middleware (Basic)

This example will show how to create basic logging middleware in Go.

A middleware simply takes a `http.HandlerFunc` as one of its parameters, wraps it and returns a new `http.HandlerFunc` for the server to call.

```go
// basic-middleware.go
package main

import (
    "fmt"
    "log"
    "net/http"
)

func logging(f http.HandlerFunc) http.HandlerFunc {
    return func(w http.ResponseWriter, r *http.Request) {
        log.Println(r.URL.Path)
        f(w, r)
    }
}

func foo(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintln(w, "foo")
}

func bar(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintln(w, "bar")
}

func main() {
    http.HandleFunc("/foo", logging(foo))
    http.HandleFunc("/bar", logging(bar))

    http.ListenAndServe(":8080", nil)
}
```

```sh
$ go run basic-middleware.go
2017/02/10 23:59:34 /foo
2017/02/10 23:59:35 /bar
2017/02/10 23:59:36 /foo?bar

$ curl -s http://localhost:8080/foo
$ curl -s http://localhost:8080/bar
$ curl -s http://localhost:8080/foo?bar
```

# 9. Middleware (Advanced)

This example will show how to create a more advanced version of middleware in Go.

A middleware in itself simply takes a `http.HandlerFunc` as one of its parameters, wraps it and returns a new `http.HandlerFunc` for the server to call.

Here we define a new type `Middleware` which makes it eventually easier to chain multiple middlewares together. This idea is inspired by Mat Ryers’ talk about Building APIs. You can find a more detailed explaination including the talk [here](https://medium.com/@matryer/writing-middleware-in-golang-and-how-go-makes-it-so-much-fun-4375c1246e81).

This snippet explains in detail how a new middleware is created. In the full example below, we reduce this version by some boilerplate code.

```go
func createNewMiddleware() Middleware {
    // Create a new Middleware
    middleware := func(next http.HandlerFunc) http.HandlerFunc {
        // Define the http.HandlerFunc which is called by the server eventually
        handler := func(w http.ResponseWriter, r *http.Request) {
            // ... do middleware things
            // Call the next middleware/handler in chain
            next(w, r)
        }
        // Return newly created handler
        return handler
    }
    // Return newly created middleware
    return middleware
}
```

  
This is the full example:

```go
// advanced-middleware.go
package main

import (
    "fmt"
    "log"
    "net/http"
    "time"
)

type Middleware func(http.HandlerFunc) http.HandlerFunc

// Logging logs all requests with its path and the time it took to process
func Logging() Middleware {
    // Create a new Middleware
    return func(f http.HandlerFunc) http.HandlerFunc {
        // Define the http.HandlerFunc
        return func(w http.ResponseWriter, r *http.Request) {
            // Do middleware things
            start := time.Now()
            defer func() { log.Println(r.URL.Path, time.Since(start)) }()
            // Call the next middleware/handler in chain
            f(w, r)
        }
    }
}

// Method ensures that url can only be requested with a specific method, else returns a 400 Bad Request
func Method(m string) Middleware {

    // Create a new Middleware
    return func(f http.HandlerFunc) http.HandlerFunc {
        // Define the http.HandlerFunc
        return func(w http.ResponseWriter, r *http.Request) {
            // Do middleware things
            if r.Method != m {
                http.Error(w, http.StatusText(http.StatusBadRequest), http.StatusBadRequest)
                return
            }
            // Call the next middleware/handler in chain
            f(w, r)
        }
    }
}

// Chain applies middlewares to a http.HandlerFunc
func Chain(f http.HandlerFunc, middlewares ...Middleware) http.HandlerFunc {
    for _, m := range middlewares {
        f = m(f)
    }
    return f
}

func Hello(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintln(w, "hello world")
}

func main() {
    http.HandleFunc("/", Chain(Hello, Method("GET"), Logging()))
    http.ListenAndServe(":8080", nil)
}
```

```sh
$ go run advanced-middleware.go
2017/02/11 00:34:53 / 0s

$ curl -s http://localhost:8080/
hello world

$ curl -s -XPOST http://localhost:8080/
Bad Request
```

# 10. Sessions

This example will show how to store data in session cookies using the popular [gorilla/sessions](https://github.com/gorilla/sessions) package in Go.

Cookies are small pieces of data stored in the browser of a user and are sent to our server on each request. In them, we can store e.g. whether or not a user is logged in into our website and figure out who he actually is (in our system).

In this example we will only allow authenticated users to view our secret message on the `/secret` page. To get access to it, the will first have to visit `/login` to get a valid session cookie, which logs him in. Additionally he can visit `/logout` to revoke his access to our secret message.

```go
// sessions.go
package main

import (
    "fmt"
    "net/http"

    "github.com/gorilla/sessions"
)

var (
    // key must be 16, 24 or 32 bytes long (AES-128, AES-192 or AES-256)
    key = []byte("super-secret-key")
    store = sessions.NewCookieStore(key)
)

func secret(w http.ResponseWriter, r *http.Request) {
    session, _ := store.Get(r, "cookie-name")

    // Check if user is authenticated
    if auth, ok := session.Values["authenticated"].(bool); !ok || !auth {
        http.Error(w, "Forbidden", http.StatusForbidden)
        return
    }

    // Print secret message
    fmt.Fprintln(w, "The cake is a lie!")
}

func login(w http.ResponseWriter, r *http.Request) {
    session, _ := store.Get(r, "cookie-name")

    // Authentication goes here
    // ...

    // Set user as authenticated
    session.Values["authenticated"] = true
    session.Save(r, w)
}

func logout(w http.ResponseWriter, r *http.Request) {
    session, _ := store.Get(r, "cookie-name")

    // Revoke users authentication
    session.Values["authenticated"] = false
    session.Save(r, w)
}

func main() {
    http.HandleFunc("/secret", secret)
    http.HandleFunc("/login", login)
    http.HandleFunc("/logout", logout)

    http.ListenAndServe(":8080", nil)
}
```

```sh
$ go run sessions.go

$ curl -s http://localhost:8080/secret
Forbidden

$ curl -s -I http://localhost:8080/login
Set-Cookie: cookie-name=MTQ4NzE5Mz...

$ curl -s --cookie "cookie-name=MTQ4NzE5Mz..." http://localhost:8080/secret
The cake is a lie!
```

# 11. JSON

This example will show how to encode and decode JSON data using the `encoding/json` package.

```go
// json.go
package main

import (
    "encoding/json"
    "fmt"
    "net/http"
)

type User struct {
    Firstname string `json:"firstname"`
    Lastname  string `json:"lastname"`
    Age       int    `json:"age"`
}

func main() {
    http.HandleFunc("/decode", func(w http.ResponseWriter, r *http.Request) {
        var user User
        json.NewDecoder(r.Body).Decode(&user)
        fmt.Fprintf(w, "%s %s is %d years old!", user.Firstname, user.Lastname, user.Age)
    })
    http.HandleFunc("/encode", func(w http.ResponseWriter, r *http.Request) {
        peter := User{
            Firstname: "John",
            Lastname:  "Doe",
            Age:       25,
        }
        json.NewEncoder(w).Encode(peter)
    })

    http.ListenAndServe(":8080", nil)
}
```

```sh
$ go run json.go

$ curl -s -XPOST -d'{"firstname":"Elon","lastname":"Musk","age":48}' http://localhost:8080/decode
Elon Musk is 48 years old!

$ curl -s http://localhost:8080/encode
{"firstname":"John","lastname":"Doe","age":25}
```

# 12. Websockets

This example will show how to work with websockets in Go. We will build a simple server which echoes back everything we send to it. For this we have to `go get` the popular [gorilla/websocket](https://github.com/gorilla/websocket) library like so:

`$ go get github.com/gorilla/websocket`

From now on, every application we write will be able to make use of this library.

```go
// websockets.go
package main

import (
    "fmt"
    "net/http"

    "github.com/gorilla/websocket"
)

var upgrader = websocket.Upgrader{
    ReadBufferSize:  1024,
    WriteBufferSize: 1024,
}

func main() {
    http.HandleFunc("/echo", func(w http.ResponseWriter, r *http.Request) {
        conn, _ := upgrader.Upgrade(w, r, nil) // error ignored for sake of simplicity
        for {
            // Read message from browser
            msgType, msg, err := conn.ReadMessage()
            if err != nil {
                return
            }
            // Print the message to the console
            fmt.Printf("%s sent: %s\n", conn.RemoteAddr(), string(msg))
            // Write message back to browser
            if err = conn.WriteMessage(msgType, msg); err != nil {
                return
            }
        }
    })
    http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
        http.ServeFile(w, r, "websockets.html")
    })
    http.ListenAndServe(":8080", nil)
}
```

```html
<!-- websockets.html -->
<input id="input" type="text" />
<button onclick="send()">Send</button>
<pre id="output"></pre>
<script>
    var input = document.getElementById("input");
    var output = document.getElementById("output");
    var socket = new WebSocket("ws://localhost:8080/echo");

    socket.onopen = function () {
        output.innerHTML += "Status: Connected\n";
    };
    socket.onmessage = function (e) {
        output.innerHTML += "Server: " + e.data + "\n";
    };
    function send() {
        socket.send(input.value);
        input.value = "";
    }
</script>
```

```sh
$ go run websockets.go
[127.0.0.1]:53403 sent: Hello Go Web Examples, you're doing great!
```

# 13. Password Hashing (bcrypt)

This example will show how to hash passwords using bcrypt. For this we have to `go get` the golang bcrypt library like so:

`$ go get golang.org/x/crypto/bcrypt`

From now on, every application we write will be able to make use of this library.

```go
// passwords.go
package main

import (
    "fmt"
    "golang.org/x/crypto/bcrypt"
)

func HashPassword(password string) (string, error) {
    bytes, err := bcrypt.GenerateFromPassword([]byte(password), 14)
    return string(bytes), err
}

func CheckPasswordHash(password, hash string) bool {
    err := bcrypt.CompareHashAndPassword([]byte(hash), []byte(password))
    return err == nil
}

func main() {
    password := "secret"
    hash, _ := HashPassword(password) // ignore error for the sake of simplicity
    fmt.Println("Password:", password)
    fmt.Println("Hash:    ", hash)
    match := CheckPasswordHash(password, hash)
    fmt.Println("Match:   ", match)
}
```

```sh
$ go run passwords.go
Password: secret
Hash:     $2a$14$ajq8Q7fbtFRQvXpdCq7Jcuy.Rx1h/L4J60Otx.gyNLbAYctGMJ9tK
Match:    true
	```