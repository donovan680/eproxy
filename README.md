eproxy is a simple epoll based efficient TCP proxy for Linux
It connects two TCP ports to each other and communicates zero copy.

It is not trying to compete with the "big boy" load balancers, 
but is very easy to adapt for experiment. It should be fairly
efficient however.

Simple port forwarder

	proxy inport outip outport

Uses pipes to splice two sockets together. This should give something
approaching zero copy, if the NIC driver is capable. 

This method is rather file descriptor intensive (4 fds/conn), so make sure you 
have enough. 

This is a simple Port forwarder program using ZERO COPY ..
( splice() ) 
I will use it as Load balancer for HTTP connection 
---1 > You need to add little code to retrieve HTTP request header COOKIE from the incoming http connection.... say I have 10 HTTP servers.....
You will maintain a C++ STL MAP.... which will have HASH VALUE of cookie as a key and SERVER IP as Value You need to write a small method which will generate HASH value from 0-9 for all fetched cookie. -------------------------------------------------------- 
1. It will fetch cookie from HEADER 
2. Generate hash 0 - 9 integer value ( pls make it variable so that I can increase it when my http server count will be increased) 
3. using above hash value it will get outgoing server IP from STL MAP to connect ----------- It will ensure that connection with same cookie always go to same HTTP server.....otherwise session will not maintain.. ==============================================
I have attached a black image above you need to fix the CRASH......
it is happening during idle connection deletion the program is using splice()....
for better performance we will use read() method just to read the header value to get cookie ....
after that we need to write the header to socket using write() as that splice() will take care all transfer as usual there a method called tree() ..it fetch data but does not consume... splice() fetch and consume ..both //

sample get header GET / HTTP/1.1 
Host: myhost.com Connection: Keep-Alive Accept: text/html, image/gif, image/jpeg, image/req-fpost2, *; 
q=.2, */*; 
q=.2 User-Agent: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; Proxy-Connection: Keep-Alive Accept: image/fpost2, *; 
q=.2, */*; 
q=.2 Cache-Control: no-store Pragma: no-cache Expires: Fri, 01 Jan 1990 00:00:00 GMTCookie: namex==UTO5kjNyojbp1GZhpjM4ETOyIjNzQjMwYTM 

POST / HTTP/1.1Host: myhost.comConnection: Keep-AliveAccept: text/html, image/gif, image/jpeg, image/req-fpost2, *; q=.2, */*; q=.2User-Agent: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;Proxy-Connection: Keep-AliveAccept: image/fpost2, *; q=.2, */*; q=.2Cache-Control: no-storePragma: no-cacheContent-Length: 2Expires: Fri, 01 Jan 1990 00:00:00 
GMTContent-Type: application/octet-streamCookie: namex==UTO5kjNyojbp1GZhpjM4ETOyIjNzQjMwYTMaa ================ //
Return till \r\n\r\n
int getHTTPHeader(char * buf, int sock) 
{ 
int success = 0; 
int buf_idx = 0; 
     while (buf_idx < BUFSIZE && 1 == read(sock, buf + buf_idx, 1)) 
      { 
       if (buf_idx > 2 && '\n' == * (buf + buf_idx - 0) && '\r' == * (buf + buf_idx - 1) && '\n' == * (buf + buf_idx - 2) && '\r' == * (buf + buf_idx - 3)) 
       { 
        success = 1; buf_idx++; 
	*(buf + buf_idx) = '\0'; break; 
       } 
       buf_idx++; 
    } 
       return success;
 } 
 =====..equal distribution is a problem but please make sure connections having SAME COOKIE value go to same Destination server. (sum)%10 is very bad..I tested already... RAMDOM () distribution is very perfect... but please make sure connections having SAME COOKIE value go to same Destination server. 
 Please use RANDOM() distribution but if same cookie already active ..
 we need to pick up the same IP ==================================================================================  it will be used instead of HAPROXY....... 
 and expecting good load ..it will be a new experience.. 
