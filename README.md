Golang HTML5 SSE Example
========================

This is an minimalistic example of how to do
[HTML5 Server Side Events](http://en.wikipedia.org/wiki/Server-sent_events)
with [Go (golang)](http://golang.org/).  From the server's perspective,
SSE is nearly identical to long polling.  The client makes a GET request
that establishes a TCP connection.  The server keeps this connection open
and sends events to the client when they are available. In this example,
the server pushes a new event every five seconds, consting of a short
message with the current time.  Any number of clients can be
connected: they will all receive the same events if they're connected
concurrently.  (This is achived using Go's channels and a fan-out
pattern.  In other languages you may need to use some kind of pubsub
messaging, like Redis or Zeromq.)

The main advantage of HTML5 SSE over long polling is that there is a nice
API for it in modern browsers, so that you need not use iframes and such.
SSE is easier than Websockets in the sense that it communicates exclusively
over HTTP and therefore does not require a separate server.  Websockets,
however, supports two-way real-time communication between the client and
the server.

## Installing

Check out the repository from GitHub

	git clone https://github.com/kljensen/golang-html5-sse-example

## Running

To run the server, do 

	go run ./server.go

Then point your web browser to `http://localhost:8000`.
You should see output in the browser like the following:

	Yo Duder, here are some facinating messages about the current time:
	Message: 20 - the time is 2013-03-08 21:08:01.260967 -0500 EST
	Message: 21 - the time is 2013-03-08 21:08:06.262034 -0500 EST
	Message: 22 - the time is 2013-03-08 21:08:11.262608 -0500 EST
	Message: 23 - the time is 2013-03-08 21:08:16.263491 -0500 EST
	Message: 24 - the time is 2013-03-08 21:08:21.264218 -0500 EST
	Message: 25 - the time is 2013-03-08 21:08:26.264433 -0500 EST

And, you should see output in the terminal like the following

	2013/03/15 03:29:07 Sent message 0 to 0 attached clients
	2013/03/15 03:29:09 Added new client
	2013/03/15 03:29:11 Finished HTTP request at  /
	2013/03/15 03:29:11 Added new client
	2013/03/15 03:29:12 Sent message 1 to 2 attached clients
	2013/03/15 03:29:17 Sent message 2 to 2 attached clients
	2013/03/15 03:29:22 Sent message 3 to 2 attached clients
	2013/03/15 03:29:27 Sent message 4 to 2 attached clients
	2013/03/15 03:29:31 Finished HTTP request at  /
	2013/03/15 03:29:31 Added new client
	2013/03/15 03:29:32 Sent message 5 to 3 attached clients
	2013/03/15 03:29:37 Sent message 6 to 3 attached clients
	2013/03/15 03:29:42 Sent message 7 to 3 attached clients
	2013/03/15 03:29:47 Sent message 8 to 3 attached clients
	2013/03/15 03:29:52 Sent message 9 to 3 attached clients
	2013/03/15 03:29:57 Sent message 10 to 3 attached clients
	2013/03/15 03:29:57 Finished HTTP request at  /events/
	2013/03/15 03:29:57 Finished HTTP request at  /events/
	2013/03/15 03:29:57 Removed client
	2013/03/15 03:29:57 Removed client

## Thanks

This code is based off of a few sources, mostly

* [Leroy Campbell's SSE example in Go](https://gist.github.com/artisonian/3836281); and,
* the [HTML5Rocks SSE tutorial](http://www.html5rocks.com/en/tutorials/eventsource/basics/).

 
## License

Copyright (c) 2013 Kyle L. Jensen (kljensen@gmail.com)

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
