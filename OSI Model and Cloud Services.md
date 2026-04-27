- OSI – Open Systems Interconnection
- a layered framework for design of network systems that allows for communication across all types of computer system

**Layers:**
- Application – network process to application
- Presentation – data representation and encryption
- Session – interhost communication
- Transport – end-to-end connections and reliability
- Network – path determination and logical addressing
- Data Link – physical addressing
- Physical – media, signal and binary transmition

- Intermediate nodes – involve only the first three layers
- Peer-to-Peer Process?
	- Layer n, use the services provided by layer n-1 and provides services for layer n+1
	- The process on each machine that communicate at a given layer are called peer-to-peer process
	- Use protocol


## Layer 1 - Physical layer
- Coordinates the function required to transmit a bit stream over a physical medium
- Deal with the mechanical/electrical spec of the interface and transmission medium
- Defines the procedures and functions that physical devices and interfaces have to perform for transmission to occur

**Concerned with:**
- Physical characteristics of interfaces and media
- Representation of bits – Bits must be encoded into signals –electrical or optic
- Data rate –the number of bits sent each second
- Synchronization of bits
- Line configuration – connection of devices to the medium
- Physical topology – How devices are connected to form a network
- Transmission mode – Direction of signal transmission between two devices

>[!note] 
>The physical layer is responsible for transmitting individual bits from one node to the next.

## Layer 2 - Data Link layer
- Responsible for node-to-node delivery
- Makes appear error free to the network layer

**Responsibilities include:**
- *Framing* – divides the stream data to manageable data units – frame
- *Physical addressing* – adds a header to the frame –to define the physical address of sender( source address) and receiver (destination address). Eg : A3-34-45-11-92-F1
- *Flow control* – to prevent overwhelming at the receiver
- *Error control* – provides reliability – to detect and retransmit damaged or lost frames, also prevent duplication of frames - trailer
- *Access control* – require a protocol to determine which device has control over the link at any given time –> same link with two or more devices connected.

>[!note] 
>The data link layer is responsible for transmitting frames from one node to the next.


## Layer 3 - Network layer
- Responsible for the source-to-destination delivery of a packet possibly across multiple networks (links)
- If two systems are attached to different networks, we need the network layer protocol to accomplish source-to-destination delivery

**Specific responsibility:**
- Logical addressing – to distinguish the source and destination systems when a packet passes the network boundary – also known network address. Eg : 192.10.64.20
- Routing – internetwork/large network – route the packet to the final destination

>[!note] 
>The network layer is responsible for the delivery of packets from the original source to the final destination.

## Layer 4 - Transport Layer
- Review of a network layer responsibility:
	- Responsible for source-to-destination (end-to-end) delivery of the entire message
	- Individual packet – treats each packet independently
- transport layer
	- Ensures the whole (entire) message arrives intact and in order
	- Oversee both error control and flow control at source-to-destination level
- To added security, transport layer create a connection between the two end ports
	- Connection - Single logical path between the source and destination
- Creating connection involves 3 steps:
	- Connection establishment
	- Data transfer
	- Connection release
- Has more control over sequencing, flow, error correction and detection

**Specific responsibilities:**
- Service-point addressing
	- Computers often run several programs at the same time
	- From a specific process (running program) on one computer to a specific process (running program) on the other
	- TL header must include a service-point address or port address
- Segmentation and reassembly
	- Segment – add a sequence number into message segment
- Connection control
	- Can be either connectionless (independent packet) or connection oriented
- Flow control
	- End-to-end flow control ( across multiple networks)
- Error control
	- End-to-end error control ( across multiple networks)

>[!note] 
>The transport layer is responsible for delivery of a message from one process to another.

## Layer 5 - Session Layer
- The network dialog controller
- Establishes, maintains, and synchronizes the interaction between communicating systems

**Responsibilities:**
- Dialog control
	- allows two systems to enter into a dialog
	- communication between two process – half-duplex or full-duplex
- Synchronization
	- allows a process to add checkpoints (synchronization points) into a stream of data
	- E.g.: sending a file..

## Layer 6 - Presentation Layer
- Concerned with the syntax and semantics of the information exchanged between two systems.

**Responsibilities:**
- Translation
	- The process (running programs) in two systems are usually exchanging information
	- Different computers use different encoding systems
	- Responsible for interoperability between different encoding methods
	- Sender machine change the information from its sender-dependent format into a common format
	- Receiver machine change the common format into its receiverdependent format
- Encryption
	- Encryption - transform the original information to another form and sends it over the network
	- Decryption - reverse process at the receiver side
	- assure privacy - to carry a sensitive data/information
- Compression
	- Reduces the number of bits to be transmitted
	- multimedia data transmission – such as text, audio and video

## Layer 7 - Application Layer
- Enables user , whether human or software to access the network
- Provides user interfaces and support for services such as email, remote file access, shared database mgmt and transfer etc
- No trailer or header are added here

**Specific services**
- Network virtual terminal
- File transfer, access, and management (FTAM), FTP –access/manage/control files in a remote computer
- Mail services – SMTP, X.400 – store and forward email
- Directory services – X.500 – provides distributed database sources

>[!note] 
>The application layer is responsible for providing services to the user.

## Summary
- Application – access to network resources
- Presentation – translation, encryption, compression
- Session – manage sessions
- Transport – end-to-end message delivery, error recovery
- Network – to move packets from source to destination, provide internetworking
- Data Link – organize bits to frames, provide node-to-node delivery
- Physical – bits transmission, provide mechanical and electrical specifications

# TCP/IP Protocol Suite
- Developed prior to the OSI model
- 5 layers – also known Internet model
- The three topmost layers in the OSI model are represented in TCP/IP by a single layer – application layer
- TCP/IP is a hierarchical protocol – the upper-level protocol is supported by one or more lower-level protocols
- E.g.: @ TL – TCP, UDP; @NL - IP


**Layers:**
- Application Layer – HTTP, SMTP, FTP
- Transport layer – TCP, UDP, SCTP
- Network layer – IP
- Data link layer – Ethernet, Wi-Fi
- Physical layer – Twisted pair, optical fibers, satellite

# Cloud Services
- Cloud computing is a model for enabling convenient, on-demand network access to a shared pool of configurable computing resources (e.g., networks, servers, storage, applications, and services) that can be rapidly provisioned and released with minimal management effort or service provider interaction (National Institute of Standards and Technology)
- This cloud model promotes availability and is composed of five essential characteristics, three service models, and four deployment models.
- Cloud computing is Internet-based computing, whereby shared resources, software, and information are provided to computers and other devices on demand, like the electricity grid. Cloud computing is a style of computing in which dynamically scalable and often virtualized resources are provided as a service over the Internet. (Wikipedia)
- Cloud is a type of parallel and distributed system consisting of a collection of interconnected and virtualized computers that are dynamically provisioned and presented as one or more unified computing resources based on service-level agreements established through negotiation between the service provider and consumers.(Buyya)

## Service Models Overview
- **Infrastructure as a Service (IaaS)** - build a new house?
	- You can rent some virtualized infrastructure and build up your own IT system among those resources, which may be fully controlled.
- **Platform as a Service (PaaS)** - buy an empty house?
	- You can directly develop your IT system through one cloud platform, and do not care about any lower level resource management.
- **Software as a Service (SaaS)** - Similar to live in a hotel?
	- You can directly use some existed IT system solutions, which were provided by some cloud application service provider, without knowing any detail technique about how these service was achieved.