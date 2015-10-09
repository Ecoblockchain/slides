# Chat server with nicknames.

Let's expand on out last example and add nickname support to our chat server. The use case is essentially the same, expect
that when you run the client, you should pass an argument indicating your nickname. When the client sends information to
the server, it should include the given nickname as well as the message. The server should then send the message and the 
nickname to each client.

## Tips

You can build up on the solution for problem 2 to solve this problem. One important thing to note is that we now need to send
structured information to the server in order to be able to send more than just the message. We can of course use JSON for
this, but instead of encoding and decoding the messages everytime we send info to the server, we can use a module to help
us out with that. It's called `duplex-json-stream` and you can use it to wrap a stream so that it turns it into an `object`
stream. So for example if you do this

```js
socket = jsonStream(socket)
```
Now you can do the following

```js
socket.write({username: username, message: message})
```

and when you do
```js
socket.on('data', function(data) {...})
```
`data` is an object instead of a string.

You obviously need to use this module in both the client and the server.

## Testing.

Open 3 terminals, run "node server.js" on one of them and "node client.js" on the other 2. Clients should be able to chat
and you should be able to see the nicknames of the clients.
