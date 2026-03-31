| TCP/IP Layer | Communication Type           | Protocol Examples   |
| ------------ | ---------------------------- | ------------------- |
| Application  | Application-to-Application   | HTTP, FTP, DNS      |
| Transport    | Process-to-Process           | TCP, UDP            |
| Network      | Host-to-Host, routing        | RIP, BGP, OSPF, IP  |
| Link         | Adjacent Nodes               | TDM, FDM, CDMA      |
| Physical     | Raw binary data transmission | CAN, USB, Bluetooth |
>[!summary] Transport Layer Purpose:
>Logical End Systems Communication
>- Hides network infrastructure details (topology, wire types, etc.);
>- “*Logical*”: an illusion of a direct hosts connection
>- “*End system*”: an Operating System and network application processes running on an end host;
>- “*Socket library*”: network programming library in many programming languages

## Sockets: Application/Transport Layer Interface
![](Pasted%20image%2020260331073023.png)

- Every socket is associated with a port number and an IP address;
- Multiple sockets can correspond to a same port (e.g. to handle HTTP requests from multiple clients)


## Socket Programming
for the development of network apps by using socket libraries

**Socket Libraries:**
- For network applications development
- Hide many network aspects
- Introduced in Berkley Software Distribution (BSD) UNIX 4.2 and treated as files
- Implementation varies between Operating Systems

## Multiplexing and Demultiplexing
**Multiplexing**:
- Collecting messages from different processes through sockets;
- Appending transport layer headers;
- Segmentation: dividing messages into smalled portions

**Demultiplexing**:
- 
