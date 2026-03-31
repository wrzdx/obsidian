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
| Function                   | Description                                                                                                                 |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| `socket(…)`                | To create a network socket<br>`{c} int socketFD = socket ( addressDomain, socketType, protocolCode )`                       |
| `bind(…)`                  | To bind a socket to a specific port<br>`{c} int status = bind ( socketFD, socketAddress, addressLength )`                   |
| `listen(…)`                | To put socket into listening mode                                                                                           |
| `connect(…)`               | To connect to server<br>`{c} int status = connect ( socketFD, remoteSocketAddress, addressLength )`                         |
| `accept(…)`                | To accept connection from client<br>`{c} int connectionSocketFD = accept ( socketFD, &clientSocketAddress, addressLength )` |
| `send(…)`, `recv(…)`       | To exchange data in case of TCP                                                                                             |
| `sendto(…)`, `recvfrom(…)` | To exchange data in case of UDP                                                                                             |
| `shutdown(…)`              | To close TCP connection                                                                                                     |
| `close(…)` from `<unistd.h>`                 | To close a socket                                                                                                           |

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

### TCP
#### Server Side Implementation
```c 
#include <netinet/in.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/socket.h>
#include <unistd.h>

#define BUFFER_SIZE 1024

int main(void) {
  // Predefined constants <netinet/in.h>:
  // PF - "Protocol Family", AF - "Address Family"
  // Predefined constants <sys/socket.h>:
  // STREAM - for TCP, DGRAM - for UDP
  int serverSocket = socket(PF_INET, SOCK_STREAM, 0);

  if (serverSocket == -1) {
    perror("Failure to create socket");
    exit(EXIT_FAILURE);
  }

  // sockaddr - predefined structure to store socket address (IP + Port + Other)
  // IN - Internet Namespace
  struct sockaddr_in sa;
  memset(&sa, 0, sizeof(sa));

  // Initialization
  // htons/htonl to unify host number to network one
  sa.sin_family = AF_INET;
  sa.sin_port = htons(1111);
  sa.sin_addr.s_addr = htonl(INADDR_ANY); // Accept addresses

  // Bind socket and address
  int bindCode = bind(serverSocket, (struct sockaddr *)&sa, sizeof(sa));
  if (bindCode == -1) {
    perror("Failure to bind socket and address");
    exit(EXIT_FAILURE);
  }

  // Listen, client queue size is 10
  int listenCode = listen(serverSocket, 10);
  if (listenCode == -1) {
    perror("Failure to listen socket");
    exit(EXIT_FAILURE);
  }

  // Dealing with client connections in an endless loop
  char buffer[BUFFER_SIZE];
  for (;;) {
    int connectionSocket = accept(serverSocket, NULL, NULL);
    if (connectionSocket == -1) {
      perror("Failure to accept socket");
      exit(EXIT_FAILURE);
    }

    int recsize = recv(connectionSocket, (void *)buffer, sizeof(buffer), 0);

    if (recsize < 0) {
      perror("Failure to recieve msg");
      exit(EXIT_FAILURE);
    }

    printf("datagram: %.*s\n", (int)recsize, buffer);

    int shutdownCode = shutdown(connectionSocket, SHUT_RDWR);
    if (shutdownCode == -1) {
      perror("shutdown failed");
      close(connectionSocket);
      close(serverSocket);
      exit(EXIT_FAILURE);
    }

    close(connectionSocket);
  }

  close(serverSocket);
  return EXIT_SUCCESS;
}
```

#### Client Side Implementation
```c
#include <arpa/inet.h>
#include <netinet/in.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/socket.h>
#include <unistd.h>

#define BUFFER_SIZE 1024

int main(void) {
  int clientSocket = socket(PF_INET, SOCK_STREAM, 0);

  if (clientSocket == -1) {
    perror("Failure to create socket");
    exit(EXIT_FAILURE);
  }

  struct sockaddr_in sa;
  memset(&sa, 0, sizeof(sa));
  sa.sin_family = AF_INET;
  sa.sin_port = htons(1111);

  int res = inet_pton(AF_INET, "127.0.0.1", &sa.sin_addr);
  int connectCode = connect(clientSocket, (struct sockaddr *)&sa, sizeof(sa));

  if (connectCode == -1) {
    perror("Failure to connect server");
    exit(EXIT_FAILURE);
  }

  char msg[] = "Hello server!";
  send(clientSocket, msg, strlen(msg), 0);

  close(clientSocket);
  return EXIT_SUCCESS;
}
```


### UDP
#### Server Side Implementation
```c
#include <netinet/in.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/socket.h>
#include <unistd.h>

#define BUFFER_SIZE 1024

int main(void) {
  int serverSocket = socket(PF_INET, SOCK_DGRAM, 0);

  if (serverSocket == -1) {
    perror("Failure to create socket");
    exit(EXIT_FAILURE);
  }

  struct sockaddr_in sa;
  socklen_t fromlen = sizeof(sa);
  memset(&sa, 0, sizeof(sa));
  sa.sin_family = AF_INET;
  sa.sin_port = htons(1111);
  sa.sin_addr.s_addr = htonl(INADDR_ANY); // Accept addresses

  int bindCode = bind(serverSocket, (struct sockaddr *)&sa, sizeof(sa));
  if (bindCode == -1) {
    perror("Failure to bind socket and address");
    exit(EXIT_FAILURE);
  }

  char buffer[BUFFER_SIZE];
  for (;;) {
    int recsize = recvfrom(serverSocket, (void *)buffer, sizeof(buffer), 0,
                           (struct sockaddr *)&sa, &fromlen);

    if (recsize < 0) {
      perror("Failure to recieve msg");
      exit(EXIT_FAILURE);
    }

    printf("datagram: %.*s\n", (int)recsize, buffer);
  }

  return EXIT_SUCCESS;
}
```

#### Client Side Implementation
```c
#include <arpa/inet.h>
#include <netinet/in.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/socket.h>
#include <unistd.h>

#define BUFFER_SIZE 1024

int main(void) {
  int clientSocket = socket(PF_INET, SOCK_DGRAM, 0);

  if (clientSocket == -1) {
    perror("Failure to create socket");
    exit(EXIT_FAILURE);
  }

  struct sockaddr_in sa;
  memset(&sa, 0, sizeof(sa));
  sa.sin_family = AF_INET;
  sa.sin_port = htons(1111);

  int res = inet_pton(AF_INET, "127.0.0.1", &sa.sin_addr);
  char buffer[200];
  strcpy(buffer, "hello world!");
  int bytes_sent = sendto(clientSocket, buffer, strlen(buffer), 0,
                          (struct sockaddr *)&sa, sizeof(sa));

  if (bytes_sent < 0) {
    perror("Failure to send msg");
    exit(EXIT_FAILURE);
  }

  close(clientSocket);
  return EXIT_SUCCESS;
}
```

## Key Implementation Stages
### Server Side

| Step | Description                                      | Function Used |
| ---- | ------------------------------------------------ | ------------- |
| 1    | Create a TCP or UDP socket                       | `socket(…)`   |
| 2    | Assign a free port to socket                     | `bind(…)`     |
| 3    | Set socket to listen mode<br>(mandatory for TCP) | `listen(…)`   |
| 4    | Await and handle connection requests:            |               |
| 4a   | Accept (or decline) an incoming connection       | `accept(…)`   |
| 4b   | Receive message                                  | recv(…)       |
| 4c   |                                                  |               |
|      |                                                  |               |
| 5    |                                                  |               |
