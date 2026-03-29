## Networks classification

| Network Criteria                           | Examples                                                                                                                                                                          |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Scale                                      | **PAN:** Personal Area Network<br>**LAN:** Local Area Network<br>**MAN:** Metropolitan Area Network<br>**WAN:** Wide Area Network<br>![](Pasted%20image%2020260329143541.png)<br> |
| Transmission Medium                        | Optical, Coaxial, Radiowaves, Infrared<br><br>![\|400](Pasted%20image%2020260329145648.png)<br>                                                                                   |
| Protocols/Technologies supported           | LAN: **Ethernet** <br>MAN: **Distributed Queue Dual Bus** <br>WAN: **Cable Modem**, **Digital Subscriber** or **Leased Line** <br>BAN, PAN: **Bluetooth**, **Wi-Fi**              |
| Network Topology<br>(physical and logical) | Bus, Ring, Star, Tree, Hierarchical, Mesh                                                                                                                                         |
| Performance Metrics                        | **Bandwidth** (bits/sec) – max. transfer rate; <br>**Throughput** (bits/sec) – actual/average transfer rate; <br>**Packet Loss**, **Error bit rate**                              |
| Proprietary Type                           | **Open systems:** OSI-compliant, standard protocols; <br>**Proprietary systems:** private technologies and protocols                                                              |

| Cryteria    | LAN            | MAN               | WAN                  |
| :---------- | :------------- | :---------------- | :------------------- |
| Technology  | Ethernet, WiFi | DQDB, ATM         | Leased Line, Dial-Up |
| Range       | Up to 2km      | 5-50km            | Above 50km           |
| Speed       | Very High      | Average           | Low                  |
| Ownership   | Private        | Private or Public | Private or Public    |
| Maintenance | Easy           | Difficult         | Very Difficult       |

### Physical Network Topology
A physical interconnection layout between network nodes (routers, switches, etc.)

![](Pasted%20image%2020260329150714.png)

- The most *fast* and *reliable*, but *expensive* as well – **Full Mesh**.

Assumption of *bidirectional communication* channels is NOT always valid (e.g. due to admin configs)


### Logical Topology:
Actual data flow between nodes

````col
```col-md
flexGrow=1
===
**Physical Topology:**
![](Pasted%20image%2020260329151308.png)
```

```col-md
flexGrow=1
===
**Logical Topology:**
![](Pasted%20image%2020260329151321.png)
```
````


## Internet: Organization Principles
**Local or Regional Internet Service Provider (ISP)**
- Example: Tattelecom
- Provides an Internet connection to local communities or small regions
- Services: IP address allocation, domain name registration, web hosting, etc.
- Owns MAN or WAN networks

**Content Provider Network**
- Servers network of a content provider (e.g. Youtube.com, Google.com)
- Numerous user requests are handled by different servers
- Needed for handling simultaneous requests with acceptable quality (delays)
- Can be either local or geographically distributed network

**Enterprise Network**
- Midsize or large enterprise IT infrastructure
- Local Area Network (LAN)

**Mobile Network**
- A large-scale wireless network
- Radio waves transmission medium
- Multiple radio base stations over a large area
- Mobile hosts dynamically reconnect between stations

**National or Global Internet Service Providers (ISP)**
- Some Russian national ISPs: Rostelecom, MTS, Relkom (Demos)
	- Demos – the first ISP in Russia (1989) owning *“.su”* domain
	- Provide an Internet connection across a country
	- Services:
		- IP address allocation to local providers or end users;
		- 