## Process Identification: Host IP Address + Process Port Number
- To address a specific process running on a network host, in addition to an IP address, an additional identifier is needed, called “*Port*”
- Process is identified by the IP of a host machine and its own port number
- Standard application-layer protocols have reserved port numbers
- Ports 0-1023 are reserved;
- Other ports are available for user applications: 1024 - 49151 for server apps; 
- 49152 - 65535 for client apps

## Overview Of Application Layer Protocols
| Protocol | Primary Purpose                                                 | Statefulness                                                             | Persistency                                                                                                | Port Number                             | Transport Protocol |
| -------- | --------------------------------------------------------------- | ------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------- | --------------------------------------- | ------------------ |
| **HTTP** | Web page retrieval <br>(rarely, emails, exchange)               | Stateless                                                                | Either persistent or not, subject to configuration                                                         | 80 - no encryption; <br>443 – encrypted | TCP                |
| **FTP**  | Large files download                                            | Stateful                                                                 | Control connection – persistent; <br>Data connection – non-persistent                                      | 21 – control con.; <br>20 – data con.   | TCP                |
| **SMTP** | Emails sending from a client to a server, or between servers    | Stateless                                                                | Persistent (multiple emails can be sent within the same connection)                                        | 25 – no encrypt.; <br>587 – encrypted   | TCP                |
| **IMAP** | Emails receival by a client (emails remain on a server)         | Stateful <br>(e.g. to manage client organization of emails into folders) | Either persistent or not, subject to configuration                                                         | 143 – no encrypt.; <br>993 – encrypted  | TCP                |
| **POP**  | Emails receival by a client (emails are downloaded to a client) | Stateless                                                                | Persistent                                                                                                 | 110 – no encrypt.; <br>995 - encrypted  | TCP                |
| **DNS**  | Translation of host names to IP addresses                       | Stateless                                                                | Non-persistent                                                                                             | 53                                      | UDP                |
| **DHCP** | IP assignement and other configurations to network hosts        | Either stateful or stateless, subject to configuration                   | Typically non-persistent, but can be configured as persistent (e.g. to give the same IP whenever possible) | 67 – server side; <br>68 – client side  | UDP                |

