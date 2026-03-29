## Point-to-Point
The simplest network.

### Communication channel
![](Pasted%20image%2020260329060537.png)

#### Characteristics:

- Data transfer direction (single or bi-directional)
- Wired or wireless
- Throughput and latency/delay
- Error proness (bits flip)

### Network Interface Controller (NIC)
![](Pasted%20image%2020260329110056.png)

#### Characteristics:

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

#### Purposes:

- To schedule nodes for data sending
