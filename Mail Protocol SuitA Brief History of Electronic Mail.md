![](Pasted%20image%2020260330104728.png)
## Electronic Mail Timeline
![](Pasted%20image%2020260330105059.png)

## Email Address Format
![](Pasted%20image%2020260330105316.png)

## Client-Server Architecture for Emails Exchange
**Mail server** – a hardware machine (physical server); 
**SMTP server** – a program to get emails from senders, and forward them further to a destination server; 
**POP (or IMAP) server** – a program to enable the retrieval of emails by a destination client

> [!note] 
> HTTP is not dedicated for email communication, but can be used together with web clients (for sending and retrieving emails)

|                  | Mail User Agent (client)                                                                  | Mail Server                                                                                                                                                                                                                      |
| ---------------- | ----------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Program Examples | Microsoft Outlook; Mozilla Thunderbird, etc.                                              | Microsoft Exchange Server; HCL Domino, etc.                                                                                                                                                                                      |
| Functionality    | 1) Accesses and manages user emails;<br>2) Downloads and stores emails on a local machine | 1) Receives emails from other mail servers; <br>2) Stores emails (as a remote storage); <br>3) Distributes emails to local clients; <br>4) Transfers emails from the outgoing queue to other mail servers (Mail Transfer Agents) |

## POP vs. IMAP Email Retrieval Protocols

|                             | IMAP (Internet Message Access Protocol)                                                                                                         | POP (Post Office Protocol)                                                                                                           |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Email Storage <br>Location  | Emails are stored at one place – the mail server                                                                                                | Emails are downloaded from a mail server to (a) local machine(s), and then removed from a server (subject to a server configuration) |
| Stateful/Stateless          | Stateful (memorizes emails read from previous sessions)                                                                                         | Stateless (across multiple POP sessions)                                                                                             |
| Additional features         | The ability to organize emails in folders, and similar, aiming to improve user experience across sessions                                       | Not designed for                                                                                                                     |
| Security / Data Protection  | All emails and attachments are stored on a remote mail server, which might not be controllable by a user                                        | Data is copied to a local user machine, and is typically removed from a mail server                                                  |
| Storage requirement         | Local storage capacity is not consumed; <br>Server storage capacity is consumed instead                                                         | Local storage capacity is consumed, but No server storage capacity is consumed (for storing emails)                                  |
| Reliability / Accessibility | Emails and attachments are not accessible, when a mail server is down; <br>An active internet connection is typically required to access emails | Emails are accessible independently of the presence of an active internet connection, or a mail server state                         |

