# UDP Client-Server implementation in C

## Theory

In UDP, the client does not form a connection with the server like in TCP and instead just sends a datagram.  
Similarly, the server need not accept a connection and just waits for datagrams to arrive.  
Datagrams upon arrival contain the address of the sender which the server uses to send data to the correct client.

![udp chart](img/udp-chart.png)

## The entire process can be broken down into the following steps: 

**UDP Server:**

1. Create a UDP socket
2. Bind the socket to the server address
3. Wait until the datagram packet arrives from the client
4. Process the datagram packet and send a reply to the client
5. Go back to Step 3

**UDP Client:**

1. Create a UDP socket
2. Send a message to the server
3. Wait until response from the server is received
4. Process reply and go back to step 2, if necessary
5. Close socket descriptor and exit

## Functions:

```
int socket (int domain, int type, int protocol)
```
Creates an unbound socket in the specified domain.  
Returns socket file descriptor.

**Arguments:**

- domain: Specifies the communication ( AF_INET for IPv4/ AF_INET6 for IPv6 )
- type: Type of socket to be created ( SOCK_STREAM for TCP / SOCK_DGRAM for UDP )
- protocol: Protocol to be used by the socket. 0 means use default protocol for the address family.

```
int bind (int sockfd, const struct sockaddr *addr, socklen_t addrlen)
```
Assigns address to the unbound socket.

**Arguments:**
- sockfd: File descriptor of a socket to be bonded 
- addr: Structure in which address to be bound to is specified 
- addrlen: Size of addr structure  

```
ssize_t sendto (int sockfd, const void *buf, size_t len, int flags,
                const struct sockaddr *dest_addr, socklen_t addrlen)
```
Send a message on the socket.

**Arguments:**

- sockfd: File descriptor of the socket 
- buf: Application buffer containing the data to be sent 
- len: Size of buf application buffer 
- flags: Bitwise OR of flags to modify socket behavior 
- dest_addr: Structure containing the address of the destination 
- addrlen: Size of dest_addr structure  

```
ssize_t recvfrom (int sockfd, void *buf, size_t len, int flags,
                 struct sockaddr *src_addr, socklen_t *addrlen)
```
Receive a message from the socket.

**Arguments:**

- sockfd: File descriptor of the socket 
- buf: Application buffer in which to receive data 
- len: Size of buf application buffer 
- flags: Bitwise OR of flags to modify socket behavior 
- src_addr: Structure containing source address is returned 
- addrlen: Variable in which size of src_addr structure is returned 

```
int close (int fd)
```
Close a file descriptor.

**Arguments:**

 - fd: File descriptor
