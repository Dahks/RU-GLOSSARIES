
Circuit switched
- a dedicated connection between hosts
	- one route


Packet switched
- Packets can take any number of routes between hosts
- better fault tolerance
- possible because of fibre optic networking




![Screenshot 2024-11-16 at 09.45.47.png](../images/Screenshot%202024-11-16%20at%2009.45.47.png)
The OSI model
- 7 separate layers for different aspects of communication
- each layer performs clearly defined functions
- minimizes dependency across layers (only depends on previous layer)
- in practice only the first 3.5 layers are used

TCP/IP reference model
- Application
- Transport
- Internet
- Link (data link & physical in OSI)

Sockets
- an abstraction of ip address and port number
- non-blocking
	- server is listening for data from other end but how long to wait?
	- server checks for data but continues if there isn't any
	- returns an error "operation would block" if read buffer is empty or send buffer is full
- blockign socket
	- server waits until it receives at least 1 byte
- socket options
	- man7 socket
- operatiuons
	- bind
		- for server, bind socket to port for listening
	- connect
		- for client to connect to socket that server is listening on
	- listen
		- for server to listen for incoming connections and establish a connection
		- sets socket to listening state
	- accept
		- accepts an incoming conection
		- client is handed off to their own two-way socket
		- listen socket is specifically used for incoming connections
	- send
		- for sending messages between sockets
	- recv
		- for receiving messages from other side

ports
- 16 bit unsigned integer - specific to host
- 0 - 1023 are well known ports assigned by the OS
- 1024 - 65535 are Registered / Ephemeral ports available to applications


byte order
- network byte order is big-endian
- intel architecture is little endian

htons
- host to network byte order

client-server architecture
- client
	- initiates connection to server
	- interfaces directly to user
	- communicates with server
- server
	- waits for conections from client
	- provides services to the client
	- communicates with the clients
	- handles many clients simultaneously

P2P
- some or all peers take on a server role
- organized topologies tend to emerge at scale
- software needs to be both a client and a server


Socket programming map
![Screenshot 2024-11-16 at 09.51.38.png](../images/Screenshot%202024-11-16%20at%2009.51.38.png)



Coneceptual models for network software


Protocols


Standards
- major standards organizations cover data-communications
- industry standards
	- CCITT
	- IEEE
	- ISO
	- IETF
		- Internet Standards via RFC 

RFC - request for comments
- Innovations, proposals, occasional jokes
- may later be published by IETF as formal standard
- anyone can submit an RFC


![Screenshot 2024-11-16 at 11.03.56.png](../images/Screenshot%202024-11-16%20at%2011.03.56.png)


Information theory
- study of the quantification, storage and communication of information
- how to know signal is not noise
- how to separate noise from signal
- how to efficiently transmit and receive information
	- encoding and decoding
	- detecting and correcting transmission errors
- maximum amount of information we can transmit / receive
- how much information do we need to describe a system
- what
	- defines essence of a communication system
	- determined mathematical limits on the amount of information a given channel can carry
	- includes concepts of noisey (error prone) channels
- Shannon Limit on information in a single channel
	- C = B * log2(1 + S/N)
		- C - maximum channel capacity
			- depends on max frequency that can be used on a given medium and on the energy required to transmit that signal - hence why fibre better than copper
		- B - Bandwidth in Hz
		- S - signal power over bandwidth (Watts)
		- N - average power of the noise
- lower frequencies propagate further and require less energy than higher ones

Nyquist limits
- minimum number of samples needed to reconstruct a signal
- Applies generally to any oscillating signal / system
	- must have 2 full cycles to be able to accurately reconstruct
- Nyquist rate
	- upper bound on the symbol rate across a bandwidth limited channel
	- maximum possible transmission rate
- 2 * Bandwidth Hz (cycles per second)

Signals
- used to transmit information
- become distorted over long distances
	- attenuation (get quieter)
	- noise introduced by transmission / reception


Fisher consensus
- It is impossible to guarantee that any asynchornously connected set of nodes (computers) can ever agree on even a single bit value
- Can't be solved
	- have to work around (synchronize)
		- expensive
		- costs information capacity and often compute time
			- process / machines  have to wait for everything to report
	- or live with it (catch errors when they happen)

Information
- a unit of information is a bit
- a measure of different data


bandwidth
- either
	- signal processing
		- the difference between the highest and lowest frequency in a signal (Hertz)
	- data communications
		- maximum rate of data transfer across a given path (in bits/sec)


Properties of media in the physical layer
- Copper drops 
	- packets are corrupted by noise and are dropped
- Glass Breaks
	- practically error free
- Wireless blocks
	- high error rates
- satellites have really long delays


Copper
- Dominated early networking
	- via dedicated links for data communication 
- relatively low capacity and lots of errors
- favored transmission protocols
	- favoured computational solutions over transmission solutions
		- error detection and correction over re-transmission
	- everything possible was done to preserve bandwidth
	- still influences some protocols
- limited length (depending on calbe type) (max 100m)
- requires repeaters
- high error rate (compared to fiber)
- very cheap

Fiber-optic networking
- very low error rate
- very high transmission speeds
- uses far infrared to ultraviolet light
- Light moves through a glass core
- Actual speed in a fiber-optic cable depends 
	- refractive index of glass core
	- wavelength of light being used
- Speed of lighti n cable = speed of light / refractive index of cable
- pros
	- thinner (important for cabling considerations)
	- much higher capacity
	- less signal degradation with distance (requires fewer repeaters)
	- lower power
- const
	- more expensive (40$/m)
	- cannot be easily joined together 
		- splicing - specialized job
	- ends have to be periodically inspected and cleaned
		- 1 micrometer dust particle on a single-mode core can block up to 1% of light -> 9 micrometers is enough to completely block it
		- laser can burn residue and cause damage
		- NEVER 
			- look into the end of a fiber-optic cable
			- touch the end of a fiber-optic cable
	- fragile - must not be bent too much
	- copper is usually already available


Wireless
- sends same information to all nodes
- physical and data link layers use different protocols and have notably different characteristics than copper and fiber
	- (i.e. comes in instead of link layer in 4-layer)
- Disadvantage (inherently from being a broadcat medium)
	- high losses due to interference
	- high losses due to interference
	- frequency use has to be carefully regulated
	- higher delays and jitter
	- lower security

Broadcast medium
- Broadcast media send the same information to all nodes
	- inherently lower information capactiy than equivanelt point-to-point network

Other media
- Offline media import / export
	- send physical media to a third party service provider who uploads data on your behalf

Delays, speeds, bandwidth (sjá 131)
- transmission rate / capacity / andwidth
	- how much data can be sent on a link per time unit
- transmission delay
	- how long does it take to send some amount of data
- Propagation speed
	- how fast does the signal travel in a medium
- propagation delay / latency
	- how long after the signal was sent does receiver receive it
- Queueing delay
	- time data spends ina queue waiting to be transmitted
- Processing delay
	- processing tiem of computer between receiving some data and transmitting it further (or responding)



The protocol stack
- builds upwards in complexity and services offered
- higher levels are responsible for 
	- reliability
	- data order
	- etc.
- higher levels should not be aware of lower level's details
	- interface between layers is similar to a contract
	- lower layer provides specified services to upper layer
- Lower layers should be plug and play
	- e.g. IP should be blissfully unaware of the transfer media being used
		- but can matter at application layer

Design choices
- fixed packet size vs. variable packet size
- Synchronous vs. asynchronous
	- synch protocols send packets at fixed times
	- one way to duck consequences of Fischer concesnus
- Error correction vs. retransmission
- Ack or don't but rather detect missing
	- ack creates significant overhead
- connectionless vs connection oriented
	- connectionless : message can be sent without prior arrangement
	- connection oriented : set up connection then talk / do (phones and tcp)

Synchronized vs Unsynchronized communication
- Recurring problem / solution approach in datacomms
- synchronous
	- syncrhonized by some kind of external clock
	- receiver expects frames to arrive at fixed frequency
	- uses clock to read frames from the wire
	- problems include drift, and in the limit Einstein and Fisher
	- fixes Fischer Consensus 
- Asynchronous communication
	- not synchronized
	- frames have to have start / end frame markers or a known frame length
	- incurs a high overhead



Three main variants of protocols
- unacknowledged connectionless service 
	- e.g. Ethernet
- acknowledged connectionless service
	- e.g. WiFi
- acknowledged connection-oriented service
	- e.g. TCP

Data link protocols
- Ethernet Local Area Networks (LAN)
- Point-to-Point (PPP)
	- telephony protocol thatt provides datalink over duplex circuits
	- duplex - can communicate in both directions
	- half-duplex - both direction but only one at a time (e.g. walkie talkie)
	- full-duplex - both direction simultaneouly
- data link protocols respond to requests from the network layer
- Issue requests to the physical layer
- functions
	- provide a well-defined interface to the network layer
	- deal with transmission errors
	- regulates the flow of data so that slow receivers aren't swamped by fast senders
- Interface to network layer
	- perform character encoding, transmission, reception and decoding
	- determine start and end of packets (framing)
	- simple transmission error handling 
		- error detection and correction
	- error recovery
		- may be delegated to (or repeated by) a higher level
		- datalink layer is not required to guarantee data integrity
		- "upper layers will recover or die in the attempt"
- data is sent in separate frames
	- but how to find the frame?
	- do e.g.
		- transmit the length of the frame
			- header field includes length of the frame
			- header itself should be fixed length
				- restricts the length of the lenght field
				- restricts packet size as a result
			- difficult to recover from errors in the length count itself
			- how do you find the next header
		- use a fixed length frame
			- easy but less efficient
			- Fragmentation if message is longer than the frame
				- there is no optimal frame length
				- can be very inefficient
				- makes some queueing problems easier
				- reduces jitter
		- use a flag or pattern to indicate start / end of frame
			- if the data contains the bit pattern used as a flag
				- flag bytes with byte stuffing
				- flag bits with bit stuffing

ATM (asynchronous transfer mode)
- cell based switching for high speed data transmission
- 53 byte cell size
	- US and European parties couldn't agree

Character based frame signalling (Flag Byte)
- ASCII contains some symbols for this
- what if flag byte occurs in data (e.g. in binary data)
	- byte stuffing
		- if sender sees a FLAG in the data inject and ESC byte
		- Receiver sees ESC followed by FLAG - remove ESC and continue
		- Receiver sees only FLAG - genuine end of frame
		- Similarly for ESC, inject another ESC
		- must ESC ESC as well!
		- imposes a particular character format
	- bit stuffing (bit oriented framing)
		- use pattern of bits to signal start or end frame
			- e.g. each frame begins with 01111110
			- bit stuffing inserts a 0 after any 5 bits in the data (other than the idle frame guys)
			- receiver ignores 0 after any 5 bits in the data
		- advantages
			- can vary length of the flag
			- longer flag will reduce need for stuffing
			- short packets use a short flag - less overhead and likelihood
			- can also combine with other techniques for efficiency or safety, e.g. send frame length and use start/stop flags
- FLAG errors e.g. corruptions
	- may either detect premature end of frame
	- run on too long into next frame
		- frame checksum will fail at receiver
	- can then find next frame by looking for FLAG
- Bad frames will be dropped, either datalink protocols resend or higher layer need to recover somehow.


information per layer
- physical layer -- bit
- data link layer -- frame
- network layer -- packet
- transport layer -- segment (TCP) or datagram (UDP)

Error detection and correction
- type of error dependent on medium
	- single bit errors
		- 1 swapped bit
	- Burst errors
		- many fucked bits in a range, otherwise fine
		- common in wireless

Parity check (error detection)
- Use parity bit / check bit
- count number of bits in a frame
	- if no. of 1 bits is ODD, parity bit is 1
	- if no. of 1 bits is even, parity bit is 0
	- Number of 1 bits is always even
	- (special case of cyclic redundancy check CRC)

Error correction
- add redundant information to the frame
- allows errors to be detected and corrected
- tradeoffs
	- the more information added, the longer the frame
		- increases probability of erorr
		- increases transmission cost / processing
		- increases cost of processing at receiver
	- avoids cost of having to retransmit the frame
- increases size of message in proportion to redundancy
- detect n bits of error, correct n-1 bits
- important result
	- can never guarantee all errors will be detected
	- can guarantee a lower bound on errors
	- cost of error correction / detection is a significant overhead
- information theory limits on transmission on a channel


Hamming codes (error deteciotn and correction)
- Add parity bits at powers of 2 to the data bits
- each parity bit calculates parity for a subset of the bits in the message
	- data bits (1s) is even
		- e.g. p1 = p7 xor p5 xor p3
	- parity bits themselves not included in the checks
- parity bit 
	- nr. 1  -> covers all bit positions with a 1 (1, 3, 5, 6, 9, etc.)
	- nr. 2  -> covers all bit positions with a 1 in second position (2, 3, 6, 7, e.g. 010)
	- nr. 4 -> covers all those in position 3 (0100) (4-7,12-15, 20-23)

Cyclic Redundancy Checks (CRC)
- error correcting
- based on theory of cyclic error-correcting codes
- takes advantage of maintaining known additional information at each end
- how
	- divide string (frame) by a generator polynomial G(x)
	- add the remainder R(x) onto the end of the frame
	- receiver divides frame by G(x) - non-zero remainder indicates error

Error control
- how does the sender know that a packet has been received?
- receiver sends back acknowledgment frames
	- ACK - acknowledgment
	- NACK - Negative acknowledgment - error in frame
- if receiver doesn't get the frame
	- then a timer on ack is kept
	- must be received within a specified interval
- suppose receiver gets multiple copies of a frame
	- frame header includes sequence number

Flow control
- what happens if one end sends faster than the other one can receive (and process)
- two approaches
	- negotiate a fixed speed between sender / receiver
	- feedback-based - receiver tells sender to paus
- typically fixed speed used at lower protocol levels
- higher levels use some kind of feedback
- or simply use the convention of send message then wait for response


Point to point vs broadcast
- local wired protocols exist that use broadcast e.g. Ethernet or token ring
- relies on local network capacity being larger than applied traffic

Multiplexing
- multiple hosts can share a connection (provided they don't try to all use it simultaneously)

Statistical multiplexing / multiple access protocol
- dynamically allocate bandwidth based on the actual traffic demands of each stream, rather than pre-allocating some resource
- no fixed allocation of packet transmissions
- packets are mutliplexed as they arrive
- ![Screenshot 2024-11-16 at 14.21.38.png](../images/Screenshot%202024-11-16%20at%2014.21.38.png)
- pros
	- efficient - maximizes use of capacity
- cons
	- too much traffic from hosts will cause blocking
		- flow control must slow down traffic to fit available bandwidth
		- traffic may vary accroding to time of day (home vs. business)
	- also relies on being able to queue or delay packets
		- problematic for applications with low latency requirements
- statistical as in depends on
	- number of hosts
	- amount of traffic
	- frequency of traffic
	- capacity of channel
	- amount of moeny (capital) avaialable

network provisioning
- given a set link capacity how many users can be provisioned and maintain performance guarantees
	- oversubscription
- makes attaching to the netwrok cheaper but technically less reliable

multiple access protocols
- statistical multiplexing
- time division multiplexing
- optimal
	- given a broadcast channel of rate R bps
		- when one node wants to transmit it can send at rate R
		- when M nodes want to transmit, each can send at average rate R/M
		- fully decentralized
			- no special node to coordinate transmissions
			- no synchronization of clocks, slots
		- simple - but also impossible :)


Time division multiplexing (TDM)
- alternatively can use a fixed allocation - TDM
	- available bandwidth is divided equally between hosts
	- each host gets his own slot
	- can only transmit using that slot and at no other time
- pros
	- hosts are guaranteed a certain bandwidth (Quality of Service)
	- easier to syncrhonize when applications requireit
- cons
	- wasteful if host doesn't use its allocation, nothing else can


Network engineering
- the problem of ensuring networks meet user's requirements
	- fault tolerance (availability)
	- capacity (throughput)
	- latency
	- cost
		- cost of network equipment
		- running cost - connection to Internet

Addressing
- so that ends can identify each other

Internet chronologically
- 1970 - Alohanet
- 1972 - Ethernet
- 1974 - A protocol for packet network itercommunication
	- outlined TCP
	- subsequently borken up into TCP, UDP and IP
- 1981 - RFC 791 describes IPv4
- 1982 - TCP/IP adopted as a formal standard
- 1986 - NSFNet - US supercomputer access 56kbit/s
- 1989 - MCI mail and compuserve - beginning of public Internet
- 2010 - International Space station connected to the Internet


The Internet
- a collection of many networks

Scaling
- constraints on systems that depend on size
- 3 key attributes affecting scaling
	- topology
	- latency
	- size (number of nodes)

Topology
- group size 
	- maximum connectedness at a node
	- i.e. maximum no. of single hop connections that a given node can support
	- depends on
		- bandwidth
		- application requirements
		- cpu
		- larger network considerations
- Strictly hierarchical
	- best topology for control purposes (e.g. botnets)
	- worst topology for exchanging information
	- robust to broadcast storms with increasing N
	- required if consensus must be guaranteed
	- favoured by long communication latencies
- full mesh
	- information capacity scales as L(L - 1)
	- best topology for exchanging information for small groups
	- size is bounded by the group size
	- worst topology for control
	- vulnerable to broadcast storms
- partial mesh
	- information capacity scales as L sqrt(N)
	- cannot guarantee consensus
	- depending on error rate, voting algorithms can provide strong guarantees
	- vulnerable to broadcast storms with increasing N
- Organized mesh
	- topology that can scale to large N and grow capacity
	- similar issues to other mesh topologies
	- allows arbitrary scaling with the assumption that significant amounts of traffic can be retained in local groups of communicatting nodes
	- glæra 727
	- the internet

Fischer consensus
- it is impossible to guarantee that any asynchronously connected set of nodes (computers), can ever agree on even a single bit value
![Screenshot 2024-11-16 at 15.06.50.png](../images/Screenshot%202024-11-16%20at%2015.06.50.png)


Latency
- communication speed / latency
	- time taken to send a message between two nodes
- processing speed
	- time taken to process a message by the recipient
- long communication latency favour hierarchical networks
- short communicatio latency favours distributed ones

Hierarchical vs mesh
- Hierarchical
	- pros
		- relatively simple
		- single piont of control
		- good for synchronization
	- cons
		- fragile - single point of failure
		- low information capacity
		- cannot scale to large N (nodes)
		- good at high latency communication
		- vulnerable to broadcast storms
- Mesh
	- pros
		- robust - hard to crash
		- high information capacity
		- scales to large N
	- cons
		- complicated
		- no single point of control
		- impossible to guarantee consensus
		- poor performance
		- very vulnerable to broadcast storms

Local Area Networks


network hub
- simple connection devices
- connects several devices onto one link
- broadcast received packets to all connected devices
- bandwidth split between all connected devices
- now being phased out in favour of network switches

Network switch
- connect directly to computers, printers, phones, etc.
- packets only sent to destination computer
- unmanaged - works out of the box with no configuration
- managed can be controlled and customised
- handles a LAN

Routers
- forward packets between (local) networks



Medium Access Protocols (MAC)
- control access to a single shared broadcast channel
	- implement some sort of multiplexing algorithm
- range of protocols and approahces
- terms
	- interference
		- two or more hosts broadcast simultaneously
	- Collision
		- node receives two or more signals at the same time
- 3 classes
	- channel partitioning
		- fixed division of channel into pieces (time slots, frequency, etc.)
		- each node allocated exclusive use of specific piece of channel
		- e.g.
			- time division multiplexing (TDM)
			- frequency division multiplexing (FDMA)
	- random access
		- hosts use channels ad hoc
		- protocol provides recovery mechanisms for collisions
		- engineered to reduce frequency of broadcast
		- e.g.
			- ALOHA
			- S-ALOHA
			- CSMA
				- carrier sensing - typically used for wire
	- turn taking
		- nodes take turns, but can take longer if they need to
		- some form of polling from central controller
		- token passing
		- e.g.
			- bluetooth
			- FDDI
			- token ring

Random access MAC protocols
- Node transmits when it has a packet to send
	- collisions occur if they both send at once
- algorithms to try to recover from collisions
- typically some kind of back off and try again scheme
	- each host colliding waits a random time t
	- waits longer for each subsequent collision until success

ALOHAnet
- Additive Links On-line Hawaii Area
- developed at the university of Hawaii in 1960s
- used to link schools on the Hawaiian Islands (no telephone networks)
- First public demonstration of a wireless packet data network 1970
- 1972 extended to create Ethernet
- how 
	- Radio station would send transmission when it wanted
		- receiver would reply with ACK
	- if no ACK - assume collision
	- pick a random back off time, and then retransmit
- problems
	- didn't check if another station is already transmitting
	- fixed with Slotted ALOHA
		- assigned transmission slot times and used fixed frame size

CSMA : carrier sense multiple access
- listen before transmission
- only send if the channel is free
- reduces collisions a little
- but, if more than 1 node is waiting collision is likely when they both start
	- wait and listen a further random time before starting
- Applied with detection of collisions
	- when collision is detected, the node aborts
	- reduces channel loss
	- uses Binary Exponentiation backoff (with randomness)
- collision detection applicability
	- Easy in wired lan (compare recieved / transmitted signal strength)
	- Difficult in wireless (local transmission overwhelms received)

polling - MAC protocols
- masted node invites slave nodes to transmit in turn
- typically used with dumb slave devices
- concerns
	- polling overhead
	- latency
	- single point of failure (master)

Token Ring
- control token passed from one node to another sequentially
- data
	- node waits until has token and then sends data
	- finished, sends token to next node
- no data
	- node immediately sends token to next node
- issues
	- overhead of token packets
	- higher latency
	- single point of failure (node with token) causing deadlocks


Ethernet II
- published as standard in 1982 - IEEE 802.3 (not exactly the same as Ethernet II)
- frame length maximum of 1500 octets (bytes)
	- Gigabit Ethernet and other higher-speed variants support Jumbo frames
- 64 bit Preample 
	- a repeating 10 pattern (ending in 11) used for clock syncrhonization between NIC's

Addressing
- communicating hosts must be able to uniquely identify each other
	- guarantee uniqueness - Single point of allocation
	- Otherwise - Fisher Consensus problem
- Ideally, addressing helps with routing (also a hard problem)
- MAC protocols requier some form of identification immediately when hosts are on the LAN
- as hosts are sharing a medium this must be unique

MAC address
- Unique Identifier assigned toa Network Interface Controller (NIC)
- In theory, isseud by Manufacturer's and glboally unique
	- divide and conquer algorithm for allocation
- Usually burnt into ROM of NIC
- OUI - Organizationally Unique identifier
	- specifying the manufacturer of the NIC
- MAC is 48 bytes -> should last until 2080
	- first 3 bytes - OUI
	- last 3 bytes - NIC specific
	- first two bits in first byte
		- 0 -> unicast / broadcast (message)
		- 1 -> globally unique (OUI enforced) or locally administered (1) e.g. in virtual environments
	- (IEEE recommendation is to move to EUI-64)


Ethernet addressing


Unicast
- Frame is intended for just the addressed interface (NIC)
- flood
	- switch (network equipment) forwards frame to all known hosts
	- used if switch doesn't recognize address

Multicast
- frame is forwarded to all local hosts - they can ignore it

Broadcast
- FF:FF:FF:FF:FF - sent to all hosts for processing


ARP - address resolution protocol
- For getting MAC address of unknown (if IP is known)
- local hosts and switches will typically cache ARP messages
	- so they don't have to fetch them again and again
- ARP table has mapping of MAC addresses to IP addresses
	- can be done dynamically or statically
	- static : administrator defines mapping manually
- broadcast to all hosts used if target hosts's address not in cache
- how 
	- before sending frame (if on same LAN (network part of IP))
	- check ARP cache for destination device MAC address
	- generate ARP request frame
	- Broadcast ARP request frame
	- other side
		- prcoess ARP frame
		- generate ARP reply frame (if it's for me)
		- update ARP cache (for replying later)
		- send ARP reply frame
	- process ARP reply frame
	- Update ARP Cache
- Link layer or Network Layer Protocol?
	- both :) (level 2 and 3 protocol)
	- bridges between the two

Reverse ARP
- client broadcast for an IP address

Proxy ARP
- connect two subnets via a single router

TDM - time dvision mutliiplexing
FDMA-  frequency division multiple access

WAN - wide area network

FDDI - fiber distributed data interface


Network services
![Screenshot 2024-11-16 at 16.04.33.png](../images/Screenshot%202024-11-16%20at%2016.04.33.png)



What guarantees can or should a Network offer?
- guaranteed delivery
- in order packet delivery
- guaranteed delivery within a specified time
- guaranteed bandwidth
- security
- IN DETAIL
- guaranteed delivery
	- all packets sent will eventually arrive at destination
	- issue if forced to take same path
- in order packet delivery
	- packets arrive in the order they are sent
	- issue if multiple paths allowed
- guaranteed delivery within a specified time
	- packets will arrive within a specified time
	- issue if there is congestion
- guaranteed bandwidth
	- sending host is guaranteed a specified bit rate (e.g. 1Gbps) to the destinatino
	- inefficient if not fully utilized
- security
	- no eavesdropping
	- no diversion to different hosts

LAN
- local to an office, floor, building, campus
- different degrees and different hardware
- scaling up requires linking LAN's together

WAN (wide area networks)
- connect LANs together
- allow traffic from one LAN to be sent / received at another
- problem of WAN is to be able to operate at scale
	- longer RTT
	- different infromation capacity domain
	- planetary level WAN development has taken 50 years
- Architectures
	- X.25
		- extensive error detection and correction
		- guaranteed delivery in order
	- ATM
		- dedicated circuit between two ends
		- guaranteed delivery
		- bounded delay
		- guaranteed bandwidth
	- Internet
		- connectionless
		- best effort service
		- no guarantees on anything

MAN (metropolitan area network)
- interconnection of networks in a city

Store and forward packet switching

Circuit switching vs packet switching
- an issue of Quality of Service

Circuit switching
- connection oriented
- dedicated circuit between two ends
- championed by phone companies
- allows packet delivery rate and bandwidth to be guaranteed
	- (no random dynamic activity can affect it really)

Packet switching
- connectionless
- championed by DARPA and university development
- packets sent through network on arbitrary routes
- no guarantees of deliveery, rate or bandwidth
- best effor


Problems to be solved in WANs
- Addressing
- Routing
- Fragmentation
- Reliaility
- Order
- time
- Scale
- IN DETAIL
	- Addressing
		- How are hosts identified to each other
	- Routing
		- how do packets konw which address and where to go to (or routers konw here to send them)
	- Fragmentation
		- if large packets are broken up, how are they put back together
	- Reliaility
		- how are errors handled
	- Order
		- how is data delivered in the order sent
	- time
		- how long do we allow for end to end delivery
		- when can the network layer give up
	- Scale
		- how many nodes can the network accomodate?
		- how much traffic can they generate


reliable delivery (w.r.t. WAN)
- all packets sent are delivered 
- or the connection is dropped
- and in order
	- all packets sent are delivered in the order which they are sent
	- or the connection is dropped
	- e.g. TCP


reliable delivery (w.r.t. WAN)
- packets of data can be arbitrarily dropped without dire consequence or reaction - e.g. IP and UDP

Architectural principles of the Internet
- connectivity is its own reward
- end-to-end functions require end-to-end protocols
- experience trumps theory
- all designs must scale
- be strict when sending and tolerant in receiving
- circular dependencies must be avoided
- modularity is important. keep things separate whenever possible
- keep it simple - avoid options and parameters when possible

The Internet protocol stack
![Screenshot 2024-11-16 at 16.18.51.png](../images/Screenshot%202024-11-16%20at%2016.18.51.png)
![Screenshot 2024-11-16 at 16.19.44.png](../images/Screenshot%202024-11-16%20at%2016.19.44.png)


IP datagram
- a basic network transfer unit
	- a self-contained independent entity of data carrying sufficient infromation to be routed from the source to the destination computer without reliance on earlier exchanges between this source and destination computer and the transporting network
- contains a header and then some payload
- IP is unreliable
- transmitted in big-endian order (network byte order)


IP fields
- IHL
	- header length (options field in header is not mandatory)
- type of service
	- indicates type of traffic
	- now known as diff serv code point
	- has never erally been used
- total elgnth (of entire datagram)
- ID - used to identify datagramfragments
- Flags - whether datagram can eb fragmented, fragmentation control
- frag offset (used in frag reassembly)
- TTL
- Protocol - layer 4 protocol sending IP packet
- header checksum (on header only)
- IP options (debuggin ( record route) and research)

Fragmentation in IP
- within the network there are no guarantees
- datagrams can be arbitrarily borken up and reassembled
- MTU : maximum transmission Unit for link
	- can be less than IP datagram size
	- Routers must then break datagram into fragments
- IP packets can be lost - so needto konw
	- offset, sequence, last fragment

How do hosts find each other
- LAN
	- MAC address is used to build a shared table
- Internet - IP address
- ARP maps between them
- IPv4 still dominates internet addressing

IPv6 removes
- IHL, type of service, total length (just payload), flags, fragmentation TTL (use hop limit), protocol and more

IP addresses
- high end bits are network identifier
- other bits are host
- used to be classful network architecture 
	- A, B, C
- Subnetworks
	- a logical division of the IP network address space 
	- written using / to provide a shorthand reference
	- 198.0.1.130/24 -> 24 bits allocated to network prefix (last 8 bits are host address)
- Scaling issues
	- original
		- Networks could only be assigned on the 8 bit boundary
		- address ranges did not map onto address requirements
- addreses allocated via Internet Assigned Numbers Authority Regional Registiries
	- AFRINIC
	- APNIC
	  ARIN
	  LACNIC
	  RIPE NCC
	  etc.

How many addresses available in range  = 2^{32 - mask}


Reserved addresses
- 127/8 range
- 10/8
- 192.169/16
- 224-239 - multicast
- limited local broadcast 255.255.255.255/32


Classless interdomain routing (CIDR)
- introduced in 1993 to replace classful
- goals
	- slow down growth of Internet routing tables
	- slow exhaustion of IPv4 addresses
	- Network could be assigned on any bit boundary
	- AS (autonomous system) - the entity that controls an internet routing policy

Network address translation NAT
- Problem
	- not enough IP addresses for everybody
	- not everybody wants one - security issues
- remaps one IP address space to another
	- can hide an entire network behind one public IP address
	- rewrite source IP address on outgoing traffic
	- remembers mapping of IPs for network behind it
- Impact incoming connectivity
	- NAT device can easily track outgoing traffic and remap
	- much more difficult to matchin incoming traffic to destination
- limited by port range on NAT device
- Creates problems as well
	- any kind of p2p application
		- generally isn't possible to directly connect to a server behind a NAT
		- devices behind a NAT cna connect to the server though
	- Anybody who wants to host an Internet application on their home network
		- ISP agreements may also prevent this (bandwidth restrictions)
	- distributed applications (multi-user games, phone/chat applications)
	- this was not the design intent for the Internret (to have one public IP for multiple devices)
- NAT translation table hsa WAN side and LAN side
	- NAT changes source address of outgoing and destination of incoming (if some connection existed prior, else drop)
- security considerations
	- removes your home devices from the public Internet
	- also often includes some firewall capabilities
	- but port forwarding disbles this protection for that port
	- most devices on the internet are constantly being scanned
- NAT and IP exhaustion
	- fixes the issue that there aren't enough public addresses for everybody
	- NAT remaps one IP address space to another and can thus encapsulate many internet objects at once with just one public facing address


NAT traversal techinques
- bypass security policy of NAT <- firewall stuff
- NAT violates principle that addressing is no longer end to end
	- issue is incoming connections - which computer is their destination
- number of ways to solev this
	- TURN
		- traversal using relays around NAT
	- NAT hole punching
	- STUN
		- Session traversal utilities for NAT
			- package of methods to circumvent NAT
	- ICE
	- UPnP
		- protocol to allow request to router to open port
		- allows NATed host to learn public IP address
		- add/remove port mappings with lease times
		- (automated static NAT port map configuration)
		- various security issues
	- NAT-PMP
		- runs over udp and uses port 5351
- Legitimate technique
	- static configuration
		- statically configure incoming connection requests at given port to server -> always forward traffic to this port to specific MAC address (machine) inside the LAN
- Hole punching
	- Assuming two hosts konw each other's NAT IP addresses
		- can try and guess the port being used by the NAT
		- somewhat dubious
	- TCP hole punching
		- Both hosts reuse the same local endpoint to try to connect simultaneously (violates TCP standard)
		- relies on the SYN packet getting through on one side
	- relaying
		- NAed client established connection to relay
		- external client connects to relay
		- relay bridges packets between the two connections


Addressing and routing are related to NP complete problems
- Addressing
	- how do addresses get assigned
	- is there some kind of central allocation
	- if not, how are they guaranteed unique
- Routing
	- is there some kind of central route finder
	- if not how is routing responsibility distributed
- both operate within Fisher consensus issues
- General appraoch : delegate and distribute authority


Wide area addressing
- how to solve it
	- store a directory with routing details of each address (centralized)
	- or encode the routing information in the address (distributed)
- For large networks, information limits prevent centralized solutions
	- Postal System (WAN) - address encodes dlivery infromation
	- IPv4, IPv6 - address encodes delivery infromation (DNS, etc.)
	- MAC (LAN) - address is a unique identifier, no delivery information - must use ARP

Post office addressing
- the Address encodes the route
- hierarchical (often breaks down locally)
- each address must be unique
- Address allocation is decentralized
	- each country/city/street can allocate its own addresses independently
	- name must be unique at their level
- Each delivery hub only needs to know how to send to the next hub
- IP addressing works exactly the same
- MAC addressing is simlar
	- delegation to manufacturers within their range
	- LAN's then rely on broadcast messages to fill in address tables (locally)

IPv6
- includes a simplified header format
	- fixed-length 40 bytes
	- no fragmentation allowed
	- next header - upper layer protocol being carried or Options
	- no checksum
- ICMPv6 - additional messages, packet too big
- backwards compatibility
	- tunneling used for routers which don't support IPv6
	- IPv4 routers carry IPv6 as a payload in an IPv4 datagram
- addresses
	- 128 bits in length adn written as a string of hexadecimal values
	- for displaying
	- omit leading 0s
	- omit all 0 segments (double colon - but can only be done once else it is ambiguous) (but can do many at once :) if they are contiguous)
	- structure
		- first 48 bits are global routing prefix
			- registires get first 12 bits
			- ISPs get the next 32 bits
			- organizations get 48 bits from the isp i think
		- subnet is in maximum 16 bits
		- last 64 bits are used for host

IP address exhaustion
- original decentralized network design was subtly biased towards central control
- ANT is necessary to allow computers access to the Internet
- Doesn't allow them readily to access each other
	- p2p is hard
	- need a central point to co-ordinate
	- therefore applications are mostly client-server (heavily hierarchical controlled by a central party)
- P2P applications possible but operate at a disadvantage


ICMP - internet control message protocol
- used to send error messages
- used for debugging
- starts after IP header
- maximum length is 576 bytes
- cotnains the IP header of the packet that caused the error message plust at least the first 8 byts of its data
- has been used to create covert communication channels (ICMP tunnels)
- e.g. message types
	- destination unreachable
		- packet could not be delivered
	- time exceeded
		- ttl hit 0
	- parameter problem
		- invalid header field
	- source quench
		- choke packet
	- redirect
		- teach a router about geography
	- echo and echo reply
		- check if a machine is alvie
	- teimstamp request / reply
		- echo but with timestamp
	- rotuer advertisement / solicitation
		- find a nearby router
- traceroute uses packets with smaller and smaller TTL - see when error occurred via ICMP to see what router was stopped at


IP vs. Transport layer services
- IP only provides best effort delivery between hosts, not proceses








UDP (user datagram protocol)
- uses port numbers to address process (sockets) on a host
- connectionless protocol
	- checksums for data integirty
	- port number addressing
- no end to end guarantees
	- udp datagram can be 
		- delivered in any order
		- dropped at any point
	- lack of overhead means UDP should be delivered faster
- Very simple protocol
- preferred for trouble shooting, logging, congestion or non-critical traffic etc.
- Originally intended for real time, unreliable applciations
- UDP header includes
	- length - of header + payload
- checksum
	- optional in IPv4 (not in IPv6) (0 if unused)
	- may be used for error checking of the header and data
	- 16 bit ones' complement of the ones' complement sum of IP pseudo header, UDP header (with checksum field set to 0) and payload (padded with 0s if necessary)
	- pseudo header 
		- stuff from ip header


TCP (transmission control protocol)
- uses port numbers to address process (sockets) on a host
- Provides network guarantees
	- all packets will be delivered (reliability)
	- ... in the order they were sent
	- or connection will be dropped
	- NO guarantees about HOW LONG this will take
	- guaranteed reliable, in-order packet delivery or your connection gets dropped
- e.g. file transmission
- implemented using IP datagram packets
- connection-oriented
	- a connection is required
	- sender and receiver must establish 
		- a connection between one another
- two-way connection
	- sender
	- receiver
- involves receive and send buffers
	- Kernel/OS is responsible for segment reassembly (TCP layer)
		- NIC is responsible for handling Ethernet frames correctly
		- allows TCP/IP to run over different low level protocols at each end
	- Traffic stream is reassembled in correct order
	- out of order packets arriving too early are queued
	- lost / delayd packets requested for retransmission
- Flags
	- URG
		- Urgent data, prioritise
	- ACK
		- acknowledgement
	- PSH
		- send data to application immediately
	- RST
		- reset
	- SYN
		- establish connection (first packet)
	- FIN
		- terminate connection
	- ECE
		- ECN-Echo
		- if SYN flag = 1 - peer is ECN capable
		- syn flag = 0 - network congestion notification
	- CWR
		- congestion window reduced
	- NS
		- ECN-nonce (experimental RFC)
- some options
	- maximum segment size (MSS)
	- window scale
	- SACK (selective acknowledgement permitted)
	- timestamps
- Segment numbers (included in each TCP segment)
	- Sequence number
		- number of byte in stream of first byte in segments' data
	- acknowledgment number
		- number of next byte expected
	- states maintained to know what has arrived and what hasn't 
	- both sides maintain separate counters for sent and received traffic
	- ISL - initial sequence number
		- range 0, 4294967295
			- so that a spoofed entry has a harder time of intercepting
- server and client hosts have to handle consequences of semgnets 
	- arriving out of order
	- being deleayed
	- being dropped
- Maintain local state to do so
	- Transmission control block (TCB)

piplined vs. stop and wait
![Screenshot 2024-11-16 at 17.56.15.png](../images/Screenshot%202024-11-16%20at%2017.56.15.png)



Raw socket
- so that header is not automatically generated use sock opt IP_HDRINCL


Sliding window protocols
- sender keeps a buffer with sent segments
- the receiver keeps a similar buffer
- sender doesn't delete the segment it has sent, until it receives an acknowledgment from the receiver
- when it does, it advances its pointer in the window to the next unacknowledged segment
- ![Screenshot 2024-11-16 at 17.58.17.png](../images/Screenshot%202024-11-16%20at%2017.58.17.png)
- window partitions the sequence of packets into three sets
	- those that have been successfully transmitted and acknowledged
	- those that have still to be acknowledged
	- and those that have yet to be transmitted

Reassembly in TCP
- begins with each segment having a sequence number
	- hosts know the order segments were sent in
- Host and client use timeouts
	- give up on waiting semgents
- how long should the timeout be?
	- too short
		- premature timeout -> unnecessary retransmission
	- too long
		- slow reaction to lost packets
	- depends on rount trip time
		- dpeends on medium being used for transmission and how far away the hosts are
	- implies hosts and client have to measure RTT
- Connection is seen by application as a single stream of data
- TCP/IP originally used as a file transfer protocol

client
- connect
- send
- close()

server
- listen
- accept
- recv
- close()

How does the receiver know the TCP data length
- there is no length field in TCP header
- implementation dependent on TCP standard
- any lower level protocol will have to provide the source address, destination address and protocol fields and some way to determine the TCP length, bot hto tprovide functional equivalent service of IP and to be used in the TCP checksum

TCP does not include a length field


TCP protocol phases
- connection establishment
- data transfer
- connection termination

TCP endpoint states
- LISTEN 
	- represents waiting for a connection request form any remote TCP and port
- SYN-SENT
	- represents waiting for a matching connection request after having sent a connection request
- SYN-RECEIVED
	- represents waiting for a confirming conenction request ack after having both received and sent a connection request
- ESTABLISHED
	- represents an open connection, data received can be delivered to the user
	- normal state for the data transfer phase of the connectoin
- FIN-WAIT-1
	- waiting for a connection termination request from the remote TCp or an ack of the eonnction termination request previously sent
- FIN-WAIT-2
	- waiting for a connection termination request from the remote TCP
- CLOSE-WAIT
	- waiting for a connection termination request from the local user
- CLOSING
	- represents waiting for a connection temrination request ack from the remote tcp
- LAST-ACK
	- waiting for an ack of the connection termination request previously sent ot the remote tcp (which includes an akc of its conneciton terminatino request)
- TIME-WAIT
	- waiting for enough time to pass to be sure the remote tcp received the ack of its connection termination request
- CLOSED
	- represents no conneciton state at all

active close vs passive close tcp
- active close -> the one that initiates the close
- passive close -> the other side

![Screenshot 2024-11-16 at 18.25.38.png](../images/Screenshot%202024-11-16%20at%2018.25.38.png)
- what can go wrong?
	- server doesn't receive SYn
	- client doesn't receive SYN+ACK
	- server doesn't receive ACK
	- server receives duplicate SYN

![Screenshot 2024-11-16 at 18.26.57.png](../images/Screenshot%202024-11-16%20at%2018.26.57.png)


Denial of service attack
- objective is to take down the hosts

SYN flooding - Denial of service attack
- oeprates by causing servers to use up their resources (memory)
- server has to remember state of connecting clinets
	- each open connection consumes some amount of memory
	- server will eventually teimout
- typicall organised using botnets (Distributed Denial of Service DDoS)
- send spoofed SYN packets
	- server responds with SYN acks that go nowhere
- Countermeasures
	- INcrease TCP backlog
	- reduce the SYN-RECEIVED timer
	- SYN Cahces - reduce size of state stored by server
	- SYN cookeies - reduce state storage to 0
	- Development of stateless connect protocols
		- stream control transmission protocol (SCTP)

SYN cookies
- moves state of connection into the ack field
- transmission ctonrol block (TCB)
	- server computes hash of basic TCB
	- sends this in ack field in SYN + ACK
	- client returns this when completing connection
	- more information being stored in TCP timestamp to preserve high-performance optimization
- Alters TCP syncrhonization procedures from RFC 793

TCB - transmission control block
- A special block of data associated with a table that contains all TCP connections
- a set of timers and three software modules
	- main module
	- input processing module
	- output processing module

SO_REUSEADDR
- closing a TCP connection puts its socket into TIME-WAIT
- has to stay at least 2 * maximum segment lifetime
- allows outstanding packets to drain from entwork
- most implementations do not allow connections in this state
- reuseaddr disables it

TCP round trip time (RTT)
- TCP timers have to adjust to Round Trip Time on connection
	- too short and you get a premature timeout and excess retransmissions
	- Too long and you get slow reaction to segment losses
	- RTT is variable
- Endpoints measure RTT from packets and adjust timeout appropriately
- Measured via exponential weighted moving average
	- (influence of past sample decreases exponentially fast)
	- estimatedRTT(t) = (1 - alpha) * estimatedRTT (t-1) + alpha * SampleRTT(t)
		- lerping with two variables :)
	- alpha = 0.125
- SampelRTT
	- timeout interval - estaimated RTT plust safety margin
	- estimate SampleRTT deviation from estimated RTT
	- devRTT = (1-beta) * DevRTT(t - 1)  + beta |sampleRTT(t) - EstimatedRTT(t)|
	- beta = 0.25
	- timeoutInterval(t) = estaimtedRTT + 4 *  DevRTT(t)
- TCP timeouts vary according to underlying conditions

TCP timeout
- what happens?
	- depends on state client / server are in
	- during transfer - packets will be retransmitted
		- retransmit segment(s) that caused timeout
		- restart timer

SACK - selective acknowledgment
- TCP sockets typically transmit sequences of pakcets
- don't wait for each packet to be acked first
- allow missing packets to be requested


TFTP (trivial file transfer protocol)- sourcerer's apprentice syndrome
- issue in stop and wait
- TFTP required the generation of a reply packet to any packet
- consequence was delayed packets triggered two acks
- the receipt of those acks triggered two more packets
	- every packet following is duplicated


Network congestion collapse issues
- common in early internet
	- retransmission of dropped packets increased load which caused more packets to be dropped
	- first intervention was to make TCP/IP reliably unreliable
		- end computers dropped connection if too many delayed/lost packets
- Original idea
	- TCP for applications that were not time sensitive 
		- needed reliable connections
		- network handles the nasty error correction/detection/reordering
	- UDP for applications that were time sensitive
		- transmission is faster - less reliable
		- because pakcets are time sensitive no poin in delivering them too late
- Congestion control and fairness
	- we thought we could drop TCP in leau of UDP (TCP will recover, UDP will not)
	- this caused TCP starvation because some applications started using UDP for reliable traffic
		- by effectively re-implementing TCP but without congestion adaptive behavior
	- UDP packets are now preferentially dropped by backbone routers as a consequence


Errors from the view of the network
- missing / delayed packets
- timeouts being too long or too short when reacting to errors
- network congestion due to too much traffic
- behavior of protocol triggering network congestion
- especially: tragedy of the commons type errors

TCP evolution
- 1988 - Tahoe
	- congestion avoidance and control
	- fast retransmit
- 1990 - RENO
	- modified congestion avoidance algorithm
	- fast recovery
	- reactive 
	- (fixing tahoe)
- 1994 - Vegas
	- New techniques for congestion detection and avoidance
	- attempt to be more proactive
- 2000 - Westwood
	- adaptions for high-speed environments
	- modifications for large bandwidth-delay and packet loss
		- WiFi/Cellular network behavior
		- aka leaky pipes
- 2014 - Borman
	- Extension for high performance

Flow control (throttling)
- what
	- management of data flows
	- avoid sending data too quickly (overwhelming the sender)
	- attempt to avoid sending data too slowly
- how
	- sliding window and window sizes
		- receiver advertises a window size to sender
		- sender cannot send more unacknowledged bytes than this
	- option for TCP window scaling
		- multiplier on header window size (right shift by value in header options, advertised during setup, must be supported by both sides, otherwise ignored)
	- sender window size is controlled by the receiver's window value
	- actual window size may be smaller if there is network congestion
	- can be changed with setsockopt

Optimal window size
- capacity of available network path
	- capacity(bits) = bandwidth(bits/s) * RTT(s)



Long Fat networks (LFN)
- have a large bandwidth-delay product
	- Bandwidht * rtt > 10^5

- TCP
	- originally intended for slow file transfer (FTP)
	- e-mail, usenet, IRC
- No WiFi or Cellular Internet
	- much higher delays than wired connecitons
	- higher errors, more prone to large dropouts
	- require more buffering end to end
- Requires large buffers end to end - can potentially increase overall delay
- no centralized way to control overall network load
	- internet is inherently decentralized
- large enough networks can always be overloaded
- congestion handling had to be built into its protocol
	- TCP connections will attempt to perform end to end flow control


![Screenshot 2024-11-16 at 19.10.39.png](../images/Screenshot%202024-11-16%20at%2019.10.39.png)
- goodput -> data that gets through without being dropped

Keepalive
- endpoints with low traffic can periodically exchange keepalive packets
	- stops connection being automatically torn down due to no traffic
- enabled with setsockopt

Network overhead (badput)
- IP packet overhead
	- IP setup - SYN, SYN ACK, FIN, FIN, ACK, ACK
	- don't carry data
- TCP & UDP packet overhead
	- headers

Piggyback ACKs (Delayed acknowledgments)
- A host may delay sending an ACK response by up to 500 ms
- But with a stream of full-size semgnets, must ack every second data segment
- ACKs can then be placed on data traffic going the other way (potential saving of 40+ bytes everytime this is done)
- potentially improves performance / traffic with small packets
- Can create silly window syndrome
- Can interact badly with Nagle's algorithm


Silly window syndrome
- what
	- ?
- how to fix
	- can be hard to recover
	- forced receiver to wait until it has a reaonsable amount of buffer space
	- whichever is smaller
		- wait until buffer is half empty
		- wait until can handle the starting Max Segment Size (MSS)
	- goal
		- sender doesn't send small segments
		- receiver doesn't ask for them

Nagle's algorithm
- attempt to limit number of small packets / connection
- typically on by default
- as long as there is a sent packet outstanding (no ack)
	- sender will buffer data arriving to be sent
- Data is then sent
	- when segment amount of data has been received
	- ACK arrives for previous segment
- issues
	- should disable when working with real time traffic
	- can be problematic with timeouts
		- if using aggressive (relatively short) timeouts
		- connection can eb dropped, whilst Nagle is delaying traffic
		- Servers may do this if handling lots of connections
			- Don't want stale connections around any longer than necessary
	- Can create deadlock with dealeyd ACKS (piggy back acks)
		- receiver watis fro data to piggyback ack on
		- sender waits for an ack to send data

ACK starvation
- asymmetric traffic
	- large flows in one direction
	- small or no traffic coming back
- ACk starvation can occur if no traffic to piggy back on
- typically some kind of bug in underlying network software
- manifests intermittently because not seen with normal traffic


TCP timer management
- Retransmission (RTO)
	- waiting for a segment ACK
- Persistence
	- used to periodically send window probes
- Keepalive
	- length of time without data before server tears down conneciton
	- default is 120 minutes (2 hours)
	- to keep connection open
	- keepalive packet
		- a packet with no data, and ack bit on
		- reply is also no data, ack bit on
- Time-waited
	- connection termination (TIME-WAIT)

Slow start algorithm
- Congestion window
	- sender's window size can be altered by network congestion
		- overrides user settings
	- sender hs 2 window sizes
		- Receiver's advertised window size
		- congestion window size (CWND)
		- Actual size min(Receiver's size, CWND)
- Congestion control
	- additive increase - multiplicative decrease
	- sender slowly increases transmission rate (window size) until reaches limit or segment losses occur (signaling congestion)
	- Start of connection
		- CWND = MSS
		- for each Acked segment : CWND += 1 MSS
		- until reaches half the allowed window size
		- after this, increase sublinearly : CWND += 1 / segment ACK
			- until threshold is reached or ACK timeout occurs
	- quick initial growth - increases exponentially for half the threshold size
	- slow start is required of all TCP connections
	- when ACK timeout treat as congestion symtpon
		- reduce threshold
		- threshold value is set to 1/2 the last CWND
		- CWND = 1 MSS
		- Rinse, repeat
- Issues with slow start
	- assumes unacknowledged segments are always due to network congestion
		- but could be caused by poor data link layers, e.g. wireless and cellular
	- performs badly with short lived connections
		- doesn't have time to converge
		- can't always hold connections open (persistence)

![Screenshot 2024-11-16 at 21.03.06.png](../images/Screenshot%202024-11-16%20at%2021.03.06.png)




Fast retransmit and fast recovery
- if TCP detect an out of order segment
	- generate an immediate ACK (duplciate ACK)
	- inform sender what segment number is expected
- if 3 or more consecutive duplicate ACKs received
	- retransmit immeidately - fast retransmit
	- reset threshold to half last CWND
	- each new ACK increases CWND by MSS/CWND
- slow start remains, small change to congestion handling arithmetic
- TCP RENO
	- added fast recovery
	- at congestion (lost ACK)
		- save half CWND as threshold and as new CWND
		- i.e. skip slow start
		- once threshold is reached, CWND += 1 RTT

![Screenshot 2024-11-16 at 21.06.49.png](../images/Screenshot%202024-11-16%20at%2021.06.49.png)


Average throughput of TCP connection
- common complaint is TCP gives artificially low throughputs
	- ignore slow start, assume always have data to send
	- w: Window Size w: window size where loss occurs
		- congestion adaption moves w between 0.5W and W 
		- average window size == 0.75W
		- average throughput == 0.75W/RTT
- You can get better throughput with multiple TCP connections but it depends
	- if OS threshold is incorrectly set too low
	- limit on connection will be less than actual bandwidth
	- limit is on each connection
	- -> multiple connections will improve throughput

Buffer management
- ciritcal to protocol behavior
- all network participants have send/receive buffers
- controlled somewhat independently
	- Buffer management may work at cross purposes to TCP/IP
	- routers have to protect themselves and their traffic
		- can't (shouldn't) interfere with TCP/IP packets
- Network components buffer as much as they can
- drop pakcets that come in and can't be uffered (Tail drop)
	- biased against bursty traffic
- issues
	- unfair allocation of buffer space to flows
	- TCP global syncrhonization
		- connections hold traffic back / send ti simultaneously
		- can create wave effects

Random early detection
- In buffers (when they get full) randomly drop packets instead of Tail dropping
- fairer: more packets a host sends, more likely to be dropped


Active Queue management (AQM)
- detect early signs of congestion
- Use ECN to try and maintain a good average queue size
- if managing lots of connections (router) randomly notify

Explicit Congestion Notification (ECN)
- must be negotiated by all participants
- works in conjunction with AQM (active queue management)
- reouter explicitly marks packets to signal congestion
	- Uses TCP header flags
		- ECN-echo (ECE), Congestion window reduced (CWR)
	- not end-to-end
	- must be supported by router, sender and receiver
- ECN compliant senders initiate congestion avoidence
- packets from non-ECN flows are dropped (RED)
- how
	- Packets aren't (shouldn't be) dropped
	- ECN notification is sent instead
		- with RED, ECN sent instead of packet drop
	- If it works, sender adapts as if a packet was dropped
		- changes congestion Window
- i.e. act before packet drops actually occur
- problems
	- low-rate denial of service attacks
	- RED algorithms notably vulnerable
		- Attack causes oscillating TCP queue size
		- RED chips in to make things worse


 Robust Random Early detection (RRED)
- attempt to filter out attack packets
- assume well behaved hosts will back off
- preemptively drop packets from hosts that don't


TCP Cubic
- designed for high bandwidth / high latency entworks
- window is a cubic function of time since last congestion event
- window size depends on previous congestion event
- does nto rely on ACK receipt
	- windows size quickly grows to previous limit
	- plateaus - grows very slowly probing for more bandwidth
	- grows quickly if it finds some
- window growth is independent of RTT
	- fairer to further away streams
- Increases window to be real-time dependent, not RTT dependent
- around max window size, growth becomes almost zero, but then gets larger


Bridging between the local network and the Internet(work)
- Protocols conceptually at the same level as IP (but all use IP)
	- DHCP Dynamic host control protocol
		- host address assignment
	- ICMP Internet Control Message Protocol
		- As used by ping
		- Encapsulated in IP packets
		- increasingly being blocked by routers / firewalls
		- can be used to scan ports, probe for hosts
	- ARP Address Resolution Protocol
		- Replaced by NDP (Neighbor Discovery Protocol) in IPv6


ARP
- bridges between IP address (Internet) and MAC address (local network)
	- IP address has dynamic / static assignment
	- MAC is statically assigned (usually)
- Uses own protocol - runs over Ethernet ARP packet
- security iessues
	- ARP spoofing / cache poisoning / ARP poison routing (Man in the Middle attack)
		- attempt to associate attacker's MAC address with a target host IP address
		- Attacker's machine will now receive target's traffic
		- there is no atuhetnication in ARP protocol
		- Requires direct access to local network
	- Defence
		- cross check IP and MAC assignments
		- Kernel software to reject uncertified ARP responses
		- Restrict access to local network to know MAC addresses


DHCP : Dynamic host configuration protocol
- Connectionless, UDP protocol
- UDP port numbers
	- client 68
	- server 67
- Dynamically assigns IP address and other network configurations to a host
- Clients lease DHCP addresses for configured time
	- hosts can have more than 1 IP address (2 LAN prots, or wifi etc.)
- how
	- client broadcasts DHCPDISCOVER message
		- can request its last known IP address (config)
	- server responds with DHCPOFFER
		- reserves IP address for client, sends info to client
	- Client broadcasts with DHCPREQUEST message
		- requesting address offered by server
		- May receive multiple offers, only accepts one
	- server sends DHCPACK
		- lease duration, other network config, lists DNS servers etc.
		- negotiation complete
- BOOTP
	- can configure DHCP so that client is sent a file
![Screenshot 2024-11-16 at 21.48.30.png](../images/Screenshot%202024-11-16%20at%2021.48.30.png)


	- TFTP (trivial file transfer protocol)
		- no user authetnication
		- no error recovery on large file transfer
		- uses UDP
	- Typically used to download software
		- dumb devices (terminals)
		- bricked devices (recovery)


Issues of scaling the net to planetary level
- Must be ableto assign network address locally
- must be able to manage networks locally (distributed responsibility)
- must be fault tolerant (adapt to)
	- changes in links and addresses
	- equipment failure
	- network congestion
- all without any form of real-time central control


Bridging
- creating a simple aggregate network from multiple network segments
- e.g. connecting two LAN segments
- relies on MAC address


Routing
-  selecting a path for traffic in a netowkr or between multiple networks
- Types 
	- datagram routing
		- route chosen packet on packet by packet basis
	- virtual circuit routing
		- route chosen per distinct connection
		- e.g. phone calls/phone networks
		- once set up, all traffic on circuit takes the same path
		- routers have tables to be able to forward the same way all the time
	- static routing
		- route chosen as a prearranged, hard defined, set of relationships
- Depends on 
	- length of the link
	- speed
	- delay on the link
	- congestion
	- monetary cost
	- (peering agreements)
- Routing algorithms
	- used to make decisions about the best path to use
- Routing protocols
	- implement routing algorithms
- how
	- can't be solved (well) by looking at each data stream separately
	- a real time constrained information transfer problem
![Screenshot 2024-11-17 at 08.43.05.png](../images/Screenshot%202024-11-17%20at%2008.43.05.png)
![Screenshot 2024-11-17 at 08.30.07.png](../images/Screenshot%202024-11-17%20at%2008.30.07.png)


Autonomous system (AS)
- A network typically controlled by a single entity (e.g. ISP or large organization) with independent connections to multiple networks
- has a single and clearly defined routing policy
- is assigned a unique number (ASN) from IANA

Interior Gateway protocol (IGP)
- protocol used to exchange routing information within an AS
- e.g. internal company/corporate network

Exterior Border Gateway protocol (eBGP)
- used to exchange routing and reachability information between ASs

Interior Border Gateway protocol (iBGP)
- Full mesh protocol used within an AS

Routing table, routing information base (RIB)
- table stored in router or networked computer
- lists routes to known network destinations
	- may include metrics / weights for those routes
	- e.g. distances
- contains information about the local network topology
- goal of routing protocols is to construct routing tables

Forwarding table (Content-addressable memory (CAM) table)
- used to relay packets between connected network segments
- optimised for fast lookup of destination addresses
- precise role depends on network location
- maps input network interface to correct output network interface
	- at periphery - map MAC addresses to ports
	- in centre, routing tables used to generate a forwarding table
- forwarding decision also depends on type of forwarding
	- unicast
	- multicast
	- broadcast


Local Area networks
- handles local netowkring
	- Ethernet and MAC addresses
	- Do not need IP address layer for some things to work
- May want physically separate networks
	- elementary security e.g. control access
- limits on cable lenght
- limits on number of machines on LAN

Bridges
- Dumb devices that allow lANs to be inter-connected
	- one of the ways VPNs can be configured on your local host 
	- when this is the case ifconfig (typically) only shows one ip address
- rely on forwarding tables - no routing
- broadcasts used to find unknown hosts
- also used to connect LANs to routers
- Devices often build up forwarding tables from information derived from broadcasts (or observed traffic)

NAT device perofmrs address translatino and forwarding, but does not make routing decisions

Routin protocols
- Interior Gateway protocols (IGP)
	- open shortest path first (OSPF)
	- routing information protocol (RIP)
	- Intermediate system to intermediate system (IS-IS)
	- Enhanced Interior Gateway Routing Protocol (EIGRP)
- Exterior Gateway Protocols
	- Esterior gateway protocol (EGP)
	- border gateway protocol (BGP)

Routing algorithms
- goal
	- reliable
	- fair
	- optimal
	- maximize total network throughput
	- minimise total packet delay (latency)
		- problematic if all the packets want to go the same way
	- stable - must converge to some kind of solution (equilibrium)


Sink tree
- only showing optimal routes to each node 
- DAG

Shortest path routing
- Bellman-Ford : centralised and distributed
	- distance vector routing
- Dijkstra' algorithm
	- Link state routing

Distance Vector Routing
- Each router maintains a table (vector)
	- best known distance to each destination
	- Which output link to use to get there
- Router is assumed to know distance
	- can be measured, or set
	- e.g. use router ping to measure RTT and delay
	- or examine output queues to that link (congestion)
- Distance vector algorithm (Bellman ford incomplete information)
	- dx(y) = min(c(x,v) + dv(y))) -> (cost of least-cost path from x to y)
		- dv -> cost from neighbor v to destination y
		- c(x,v) cost to neighbor v
	- dx(y) = estimate of least cost from x to y
	- node x knows
		- cost to each neighbor v c(x,v)
		- maintains its neighbors' distance vectors. For each neighbor v,x maintains
- From time-to-time each node sends its own distance vector estimate to neighbors
- when x receives new DV estimate from neighbor, it updates ist own DV using B-F equiation
- under minor, natural conditions, the estimate Dx(y) converges to the actual least cost dx(y)
- link cost changes
	- node detects local link cost change
	- updates routing info, recalculates distance vector
	- if DV changes, notify neighbors
- idioms
	- good news travels fast
	- bad new travels slow
- Properties
	- iterative
	- asynchronous
	- distributed
![Screenshot 2024-11-17 at 09.24.41.png](../images/Screenshot%202024-11-17%20at%2009.24.41.png)
![Screenshot 2024-11-17 at 09.25.12.png](../images/Screenshot%202024-11-17%20at%2009.25.12.png)


Routing information protocol (RIP)
- automatic routing protocol used in early Internet
- limit of 15 hops (to prevent routing loops)
	- poor scalability
- RIPv1 routers broadcast routing table updates every 30s
	- as Internet grew, massive bursts of traffic every 30s
- poor convergence
- various methods used to prevent known routing problems
	- split-horizon route advertisment
		- prevents routing loops
		- forbids router from advertising a route back on the interface that provided it
	- route poisoning
		- sends update with an inf metric
		- indicates that previously advertised route has gone down
	- holddowns
		- prevent delayed update messages changing metric
	- uesd UDP (reserved port number 520)

Count to infinity problem
- B had path to C which A knew of. C then drops. B sees that A has path to C but htat was through B. Still picks up that number, which reduces As number etc.


Link state routing
- Each router starts up and performs the following
	- discover neighbors and learn their network addresses
	- measure the delay or cost to each of its neighbors
		- RTT
	- construct a routing announcement with this information
	- send this to all other routers (not just neighbors)
		- aka flooding
	- compute shortest path to every other router
- this distributes (over time) complete information on network to all routers
- uses Dijkstra's algorithm
- centralised
	- single node gets topology information and computes routes
	- routes then broadcast to rest of the network
- distributed
	- each node i broadcasts d_ij to all j to its neighbors
	- who in turn flood their neighbors
	- all nodes then calculate shortest paths
	- Open Shortest Path First (OSPF) (Interior gateway protocol)
- Issues
	- algorithm complexity
		- n nodes
		- each iteration need to check all nodes w not in N
		- O(n^2) - O(n log n) possible
	- Oscillations possible
		- if equal cost of two (or more) paths

Distance vector vs linnk state
- distance vector
	- uses hop count for metric
	- network information at 1 hop remove
	- relies on timed/periodict updates
	- slow convergence
	- sucseptible to routing loops
- link state
	- uses shortest path
	- gets entire network topology
	- event triggered updates
	- faster convergence
	- less susceptible

hierarchichal routing
- different routing decisions
	- US ISP - chepar to connectt via Century Link
	- peering agreements

Autonomous system (AS)
- AS is a connected group of one or more IP prefixes run by one or more network operators which has a single and clearly defined routing policy
- Have an ID number - ASN -> 32 bit numbers
- allocated by IANA -> delegated to Regional Internet Registries (RIR)
- each ASN must have a unique AS to participate in BGP routing
	- Border gateway Protocol (BGP) is used between ASNs



![Screenshot 2024-11-17 at 10.32.40.png](../images/Screenshot%202024-11-17%20at%2010.32.40.png)


BGP hijacking
- Routing manipulation (BGP hijacks) are prevalent today and impact Bitcoin traffic

Path determination (routing)
- packet routing problem is believed to be NP-hard



NP-Complete routing problems
- path-constrained, path-optimized
	- select shortest path meeting specified constraints
- multi-path-constrained routing
	- find multiple paths meeting constraint
	- issue for high performance/traffic environments
- being studied for more elaborate routing constraint shcmes

how to distribute table updates
- flooding 
	- broadcast to all
	- scaling issues
	- typically used on local campuses
- peer update
	- propagation delay issues
	- updates to directly connected / trusted peers)
- neither guaranteed to be secure

Routin size
- size of routing tables
- time taken to calculate routes
- managing number of routing change announcements

Inernet is organized as organized mesh
![Screenshot 2024-11-17 at 10.39.22.png](../images/Screenshot%202024-11-17%20at%2010.39.22.png)


Interior gateway protocols : IGPs
- AS can choose its own interior routing scheme or schemes
- responsile for 
	- all interior routing
	- routing to and from other ASs
- Four types
	- Multihomed
		- maintains connections to more than 1 AS
	- Stub
		- Connects to only one AS
	- Transit
		- allows connections through itself to other ASs
	- Internet Exchange point (IP, IXP)
		- physical infrastructure
		- used by ISPs or content delivery networks to exchange traffic

Oper Shortest Path First (OSPF)
- Open - publicly available
- widely used in enterprise networks - companies / corporate
- uses link state algorithm
	- maintains map of network topology at each node
	- computes routes using Dijsktra's algorithm
- Advertisements - announcements of table changes
	- sent directly over IP
- All messages are authenticated
- Multiple same cost paths are allowed
- Type of sevice (TOS)
	- supposed to provide different routes per type of traffic
	- never implemented in practice
- Supports unicast and multicast
	- multicast is implemented using a group scheme
	- hosts join a multicast group
	- routers automatically distribute traffic to group members
- Supports a two-layer hierarhcy (Hierarchical OSPF)


Hierarchical OSPF
- ![Screenshot 2024-11-17 at 12.00.23.png](../images/Screenshot%202024-11-17%20at%2012.00.23.png)

Link State routing
- On startu each router examines its links
- measures a cost of the links for each neighbor
	- e.g. 
		- delay via ICMP echo packet
		- link bandwidth, actual cost ($), etc.
- Construct a packet of all information that it knows
- sends the packet to all other routers in the network (flood)
- process updates from network and sends updates to network

Is-IS - intermediate system to intermediate system
- Interior Gateway protocol - used by transit and core networks
- link state routing
- uses Dijkstra algorithm to compute best path
- operates directly above level 2 (uses own protocol, not IP)
	- protocol neutral - can support IPv6 without modification
- practically a better option than OSPF
	- even though OSPF is competitive
	- migration to IPv6 is easier with IS-IS
	- most larger ISPs had deployed IS-IS and had no reason to change

Border Gateway Protocol
- The glue that holds the Internet together
- Routing protocol used to interconnect Autonomous Systems (AS)
- allows routers to create a distributed routing table of IP prefixes
- Allows ASs to discover routes
- Routing is based on local criteria (not necessarily efficiency criteria)
	- e.g. peering agreement, cheap, length, etc.
- BGP lacks basic authentication mechanism
- Allows each AS to
	- obtain reachability information from neighboring ASs (eBGP)
	- Propagate this information to all AS-internal routers (iBGP)
	- Determine good routes to other networks (based on reachability and policy)
	- advertise its own existence
- Path Vector routing protocol
	- only installs "best path" into the routing table
	- only announces "best path" to other BGP peers
	- "Best path" can be manually controlled
- Uses TCP as transport protocol (via port 179)
- Needs to worry about politics sometimes
	- use something because its cheaper
	- never send traffic from the Pentagon through Iraq
	- etc.
- Decision process
	- WEIGHT
		- at local router, used to prefer one of multiple uplinks
	- LOCAL-PREF
		- at Local ASN - prefer one of serveral routers
	- LOCALLY GENERATED
		- local routes preferred over external
	- AS-PATH length
		- preference to shortest AS_PATHS
	- ORIGIN
		- Prefer 0-IGP over 1-EGP
	- MED
		- preference is given to lowest MED metric (Multi-Exit-Discriminator)
			- cold-potato or best-exit routing 
			- most networks use hot-potato -> get rid of foreign traffic
- BGP neighbors must be manually configured
- single TCP connection between routers
- All BGP message are sent as unicast 
- BGP routers may only belong to a single AS
- Once BGP peering established, keepalive messages sent every 60s by default
- UPDATE messages contain Network Layer reachiability information (NLRI)
- ASs share BGP message containing routes (example route)
	- PREFIX: 128.16.64/22; AS-PATH AS3 AS131; NEXT-HOP 201.44.13.125
	- router may receive multiple routes for same prefix but has to select 1 route (the best / shortest AS-PATH)
- inside
	- use NEXT-HOP attribute, the IP address of the router interface that begins the AS PATH
	- use OSPF to find shortest path from router receiving to the NEXT-HOP
	- router identifies port for route (along the OSPF shortest path)
	- adds prefix-port entry to its forwarding table

Path vector routing protocols
- use distance between themselves and destination as metric
- uses Bellman-Ford algorithm or similar
- Routers don't know the entire network topology
- they know the (locally) best output link for a given IP range
- Router appends its identifier to current path in updates
- allows loops to be avoided

Interior Border Gateway Protocol (iBGP)
- used with transit ASs
- BGP router must add its own AS number (ASN) when forwarding to another AS
	- to prevent routing loops from occurring
	- BGP will drop a route if it sees its own ASN in the AS_PATH list
	- if router forwards BGP within its own AS - will see its own ASN
		- internal BGP is used in this case

Hot Potato routing
- suppose there are more best inter-routes
- choose route with closest NEXT-HOP via OSPF

How does an entry get in forwarding table
- router becomes aware of prefix via BGP route advertisements from other routers
- Determines router output port for prefix
	- use BGP route selection to find best iner-AS route
	- Use OSPF to find best intra-AS route leading to best inter-AS route
	- Router identifies router port for that best route
- Enter prefix-Port entry in forwarding table


Cryptographic hash function
- function which maps arbitrary size data (input) to fixed length output
- designed to be a 1-way function - infeasible to reverse (invert)
- five important properties (for the function)
	- deterministic : same message -> same hash
	- Computable (quick to generate)
	- infeasible to reverse
	- small changes to message create an uncorrelated hash message
		- otherwise would be possible to reversse
	- Infeasible to get 2 messages with same hash value
- Application
	- used to verify file integrity (is copy the unchanged original?)
	- also used to identify the file
		- file signature
	- digital dignatures
		- guarantee of authenticity of message
	- password verification
		- store cryptographic hash of password
		- avoid storing password in cleartext or even encrypted
		- original password cannot be determine from stored hash

Message-digest algorithm : MD5
- Widely used hash function / algorithm
	- returns 128-bit hash for message
- used to provide guarantee original file is same as copy
- WAS widely used as cryptographic hash function
- examples
	- provide 1-way hash for a password (Linux)
	- BGP spoof protection
	- lightweight directory access protocol (LDAP)
- DONT USE

Old BGPSEC (using MD5)
- protect BGP against spoofed messages
- Each segment sent on BGP conenction, protected with MD5 digest
- hash of
	- TCP pseudo-header
	- TCP header, excluding options, with 0 checksum
	- TCP segment data
	- independent key known to both routers
- except
	- All information required to compute MD5 authetnication is present in the packet except the secret
	- runs over TCP - standard TCP attacks work, e.g. syn flooding and sequence number guessing


Secure gateway protocols
- S-BGP
	- academic - not deployed
- BGPSEC - BGP-4
	- relies on RPKI
	- Uses signed messages
	- Route Origin Authorisation (ROA)
		- digitally signed authority for route advertisement
		- contains address prefix and range of allowed sizes
		- originating ASN
	- how to know the route path is valid (AS pov)
		- it doesn't 
		- no way to validate that the authorised AS is providing a valid path
- RPKI
	- Resource Key Inftrastructure (attests AS/IP allocation)
	- protects against prefix / subprefix hijacks
	- protects agains route leaks
	- provides certification of number holdings in registry
	- can be circumvented (route leaks and path shortening)
- NEXT-AS attack is a thing


Domain Name System (DNS)
- Arpanet : IPs were mapped to host name in hosts.txt file
	- maintained by some guy
	- additions/deletions/cahnges were performed manually
- Berkley Internet Name Domain (BIND)
	- most widely used DNS software on the Internet
- Decentralised hierarchical naming system
- distributed, hierarchical database
- maps user firnedly computer names and url's to computer IP addresses
	- can map more than one computer to the same name
	- aliasing - allows load distribution across multiple hosts
- reverse mapping IP address => name
- relies on local servers and caching for performance
- 13 authorities provide 1058 top level domains
![Screenshot 2024-11-17 at 13.11.10.png](../images/Screenshot%202024-11-17%20at%2013.11.10.png)


TLD, autoritative servers
- top-ljevel domain servers
	- responsible for .com, .org, etc.
- Autoritative DNS servers
	- organization's own DNS servers providing authoritative hostname to IP mappings for organization's name hosts
	- can be maintained by organization or service provider


DNS resolver

Local DNS server
- not strictly part of the hierarchy
- each AS, ISP, company, etc. has one or more (typically at least 2) default name servers
- local hosts query is first sent to local DNS
	- maintains local cache of known name-IP address translations
	- acts as proxy, forwards query into public DNS hierarchy
	- caches may be out of date for some time

DNS name resolution example
- iterated query
	- contacted server rplies with name of server to contact

5 addressing methods
- unicast addressing
	- 1 to 1
- broadcast
	- 1 to all (local networks)
- multicast
	- 1 to many (addres can specify subset of nodes to receive)
- anycast
	- 1 to 1 form a set based on distance
- geocast
	- 1 to many based on physical networks (mobile, ad hoc networking)


Internet Corporation for Assigned Numbers and Names (ICANN)
- maintains protected cryptographic keys to control root level DNS
- ICANN delegates regional reopnsibility to accredited registrars
- TLDs can delegate authoritative control to the next lower level
	- US and Canada delegate to the state level
	- UK, Spain, etc. have opted for functional models .co=company
	- The owner of domain name can delegate anything "to the left"
- FQDN - Fully Qualified Domain Name techincally ends with a dot

BIND
- path of query
	- local machine resolver (cache)
	- local DNS caching reolve (cache)
	- regional server / authoritative server
- primary, secondary and tertiary name server can be configured
- when any DNS cannot resolve a request it bounces up to a root-server
- propagation of changes can take several hours
- resolvers use UDP for single name requests
- resolves may als ofill in a partial name and query
- tCP for groups of names
- recursive Query
	- refer query up the hierarchy
- iterative query
	- reply or give me next server in hierarchy
- each entry has a TTL
- can also specify type of service (e.g. MX = mail)

![Screenshot 2024-11-17 at 13.21.56.png](../images/Screenshot%202024-11-17%20at%2013.21.56.png)


DNS record
- DNS : distributed database storing resource records (RR)
- RR -> (name, value, type, ttl)
- types
	- A
		- name is hostname, value is IP address
	- NS
		- name is domain
		- value is host name of authoritative name server for this domain
	- CNAME
		- name is alias name for some canonical name
		- value is canonical name
	- MX
		- value is name of mail server associated with name
- Message format
	- query and reply with same format
	- message header
		- identification - 16 bit number for query, reply to query uses same number
	- flags
		- query or reply
		- recursion desired
		- recursion available
		- reply is authoritative


Attacks
- DOS (Denial of service) - a direct attack on DNS server
- DNS amplification / reflection attack
- DNS hijacking
- cache poisoning
	- set name to map to wrong ip address
- DNS tunnelling (UDP port 53)
- DNS server performance attacks (Slow Drip, Syn floods, NXDomain)

DNS amplification attakcs
- A DDoS that relies on the use of publically accessible open DNS servers to overwhelm a victim system with DNS reponse traffic
- attacke sends DNS name lookup request to an open DNS server with the source address spoofed to be the target's address
- DNS then sends the DNS record response to the target
- Attacker requests as much zone information as possible to maximize the amplification effect

DNSSEC
- company level : separate servers for internal and external resolution
- internal server inside the company network
- monitor DNS servers carefully (real time load, etc.)
- Adds cryptographic key protection to DNS server records
- provides origin authentication and integrity assurance
- signed origin attestation chain (PKI) starting at root

dig & nslookup -> DNS tools

Advise
- if you care where your traffic is routed, monitor it
- encrypt it, even if you don't care
- monitor encryption methods, their seucirty decayse over time


P2P overlay networks

P2P networking
- Peer - one that is of equal standing with another
- Networking in theory
	- p2p leverages the end nodes capabilities
	- escapes from the dumb terminal paradigm
	- in particular, allows end nodes to communicate with each other directly as opposed to classical hierarchical models (e.g., client/server)
- In practice - much more complex
	- e.g. status of intelligent browsers vs servers
	- at what level of the network is it P2P
- core concepts
	- self-organizing - no central management
		- may not be entirely true
		- source code, pre-arranged structures can embody organisation
	- resource sharing by end devices i.e. files, CPU, data
	- peers all have same capabilities and are more or less equal
	- large numbers of peers in entworks
	- based on voluntary collaboration e.g. SETI at home, Wikipedia
	- Principle are not always implemented in practice
- Principle - all nodes have equal network access
	- capacity scales as Lsqrt(N) (L no. of link connections) (N no. of nodes)
	- demand scales with N
	- L typically a function of bandwidth and CPU capacity
	- significant issues with Fisher Consensus
- in practice
	- for sufficiently large L and sufficiently small N scaling issues may not be apparnet
	- otherwise need to self-organize into group of groups structures
	- or increase L, reduce N, accept limit on scaling
- Structured P2P
	- lhas defined topology
	- peers and objects in networks have identifiers
	- distributed indexing provides object location
- unstructured P2P
	- objects have no special identifier
	- location of objects is not know apriori
	- each peer responsibible for its own objects
	- some form of search protocol used to locate
- technical impediments
	- NAT
		- Block direct access to local hosts
	- Firewalls
		- Blocks incoming connections
		- port 80 sometimes used to circumvent
	- Asymmetric Bandwidth
		- P2P creates demand for uplink as well as downlink bandwidth
		- ISPs overprovision uplink capacity in particular
- Technological challenges
	- linking hosts together scalably
		- random association may link widely separated hosts
		- true scaling requires some form of link related localism
	- hosts must be able to join and leave ad hoc
		- network churn can be very destabilising
	- locating objects / hosts / facilities within the P2P system
		- same issues as in internet, addressing and routing
	- tragedy of the commons issues
		- avoid leeching
		- distributing load equitably
		- file sharing - retaining complete copies across network
		- finding and keeping rare items


P2P history
- 1999 Napster -> coined term P2P
	- central servers were single point of failure
- 2000 Gnutella -> fully decentralised (rapidly hit scaling problems)
	- ultra-peers 2001
	- gnutella 2 - 2002 (new protocol and explicit topology (leaf/hub))
- 2000 bit torrent
	- 2004 responsible for 25% of all Internet traffic
	- distributed hash table for content indexing

![Screenshot 2024-11-17 at 13.46.53.png](../images/Screenshot%202024-11-17%20at%2013.46.53.png)


Addressing and routing in p2p
- centralization
	- single point to find things (e.g. a database)
	- can partition data across multiple databases
		- each DB has its own slice of the entire dataset
		- front end to direct requests to correct server
		- Divide and conquer
	- no consensus issues
	- poor fualt tolerance
		- but can replicate servers
		- single point of attack for adversary
- Distribution is hard
	- replication and fault tolerance is usually a given
	- scaling usually not a problem
		- organised distributed topology can be designed cf. skype
		- or will emerge (survivorship bias)
	- finding things is hard
		- peers have to have ways to query other peers efficiently
		- risk of causing broadcast storms
	- Fisher consensus fails -> any kind of guarantee is difficult

Early P2P data location methods
- Napster relied on central servers - easy but not robust
- Gnutella and similar relied on flooding query model
	- each search broadcast to next-hop peer
	- they recursively multicast request as required
	- eventually a machine replies it has the answer
	- advantages - extremely decentralised, very robust
	- disadvantages - extermely easy to create a broadcasts storm
		- TTL introduced to reduce this but
		- issue then becomes finding scarce files


Distributed Hash Table Algorithms (DHT)
- design goals
	- index and distribute entire dataset in network
	- scalable
	- handles node churn (rapid joining and leaving)
		- can also become broadcast storm issue
- Examples (roginal four)
	- content addressable network (CAN)
	- chord
	- pastry
	- tapestry
- Common approach
	- assign random (160-bit) ID to each node
	- define a metric topology on the 160-bit numbers, i.e. the space of keys and node IDs
	- each node keeps contact infromatino to O(log n) other nodes
	- provide a lookup algoriithm, which finds the node, whose ID is closest to a given key
		- we need a metric that identifies closest node uniquely
	- store and retrive a key / value par at the node whose ID is closest to the key


Content addressable networks (CAN)
- search space
	- d-dimensional coordinate space
- each node owns a  distinct zone in the space
- each node keeps links to the nodes responsible for zones adjacent to its zone (in the search space) ~2d on avg
- each key hashes to a point in the space
- Node joining
	- space is partitioned over a grid
	- First node to join owns grid
	- second node splits with first
	- third node is attached to node 1 or node 2 at random
		- takes half of their space
		- rinse, and repeat
	- on leaving, node's space is merged with adjacent ndoe
![Screenshot 2024-11-17 at 14.04.04.png](../images/Screenshot%202024-11-17%20at%2014.04.04.png)

Overlay networks
- A logical network laid on top of the internet
- DHTs used to create an overlay network for the P2P cloud
- node has to be able to efficiently join and leave network
- each node uses the algorithm provided by DHT
- picks neighbors and consequently creates a topology basedo n some idea of closeness
- hash kesy are created to identify similar objects
	- distributed among nodes
	- used to more or less efficiently route to desired destination


Chord (2001)
- P2P DHT with O(log n) search time
	- each step halves the topological distance to the target (expected log n hops to the target)
- each ndoe has a key which is the hash of the node's identifier
	- e.g. host IP address (reusing existing structure)
- each data item has a key which is the hash of it's file identifier
- any hash function ca neb used - paper used SHA-1
- N hash values are conceptually arranged in a circle, modulo N
![Screenshot 2024-11-17 at 14.03.52.png](../images/Screenshot%202024-11-17%20at%2014.03.52.png)
- each node is found at the location on the ring equal to its key
- each data item is stored in the smallest value >= to the data ey (modulo N)
- each node keeps local "finger table)
	- stores node keys K + 1, K + 2, K + 4, K + 8 (k is node's key)
- to find a key, find closest node in table without being > key
	- forward query to that node
	- results in a determinsitc way to find location based on data
- Node joining and leaving
	- when a node joins, it must create its own finger table
	- and other nodes must adjust theirs
	- original paper did not describe how this is done
	- requires some kind of bootstrapping node
		- typically implemented by using any node in the ring
		- still requires a way to find that node

Bitcoin
- uses own custom protocol over TCp
- peer discovery is by address rumoring (gossip protocols)
	- hosts randomly pick other hosts to exchange information
	- protocols attempt to put upper bounds on cost
- set of known good noes to begin with
- protocol falls back on a set of hardcoded peers

P2P networks current state
- a lot of different P2P protocols, mostly derived from DHT
- each is standalone, no interworking, not evengateways
- throwback to begginings of unconnected LANs
- scaling, routing, and reliability continue to be research issues
- lots of work still to be done


The application layer
- any networked application
- transport-layer service models
- client-server paradigm
- peer-to-peer paradigm
- application-layer protocols and infrastructure
	- HTTP
	- SMTP, IMAP
	- DNS
	- video streaming systems, CDNs

Client-server paradigm
- server
	- always-on host
	- permanent IP address
	- often in data centers for scaling
- clients
	- contact and communicate with server
	- may be intermittently connected
	- may have dynamic IP addresses
	- do not communicate direclty with each other
- eg.
	- HTTP
	- IMAP
	- FTP

Peer-to-peer architecutre (P2P)
- no always-on server
- arbitrary end systems directly communicate
- peers request service from other peers
	- self scalability - new peers bring new service capacity, as well as new service demands
- peers are intermittently connected and change IP addresses
- e.g. P2P file sharing (BitTorrent)


inter process communication
- IPC within same host (defined by OS)
- process in different hosts communciate by exchanging messages
- client process
	- process that initiates communication
- server process
	- process that waits to be contacted

Sockets
- process sends / receives messages to / from its socket
- socket is analogous to a door
	- sending process shoves message out door
	- sending process rlies on transport infrastructure on other side of door to deliver message to scoket at receiving process
	- two sockets involved (one on each side)

Application-layer protocol defines
- types of messages exchanged (request,response)
- messsage syntax (fields in message and how delineated)
- message semantics (meaning of info in fields)
- rules when and how to send & respond to messages

potential requirements from application
- data integrity
	- tolerates loss?
- timing
	- require low delay to be effective?
- throughput
	- require minimum amount of throughput to be effetive?
- security
	- encryption, data integrity, etc.

TCP offers
- reliable transport between sender and reciever
- flow control (sender won't overwhelm receiver)
- congestion control (trhottle sender when network overloaded)
- connection-oriented (setup required between client and server)
- does not provide
	- timing
	- minimum throughput guarantee
	- security

![Screenshot 2024-11-17 at 14.30.30.png](../images/Screenshot%202024-11-17%20at%2014.30.30.png)


Transport layer security (TLS)
- provides encrypted TCP connections
- data integiryt
- end-point authentication
- Apps use TLS liraries (application) that use TCP in turn
- cleartext is sent into socket, but traverses the internet encrypted

Web and HTTP
- a webpage
	- consists of objects, each of which can eb stored on different web servers
	- objects can be HTML file, image, audio file, etc.
	- web page consists of base HTML-file which includes several referenced objects, each addressable by URL

HTTP - hypertext transfer protocol
- Web's application-layer protocol
- client/server model
	- client
		- the browser that requests, receives (using HTTP) adn displays Web objects
	- server
		- web server sends (suing HTTP) objects in response to requests
- HTTP
	- stateless
		- server maintains no information about past client requests
		- hard to do anyway
	- uses TCP
		- client initiates TCP connection to server, port 80
		- server accepts
		- http messages (application layer protocol messages) exchanged between browser (HTTP client) and Web server (HTTP server)
		- TCP connection closed
- two types of connections
	- non-persistent
		- TCP connection opened
		- at most one object sent over TCP connection
		- TCP connection closed
		- (downloading multiple objects requires multiple connections)
		- issues
			- requires 2 RTTs per object
			- OS overhead for each TCP connection
			- browsers often open multiple parallel TCp connections to fetch referenced objects in parallel
	- persistent
		- TCP connection opened to server
		- multiple objects can be sent over single TCP connection between client and that server
		- TCP connection closed
		- server leaves connection open after sending response
		- subsequent HTTP messages between same client/sever sent over open connection
		- client sends requets as soon as it encounters a referenced object
		- as little as one RTT for all referenced objects (cutting response time in half)
- two types of messages
	- request
		- POST
			- user input sent form client to server in entity body of HTTP POST request message
		- GET
			- for sending data to server
			- include user DATA in URL field of HTTP GEt request message (follwing a ?)
		- HEAD
			- request headers only (the ones that would be returned if URL were requested with an HTTP GET method)
		- PUT
			- uploads new file (objects) to server
			- completely replaces file that exists at specified URL with content in entity body of POST HTTP request message
	- response
		- status codes
			- 200 OK
			- 301 moved permanently
			- 400 bad request
			- 404 not found
			- 505 http version not supported

Cookies 
- for maintaining user / server state between transactions
- 4 components
	- cookie header line of HTTP response message
	- cookie header line in next HTTP request message
	- cookie file kept on user's host, managed by user's browser
	- back-end database at web site
- what cookies can be used for
	- authorization
	- shopping carts
	- recommendations
	- user session state (Web e-mail)
- how to keep state
	- at protocol endpoints
		- maintain state at sender / receiver over multiple transactions
	- ine message
		- cookies in HTTP messages carry state
- cookies and privacy
	- cookies permit sites to learn a lot about you on their site
	- third party persistent cookies (tracking cookies) allow common identity (cookie value) to be tracked across multiple web sites 
	- e.g. ad service on websites -> get fetched across multiple sites and keep track of web browsing over sites. Can then return targeted ads based on browsing history
- can be used for 
	- tracking user behavior on a given website (first party cookies)
	- track user behavior across multiple websites (third party cookies) without user ever choosing to visit tracker site
	- tracking may be invisible to user
		- rather than displayed ad triggering HTTP GET to tracker, could be an invisible link


Web caches (proxy servers)
- goal: satisfly client requests without involving origin server
- user configures browser to point to a (local) web cache
- browser sends all HTTP requests to cache
	- if object in cache: cache returns object to client
	- else cache requests objects from origin server, caches received objects, then returns object to client
- act as both client and server
	- server for original requesting client
	- client to origin server
- server tells cache about object's allowable caching in response header
- why?
	- reduce response time for client request (cache closer to client)
	- reduce traffic on an institution's access link
	- internet is dense with caches
		- enables poor content providers to more effectively deliver content

 HTTP1.1 
 - introduced multiple, pipelined GETs over single TCP connection
- server responds in order (FCFS) to GET requests
- with FCFS, small object may have to wait for transmission (head-of-line blocking) behind large objects
- loss recovery (retransmitting over lost TCP segments) stalls object transmission


HTTP/2
- goal : decreased delay in multi-object HTTP requests
- over single TCP connection
	- recovery from packet loss still stalls all object transmissions
		- incentive to open multiple parallel TCP connections to reduce stalling, increase overall throughput
	- no security over vanilla TCP connection
- increased flexibility at server in sending objects to client
	- methods, status codes, most ehader fields unchanged from HTTP 1.1
	- transmission order of requested objects based on client-specified oject priority (not necessarily FCFS)
	- push unrequested objects to client
	- divide objects into frames, schedule frames to mitigate HOL blocking
![Screenshot 2024-11-17 at 15.42.29.png](../images/Screenshot%202024-11-17%20at%2015.42.29.png)
![Screenshot 2024-11-17 at 15.42.36.png](../images/Screenshot%202024-11-17%20at%2015.42.36.png)


HTTP/3
- adds
	- security
	- per object error- and congestion- control (more pipelining) over UDP

E-mail
- three major components
	- user agents
	- mail servers
	- simple mail transfer protocol SMTP

user agent
- mail reader
- to compose, send and read mail

mail servers
- mailbox 
	- contains incoming messages for user
- message queue
	- of outgoing (to be sent) mail messages

SMTP protocol
- protocol for exchanging e-mail messages
- delivery / storage of e-mail messages to receiver's server
- between mail servers to send email messages
	- client : sending mail server
	- server : receiving mail server
- Uses TCP to reliably transfer email message from client (mail server initiating connection) to server, port 24
- three phases of transfer
	- SMTP handshake (greeting)
	- SMTP transfer of messages
	- SMTP closure
- command/response interaction (like HTTP)
	- commands: ASCII text
	- response: status code and phrase
- Multiple objects sent in multipart message
- uses persistent connection
- requires message (header & body) to be in 7-bit ASCII

Mail access protocol : retrieval from server
- IMAP - Internet mail access protocol
	- messages stored on server
	- IMAP provides 
		- retrieval
		- deletion
		- folders of stored messages onserver

HTTP 
- gmail
- Hotmail, etc. provide web-based interface on top of SMTP 8to send) and IMAP or POP to retreive e-mail message

Video streaming and CDNs
- challenge: 
	- scale 
		- how to reach 1B users?
	- heterogeneity
		- different users have different capabilities
		- (how much data they can receive, and how fast)
- Solution
	- distributed application-level infrastructure

Multimedia: video
- a sequence of images displayed at constant rate (x images / sec)
- digital image 
	- an array of pixels, each represented by bits
- coding
	- use redundancy within and between images to decrease number of bits used to encode image
		- spatial (within image)
			- instead of sending N values of same color, send only two values, color and number of repeated values
		- temporal (from one image to next)
			- instead of sending complete frame at i + 1, send only differences from frame i
- CBR (constant bit rate)
	- video encoding rate fixed
- VBR (variable bit rate)
	- video encoding rate changes as amount of spatial, tempooral coding changes
- Streaming stored video
	- challenges
		- server-to-client bandwidth will vary over time
			- changing network congestion levels 
		- packet loss
			- will cause delay playout or result in poor video quality
		- continuous playout constraint
			- during client video playout, playout timing must match original timing
			- but netwrok delays are variable so will need client-side buffer to match continuous playout constraint
		- client interactivity
			- pause, fast-forward, rewind, jump through video
		- video packets may be lost, retransmitted

DASH
- for streaming multimedia
- Dynamic, Adaptive Strewaming over HTTP
- server
	- divides video file into multiple chunks
	- each chunk encoded at multiple different rates
	- different rate encodings stored in different files
	- files replicatd in various CDN nodes
	- manifest file: provides URLs for different chunks
- client
	- periodically estimates server-to-client bandwidth
	- consulting manifest, requests one chunk at a time
		- chooses maximum coding rate sustainable given current bandwidth
		- can choose different coding rates at different points in time (depending on available bandwidth at time) and from different servers
- Intelligence at client, he determines
	- when 
		- to request chunk (so that buffer starvation or overflow does not occur)
	- what encoding rate 
		- to request (higher quality when more bandwidth)
	- where
		- to request chunk (can request from URL server that is close to client or has high available bandwidth)
	- Streaming video = encoding + DAH + playout buffering


Content distribution networks (CDNs)
- challenge
	- how to stream content (selected from millions of videos) to hundreds of thousands of simultaneous users
		- option 1 : single, large server
			- single point of failure
			- point of network congestion
			- long (and possibly congested) path to distant clients
			- DOES NOT SCALE
		- option 2: store / serve multiple copies of videos at multiple geographically distributed sites
			- enter deep
				- push CDN servers deep into many access networks 
					- close to users
			- bring home
				- smaller number (10s) of larger clusters in POPs near access nets

What is security all about
- preventing man in the middle attacks
	- interception
	- monitoring
	- data theft
- identification
	- who are you?
	- are you still you?
- Authentication
	- signatures
	- validating that digital items haven't been altered
- possession
	- are you the certified owner of this digital asset


Out of band (OOB)
- transmitted using a different media to the main communication
- e.g. internet access to banks , but cellphone authorisation to login


Plaintext - unencoded original message


Nonce 
- arbitrary or random number that is only used once
	- number only used once
	- used to provide non-predictability

A cryptosystem should be secure even if everything about the system, except the secret key, is public knowledge

Cryptographic key
- a piece of information (parameter) that determines the functional output of a cryptographic algorithm
	- typically a sting of bits of pre-determined lenght
	- but anything can be a key
	- symmetric key
		- same key is used to encrypt and decrypt
	- asymmetric key
		- two different keys
		- one to encrypt
		- one to decrypt

Substitution cipher
- substitute one thing for another

Vigenere cipher
- form of a polyalphabetic cipher
- bsaed on series of interwoven caesar cipherse, based on letters of keyword
- resisted deciphering for 300 years

breaking substitution ciphers
- easy to attack using frequency analysis
	- varying frequency of use of different letters
	- for english, e is most common, z is least
	- typically requires about 50 letters of ciphertext (per letter in the keyword) to break

code
- specifically used as a term for block substitution

ciphers
- based on some form of permutation algorithm and a private key
- attacks
	- analyse letter and word frequency
	- compare konwn plaintext with ciphered text
	- randomness in ciphered text is highly desirable
- codes map words using a dictionary like codebook
	- need codebook or large cample of ciphertext / context to break
	- but much more overhead in setting up

One time pad
- only unbreakable protocol (Shannon 1949)
- randomly generated "infinite" lenght key (pad)
- combined with plaintext
- both sides must have a copy of the pad (key exchange problem)
- no other relationship between plain and cipher text
- must be used once
- source pad must remain secret
- key length must be equal or greater than text
- there is no protection of the message, no way to know if message has been changed
- why
	- because key is perfectly random, so is the ciphertext
		- no way to extract information

Practical challenges of widespread encryption
- encryption and decryption by users must be fast if large amounts of data
	- considerable overhead on more elaboreate schemes
	- infeasible for many uses (waiting time for userse)
- decryption by attackers must be as impossible as practical
	- probably fine if it theoretically takes a efw million years of compute time
- key distribution
	- how to agree on a key in the first place?
	- how does the key get distributed for use?

Symmetric key exchange
- assume n users using a common network
	- any two may wish to communicate with each other
- with symmetric key exchange
	- each user must store (n - 1) symmetric keys (one for each user)
	- how to redupiate key if one is cracked
	- adding, removing, refreshing users and keys?

Public key cryptography
- each user has a pair of keys
- public key is public
- private key is kept strictly secret
- public key is used to encrypt, private key used to decrypt
- elegant solution to the problem
- First published by Diffie-Hellman
- asymmetric
- public key is available to encryppt message
- private key is used to decrypt
- relis on mathematical functions with no efficient solution
- typically incorporate random numbers
	- hence the source of the random numbers can be a problem
- typically used for short messages
	- i.e. key exchange to setup symmetric encryption


Algorithm design : trapdoor functions
- algorithms rely on three hard mathematical problems
	- integer factorization (RSA)
	- discrete logarithm (Diffie-Hellman)
	- Elliptic-curve discrete logarithm
		- y^2 = x^3 + ax + b, random number (private key) point on the curve (public)
		- requires attacker to solve elliptic curve discrete algorithm problem
- Principle is 
	- realtively cheap to compute with complete information
	- intractable to reverse the computation with only partial information
		- key is the missing information

Diffie-Hellman key exchange
- create a shared secret between two participants using a public communication channel
- uses public-key cryptography
- use
	- modular arithmetic
	- coprime -> gcd = 1
![Screenshot 2024-11-17 at 16.58.24.png](../images/Screenshot%202024-11-17%20at%2016.58.24.png)
![Screenshot 2024-11-17 at 16.58.34.png](../images/Screenshot%202024-11-17%20at%2016.58.34.png)
![Screenshot 2024-11-17 at 16.58.45.png](../images/Screenshot%202024-11-17%20at%2016.58.45.png)


RSA
- security relies on the difficulty of factoring large composite numbers
![Screenshot 2024-11-17 at 17.01.02.png](../images/Screenshot%202024-11-17%20at%2017.01.02.png)
- the method
	- choose two large prime numbers p, q
	- compute n = pq (n will be used as the modulus for the private and public keys)
	- compute z = lcm (p - 1, q - 1) (lcm = lowest common multiplicator)
	- choose integer e, such that e < n, and e and z are coprime (relatively prime)
	- choose d as d = e^-1 (mod(z)) (d is the modular multiplicative inverse of e (modulo z))
	- public key = (n, e), private key is (n, d)
![Screenshot 2024-11-17 at 17.02.52.png](../images/Screenshot%202024-11-17%20at%2017.02.52.png)
![Screenshot 2024-11-17 at 17.04.38.png](../images/Screenshot%202024-11-17%20at%2017.04.38.png)
![Screenshot 2024-11-17 at 17.04.52.png](../images/Screenshot%202024-11-17%20at%2017.04.52.png)
![Screenshot 2024-11-17 at 17.05.32.png](../images/Screenshot%202024-11-17%20at%2017.05.32.png)
![Screenshot 2024-11-17 at 17.05.40.png](../images/Screenshot%202024-11-17%20at%2017.05.40.png)
- Key lengths are critical and algorithm being used

Quantum computers pose risk (Shor's algorithm) 
- but are they really coming? - is quantum supremacy a real thing 


Attributeion
- very difficult to be certain who originated the attack
- Issues with accurately tracing source through the network
	- cutout IPs -> and human (switcheroos)
	- multiple redirects
	- TOR and similar

Attacker objective
- read
- modify
- inject
- control

![Screenshot 2024-11-17 at 17.22.36.png](../images/Screenshot%202024-11-17%20at%2017.22.36.png)


Attack surface
- of a software environment or system
- the total of different points where an unauthorized user can try to attack the software or system
	- user IO
	- network connections to other systems
	- operating system
	- hardware
- Increase over time (with more technology)

SQL injection
![Screenshot 2024-11-17 at 17.25.40.png](../images/Screenshot%202024-11-17%20at%2017.25.40.png)



cve.org (common vulnerabilities and exposures)
indicators of compromise (IOC)


Defending yourself
- backup
	- do backups
		- protect agains accidental data loss
		- protect against modification
		- assist in identifying incidents
	- regular backup to unattached media
	- regular offise backups
	- distribute among computers
- secure the physical
	- are servers in physiccally secure areas
	- UPS (uninterruptible power supply) tested?
	- fire? earthquakes?
	- is there a complete contingent backup site plan?
	- when was it last tested?
	- is paper waste being securely shredded?
	- disposal of old hardware?

Defence strategies
- in depth
	- physical access
	- network
	- hosts or operating systems
	- applications
- in breadth
	- split up areas and protect separately
	- whitelist and blacklist
	- identify high priority targets
	- physically disable problematic interfaces e.g. usb
	- do accounting really need to browse the web?
	- should the accounting data server host a web server?

Demilitarized zone (DMZ)
![Screenshot 2024-11-17 at 17.29.55.png](../images/Screenshot%202024-11-17%20at%2017.29.55.png)
![Screenshot 2024-11-17 at 17.47.29.png](../images/Screenshot%202024-11-17%20at%2017.47.29.png)

![Screenshot 2024-11-17 at 17.30.43.png](../images/Screenshot%202024-11-17%20at%2017.30.43.png)
- keep onnections simple with as few connections as possible


Network equipment defences
- firewall
- VLANs
- VLAN ACL (access control lists)
- Micro VLANs
- static ports
- IPSEC
- intrusion detection systems'

Firewall
- isolates organization's internal net from larger Internet, allowing some packets to pass, blocking others
- what
	- all traffic entering or leaving must pass through firewall
	- must define criteria for what is (un) authorized
	- effectiveness of firewalls depends on specifying authorized traffic in terms of rules
		- what to let through
		- what to block
		- traffic patterns have to obey those rules
	- firewall itself must be effectively administered
		- updated with latest patches
		- correctly configured
	- firewalls can be implemented in both hardware and software, or a combination of both
	- firewalls frequently become a cost/performance bottleneck
- why
	- prevent denial of service attacks
		- SYN flooding
	- allow only authorized access to inside network
		- set of authenticated users / hosts
- three types of firewalls
	- stateless packet filters
	- stateful packet filters
	- application gateways
- other types?
	- ![Screenshot 2024-11-17 at 17.36.18.png](../images/Screenshot%202024-11-17%20at%2017.36.18.png)
- router-based packet filter
	- a packet filter is a network router that can accept/reject packets based on headers
	- packet filters examine each packet's headers and make decisions based on attributes such as
		- source or destination IP addresses
		- source or destination port numbers
		- protocol
		- ICMP message type
		- and which interface the packet arrived on
		- unaware of session states at internal or external hosts
		- high pseed, but primitive filtering
- host-based packet filters
	- hosts can also perform packet filtering
		- stops some unwanted traffic reaching applications
	- Kernel firewalls
		- windows firewall - GUI
		- OSX firewall - GUI
		- linux iptables


stateless packet filtering
- internal network conencted to internet via router firewall
- router filters packet-by-packet, decision to forward/drop packet based on 
	- source IP address, destination IP address
	- TCP/UDP source and destination port numbers
	- ICMP message type
	- TCP SYN and ACK bits

Access control lists (ACL)
- a table of rules applied top to bottom to incoming packets (aciton, condition pairs)

Application layer proxy
- use firewall as intermediate interface
	- external client sends a request to the server, which is intercepted by the outwards-facing firewall proxy
	- inwards-facing proxy sends request to server on behalf of client
	- server sends reply back to inwards-facing firewall proxy
	- outwards facing proxy sends reply to client
- client and server both think they communicate directly with each other, not knowing that they actually talk with a proxy
- the proxy can inspect the application data at any level of detail and can even modify the data

Next generation firewalls
- inspects payload in end-to-end or proxy application connection
- support specific application protocols
	- http, telnet, ftp, smtp, etc.
	- each rptocol supported by a specific proxy
- can be configured to filer user applications
	- can even filter detailed elements in each specific user application
- can suport TLS and SSL encrypted traffic inspection
	- in order to inspecct, proxy pretends to be external TLS server
	- proxy creates proxy server certificate with the name of the external server, signed by local proxy root private key
	- assumes that local proxy root certificate is installed on all local hosts
	- the proxy server certificate is automatically validated by local client, so user may believe that he/she has TLS conenction to the external srver![Screenshot 2024-11-17 at 17.46.08.png](../images/Screenshot%202024-11-17%20at%2017.46.08.png)
- can provide intrusion detection and intrusion prevention
- very high processing load in firewall - high volume needs high performance hardware, or else will be slow

Deep packet inspection (DPI)
- looks at application content instead of individual or multiple packets
- keeps track of application content across multiple packets
- potentially unlimited level of detail in traffic filtering


Virtual LANsa
- group of devices on one or more physical LANs that are configured as if they are logically attached to the same wire
- LANs based on lgoical instead of physical connection
- helps alleviate traffic congestion without adding more bandwidth
- used to separate out users into logcial groups of workers regardless of actual physical location
	- e.g. split up broadcast domain in a large flat network wtihout using a bunch of routers
- must be supported by the switch, i.e. can support more than one subnet
- motivation
- port-based VLAN
	- switch ports grouped (by switch management software) so that single physical switch operates as multiple virtual switches
- virtual local area network
	- switches supporting VLAN capabilities can be configured to define multiple virutal LANS over asingle physical LAN infrastructure
- 802.1Q VLAN frame format
	- ![Screenshot 2024-11-17 at 17.51.36.png](../images/Screenshot%202024-11-17%20at%2017.51.36.png)
- trunk port
	- for VLANs spanningmultiple switches
	- carries frames between VLANS defined over multiple physical switches
	- frames forwarded within VLAN can't be vanilla 802.1 frames, must use 802.1Q
		- adds/removed additional header fields for frames forwarded between trunk ports (contains VLAN ID info)

Security information and event management
- fancy shit to try and monitor if anything has been breached

network security
- confidentiality
	- only sender, intended receiver should understand message contents
	- sender encrypts message
	- receiver decrypts message
- authentication
	- sender, receiver want to confirm identity of each other
- message integrity
	- sender and receiver want to ensure message is not altered (in transit or after) without detection
- access and availability
	- services must be accessible and available to users

what can bad guys do
- eavesdrop
	- intercept messages
- inject / insert
	- actively insert messages into connection
- impersonate
	- fake / spoof source address in packet (or any field in packet)
- hijack
	- take over ongoing connection by removing sender or reciever, inserting himself in place
- deny service
	- prevent service from being used by others (e.g. by overloading resources)

Breaking an encryption scheme
- cipher-text only attack
	- attacker has a cipher text she can analyse
	- what they can do
		- brute force (search all keys)
		- use statistical analysis (key / word frequency etc.)
- known-plaintext attack
	- attacker has plaintext corresponding to cipher text
- chosen-plaintext attack
	- attacker can get ciphertext for a chosen plaintext (makes decryption easier)

Authetnication
- prove identity

man in the middle is solved somewhat with message signing


Digital signature
- cryptographic technique analogous to hand-written signatures
	- sender (Bob) digitally signs document (he is document owner / creator)
- verifianble and nonforgeable: recipient (Alice) can prove to someone that Bob an no one else (including Alice) must have signed the document
- simple digital signature for message m
	- ob signs mby encrypting with his private key Kb, creating signed mesage Kb -(m)
	- Alice verifies m signed by Bob by applying Bob's public key to the message
	- Alice verifies that
		- bob signed m
		- no one else signed m
		- bob signed m and not m'

Message digest
- computationally expensive to public-key-encrypt long messages
- goal: fixed-length, easy-to-compute digital fingerprint
- apply hash funciton h to m, get fixed size mssage digest H(m)
- large message m -> h hash function -> H(m)
- must have hash function properties
	- many-to-1
	- produces fixed-size msg digest (fingerprint)
	- given message digest x, computationally infeasible to find m such that x = H(m)
- Internet checksum is a bad hash function
- signed message digest
	- Bo sends digitally signed message
	- alice verifies signature, integrity of digitally signed message
![Screenshot 2024-11-17 at 18.15.55.png](../images/Screenshot%202024-11-17%20at%2018.15.55.png)


Need for certified public keys
- you need some authority to say who owns which public key, otherwise this is all fucked

Public key certification authorities (CA)
- bind public key to particular entity E
- entitty (person, website, router) registers its public key with CE provides proof of identity to CA
	- CA creates certificate binding identity E to E's public key
	- certificate containing E's public key digitally signed by CA -> Ca assuers you that this is E's public key



Transport-layer security (TLS)
- Securing TCP connections
- provides an API that any application can use
- widely deployed security protocol above the transport layer
	- supported by almost all browsers, web servers (port 443)
- provides
	- confidentiality vai symmetric encryption
	- integirty vai cryptographic hashing
	- authentication via public key cryptography
- what's needed
	- handhsake
		- certificates (private keys) used to authetnicat each other, to exchange or create shared secret
		- Establish TCP connection
		- do TLS hello -> Diffie Hellman to get master secret
	- key derviation
		- Alice and bob use shared secret to derive set of keys
	- data transfer
		- stream data transfer: data as a series of records not just one-time transactions
	- connection closure
		- special messages to securely close connection
- Cryptographic key
	- bad to use same key for more than one cryptographic function
	- different keys should be used for message authetnication code (MAC) and encryption
	- four keys
		- Kc : encryption key for data sent from client to server
		- Mc : MAC key for data sent from client to server
		- Ks : encryption key for data sent from server to client
		- Ms : MAC key for data sent from server to client
	- Keys are derived from key derivation function (KDF)
		- take master secret and (possibly) some additional random data to create new keys
- stream broken up into a series of records
	- each client-to-server record carries a MAC, created using Mc
	- receiver can act on each record as it arrives
	- using TLS sequence numbers (data, TLS-seq-# incoroperated into MAC) avoids re-ordering by man in the middle and replay attacks
	- use nonce
- truncation attack
	- attacker forges TCP connection close segment
	- one or both sides think there is less data than there actually is
- solution
	- record type with one type for closure
- ![Screenshot 2024-11-17 at 19.57.54.png](../images/Screenshot%202024-11-17%20at%2019.57.54.png)

TLS 1.3 cipher suite
- cipher suite
	- algorithms that can be used for key generation, encryption, MAC, digital signature
	- 1.3
		- more limited cipher suite choice than 1.2
		- only 5 choices instead of 37
		- requires diffie-hellman for key exchange (rather than DH or RSA)
		- combined encryption and authentication algorithm (authenticated encryption) for data rather than serial encryption or authentication
- Hanshake 1 RTT
	- client TSL hello message
		- guesses key agreement protocol, parameters
		- indicates cipher suites it supports
	- server TLS hello msg chooses
		- key agreement protocol, parameters
		- cipher suite
		- server-signed certificate
	- client:
		- checks server certificate
		- generates key
		- can now make application request (e.g., https GET)![Screenshot 2024-11-17 at 20.01.30.png](../images/Screenshot%202024-11-17%20at%2020.01.30.png)
- Handshake 0 RTT
	- initial hello message contains encrypted application data
		- resuming earlier connection between client and server
		- application encrypted using "reumption master secret" from earlier connection
	- vulnerable to replay attacks
![Screenshot 2024-11-17 at 20.02.43.png](../images/Screenshot%202024-11-17%20at%2020.02.43.png)


Public key infrastructure PKI
- certificate authorities are public registries for keys
- Anybody can setup / be a certificate authority
- issues
	- scalability
	- naming
		- human names
		- digital identities/identifiers?
	- dealing with compromised keys
	- revoking certificate
	- trustworthiness of the CA
	- privacy and anonymity
		- can address this with serial numbers
		- then create an authentication issue

veryfying x.509 certificates
- use indicated hash algorithm to create digest from all fields in certificate
- use CA's public key to decrypt signature and get enclosed digest
- if the two match, certificate is valid and has not been tampered with


Certification authorities
- bind public key to particular entity E
- E (peron, router) registers its public key with CA
	- E provides "proof of identity" to CA
	- CA creates certificate binding E to its public key
	- certificate containing E's public key digitally signed by CA -CA says this is E's public key
- When fetching public key
	- get the certificate
	- apply CA's public key to the certificate to get the public key

Wireless and mobile networks
- challenges
	- wirless - communication over wireless link
	- mobility - handling the mobile user who changes point of attachment to network
- wireless
	- WiFi: 802.11 - wireless LANs
	- Cellular networks
- Mobility
	- Mobile IP
	- impact on higher-layer protocols

wirless networks
- mobile (or stationary) hosts
- base station
	- typically connected to wiried network
	- relay - responsible for sending packets between wired network and wireless hosts in its area
	- e.g. cell towers - 802.11 access points
- wireless link
	- typically used to connect mobile(s) to base station, also used as backbone link
	- multiple access protocol coordinates link access
	- various transmission rates and distances, frequency bands
- infrastructure mode
	- base station connects mobiles into wired network
	- handoff : mobile changes base station providing connection into wired network
- ad hoc mode
	- no base stations
	- nodes can only transmit to other nodes within link coverage
	- nodes organize themselves into a network, route among themselves
- wireless link characteristics
	- fading / attenuation
		- wireless radio signal attenuate (loses power) as it propagates (free space "path loss")
		- (frequency * distance)^2
	- multipath propagation
		- radio signal reflects off objects arriving at destination at slightly different times
		- coherence time
			- amount of time bit is present in channel to be received
			- influences maximum possible transmission rate, since coherence times can not overlap
			- inversely proportional to 
				- frequency 
				- receiver velocity
	- noise
		- interference from other sources on wirless network frequencies : motors, appliances
		- SNR - signal-to-noise ratio
			- larger SNR - easier to extract ignal from noise (a good thing)
		- SNR vs. BER (bit error rate) tradeoff
			- given physical layer: increase power -> increase SNR -> decrease BER
			- SNR may change with mobility
				- dynamically adapt physical layer (modulation techinque, rate)
	- hidden terminals
		- ![Screenshot 2024-11-17 at 20.25.04.png](../images/Screenshot%202024-11-17%20at%2020.25.04.png)


IEEE 802.11 Wirless LAN
- all use CSMA/CA for multiple access and have base-station and ad-hoc network versions
- LAN architecture
	- wirless host communicates with base station
		- base station = access point (AP)
	- basic service set (BSS) (aka cell) in infrastructure contains
		- wirless hosts
		- access point (AP) base station
		- ad hoc mode : hosts only
- Channels
	- spectrum is divided into channels at different frequencies
		- AP admin choose frequency for AP
		- interference possible: channel can be same as that chosen by neighboring AP
		- in reality only 3 channels available (that don't collide)
- Association
	- arriving host must associate with an AP
	- Scans channels, listening for beacon frames containing APs name (SSID) and MAC addres
	- Selects AP to associate with
	- then may perform authetnication
	- typically runs DHCP to get IP address in AP's subnet
- Passive vs. active scanning
	- passive scanning
		- beacon frames sent from APs
		- association request frame sent H1 to selected AP
		- association response frame sent from selectd AP to H1
	- active scanning
		- probe request frame broadcast from H1
		- probe response frames sent from APs
		- association request frame sent H1 to selected AP
		- Association Response frame sent from selected AP to H1
- Multiple access
	- avoid collisions (2+ nodes transmitting at same time)
	- CSMA - sense before transmitting
		- don't collide with etected c-ongoing transmission by another node
	- no collision detection
		- difficult to sense collisions: high transmitting signal, weak received signal due to fading
		- can't ense all collisions in any case : hidden terminal, fading
		- goal : avoid collisions : CSMA / CollisionAvoidance


CSMA/CA - wireless
- sender
	- if sense channel idle for DIFS
		- then transmit entire frame (no CD)
	- if sense channel busy then
		- start random backoff time
		- timer counts down while channel idle
		- transmit when timer expire
		- if no ACK, icnrease random backoff interval, repeat 2
- receiver
	- if frame received OK
		- return ACK after SIFS (ACK needed due to hidden terminal problem)
- Other ideas
	- sender reserves channel use for data frames using small reservation packets
		- sender first transmits small request-to-send (RTS) packet to BS using CSMA
			- RTSs may still collide with each other (but they're short)
	- BS broadcasts clear-to-send CTS in response to RTS
	- CTS heard by all nodes
		- sender transmits data frame
		- other stations defer transmissions


![Screenshot 2024-11-17 at 21.09.43.png](../images/Screenshot%202024-11-17%20at%2021.09.43.png)
- requires 3 addresses as AP is not router

mobility within same subnet
- if the device stays within the same IP subnet the IP address can remain the same
- self-learning switch will remember how to reach H1 (which AP is associated with it)

Rate adaption
- base station, mobile dynamically change transmission rate (physical layer modulation technique) as mobile moves, SNR varies
	- SNR decreases, BER increase as node moves away from bae station
	- when BER becomes too high, switch to lowertransmission rate but with lower BER

Power management
- node-to-AP - "I am going to sleep until next beacon frame"
	- AP knows not to transmit frames to this node
	- node wakes up before next beacon frame
- Beacon frame contains list of mobiles with AP-to-mobile frames waiting to be sent
	- node will stay awake if AP-to-mobile frames to be sent, otherwise sleep again until next beacon frame


Bluetooth
- less than 10 m
- replacement for cables
- ad hoc : no infrastructure
- master controller / client devices
	- master polls clients, grants requests for client transmissions



Cellular networks
- the solution for wide-area mobile Internet
- widespread deployment/use
	- transmission rates up to 100 Mbps
- Architecture
	- mobile device
		- anything connected to the network
		- 64-bit international mobile subscriber identity (IMSI) stored on SIM (subscriber identity module) card
		- LTE jargon : user equipment (UE)
	- base station
		- at edge of carrier's network
		- manages wireless radio resources, mobile devices in its coverage area (cell)
		- coordinate device authetnication with other elements
		- similar to WiFi AP but
			- active role in user mobility
			- coordinates with nerby bsae stations to optimize radio use
		- LTE jargon : eNode-B
	- Home Subscriber service
		- stores info about mobile devices for which the HSS's network is their home network
		- works with MME in device authetnication
	- Serving Gateway (S-GW)
		- lie on data path form mobile to/from Internet
	- PDN Gateway (P-GW)
		- lie on data path from mobile to/from Internet
		- gateway to mobile cellular networks
		- looks like any other internet gateway router
		- provides NAT ervices
		- other routers:
			- extensive use of tunneling
	- Mobile management entitty
		- device authentication (device-to-network, network-to-device) coordinated with mobile home network HSS
		- mobile device management
			- device handover between cells
			- tracking / paging device location
		- path (tunneling) setup from mobile device to P-GW


control plane
- protocols for mobility management, security, authetnication

data plane
- protocols at link and physical layers
- extensive use of tunneling to facilitate mobility
- protocols
	- LTE link layer protocols
		- Packet data convergence:  header compresion, encryption
		- Radio link Control (RLC) protocol : fragmentation / reassembly, reliable data transfer
		- Medium Access: requesting use of radio transmission slots (OFDM)
	- packet core
		- tunneling
			- mobile datagram encapsulated using GPRS Tunneling Protocol (GTP), sent inside UDP datagram to S-GW
			- S-GW re-tunnles datagrams to P-GW
			- supporting mobility: only tunneling endpoints change when mobile user moves
- Associating with a BS
	- BS broadcasts primary synch signal every 5 ms on all frequencies
		- BSs from multiple carriers may be broadcasting synch signals
	- mobile finds a primary synch signal, then locates 2nd synch signal on this freq.
		- mobile then finds info broadcast by BS: channel bandwidth, configurations: BS's cellular carrier info
		- mobile may get info from multiple base stations, multiple cellular networks
	- mobile selects which BS to associate with (e.g. preference for home carrier)
	- more steps still needed to authenticate, establish state, set up data plane

The global cellular network - > a network of IP networks
- home network HSS
	- identify & services info while in home network and roaming
- all IP 
	- carriers interconnect with each other and public internet at exchange points
![Screenshot 2024-11-17 at 22.49.57.png](../images/Screenshot%202024-11-17%20at%2022.49.57.png)





Radio access network 4g radio
- connects device (UE) to a base station (eNode-B)
	- multiple devices connected to each base station
- many different possible frequencie bands, multiple channels in each band
	- separate upstream and downstream channels
- sharing 4G radio channel among users
	- OFDM Orthogonal Frequency Division Multiplexing
	- combination of FDM, TDM
- 100's Mbps possible per user/device


ODFMA : time division (LTE)
- physical resource block PRB
	- blocks of 7 * 12 = 84 resource elements
	- unit of transmission scheduling
![Screenshot 2024-11-17 at 22.37.52.png](../images/Screenshot%202024-11-17%20at%2022.37.52.png)



![Screenshot 2024-11-17 at 22.33.03.png](../images/Screenshot%202024-11-17%20at%2022.33.03.png)



Cellular compared to wired Internet
- similarities
	- edge/core distinction, but both belong to same carrier
	- global cellular network: a network of networks
	- widespread use of protocols we've studied
	- separation of data/control planes, DN, Ethernet, tunneling
	- interconnected to wired Internet
- differences from wired Internet
	- different wireless link layer
	- mobility as 1st class service
	- user identity (via SIM card)
	- business model : users subscribe to a cellular provider
		- strong notion of home network vs. roaming on visited nets
		- global access, with authetnication infrastructure, and inter-carrier settlements

mobility
- spectrum of mobility from the network perspective
	- (no mobility)
	- device moves between networks but powers down while moving
	- device moves within same AP in one provider network
	- device moves among APs in one provider network
	- device move among multiple provider networks, while maintaining ongoing connections
	- (high mobility)
- challenge
	- if a dveice moves from one network to another, how will the network know to forward packets to the new network?
- approache
	- let network (routers) handle it
		- routers advertise wlel-known name, address (32-bit IP address) or number (e.g. cell number) of visiting mobile node via usual routing table exchange
		- Internet routing could do this already with no change
		- routing tables indicate where each mobiel located via longest prefix match
		- NOT SCALABLE
	- let end systems handle it
		- functionality at the edge
		- indirect routing
			- communication from correspondent to mobiel goe through home network, then forwarded to remote mobile
		- direct routing
			- correspondent gets foriegn address of mobile and sends directly to the mobile
	- The importance of having a home
		- a definitive source of information about you
		- a place where people can find out where you are
- e.g.
	- home network
		- paid service plan with cellular provider
		- home network HSS stores identity & services info
	- visited network
		- any network other than your home network
		- service agreement with other networks to provide access to visiting mobile
- ISP / WiFi
	- no notion of global home
	- credentials from ISP (e.g. username, password) stored on device or with user
	- ISPs may have national, international presence
	- different networks : different credentials
	- architectures do exist, but not used (mobile IP)
![Screenshot 2024-11-17 at 22.56.42.png](../images/Screenshot%202024-11-17%20at%2022.56.42.png)
![Screenshot 2024-11-17 at 22.56.52.png](../images/Screenshot%202024-11-17%20at%2022.56.52.png)
- triangle routing
	- inefficient when correspondent and mobile are in same network
	- mobile moves among visited networks : transparent to correspondent
		- registers in new visited network
		- new visited entwork registers with home HS
		- datagrams continue to be forwarded from home network to mobile in new network
		- on-going (e.g. TCP) connections between correspondent and mobiel can be maintained

![Screenshot 2024-11-17 at 22.59.02.png](../images/Screenshot%202024-11-17%20at%2022.59.02.png)
- overcomes triangle routing inefficiencies
- non-transparent to correspondent
	- correspondent must get care-of-addres from home agent
	- what if mobile change visited network?
		- can be handled, but with additional complexity


configuring data-plane tunnels for mobile
- S-GW to BS tunnel
	- when mobile changes base stations, simply change endpoint IP address of tunnel
- S-GW to home P-GW tunnel
	- implementation of indirect routing
- tunneling via GTP (GPRS tunneling protocol) mobile's datagram to streaming server encapsulated using GTP inside UDP, inside datagram
![Screenshot 2024-11-17 at 23.05.26.png](../images/Screenshot%202024-11-17%20at%2023.05.26.png)

Hnadover Between BSs in same cellular network
- current (source) BS selects target BS, sends Handover request messge to target BS
- target BS pre-allocates radio time slots, responds with HR ACK with info for mobile
- source BS informs mobile of new BS
	- mobile can now send via new BS - handover looks complete to mobile
- source BS stops sending datagrams to mobile, instead forwards to new BS (who forwards to mobile over radio channel)
- target BS informs MME that it is new BS for mobile
	- MME instructs S-GW to change tunnel endpoint to be (new) target BS
- target BS ACKs back to source BS: handover complete, source BS can release resources
- mobile's datagrams now flow through tunnel from target BS to S-GW
![Screenshot 2024-11-17 at 23.07.43.png](../images/Screenshot%202024-11-17%20at%2023.07.43.png)



Mobile IP
- standardized 20 years ago
	- long before ubiquitous smartphones
	- did not see widespread deployment
- mobile IP architecture
	- indirect routing to node (vaia home network) using tunnels
	- mobile IP home agent: combines roles of 4G HSS and home P-GW
	- mobile IP foregin agent: combined roles of 4G MME and S-GW
	- protocols for agent discovery in visited network, registration of visited location in home network via ICMP extension

impact of wireles and mobility on higher layer protocols
- logically impact should be minimal
	- best effort service model remains unchanged
	- TCP and UDP can (and do) run over wirless and mobile
- put performance wise
	- packet loss/delay due to bit-errors (discarded packets, delays for link-layer retransmission) and handover loss
	- TCP interpres loss as congestion will decrease congestion window unnecessarily
	- delay impairments for real-time traffic
	- bandwidth a scarce resource for wireless links




3 key attributes control scaling properties for a network
- topology
- latency
- size (number of nodes)

multiplexing
- statistical multiplexer
- time division multiplexer

Synchronouse
- synchronized by some kind of external clock
- receiver expects frames to arrive at fixed frequency
- uses clock to read frames from the wire

asynchornous communication
- frames have start / end frame markers
- or known frame length
- high overhead, Fisher consensus

Fisher Consenus
- "It is imopssible to guarantee that any asynchrnously connected set of nodes (computers) can ever agree on even a single bit value"

![Screenshot 2024-11-19 at 16.54.34.png](../images/Screenshot%202024-11-19%20at%2016.54.34.png)


Protocol key concepts
- the upper layers will recover
- each layer adds a level of overhead - packet header
- which layer is reponsible for what
- error detection and correction
- ACKS vs NACK
- what a protocol flow diagram is
	- be able to sketch out simple protocol exchanges
	- TCP/IP setup and tear down
	- DHCP offer  / requst
- how allocated
	- MAC - statically
	- IP - statically or dynamically
	- IP address blocks - statically, hierarchical
	- DNS - statically, hierarchical

UDP Properties
- unreliable, connectionless, packet-oriented

TCP properties
- reliable, connection-oriented, stream-oriented
- why reliable? seq, ack, timeout


What are, and implications of: Jitter, Latency, Bandwidth, Loss







-----

Interesting but useless
- Originally ASCII was 7 bit characters and 8th bit was a parity check

LOOKAT
- silly window syndrome
- slide 584

good to look at 
bls 426
434


1080 - o.s.frv.

