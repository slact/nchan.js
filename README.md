== NchanSubscriber.js

A Websocket, EventSource, and Long-Polling wrapper for [Nchan](https://nchan.slact.net)

```js
// CommonJS
let NchanSubscriber = require("nchan");

// you can also include the NchanSubscriber.js script directly in the browser.
// This will export NchanSubscriber as a global variable.

var sub = new NchanSubscriber(url, opt);

//options
opt = {
  subscriber: 'longpoll', 'eventsource', or 'websocket',
    //or an array of the above indicating subscriber type preference
  reconnect: undefined or 'session' or 'persist'
    //if the HTML5 sessionStore or localStore should be used to resume
    //connections interrupted by a page load
  shared: true or undefined
    //share connection to same subscriber url between browser windows and tabs 
    //using localStorage.
}


sub.on("message", function(message, message_metadata) {
  // message is a string
  // message_metadata is a hash that may contain 'id' and 'content-type'
});

sub.on('connect', function(evt) {
  //fired when first connected. 
});

sub.on('disconnect', function(evt) {
  // when disconnected.
});
 
sub.on('error', function(error_code or evt, error_description) {
  //error callback
});
 
sub.reconnect; // should subscriber try to reconnect? true by default.
sub.reconnectTimeout; //how long to wait to reconnect? does not apply to EventSource, which reconnects on its own.
sub.lastMessageId; //last message id. useful for resuming a connection without loss or repetition.

sub.start(); // begin (or resume) subscribing
sub.stop(); // stop subscriber. do not reconnect.
```
