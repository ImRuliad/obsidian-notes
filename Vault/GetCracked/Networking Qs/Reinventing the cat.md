
> [!NOTE] https://getcracked.io/question/1312/reinventing-the-cat?topic=Networking

*You want to get cat images from an HTTP website using POSIX networking functions. What would the right order of the calls be to properly get those cat images? Write the answer in the format abcdef, no spaces.*
```
getaddrinfo()  //a 
send()         //b 
recv()         //c 
socket()       //d 
connect()      //e 
close()        //f
```


> [!success] Answer
> First, you must resolve the hostname (eg, example.com) into a valid IP address. `getaddrinfo()` returns a linked list of possible address structs for that hostname. You must then create a socket using `socket()` with one of the returned addresses. Once a socket is formed, you then establish a TCP connection with `connect()` and then send the HTTP request (e.g., `GET /cat.jpg HTTP/1.1`) to the website using `send()`. Once the request is sent, you can do a `recv()` loop to retrieve data until the connection is closed by the server, and then call `close()` to release the socket.
