
Transmission rate / capacity / bandwidth
- how much data can be sent on link per time e.g. Gbps

Transmission delay
- how long does it take to send some amount of data?

Propagation speed
- how fast does a  signal travel in a medium

propagation delay / latency
- how long after the singal was sent, does the receiver receive it?

Queueing delay
- time spent in a queue waiting to be transmitted

store-and-forward delay 
- sum of bandwidth delays out of each router along the path

Processing delay
- processing time of a computer between receiving some data and transmitting it further (or sending a response)

Protocol stack
- higher levels responsible for reliability, data order etc.

3 main variants of protocols
- unacknowledged connectionless service - Ethernet
- acknowledged connectionless service - WiFi
- acknowledged connection-oriented service - TCP/IP

Data link -> takes request from network layer, interacts with physical media

Hamming codes
- add parity bits at powers of 2 to the data bits (even) (use sliding window)

flow control -(throttling) > don't overwhelm the other end

statmul -> dynamically allocate badnwidth based on actual traffic demands of each stream
tdm -> fixed allocation (guarantees of QoS, wasteful)

network provisioning -> how many users can be provisioned on link and maintain performance guarantees?

Network engineering - ensure netwrok meets user's requirements
- fault tolerance (availability)
- capacity (throughput)
- latency
- cost (running cost, network equipment)

Scaling - constraints on system that depends on size
- topology
- latency
- size (# nodes)

Topology
- group size 
	- maximum connectedness at a node
- Strictly hierarchical
	- best topology for control purposes (e.g. botnets)
	- worst topology for exchanging information
	- required if consensus must be guaranteed
	- favoured by long communication latencies
- full mesh
	- best topology for exchanging information for small groups
	- size is bounded by the group size
	- worst topology for control
- partial mesh
	- cannot guarantee consensus
	- depending on error rate, voting algorithms can provide strong guarantees
	- vulnerable to broadcast storms with increasing N
- Organized mesh
	- topology that can scale to large N and grow capacity
	- similar issues to other mesh topologies
	- allows arbitrary scaling with the assumption that significant amounts of traffic can be retained in local groups of communicatting nodes
	- the internet


MAC - control access to a single shared broadcast channel (multiplexing alg)
- channel partitioning
- random access
- turn taking

Addressing - unique identifier and helps with routing

WAN - wide area network -> the Internet (connect LANs together)

circuit switching
- connection oriented, decidated channels, allow guaranteed packet delivery rate & bandwidth

packet switching
- connectionless, packet oriented (packet sent through network on arbitrary routes), best effort, no guarantees

IP datagram - a self-contained independent entity of data carrying sufficient information to be routed from the source to the destination computer wihtout reliance on earlier exchanges between this source and destination computer and the transporting network

Hole punching
- TCP hole punching
	- Both hosts reuse the same local endpoint to try to connect simultaneously (violates TCP standard)
	- relies on the SYN packet getting through on one side
- relaying
	- Natted client established connection to relay
	- external client connects to relay
	- relay bridges packets between the two connections

UDP - connectionless, unreliable
TCP - connection-oriented, reliable
- all packets will be reliably delivered in the order they were sent or connection is dropped
- flow control, congestion control

sliding window protocol - circular buffer (window), sent no ack, sent ack, no sent
- minimize effect of store-and-forward delays and propagation dleays, automatic brake on congestion
- self-clocking property : packets will be sent at an average rate exactly matching delivery rate (because of slowest link) thus reducing congestion
- if window too large , inflates RTT to fit the winsize

optimal window size = bandwidht (bits / s) * RTT (s)

SYN cookies-  state of connection hashed into the ack field (skip TCB until connection established)

Errors from the view of the network
- missing / delayed packets
- timeouts being too long or too short when reacting to errors
- network congestion due to too much traffic
- behavior of protocol triggering network congestion
- especially -> tragedy of the commons type errors

Nagle's algorithm issues -> should disable when working with real time traffic, short timeouts, deadlocks (piggybackACK)

TCP timers -> retransmission, persistence (window probes), keepalive, time-wait
- timeout == EstRTT + 4 * EstDev

Random early deteciotn -> drop packets randomly for fairness (don't drop tail)

AQM -> detect early signs of congestion, use Explicit congestion notification (trigger congestion avoidance) 
- act before the packet drops actually occur

bridge, between LAN and WAN
DHCP -> host address assignment, need, want?, yes, cool.
ARP -> IP to MAC addr

routing, types ->  datagram - virtual circuit - static
routing aims -> stable, reliable, fair, optimal, maximize throughput and minimize latency

components of a router
- switched backplane, line card (buffer memory and forwarder), route processor(CPU, RIB (table))

AS - a network controlled by a single entity with independent connections to multiple networks
- connected group of one or more IP prefixes run by one or more network operators which has a single and clearly defined routing policy
- has a single and clearly defined routing policy
- ASN 64 bit UID from IANA
- BGP used between them

forwarding table -> relay packets between connected network segments
routing table -> route between network segments

routing protocols
- interior gateway protocols -> OSPF, RIP, IS-IS, EIGRP
	- OSPF - link state, authenticated messages, suports 2-layer hierarchy and ToS
	- IS-IS - link state, protocol neutral, uses own protocol, not IP better than OSPF
- exterior gateway protocols -> EGP, BGP, BGPSEC
	- BGP -> (path-vector) allows routers to create a distributed routing table of IP prefixes 
	- transit or local traffic
	- BGP-policy is filtering rules - import filtering- best-path seleciton - export filtering
	- AS-PATHS, route advertisements, no routing loops
	- allows routing based on technial and policy information
	- BGPSEC -> use RPKI and ROA (digital signing)

Shortest path algorithms
- bellman-ford : centralied and distributed via distance vector routing (iterative, asynchronous)
	- good news travels fast, bad new travels slow
	- slow convergence problem
	- uses hop count for metric
	- network information at 1 hop remove
	- uses hop count for metric
	- network information at 1 hop remove
	- relies on timed/periodict updates
	- slow convergence
	- sucseptible to routing loops
- Dijkstra's algorithm : needs full information, link state routing (centralised, distributed) (oscillations possible)
	- discover neighbors and respective cost, send to all, compute shortest path to every router
	- uses shortest path
	- gets entire network topology
	- event triggered updates
	- faster convergence
	- less susceptible
- (consider size of routing tables and complexity of updates)

Hierarchical routing -> based on administrative decisions

DNS - distributed, decentralised, hierarchical database = IP addres => name

DNS query -> local machine resolver (cache) -> local DNS caching resolver (-||-) -> regional / authoritative server

dig & nslookup

P2P
- self-organizing, no central maangement, resource sharing by end devices, all equal
- structured -> defined topology, nodes with ids, distributed indexing provide object location
- unstructured -> no id, location is, reponsible for own, protocol to locate (no apriori knowledge)

Centralized P2P -> central entity is necessary to provide service + some kind of index / group database (NAPSTER)

pure P2P - any terminal entity can be removed without loss of functionality, no central entitites (Gnutella)

Hybrid P2P - super peers

DHT-Based - no central entities, connections in the overlay are fixed (CHORD)

Content addresable network - d-dimensional search space where each node represents a zone in the space keeping links to adjacent zones

server -> always-on host permanent IP address, often in data centers for scaling
client -> contacts and communicate with server, may be intermittently connected, may have dynamic IP addresses, do not communicate directly with each other

TLS
- TCP + confidentiality, data integrity, end-point authentication
- handhsake, key derivation, data transfer, connection closure
- 4 keys, encryption key and HMAC key for each side
- hello -> choose protocol -> generate key

HTTP
- web's application protocol, stateless
- non-persistent -> 1 object
- persistente -> more than 1 object (divide objects into frames to mitigate HOL blocking)
- request, response

cookies
- maintain user/server state between transactions 
- authorization, shopping carts, recommendations, user session state

web cache = proxy server

SMTP
- for exchanging e-mail mesages, delivery and storage to mail servers

Mail access protocol -> retrieve email from server (retrieval, deletion, folders)

video
- codings with redundancy 
	- spatial (within image)
	- temporal (from one image to next)
- challenges
	- varying bandwidth, packet loss, continuous playout constraint, client interactivity

DASH
- stream multimedia
- divide video file into chunk encoded at different rates, files replicatd at various CDN nodes
- manifest file : provide URLs for different chunks :: estimate bandwidth, consult manifest
- client determines, when, what encoding rate & where

CDN
- store multiple copies of videos at multiple geographically distributed sites
	- enter deep -> CDN servers deep into many access networks close to users
	- bring home -> efwer large clusters

Security
- preventing man in the middle attacks
	- interception
	- monitoring
	- data theft
- identification
	- who are you?
	- are you still you?
- authentication
	- signatures
	- validating that digital items haven't been altered
- possession
	- are you certified owner of this digital asset

OOB - out of band - transmitted using a different media to the main communication

Kerchoff's principal : a cryptosystem should be secure even if everything about the system, except the key, is public knowledge

cryptographic key -> parameter that determines the functional output of cryptographic algorithm

one time pad - > only unbreakable protocol

RSA
- choose two large prime numbers p, q
- compute n = pq (n will be used as the modulus for the private and public keys)
- compute z = lcm (p - 1, q - 1) (lcm = lowest common multiplicator)
- choose integer e, such that e < n, and e and z are coprime (relatively prime)
- choose d as d = e^-1 (mod(z)) (d is the modular multiplicative inverse of e (modulo z))
- public key = (n, e), private key is (n, d)
- (key lengths and algorithm being used are critical)


Attribution is difficult

Attack surface
- the total number of different points where an unauthorized attacker can try to attack the software or system

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

Demilitarized zone with firewalls -> have two firewalls

Ethernet star topology - host connects directly to the hub rather than to one long run of coaxial cable

Firewall
- a combination of hardware and software that isolates an organization's internal network from the Internet at large, allowing some packets to pass and blocking others
- 3 categories
	- traditional packet filters
		- examines each datagram in isolation determining whether the datagram should be allowed to pass or should be dropped based on admin-specific rule
		- decisions based on IP, protocol type, ports, TCP flag bits, ICMP message type, etc.
		- ACL - access control lists
	- stateful filters
		- track TCP connections and use this knowledge to make filtering decisions
		- track all ongoing TCp connections in a connection table
	- application gateways
		- make policy decisions based on application data
		- application-specific server through which all application data (inbound and out-bound) msut pass

router-based packet filter & host-based packet filter 

Deep packet inspection (DPI)
- look at application content instead of individual or multiple packets, keep track of application content across multiple packets, potentially unlimited level of detail in traffic fitlering

VLANs
- group of devices on one or more physical LANs that are configured as if they are logically attached to the same wire (logical rather than physical connection)
- alleviate traffic congestion without adding more bandwidth
- adds some stuff (802.1Q)

Network security considerations
- confidentiality -> only receives can view message content (sender encr, rec decr)
- authentication -> confirm identity
- message integirty -> ensure message was not altered
- access and availability -> must be accessible and available to user (no DoS)

Bad guy actions
- eavesropping
- injection / insertion
- impersonation
- hijack
- denial of service

breaking an encryption scheme
- cipher-text only atttack
- known-plaintext attack
- chosen-plaintext attack

Digital signature -> verifiable and nonforgeable

message digest

public key authorities
- entity registers is public key with CE provides proof of identity to CA which creates a certificate binding the identity to the public key, this is then signed by the CA
- dealing with ocmpromised keys and revoking certificates is hard
- trustworthines
- privacy and anonymity not possible

certificate
- get certificate, apply CA's public key to the certificate to get the public key

mobility -> handling the mobile user who changes point of attachment to network

SNR -> singal to noise ratio 
BER -> bit error rate
SNR to BER tradeoff (increase power, increase snr, decrease BER)

wireless link issues -> attenuation and multipath propagation
infrasturcture or ad hoc mode

hidden terminal problem -> fix with Request to send and clear to send
CSMA/CA -> check busy, return ack else RTS, CTS 
3 addresses

CRC used in WiFi frames to correct bit errors

power management -> go to sleep, beacon frame contains list of frames waiting to be sent

bluetooth -> master controller & client devices

Association
- passive vs. active scanning -> beacon frames

Cellular networks
- UE, base station,  home subscriber service, serving gateway, PDN gateway, mobile management entitty
- MME -> device handover, management and authentication

control plane -> mobility, security, authentication protocols
data plane -> link and physical layer protocols

LTE link layer
- packet data convergence - header compression and encryption
- radio link control - fragmentation / reassembly, reliable data transfer
- medium access - > request use of radio transmission slot OFDM

Associating with BS
- use combination of frequency division multiplexing and time division multiplexing (OFDM)
- each mobile devices is allocated one or more 0.5ms time slot in one or more of the channel frequenceies
- BS broadcasts primary synch signal every 5 ms on all frequencies
	- BSs from multiple carriers may be broadcasting synch signals
- mobile finds a primary synch signal, then locates 2nd synch signal on this freq.
	- mobile then finds info broadcast by BS: channel bandwidth, configurations: BS's cellular carrier info
	- mobile may get info from multiple base stations, multiple cellular networks
- mobile selects which BS to associate with (e.g. preference for home carrier)
- more steps still needed to authenticate, establish state, set up data plane

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

indirect routing -> through HSS
direct routing -> through visited (but non-transparent to correspondent)

internet connection through cellular -> dataplane tunnels S-GW to BS, S-GW to home P-GW tunnel

Handover Between BSs in same cellular network
- current (source) BS selects target BS, sends Handover request messge to target BS
- target BS pre-allocates radio time slots, responds with HR ACK with info for mobile
- source BS informs mobile of new BS
	- mobile can now send via new BS - handover looks complete to mobile
- source BS stops sending datagrams to mobile, instead forwards to new BS (who forwards to mobile over radio channel)
- target BS informs MME that it is new BS for mobile
	- MME instructs S-GW to change tunnel endpoint to be (new) target BS
- target BS ACKs back to source BS: handover complete, source BS can release resources
- mobile's datagrams now flow through tunnel from target BS to S-GW

Mobile IP
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


Wifi
- physical and data link layer use different protocols


Medium Access in Wifi vs. Cellular
- WIFI: CSMA/CA, RTS/CTS, asynchronous 
- Cellular: TDM, FDM, CDMA, centrally controlled

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

Fisher consensus
- "It is imopssible to guarantee that any asynchrnously connected set of nodes (computers) can ever agree on even a single bit value"

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

jitter -> variability in packet arrival times
- causes choppy audio / video, buffering or disrupted real-time apps

latency
- delay in packet delivery, impacts responsiveness in apps, noticeable in gaming & video calls

bandwidth
- maximum data transfer rate (Mbps) limits how much data can be sent, insufficient causes slow downloads and streaming issues

loss 
- dropped packets druing transmission, leads to incomplete data, reduced quality in calls / streams and application erorrs

unswitched -> cable that's tapped into (collisions happen)
fully switched -> each packet only delivered to host which addressed to (eliminates collisions)


NIC - continually monitors  arriving packets, and grabs for itself, has MAC address and OUI (6 bytes)

layers
- programming interface / library (layers communicate directly only above or below)
- Hierarchy
	- Link layer
		- LAN
			- Physical layer-  signaling mechanisms
			- logical LAN layer- the digital operations on packets
	- Internetwork layer
		- IP
	- Transport layer
		- TCP & UDP
	- Application layer 
		- (the software you use)

Internet backbone routers - IP routers that specialize in large-scale routing on the commercial Internet which generally have forwarding-table entries covering all public IP addresses and no default entry

non-backbone routers generally know all locally assigned network prefixes, or send to ISP that provides internet connectivity

Classless IP delivery algorithms vs. class based

Route leak -> accidentally offering transit service (that the AS is not set up to handle)

TIMEWAIT -> receiver responds only to duplicates of the final DATA packet

SWS -> when TCP transfers only small amounts of data (overwhelms)


Beacon frames
- sent periodically by AP, includes SSID and MAC address


![Screenshot 2024-11-17 at 10.39.22.png](../images/Screenshot%202024-11-17%20at%2010.39.22.png)


![Screenshot 2024-11-16 at 18.26.57.png](../images/Screenshot%202024-11-16%20at%2018.26.57.png)


![Screenshot 2024-11-19 at 16.54.34.png](../images/Screenshot%202024-11-19%20at%2016.54.34.png)


![Screenshot 2024-11-17 at 19.57.54.png](../images/Screenshot%202024-11-17%20at%2019.57.54.png)


![Screenshot 2024-11-17 at 22.37.52.png](../images/Screenshot%202024-11-17%20at%2022.37.52.png)