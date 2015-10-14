---
layout: post
tittle: "index"
date: 2015-10-14 19:10:57
---
# From Socket to Socket.io

Minchiuan Gao 2015-Oct

### 0. Client-Server Model And Network

all network applications are based on the same basic programming model, have similar overall logical structures, and rely on the same programming interface.(1)

Every network applicaiton is based on the client-server model.
With this model, an application consists of a *server* process and one or omre *client* process.

1. When a client needs service, it initiates a transaction by sending a request to the server. For example, when a Web browser needs a file, it sends a request to a Web server.
2. The server receives the request,interprets it,and manipulates its resourcesin the appropriate way. For example, when a Web server receives a request from a browser, it reads a disk file.
3. The server sends a response to the client, and then waits for the next request. For example, a Web server sends the file back to a client.
4. The client receives the response and manipulates it.Forexample,afteraWeb browser receives a page from the server, it displays it on the screen.

![Image of server four process](/assets/socket-four-steps.png)

**Noticw**: The clients and servers and process and not machines.  A single host could run many servers or clients, and a server or client cloud run at different hosts too.

**When regradless of the mapping of clients and servers to hosts. The client-server model is the same**.

To a host, a network is just another I/O device that servers as a source and sink for data.

### 1 The sockets Interface

The *sockets interfaces* is a set of functions that are userd in conjunction with the Unix I/O functions to build network applications. It has been implements on the most modern systems, including all Unix variants, Windows.

![get the socket hirechy](/assets/socket_hir.png)

{% highlight c%}
/* Generic socket address structure (for connect, bind, and accept) */
struct sockaddr {
    unsigned short  sa_family;   /* Protocol family */
    char            sa_data[14]; /* Address data.  */
};
/* Internet-style socket address structure */
struct sockaddr_in  {
    unsigned short  sin_family;  /* Address family (always AF_INET) */
    unsigned short  sin_port;    /* Port number in network byte order */
    struct in_addr  sin_addr;    /* IP address in network byte order */
    unsigned char   sin_zero[8]; /* Pad to sizeof(struct sockaddr) */
￼};
{% endhighlight %}

>> code snippet.


{% highlight c%}
/* The Code Snippet of Client Side */
char *host = argv[1];
int port = atoi(argv[2]);
clinetdf = Open_cliented(host, port);
Rio_readlinitb(&rio, clinented);

while(Fgets(buf, MAXLINE, stdin)!=NULL){
	Rio_written(cliented, buf, strlen(buf));
	Rio_readlineb(&rio, buf, MAXLINE);
	Fgets(buf, stdout);
}
{% endhighlight %}

Close(clientfd);

Server Side
{% highlight c%}
/* The Code Snippet of Server Side */
while (1) {
	clientlen = sizeof(clientaddr);
	connfd = Accept(listenfd, (SA *)&clientaddr, &clientlen);
	 /* Determine the domain name and IP address of the client */
	 hp = Gethostbyaddr((const char *)&clientaddr.sin_addr.s_addr,
	                        sizeof(clientaddr.sin_addr.s_addr), AF_INET);
	 haddrp = inet_ntoa(clientaddr.sin_addr);
	 printf("server connected to %s (%s)\n", hp->h_name, haddrp);
	 echo(connfd);
	 Close(connfd);
}
{% endhighlight %}

### 2 Web Socket (The socket for Web)

#### 2.1 Polling, Long Polling

What's polling: check the status of deveices or network, especially as part of a repeaed cycle.

If you want to get the most up-to-date "real-time" information, you can constantly refresh that page manually, but that's obviously not a great solution.

With *polling*, the browser sends HTTP request at regular intervals and immediatedly receives a response. It is a good solution if the exact interval of message delivery is know. However, real-time data is often not that predictable, making unnecessary requests inevitable and as a result, many connections are opened and closed needlessly in low-message-rate situations.

With *Long-polling*, the browser sends a requests to the server and the server keeps the requeset open for a set period. If a notification is received within that period, a response containing the message is sent to the client. If a notification is not received within the set time period, the server sends a response to terminate the open request.

Long polling is difficult to implement well.

Ultimately, all of these methods for providing real-time data involve HTTP request and response headers, which contain lots of additional, unnecessary header data and introduce latency. On top of that, full-duplex connectivity requires more than just the downstream connection from server to client. In an effort to simulate full-duplex communication over half-duplex HTTP, many of today's solutions use two connections: one for the downstream and one for the upstream.

The maintenance and coordination of these two connections introduces significant overhead in terms of resource consumption and adds lots of complexity.

*Simply put, HTTP wasn't designed for real-time, full-duplex communication*

>> Short Polling
{% highlight python%}
while true:
	C ==> Is there any cake?
	S ==> No, wait
	C ==> Is there any cake?
	S ==> No, wait
	C ==> Is there any cake?
	S ==> Yes, there is one!
	C ==> Is there any cake?
	...
{% endhighlight %}

>> Long Polling:
{% highlight python%}
C ==> Is there any cake?
# waiting for seconds and cook cook a new cake)
S ==> Yeah, there is one.
{% endhighlight %}
>> eat up your resources


With polling it makes unnecessary requests and, as a result, many connnections are opened and closed needlessly in low-message-rate situation. 

Web Sockets remove the overhead and dramatically reduce complexity.

#### 2.2 The Websocket is coming

To establish a WebSocket connection, the client and server upgrade from the HTTP protocol to the WebSocket protocol during their initial handshake, as shown in the following example:

{% highlight html %}
GET /text HTTP/1.1
Upgrade: WebSocket
Connection: Upgrade
Host: www.websocket.org
…\r\n 
HTTP/1.1 101 WebSocket Protocol Handshake
Upgrade: WebSocket
Connection: Upgrade
{% endhighlight %}

Once established, WebSocket data frames can be sent back and forth between the client and the server in full-duplex mode. Both text and binary frames can be sent full-duplex, in either direction at the same time.


#### The Advantage of WebSocket

1	WebSocket is a naturally *full-duplex*, bidirectional, single-socket connection. With WebSocket, your HTTP request becomes a single request to open a WebSocket connection and reuses the same connection from the client to the server, and the server to the client.

2	WebSocket reduces latency. For example, unlike polling, WebSocket makes a single request. The server does not need to wait for a request from the client. Similarly, the client can send messages to the server at any time. This single request greatly reduces latency over polling, which sends a request at intervals, regardless of whether messages are available.

3	WebSocket makes real-time communication much more efficient. You can always use polling (and sometimes even streaming) over HTTP to receive notifications over HTTP. However, WebSocket saves bandwidth, CPU power, and latency. WebSocket is an innovation in performance.

4	WebSocket is an underlying network protocol that enables you to build other standard protocols on top of it.

#### What's the Socket io

Uses the WebSocket portocol with polling as a fallback option, while providing the same interface, and simplify it.

And provide more features, including broadcasting to mutiple sockets, storing data associtaed with each client, and asynchronous I/O.

{% highlight html%}
<script src="https://cdn.socket.io/socket.io-1.2.0.js"></script>
<script src="http://code.jquery.com/jquery-1.11.1.js"></script>
<script>
  var socket = io();
  $('form').submit(function(){
    socket.emit('chat message', $('#m').val());
    $('#m').val('');
    return false;
  });
</script>

{% endhighlight %}

{% highlight js%}
io.on('connection', function(socket){
  socket.on('chat message', function(msg){
    console.log('message: ' + msg);
  });
});

io.on('connection', function(socket){
  socket.on('chat message', function(msg){
    io.emit('chat message', msg);
  });
});
{% endhighlight %}

### Reference
[1]. CSAPP[Chapter 11, Network Programming, Computer Systems: A porgrammer's Perspective, Randal E. Bryant and David R. O'Hallaron, Carnegie Mellon University](http://csapp.cs.cmu.edu/)

[2]. Stackoverflow [What's the difference with Websocket and socketio](http://stackoverflow.com/questions/10112178/differences-between-socket-io-and-websockets)

[3]. Wikipade [socket.io](https://en.wikipedia.org/wiki/Socket.IO)

[4]. Websocket Offical Site [A Quantum Leap in Scalability for the Web](https://www.websocket.org/quantum.html)
