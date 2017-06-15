# Integration Party

## Plan

We're trying to get a lot done in just a few hours, so we need to be quite organized and focused. Here is the plan: 

* Step 0
  * Make sure all the tools we need work in their basic configuration
* Step 1: 
  * Basic HTML/CSS (bootstrap)/JavaScript (no framework, using fetch) page that maintains and displays a list of messages as they’re being sent from a single page. 
  * At this point, it’s a client-only app that works on a single user’s browser tab
* Step 2: build a simple SMS client for the Twilio API
  * Install Node
  * Send a test SMS using the Twilio NodeJS library
  * Extend to be able to receive a message on the server
  * Extend to be able to read the received message and display it on the console
* Step 3: add a new endpoint to our Node server to handle messages from the  web page we created in Step 1
  * Set up simple GET endpoint
  * Read query parameter
  * Create data structure on the server to keep track of all received messages
* Step 4: add a new endpoint that returns a list of all messages received by the server
  * Set up another simple GET endpoint
  * Return a JSON response with the list of messages
  * At this point, we can receive messages from multiple clients and each client can display a history of all messages
* Step 5: Twilio integration! 
  * Apply what we learned from the previous steps to make the function that receives the text messages save each text message in the list of messages on the server
  * Magic! Now we can send an SMS message to our number and have it show up on the web app as part of the history with all the other messages

## Step 0: Foundation

As always, we want to test things when there is the least amount of moving variables possible. Here, it means we need to make sure our utilities work prior to adding any custom code. 

* Make sure node is installed and configured properly by running `node --version` on your terminal - that should give you a version number back

* Start a new terminal window and run `ngrok http 1337` - that should give you an output like this: 

```
ngrok by @inconshreveable                                                                                                                       (Ctrl+C to quit)

Session Status                online
Version                       2.2.4
Region                        United States (us)
Web Interface                 http://127.0.0.1:4040
Forwarding                    http://5d7b4bef.ngrok.io -> localhost:1337
Forwarding                    https://5d7b4bef.ngrok.io -> localhost:1337

Connections                   ttl     opn     rt1     rt5     p50     p90
                              0       0       0.00    0.00    0.00    0.00
```

We will go over what ngrok does and why we need it later

* Create a new git repo and start up your favorite editor - we're ready to go! 

## Step 1: Client-side HTML/CSS/JavaScript

Let's create 3 basic files for our "static" HTML project: 

* index.html
* webchat.js

We're going to use bootstrap to get easy formatting. Here is a baseline for index.html: 

```
<!DOCTYPE html>
<html lang="en-US">

<link rel="stylesheet" href="bootstrap.min.css">
<link rel="stylesheet" href="webchat.css">
<script src="webchat.js"></script>

<body>

<div class="container">

    <div class="jumbotron">
        <h1>Integration Party</h1>
        <h3>First we zig. Then we zag. Then we zigzag!</h3>

        <div class="progressBar">

            <div class="progress-bar progress-bar-striped active" role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" style="width: 100%">
                <span class="sr-only">In Progress</span>
            </div>
        </div>
    </div>

    <div class="panel panel-default">
        <div class="panel-heading">
            <h3 class="panel-title">Enter Message</h3>
        </div>
        <div class="panel-body">

            <div class="row">
                <div class="col-lg-10">
                    <div class="input-group">
                      <span class="input-group-addon" id="basic-addon1">Message</span>
                      <input id='user-message' type="text" class="form-control" placeholder="Enter message here" aria-describedby="basic-addon1">
                    </div>
                </div>
                <div class="col-lg-2">
                    <a class="btn btn-primary btn-lg" onclick="sendMessage()">Send</a>
                </div>
            </div><!-- /.row -->

            <div class="row">
                <div class="col-lg-2">
                    <a class="btn btn-primary btn-lg" onclick="testFetch()">Test</a>
                </div>
            </div>

        </div>
    </div>

    <div class="panel panel-default">
        <div class="panel-heading">
            <h3 class="panel-title">Message History</h3>
        </div>
        <div class="panel-body">
            <ul class="list-group" id="message-history">
              <li class="list-group-item">Cras justo odio</li>
              <li class="list-group-item">Dapibus ac facilisis in</li>
              <li class="list-group-item">Morbi leo risus</li>
              <li class="list-group-item">Porta ac consectetur ac</li>
              <li class="list-group-item">Vestibulum at eros</li>
            </ul>
        </div>
    </div>

</div>


</body>
</html>

```

We are not using any framework for the JavaScript portion of this exercise. Here is the baseline for webchat.js: 

```
console.log("Webchat client is running ..."); 

function test() { 
	console.log("Testing ..."); 
}

function sendMessage() { 
	var userMessage = document.getElementById('user-message').value; 
	console.log("About to send " + userMessage); 
}

```

As you can see, it's all pretty simple, but it should allow us to validate that 

* Our styling is working
* Our JavaScript is working 

## Step 2: Twilio

We're going to leave the standalone app for a few minutes and get a standalone Twilio application going. Then we'll see what we need to do in order to integrate them together. 

Node is a JavaScript engine that allows us to run JavaScript code outside of the browser. If you have a JavaScript file, you can run it with the `node name-of-file.js` command

Try it with your `webchat.js` file

In order to have a useful server, we need a few Node components, so let's run the following commands: 

* Initialize a new node project: `npm init`
* Install the Twilio client helper library: `npm install twilio --save`
* Install Express, which is a framework that allows us to have a server listening on a specific port (more on that below): `npm install express --save`

Now we can test the basic Twilio functionality with a new file `send-sms.js`: 

```
// Twilio Credentials 
// (replace with yours)
var accountSid = 'xxxxxxx'; 
var authToken = 'yyyyyyy'; 
 
//require the Twilio module and create a REST client 
var client = require('twilio')(accountSid, authToken); 
 
client.messages.create({ 
	// replace with your numbers
    to: "+170xxxxx", 
    from: "+1404xxxx", 
    body: "I feel an integration party brewing!", 
}, function(err, message) { 
    console.log(message.sid); 
});

```

## Sideline: networking 101

* Internet
* IP network
* Public vs private IPs

## Steps 4 and 4: Web Services

## Step 5: Integration Time

