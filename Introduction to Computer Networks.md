---
model: openai@gpt-5.4
---
### Point-to-Point
The simplest network.
![](Pasted%20image%2020260329060537.png)

### Communication channel
**Characteristics:**

- Data transfer direction (single or bi-directional)
- Wired or wireless
- Throughput and latency/delay
- Error proness (bits flip)

### Network Interface Controller (NIC)
![](Pasted%20image%2020260329110056.png)

**Characteristics:**

- To transmit (put) data into a network channel
- To take data from a network channel
- Emposes a “transmission delay”, when transmitting or receiving data (it’s different from “transfer delay”)

### Data Transfer Principles
There are several basic principles for a data transfer:

- Data is divided into small blocks – *packets*
- Every packet is transferred independently
- The bitsize of a packet depends on *a specific protocol*

### Communication Protocol
**Communication Protocol** – the agreement (*“protocol”*) on technical communication details between network nodes

Examples:
- HTTP, SMTP, IMAPS, VolP, etc.

**Purposes:**

- To schedule nodes for data sending
- To define an exchanged data format
- Other technical details

#### Time Division Multiplexing
![](Pasted%20image%2020260329113449.png)

Assigns time slots to nodes for sending data

### Multi-Point Communication
Multiple hosts share the same channel:
![|400](Pasted%20image%2020260329113736.png)

**Broadcast Communication:**
![|400](Pasted%20image%2020260329114125.png)
1) Message from one host is sent to all others
2) Each host, when receiving a message, checks its destination address:
	1) It reads a message, if it is destinated to it
	2) Otherwise, it discards a message  

**Problems:**

- Packet routing algorithms
- Network security
- Others

### Key Concepts Of Computer Networks

#### Key Network Components:

- **Hosts:** end devices exchanging data
- **Link:** device to transmit data between adjacent nodes
- **Router:** device to forward/route data
	- Router-like devices: Switch, Bridge, Hub, WiFi Access Point, Repeater 
- **Source Host:** sends data
- **Destination Host:** receives data
- **Packet:** a block of data of a pre-defined size
- **Network Address:** unique identifier for nodes
	- Media Access control (*MAC*)
	- 
