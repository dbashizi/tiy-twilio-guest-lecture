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

## Foundation

## 