1) Webpage is hosted by a server;
2) Server is identified by an IP address; 
3) User access - by a human-friendly domain name; 
4) DNS Lookup: domain name translation to IP – The most time-consuming stage

## DNS Lookup: Speed-up Optimizations

### Local caching of frequently accessed records;
````col
```col-md
flexGrow=1
===
#### Local Cache Miss
![](Pasted%20image%2020260330183851.png)

- At the first webpage request, the IP address of a server is not cached on a client side;
- Thus, a client contacts a DNS Server for obtaining the IP address

```
```col-md
flexGrow=1
===

#### Local Cache Hit

![](Pasted%20image%2020260330183936.png)

- If instead an IP address is cached, there is no need to contact a DNS server;
- Thus, caching reduces the overall time overheads for a network communication
- Note: Cached data might have a validity period, as servers might potentially change IP addresses


```
````

### Hierarchical DNS database organization

- A huge number of servers is registered over the Internet; 
- DNS database contains a lot of records; 
- Thus, the DNS database is organized as a *distrbuted hierarchical database*; 
- This allows a drastic reduction of time for a DNS lookup process

Correspondence of “*innopolis.university.ru.*” URL to the DNS hierarchy
![|500](Pasted%20image%2020260330184806.png)

> [!note] 
> “.” at the end of URL addresses is typically omitted

#### Root Servers (“*.*”)
(13 in total + multiple replications)

- Each Root DNS server knows the IP addresses of all registered *Top-Level Domain* (TLD) Servers;
- Root servers have multiple *replications* 
	- **replication** - a physical server sharing the IP address of some root server and containing its DB
- DNS Root zone is coordinated by the *Internet Assigned Numbers Authority* (IANA) organization, the part of the ICANN

#### Top-Level Domain (TLD) Servers
**Examples:** .com .university .org .ru

- A certain TLD server knows the IP addresses of the associated second-level DNS servers
	- Note: one logical server might correspond to multiple physical servers
- The database of the available TLD servers is maintained by IANA: https://www.iana.org/domains/root/db
- Country-code servers (such as “.ru”) are classified as TLD servers

#### Second-Level Domain (SLD or 2LD) Servers
**Examples:** innopolis, google

Authoritative DNS server:
- Provides or knows the IP address of the final service provider
- Owned or rented by the end organization or company
- Can be of the second or a lower level

## DNS Lookup Process

**Local DNS Server**
- Does not strictly belong to the DNS hierarchy
- Each ISP or organization typically has one dedicated DNS
- Local DNS acts as a proxy server: has its local cached DNS data
- When needed (that is data is missing in cache or becomes invalid), it forwards DNS queries from local hosts into the DNS hierarchy
![](Pasted%20image%2020260330190143.png)

````col
```col-md
flexGrow=1
===
**DNS Recursive Query**
Load is distributed across the DNS hierarchy
![](Pasted%20image%2020260330190443.png)
```
```col-md
flexGrow=1
===
**DNS Iterative Query**
More load on ISP DNS Server
![](Pasted%20image%2020260330190427.png)
```
````

>[!note] DNS Records Time Validity
>- IP addresses are not static (might change over time, even for well-known servers);
>- Data in local cache or in the ISP DNS server cache can become obsolete;
>- Periodically caches are reset and actualized;
>- A typical frequency of updates (subject to configuration): 
>	- ISP DNS server: 24-48 hours; 
>	- client local cache: 24 hours

## DNS Record Format
| Name                                         | Value                                      | Record Type                  | TTL (Time to live) |
| -------------------------------------------- | ------------------------------------------ | ---------------------------- | ------------------ |
| Canonical Host Name<br>*mail.innopolis.ru*   | IP Address<br>*188.130.155.25*             | A (IPv4)/ AAAA (IPv6)<br>*A* | (config.)          |
| Host Alias<br>*mail.university.Innopolis.ru* | Canonical Host Name<br>*mail.innopolis.ru* | CNAME<br>*CNAME*             | (config.)          |
| Mail Server Alias                            | Canonical Mail Server Name                 | MX                           | (config.)          |
| And many others                              |                                            |                              |                    |
