- Has a protocol 'ws'. Like `ws://127.0.0.1`. Ayo what ?!
- In HTTP: request is sent, and server responds with a response. Then connection is terminated. WS is not like that
- Different from Long Polling. Long polling returns data in expected resource is not ready, e.g sleep(50). Then eventually responds and __closes__ the connection.
- Connection is persistent, does not terminate unless told otherwise
- Bi-directional
- Allows real time data flow
- Different with SSE being: SSE is single sided, server driven. Whereas web socket is duplex communication where both parties may trigger certain events.
- Web socket connections are established/initiated over HTTP but later upgraded to some custom TCP layer protocol afterwards. This upgrade is made by http header.
- In traditional HTTP request, every single data (cookies, tokens, parameters etc.) is sent in header with each request. Therefore http is stateless. Each request is unaware of other requests. On the other hand, web sockets are stateful. Header info is sent only once since communication is kept open.

Server-side Events (SSE)
- Header content type is text/event-stream
- In node.js you gotta use `response.write(data:data)` in order to keep the connection open. If you use `response.send()` or `response.end()` communication will end.
- Don't know if it's specific to node.js but you gotta stream responses with `data:*` notation
- Don't know if it's specific to node.js but the message should always end with \n\n.
- Limitation: When SSE is implemented over HTTP/1.1, it suffers from a limitation of maximum number of connections; which is 6. That means any website www.fake-dev.to can open upto 6 SSE connections in a browser(multiple tabs included). It's advised to use HTTP/2, which has default limit of 100, but can be configured.

JS (vanilla) client side implementation:
```
const sseClient = new EventSource(URL); // ayo what the hell is that
sseClient.onopen = () => console.log('Connection opened!');

sseClient.onmessage = (event) => console.log(event.data);

sseClient.onerror = () => console.log('Something went wrong!')

sseClient.close(); //when not needed anymore
```

You can also capture specific type of events by declaring `event:*`

Server side:
```
res.write("event: notification\ndata: New data!\n\n");
```

Client:
```
sseClient.addEventListener('notification', (event) => {
    console.log(event.data))
};
```


This one is a decent tool for testing realtime web sockets.
