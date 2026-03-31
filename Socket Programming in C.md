A software mechanism for data exchange between local or remote processes (IPC, Inter-Process Communication service)


| C header files used | Description                                                                                                            |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **sys/socket.h**    | Core socket function and data structures                                                                               |
| **netinet/in.h**    | Data structures for representing IP addresses, TCP and UDP port numbers, and other                                     |
| **arpa/inet.h**     | Functions for manipulating with numeric IP addresses;<br>An alternative of *<netinet/in.h>* for some operating systems |
| **netdb.h**         | Translation functions of host names into numeric addresses<br>(e.g. by using DNS services) and other                   |
| **sys/un.h**        | Communication functions for *local processes* running on the same computer                                             |

>[!summary]- Core Socket Functions (from sys/socket.h)
>
| Function                   | Description                         |
| -------------------------- | ----------------------------------- |
| `socket(…)`                | To create a network socket          |
| `bind(…)`                  | To bind a socket to a specific port |
| `listen(…)`                | To put socket into listening mode   |
| `connect(…)`               | To connect to server                |
| `accept(…)`                | To accept connection from client    |
| `send(…)`, `recv(…)`       | To exchange data in case of TCP     |
| `sendto(…)`, `recvfrom(…)` | To exchange data in case of UDP     |
| `shutdown(…)`              | To close TCP connection             |
| `close(…)`                 | To close a socket                   |

````col
```col-md
flexGrow=1
===
TCP Communication
![](Pasted%20image%2020260331081726.png)
```
```col-md
flexGrow=1
===
UDP Communication
![](Pasted%20image%2020260331081741.png)
```
````

