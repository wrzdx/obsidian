````col
```col-md
flexGrow=1
===
### HTTP: webpage retrieval
![](Pasted%20image%2020260330054706.png)

Request/Response paradigm: 
- A single request at a time; 
- Every request follows with a response
- Not optimal for large file transfers

![](Pasted%20image%2020260330054753.png)

- **HTTP server** – a software process running (at a specific port) on a server hardware, which understands and serves HTTP requests;
- **Web server** – a hardware machine (server) with all its software, hard drives, databases, etc.
```
```col-md
flexGrow=1
===
### FTP: large files tranfer
![](Pasted%20image%2020260330055530.png)

Connection types: 
- Control: commands and replies; 
- Data: file transfer
  
**Control Connection**
![](Pasted%20image%2020260330055353.png)

**Data download connection**
![](Pasted%20image%2020260330055448.png)
```
````

````col
```col-md
flexGrow=1
===

| Command | Action                                                                  |
| ------- | ----------------------------------------------------------------------- |
| GET     | Retrieves information by URI (Uniform Resource Identifier)              |
| HEAD    | Same as GET, but with no “Data” field                                   |
| POST    | Sends data to a server                                                  |
| DELETE  | Removes all resources for a given URI                                   |
| CONNECT | Establishes connection to a server                                      |
| OPTIONS | Specifies communication options                                         |
| TRACE   | Performs a message loop-back test along the path to the target resource |

```
```col-md
flexGrow=1
===

| Command | Action                                 |
| ------- | -------------------------------------- |
| RETR    | Copy file                              |
| DELE    | Delete file                            |
| DSIZ    | Get directory size                     |
| MKD     | Make directory                         |
| TYPE    | Sets file transfer mode (ASCII/Binary) |
| THMB    | Get a thumbnail of a remote image file |
| ABOR    | Abort an active file transfer          |
| QUIT    | Disconnect                             |

```
````

````col
```col-md
flexGrow=1
===

| Response Code | Meaning                                                                  |
| ------- | ----------------------------------------------------------------------- |
| 1xx     | Informational Messages              |
| 2xx    | Successful                                   |
| 3xx    | Redirection                                                  |
| 4xx  | Client Errors                                   |
| 5xx | Server Errors                                      |

```
```col-md
flexGrow=1
===

| Response Code | Meaning                                 |
| ------- | -------------------------------------- |
| 1xx    | Positive preliminary reply (success. start)                              |
| 2xx    | Positive completion reply (success. finish)                           |
| 3xx    | Positive intermediate reply (command accepted, other data is requested from a client)                     |
| 4xx     | Transient negative completion reply (temporary error)                         |
| 5xx    | Permanent negative completion reply |
| 6xx    | Protected reply (encrypted) |

```
````


````col
```col-md
flexGrow=1
===
**Stateless:**
Server maintains no information about past client requests
```
```col-md
flexGrow=1
===
**Stateful:** 
Server maintains information about past client requests, the last manipulations with files, etc.
```
````

````col
```col-md
flexGrow=1
===
**Non-Persistent HTTP:** 
- At most one object sent over a connection; 
- Connection is then closed; 
- Downloading multiple objects require multiple connections (e.g. in case of a web page with images)
  
**Persistent HTTP:** 
- Multiple objects can be sent over a single connection
```
```col-md
flexGrow=1
===
**Persistency:** 
- Control connection – persistent; 
- Data connection – non-persistent
```
````

````col
```col-md
flexGrow=1
===
- Introduced at CERN by Tim Berners-Lee in 1987; 
- The foundation of data communication for the World Wide Web; 
- Widely used and actively maintained
```
```col-md
flexGrow=1
===


```
````

