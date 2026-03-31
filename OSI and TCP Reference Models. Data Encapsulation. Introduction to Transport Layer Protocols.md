## Reference: Protocols Examples for Five-Layered TCP/IP Reference Model

| Layer           | Key Purpose                                                         | Protocol Examples                                                                                                            |
| --------------- | ------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **Application** | Communication between network application endpoints                 | **HTTP:** Hypertext Transfer <br>**FTP:** File Transfer <br>**DNS:** Domain Name System As well as many others               |
| **Transport**   | Process-to-process communication                                    | TCP: Transmission Control <br>UDP: User Datagram                                                                             |
| **Network**     | Host-to-host communication Packets routing and forwarding           | **RIP:** Routing Information Protocol <br>**BGP:** Border Gateway Protocol <br>**IP:** Internet Protoco                      |
| **Link**        | Data transmission over an individual physical link                  | **TDM:** Time Division Multiplexing <br>**FDM:** Frequency Division Multiplexing <br>**CDMA:** Code Division Multiple Access |
| **Physical**    | Electronic circuit transmission technologies for a computer network | **CAN:** Controller Area Network <br>**USB:** Universal Serial Bus <br>**Bluetooth** (protocol stack)                        |
## Different Reference Models for Network Communication
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

### Original TCP/IP Four-Layered Model

| Layer                 |
| --------------------- |
| **Application**       |
| **Transport**         |
| **Internet**          |
| **Network Interface** |
