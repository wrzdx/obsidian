- **Lamport:** a failure of a computer you didn’t even know existed can render your own computer unusable
- **Tanenbaum & van Steen:** 
	- A collection of autonomous computing elements that appears to its users as a single coherent system.
	- A system in which hardware and software components of networked computers communicate and coordinate their activity only by sending messages

>[!note] Definition
>- Multiple computers communicating via a network to achieve a task.
>- These computers are called nodes — any communicating device: desktops, servers, cars, sensors.

**Why make a system distributed?**
- It’s inherently distributed
- For better scalability: While the size increases, the things shouldn’t get incrementally worse
- For better reliability: even if one node fails, the system keeps functioning
- For better performance: get data from a nearby node rather than one halfway round the world
- To solve bigger problems:
	- huge amounts of data, can’t fit on one machine
	- e.g., SETI@home

**Troubles in DS**
- Communications may fail
- Nodes crash
- Nondeterministic behaviors
- Fault tolerance is hard but essential

**Scalability of DS**
- Scalability metrics:
	- Number of users/clients
	- Geographic area ( measured in continents/countries/m2)
	- Power/resource use (measured in watts per hour, rubles per second, etc.)


**Performance of DS**
- Performance = useful work vs time/resources.
- Focus:
	- Low latency
	- High throughput



**Caching vs Replication**

Better latency and throughput: Often achieved by caching data

- Caching vs. replication
- *Replication* = multiple data copies for fault tolerance
- *Caching* = temporary copies near the user for performance

**Reliability of DS**

- Availability:
	- the proportion of time a system is in a functioning condition. If a user cannot access the system, it is said to be unavailable.
	- Availability = uptime / (uptime + downtime)
- Fault tolerance:
	- ability of a system to deliver graceful degradation during failures

**Characteristics of DS**

Components are independent (autonomous), therefore result in following characteristic aspects:

- Concurrency of components for shared resources: Non-determinism, race conditions
- Lack of global clock:
	- Coordination is done by message exchange
	- No single global notion of the correct time
- Units may fail independently
	- Network faults may isolate computers that are still running
	- System failures may not be immediately known

