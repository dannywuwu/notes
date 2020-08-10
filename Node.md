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