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


