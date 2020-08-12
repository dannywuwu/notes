# Basic Server Setup

```js
const http = require('http');

// takes in request + response objects
const server = http.createServer((req, res) => {
    console.log('request made');
});

// port, hostname (localhost is default)
server.listen(3000, 'localhost', () => {
    console.log('listening for requests on port 3000');
})
```

# Requests & Responses

**Many of these functions can be managed through the Express package**

### `req.url`

- Returns the URL appended to the hostname (ex. `localhost:3000/home`)

### `req.method`

- Returns type of request (ex. `GET`)

## Writing Reponses

3 steps:

1. Set header content
2. Write browser response
3. End response

```js
const http = require('http');
const fs = require('fs');

// takes in request + response objects
const server = http.createServer((req, res) => {
    // set header content type
    res.setHeader('Content-Type', 'text/html');

    // send html file
    fs.readFile('./views/index.html', (err, data) => {
        if(err) {
            console.err(err);
            res.end();
        } else {
            // write html data
            // res.write(data);
            res.end(data); // shorthand
        }
    })
});

// port, hostname (localhost is default)
server.listen(3000, 'localhost', () => {
    console.log('listening for requests on port 3000');
})
```

## URL paths

```js
let path = './views/';
switch(req.url){
    case '/':
        path += 'index.html';
        res.statusCode = 200;
        break;
    case '/about':
        path += 'about.html';
        res.statusCode = 200;
        break;
    default:
        path += '404.html';
        res.statusCode = 404;
        break;
}
// send html file
fs.readFile(path, (err, data) => {
    ...
}
```

## Status Codes

- Describe response type sent to browser
    - 200 - OK
    - 301 - Redirect
    - 404 - Not found
    - 500 - Server error
- Set the responses in the switch statement (when we send the HTML pages)

### Redirects

```js
case '/about-me':
    res.statusCode = 301;
    res.setHeader('Location', '/about');
    res.end();
    break;
```

- Redirect `/about-me` to `/about`
    - In the switch statement, set the header to `('Location', '/about')`

# [Express](https://expressjs.com/)

```js
const express = require('express');

// express app
const app = express();

// listen for requests on port 3000
app.listen(3000);

// the below app.get functions are similar to a large switch statement in raw node

// home page
app.get('/', (req, res) => {
    // automatically sends header + status code
    // res.send('<p>html response</p>');
    // specify that the ./ root directory is the current directory (__dirname)
    res.sendFile('./views/index.html', { root: __dirname });
})

// about page
app.get('/about', (req, res) => {
    res.sendFile('./views/about.html', { root: __dirname });
})

// redirects
app.get('/about-us', (req, res) => {
    res.redirect('/about');
})

// default case (always runs if there is no match above)

// 404 page
app.use((req, res) => {
    res.status(404).sendFile('./views/404.html', { root: __dirname });
})
```

# View Engines

- Inject dynamic data into webpages

## [EJS](https://ejs.co/)

- Generate HTML with JavaScript
    - We can use EJS to display dynamic content
    - Replace `.html` with `.ejs`

```js
// app.js updated with view engine
const express = require('express');
const app = express();

// listen for requests on port 3000
app.listen(3000);

// register view engine
app.set('view engine', 'ejs');

// express looks for views inside the ejs-views folder
app.set('views', 'ejs-views');

// home page
app.get('/', (req, res) => {
    // pass in dynamic data as object
    res.render('index', { title: 'title' });
})

// 404 page
app.use((req, res) => {
    res.status(404).render('404', { title: '404' });
})
```

### Embed Javascript into `.ejs` files

```js
// write javascript
<% const name = 'korosensei' %>
// output variable
<%= name %> // korosensei
```

### Partials

- Reusable EJS components 

```js
// include the nav component 
<% - include('./partials/nav.ejs') %>
```

# Middleware

- Functions that run on the server between the requests going in and the responses going out
- They run top to bottom (similar to a switch statement)

`app.use()`, `app.get()`, are all examples of middleware

## `next`

```js
app.use((req, res, next) => {
    console.log('new request');
    console.log('host: ', req.hostname);
    console.log('path: ', req.path);
    console.log('method: ', req.method);
    next();
})
```

- As we are not returning a response back to the browser, the app hangs unless we use the `next()` function (similar to a `continue`)
- Continue on with the rest of the code