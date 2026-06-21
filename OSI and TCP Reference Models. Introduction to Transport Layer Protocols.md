## Different Reference Models for Network Communication
````col
```col-md
flexGrow=1
===

### OSI Seven-Layered Model

| Layer                                                                                      |
| ------------------------------------------------------------------------------------------ |
| **Application**                                                                            |
| **Presentation**<br>(Also known as Translation or Syntax layer (includes data encryption)) |
| **Session**                                                                                |
| **Transport**                                                                              |
| **Network**                                                                                |
| **Data Link**                                                                              |
| **Physical**                                                                               |
- An idealized theoretical/logical view
- It divides the network communication problem into seven independent subproblems
- For each layer, there should be dedicated protocols
- Real-world implementations might differ from the original OSI model formulation


```
```col-md
flexGrow=1
===
### Original TCP/IP Four-Layered Model

| Layer                 |
| --------------------- |
| **Application**       |
| **Transport**         |
| **Internet**          |
| **Network Interface** |
- TCP/IP: Transmission Control Protocol/Internet Protocol; 
- The oldest model (defined before the OSI); 
- Initially known as the *Department of Defence (DoD)* model; 
- Has significantly evolved under the influence of the OSI model

```
```col-md
flexGrow=1
===

### Evolved TCP/IP Five-Layered Model

| Layer           |
| --------------- |
| **Application** |
| **Transport**   |
| **Network**     |
| **Data Link**   |
| **Physical**    |
- The evolution of the original TCP/IP model under the OSI influence
- The most frequently referred model in practice

```
````

>[!note] TCP/IP = Internet Suit model


## Reference: Protocols Examples for Five-Layered TCP/IP Reference Model

| Layer           | Key Purpose                                                         | Protocol Examples                                                                                                            |
| --------------- | ------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **Application** | Communication between network application endpoints                 | **HTTP:** Hypertext Transfer <br>**FTP:** File Transfer <br>**DNS:** Domain Name System As well as many others               |
| **Transport**   | Process-to-process communication                                    | **TCP:** Transmission Control <br>**UDP:** User Datagram                                                                     |
| **Network**     | Host-to-host communication Packets routing and forwarding           | **RIP:** Routing Information Protocol <br>**BGP:** Border Gateway Protocol <br>**IP:** Internet Protoco                      |
| **Link**        | Data transmission over an individual physical link                  | **TDM:** Time Division Multiplexing <br>**FDM:** Frequency Division Multiplexing <br>**CDMA:** Code Division Multiple Access |
| **Physical**    | Electronic circuit transmission technologies for a computer network | **CAN:** Controller Area Network <br>**USB:** Universal Serial Bus <br>**Bluetooth** (protocol stack)                        |
## A Brief Comparison of TCP and UDP
|                           | Transmission Control Protocol (TCP)                                                                                  | User Datagram Protocol (UDP)                                                                                                                    |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| Application <br>Examples  | • Web page download; <br>• Large file download; <br>• Emails exchange                                                | • Real-time streaming video and audio applications; <br>• DNS query resolution                                                                  |
| Brief <br>Characteristics | • Connection-oriented communication; <br>• Reliable, in-order delivery; <br>• Congestion control; <br>• Flow control | • Connectionless communication; <br>• Unreliable, unordered delivery; <br>• No guarantee on a successful delivery; <br>• “Best-effort” services |
