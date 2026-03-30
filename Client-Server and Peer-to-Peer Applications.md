## Client-Server model
![|400](Pasted%20image%2020260330092053.png)

Two types of network hosts: 
- Servers (passive) – to provide services (e.g. an HTTP server uploads a web page content);
- Clients (active) – to request those services (e.g. an HTTP browser downloads and demonstrates a web page)
  > [!note] 
       > Only clients can initiate communication to servers!

Types of servers:
- Web Servers: to provide web pages
- Mail Servers: to store/exchange emails between clients
- FTP Servers: to support operations with files
- Database Servers: to fulfil database queries
- DHCP servers: to allocate IP addresses to hosts; 
- DNS servers: to determine IP addresses of URLs

*Network server* – a (remote) computer providing services to network clients:
- Provides a high speed data upload; 
- Has high requirements to hardware; 
- Runs a specific operating system (Linux or Windows Server, other choices – more rarely); 
- Reliable and resistent to failures/attacks; 
- Supports simultaneous connections to multiple clients; 
- Consumes a lot of power leading to high operat. costs

**Major performance bottleneck:** Limited upload capacity of a server
![|800](Pasted%20image%2020260330093022.png)

*Peer-to-Peer* model aims at exploring these idle communication links instead

## Peer-to-Peer
![|800](Pasted%20image%2020260330093206.png)

> [!info] Key Idea
> Every node (peer) acts as a server and a client simultaneously (that is downloads and uploads data simultaneously)

1) File is divided into parts
2) Each part is downloaded independently by different peers, over different communication channels
3) Peers exchange missing parts of the file, by using communication channels between them, until all peers get all file parts

## Comparison

![|800](Pasted%20image%2020260330093411.png)

| **Characteristics** | **Client-Server (Centralized)**                               | **Peer-to-Peer (Decentralized)**                        |
| ------------------- | ------------------------------------------------------------- | ------------------------------------------------------- |
| **Node roles**      | Nodes are divided into clients (active) and servers (passive) | Every node acts as a client and a server simultaneously |
| **Usage Scale**     | Dominant (widely used) architecture                           | Less used                                               |
| **Complexity**      | Simpler (centralized algorithms)                              | More complex (distributed algorithms)                   |
| **Efficiency**      | Likely to decrease with the number of peers                   | Likely to increase with the number of peers             |
| **Stability**       | A single point of failure – a centralized server              | No single point of failure                              |
| **Cost**            | More expensive                                                | Cheaper (due to absence of server)                      |
| **Use Case**        | Other, except large files distr. and hierarchical databases   | Large files distribution and distributed databases      |

#### Achievable Lower Bound for a File Distribution Time: Client-Server Case
![](Pasted%20image%2020260330100444.png)
#### Achievable Lower Bound for a File Distribution Time: Peer-to-Peer Case
$u_{s}$ – server upload speed

- Case $u_{s} \leq (u_{s} + u_{1} + \dots + u_{N} / N)$:
  $$\frac{F}{u_{s}}$$
- Case $u_{s} \geq (u_{s} + u_{1} + \dots + u_{N} / N)$:
  $$\frac{NF}{u_{s}+u_{1}+\dots+u_{N}}$$

 In general:
 $$\displaystyle{\Delta t^{Distr}_{CS} \geq MAX\{\frac{F}{u_{s}}, \frac{NF}{u_{s}+u_{1}+\dots+u_{N}}\}}$$

