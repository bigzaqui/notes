##Java Jetty

- A Servlet is an object that receives a request and generates a response based on that request. 
- Stable, robust and scalable, dont be afraid to use in production
- One of the first Java HTTP servers

###1996 - today, events:
- Over time, it was discovered that I/O was limiting the performance
- Async was needed, (non blocking I/O)
- First problems on scability appeared, 10k concurrent users... Async was the solution
- Jetty is one of the first servers using Async, it managed to suspend/resume requests, so it scale well 
- Servlet 3.1 allows Async I/O, works like this:
	- my thread is replying to the client, and the client is bussy (buffer full), the thread is available for more work while the client becomes available
- Multicore CPU starts appearing, Jetty blocking adapts to use this, by reducing context switching, reduce full sharing, this is easy to see from jetty 8 to jetty 9, it gets a 30% performance boost

###Websotckets
- The web exploded around the last 5 years:
	- HTTP was not designed for this, no bidirectional, no multiplexing, no resource correlation
	-Use domain sharding to allow multiple TCP connections, because HTTP doesn't have multiplexing
	-Traditional http rendering was not enough, Websockets and SPDY were neccessary, so Servlet containers become polyglot, speaking these new protocols.
- Jetty implements websockets in 2009, pretty early in the market, so a lot of experience was gathered during the incoming years
- When benchmarking Websocket VS HTTP, the difference of latency/scale is absurd, 
- Websockets are a low level protocol, no longer reading HTTP responses :(
- Transparent proxies need to be aware of Websockets, otherwise they can just disregard the traffic... annoying

###SPDY
- Live experiment, Designed by Google, now all the big sites use it.
- Uses TLS so it hides the content of the HTTP request, proxies will see TLS and let it pass, the problem with dropping Websockets dissapears
- requests are all sent inside the "green pipes", and can be sent out of order
- SPDY push: removes RTT times by getting all the requirements with only requesting the Primary resource
	- Primary resource: index.html
	- Secondary resource: style.css, aplication.js...
	




###New concepts
- **False sharing**: lse sharing is a term which applies when threads unwittingly impact the performance of each other while modifying independent variables sharing the same cache line
- **implements runnable**: class made for threads, run() method is called on each thread.
- **CometD**: Open Web messaging protocol, using Websockets

###Resources
  - [jetty history video](https://www.youtube.com/watch?v=8QCC4HaSy58)
  - [HTTP2, websockets and SPDY](https://tpierrain.blogspot.se/2013/09/some-web-mechanical-sympathy-lets.html)
  
 