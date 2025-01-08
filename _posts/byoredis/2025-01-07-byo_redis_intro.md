# Introduction
### TCP Byte Stream and Protocol

A TCP connection produces **a continuous sequence of bytes, with no internal boundaries.**  Interpreting this byte stream is the job of an application protocol. 

### Data serialization

The message we want send via network can be an object, strings, structs, lists. However, computer network knows 0s and 1s only. 

The process of converting objects to byte stream is data **serialization** and from bytes to back to objects is called **deserialization**. 

### Concurrent Programming

Designing client is easier than a server. A client can connect to a server and then exchange information, but a server should handle multiple clients at a time. 

Modern solution to this problem is ***even based concurrency*** with ***event loops***.

## Network from Programmers point of view

### Layers of protocol

An IP Packet is just a message with some additional metadata. The tuple (src_ip, dst_ip) → represents flow of data between 2 machines. 

But there can be multiple applications on each host requiring multiple flows. So next layer of protocol (TCP,UDP) includes port number which multiplexes the data to the respective apps. 

The tuple (proto, src_ip, src_port, dst_ip, dst_port) identifies flow.

TCP and UDP adds new capability on top of IP (multiplexing).

### Requirements from the applications

Redis, HTTP/1.1 and most RPC protocols are ***request-response*** protocols. Each request message is associated with a response message. We are using TCP for this as this is reliable and ordered. 

### What is a Socket?

A socket is a *handle* to refer to a connection or something else. The API for networking is called the socket API, which is similar on different operating systems. 

On Linux, a ***file descriptor*** (just like an id / handle)is an integer which is used to represent a socket connection and it is local to the process. 

The `socket()` method allocates and return a socket fd - which is used to create connections.

### Listening and connecting

Creating a listening socket requires 3 API calls 

1. `socket()` - obtain a socket handle
2. `bind()`- set the listening IP:Port 
3. `listen()`- creates the listening socket

Then use `accept()` API to connect with the incoming connections. 

```cpp
// Pseudo code
fd = socket()
bind(fd, address)
listen(fd)
while True:
    conn_fd = accept(fd)
    do_something_with(conn_fd)
    close(conn_fd)
```

### Connection from a client

1. Obtain a socket handle via `socket()`.
2. Create the connection socket via `connect()`

```cpp
//Pseudo code
fd = socket()
connect(fd, address)
do_something_with(fd)
close(fd)
```

`socket()` creates a typeless socket; the socket type (listening or connection) is determined after the `listen()` or `connect()` call. The `bind()` between `socket()` and `listen()` merely sets a parameter. The `setsockopt()` API can set other socket parameters that will be used later.

`send()` and `recv()` - for byte stream based socket it appends to or consumes from the byte stream

`close()` is used to close the connection to release the resources.
