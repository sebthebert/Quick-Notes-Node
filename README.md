# Quick-Notes-Node

Notes about Node.js

## Node Core

`process.argv`

```node
console.log(process.argv);
```

`process.stdout.write`
`process.stdin.on`
`process.on`

`setInterval`
`setTimeout`
`clearInterval`


## Web

### Request

```node
var https = require("https");

var options = {
  hostname:
  port:
  path:
  method
};

var req = https.request(options, function(res) {
  console.log(${res.statusCode});
  res.once("data", function(chunk) {
    console.log(chunk);
  });
  
  res.on("data", ...);
  
  res.on("end", ...);
  
});

req.on("error", ...);

```

### Server

```node
var http = require("http");

var server = http.createServer(function(req, res) {
  res.writeHead(200, {"Content-Type": "text/html"});
  res.end(`
  <html>
  ...${req.url}
  </html>
  `);
});

server.listen(3000);

```

## NPM

```shell
npm -v
npm install <package>
npm ls
npm remove

# install globaly
sudo npm install -g <package>
```

```
npm init

# Save <package> dependency in package.json
npm install <package> --save

# install dependencies specified in package.json
npm install

# Remove <package> dependency in package.json
npm remove <package> --save
```

### Interesting packages

```
http
node-dev
jshint
httpster

express
cors (Cross Origin Resource Sharing)
body-parser
```

## Express

```node
var express = require("express");
var cors = require("cors");
var bodyParser = require("body-parser");
var app = express();

app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: false }));

app.use(function(req, res, next) {
  # do stuff
  next();
});

app.use(express.static("./public"));

app.use(cors());

app.get("/path", function(req, res) {
  res.json(data);
});

app.post("/path", function(req, res) {
});

app.delete("/path", function(req, res) {
});

app.listen(3000);
```
