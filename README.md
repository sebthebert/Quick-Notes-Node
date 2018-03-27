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

## WebSockets

Server:
```node
var WebSocketServer = require("ws").Server;

var wss = new WebSocketServer({ port: 3000 });
wss.on("connection", function(ws) {
  ws.on("message", function(message) {
    if (message === 'exit')
    {
      ws.close();
    }
    else
    {
      wss.clients.forEach(function(client) {
        client.send(message);
      });
    }
  });
  
  ws.send('welcome');
});
```

Client:
```node
var ws = new WebSocket("ws://localhost:3000");

ws.onopen = function() {
};

ws.onclose = function() {
};

ws.onmessage = function(payload) {
   #payload.data
};
```

## Testing Debugging

### Mocha & Chai

```
npm install chai --save-dev
```

Run in 'test' directory
```node
var expect = require("chai").expect;
var myTools = require("../lib/tools");

describe("myTools", function() {

  describe("myFunc()", function() {
    it("should do something", function() {
      var results = tools.myFunc(params);
      expect(results).to.equal(something);
    });
  });
  
  describe("myFunc2()", function() {
  
    this.timeout(5000) #2000 ms by default
    it("should do something again", function(done) {
      var results = tools.myFunc(params);
      expect(results).to.be.ok;
      done();
    });
  });
  
});
```


### Nock

Nock to mock

```
npm install nock --save-dev
```

```
var nock = require("nock");

before(function() {
  nock(url)
    .get(path)
    .reply(200, "Mock");
});


### Rewire

Mocking data
```
npm install rewire --save-dev
```

```
var rewire = require("rewire");

var data = rewire("../lib/...");

beforeEach(function() {
  this.testData = [ 
    fakedata 
    ];
  data.__set__(data_in_rewired_module, this.testData); 
});
```
