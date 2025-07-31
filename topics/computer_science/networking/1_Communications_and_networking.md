# Communications and Networking

<br>![networking image](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/resources/networking.jpg)


## Table of Contents
+ [Resources](#resources)
+ [Introduction to Communication and Networks](#introduction-to-communication-and-networks) (-> work in progress)


## Resources

- Peter L. Dordal (2020), _**An introduction to Computer Networks, 2nd**_. Loyola University. Chicago. Retrieved from [here](http://intronetworks.cs.luc.edu/current/html/index.html)
- Tanenbaum, A.S., Wetherall, D.J. (2011). _**Computer Networks, 5th**_. Pearson Education. New York. Retrieved from [here](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjFzM-z4J2EAxU_UKQEHe6ZDFEQFnoECA4QAQ&url=https%3A%2F%2Fcsc-knu.github.io%2Fsys-prog%2Fbooks%2FAndrew%2520S.%2520Tanenbaum%2520-%2520Computer%2520Networks.pdf&usg=AOvVaw0vGkjKgLWR8UnoBocnjazL&opi=89978449)
- Network direction (2023) _**Network fundamentals**_ (playlist). YouTube. Retrieved from [here](https://www.youtube.com/playlist?list=PLDQaRcbiSnqF5U8ffMgZzS7fq1rHUI3Q8).


## Introduction to Communication and Networks

### Layers

**Network layers:**
- **Link layer:** LAN (Local Area Network). Provides connection between machines within a local area (home, school, corporation…). Ethernet is a type of LAN. Components:
  - Physical LAN
  -Logical LAN
- **Internetwork layer:** IP (Internet Protocol). Provides abstraction for connecting multiple LANs (Internet).
- **Transport layer:** TCP (Transmission Control Protocol). It deals with transport, connections, and sending user data.
- **Application layer:** Software you use

**Layer models:**
- **4-layer model:** Link – Internetwork – Transport – Application
- **5-layer model** (due to IETF): Physical LAN – Logical LAN – Internetwork – Transport – Application
- **Layer:** Programming interface or library. Each layer communicates directly only to the layer immediately above or below it (2 layers).
- **LAN layer:** In charge of actual delivery of packets using LAN-layer-supplied addresses. Conceptually subdivided into 2 layers:
  - **Physical LAN layer:** Analog electrical, optical or radio signaling mechanisms, etc.
  - **Logical LAN layer:** All the digital operations on packets (kernel software interface).


### Data received

**Data rate:** Rate at which bits are transmitted in a network connection at a certain layer. Measured in kbps (kilobits/second) or Mbps (megabits/second), where kb=10³ and Mb=10⁶ bits. (not to be confused with kB [2¹⁰ bytes] or MB [2²⁰ bytes]).

**Throughput:** Overall effective transmission rate (takes into account transmission overhead, protocol inefficiencies and competing traffic). Generally measured at a higher network layer than the data rate.

**Bandwidth:** Synonym for data rate (mostly) or throughput.

**Goodput:** Application-layer throughput (amount of usable data delivered to the receiving application).


### Packets

Modest-sized **buffers** of data (built as 8-bit bytes) transmitted as a unit through some shared set of links. Called **frames** at the LAN layer, and **segments** at the transport layer.

They are prefixed with a **header** (datagram forwarding, virtual-circuit forwarding…) containing delivery information (destination address, identifier for the connection…). Internal nodes of the network (routers, switches) will try to ensure that the packet is delivered to the requested destination.

The maximum packet size supported by a given LAN is an intrinsic attribute of that LAN.

- Ethernet: 1500 bytes/packet maximum
- TCP/IP: 512 bytes originally
- Token Ring: 4 kB originally
- ATM (Asynchronous Transfer Mode) protocol: 48 bytes

Generally, each layer adds its own header: Ethernet (typically, 14 bytes) + IP (20 bytes) + TCP (20 bytes).

    [header ][        data        ]

    [header1][header2][        data        ]

How to forward packets from a large-packet LAN to/through a small-packet LAN? The IP layer addresses this.

Binary integers can be represented as a sequence of bytes in either big-endian or little-endian. RFC 1700 specifies that Internet protocols use **big-endian** byte order (**network byte order**).

Using packets allows a single link to carry, at different times, different packets from traffic to different destinations and from different senders. Packets support shared transmission lines (i.e., multiplexing of multiple commuications channels over a single cable). 

The maximum packet size represents the maximum time a sender can send before other sender get a chance. Having unbounded packet sizes could cause prolonged network unavailability for everyone else if someone downloads a large file in a single packet. Another drawback: if it is corrupted, the entire packet must be retransmitted.

When a router or switch receives a packet, it (generally) reads in the entire packet before looking at the header to decide to what next node to forward it (**store-and-forward** method), which introduces a **forwading delay** equal to the time to read in the entire packet. This delay is hard to avoid for individual packets (though some switches implement **cut-through** switching: they begin to forward the packet before it fully arrived), but if one is sending a long train of packets the significance of the delay can be eliminated by keeping multiple packets en route.

**Total packet delay** from sender to receiver is the sum of:

- **Propagation delay:** Due to speed of light (200 km/ms). Sending a packet througha 5000 kms cable will take 25 ms.
- **Bandwidth delay** (per-link delay): Sending 1000 Bytes at 20 Bytes/ms will take 50 ms.
- **Store-and-forward delay:** Sum of the bandwidth delays out of each router along the path.
- **Queuing delay:** Due to waiting in line at busy routers. At bad moments, it can exceed 1 s, but generally, it’s <10 ms, and often it’s <1 ms.


### Datagram forwarding

This is a model of packet delivery where the header contains a destination address. The routers or switches will look at this address and get the packet to its destination. Each switch has a **forwarding table** of pairs (**destination**, **next_hop**).

<br>![networking image](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/resources/net_1.png)

**Next_hop:** When a packet arrives, the switch looks up the destination address (presumed globally unique) in its forwarding table and finds the next_hop (immediate-neighbor address to which, or interface by which, the packet should be forwarded in order to bring it closer to its final destination). The next_hop value is a single entry, and each switch is responsible for only one step in the packet’s path.

**Destination:** These entries don’t have to correspond exactly with the packet destination addresses (although, they do for Ethernet datagram forwarding). For IP routing, these entries correspond to prefixes of IP addresses (this leads to huge savings in space).

Example: Switch S1 has interfaces 0, 1, 2, and S2 has 0, 1, 2, 3. If A sends a packet to B, S1 will have a forwarding-table entry indicating that destination B is reached via its interface 2, and S2 must have an entry forwarding the packet out on interface 3.

<br>![networking image](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/resources/net_2.jpg)

Each interface corresponds to the unique immediate neighbor reached by that interface. We can thus replace the interface entries (next_hop) with the name of the corresponding neighbor (more human-readable).

In datagram forwarding, each packet is forwarded “in isolation”; the switches involved don’t have any awareness of any higher-layer logical connections established between endpoints (**stateless** forwarding).

**Virtual circuits:** This is a fundamental alternative to datagram forwarding. Here, each router maintains state about each connection passing through it.

Datagram forwarding sometimes allows to use other information beyond the destination address. In theory, IP routing can be done based on the destination address and some **quality-of-service** information (this allows, for example, different routing to the same destination), although most ISPs (Internet Service Providers) ignores this (except by prearranged agreement).

By convention:

- **Switches:** Devices acting at the LAN layer and forwarding packets based on the LAN address. Ethernet switches using datagram-forwarding forward to individual nodes.
- **Routers:** Devices acting at the IP layer and forwarding on the IP address. IP routers using datagram-forwarding forward to entire networks (i.e. sets of nodes).

In IP routers within end-user sites it’s common for a forwarding table to include a catchall **default entry**, matching any non-local IP address and so needs to be routed out into the Internet at large. In LAN switches, a default entry is a single record representing where to forward the packet if no other destination match is found. Default entries make sense only when the address doesn’t represent a nearby node. This is common in IP networks because an IP address encodes the destination network, and routers generally know all the local networks. However, this is rare in Ethernets because there is generally no correlation between Ethernet addresses and locality (Ethernet switches doesn’t know what kind of device connects to a given interface [individual host, switch…]).

    S1
    destination   next_hop
    A             0
    C             1
    default       2


### Topology

A diagram with no loops is **acyclic**, or a **tree**. There is a unique path between any pair of nodes. But, if there are no loops, there is no **redundancy**, and any broken link will divide the network into two pieces that cannot communicate. If we have redundancy, we have to make decisions among the multiple paths to destination. Some protocol must exist to make that choice, Many LANs (particularly, Ethernet) prefer tree networks with no redundancy, while IP has complex protocols in support of redundancy.

    A---[S1]----[S2]
         |       |
         |       |
        [S3]----[S4]---B


### Traffic engineering

Any intentional selection of one route over another, or any elevation of the priority of one class of traffic. The route selection can either be directly intentional, through configuration, or through an algorithm (e.g., Distance-Vector Routing-Update Algorithm).

With pure datagram forwarding, used at either the LAN or the IP layer, the path taken by a packet is determined solely by its destination, and traffic engineering is limited to the choices made between alternative paths.

Datagram forwarding could be extented to take quality-of-service information into account. This information may be set by the end-user, in which case an ISP may wish to recognize it only for designated users (i.e., the ISP will implicitly use the traffic source for making routing decisions). Alternatively, that information can be set by the ISP itself, based on its bet guess as to the application (i.e., the ISP may use packet size, port number, and other contents for making routing decisions).

At LAN layer, traffic-engineering mechanisms are historically limited. At IP layer, more strategies are available.


### Routing loops

It is a potential drawback to datagram forwarding where a set of entries in the forwarding tables cause some packets to circulate endlessly (e.g.: S1 > S2 > S4 > S3 > S1). It causes the packet not to be delivered, and consumption of most bandwitdth.

Routing loops typically arise because the creation of forwarding tables is often “distributed” (no global authority). They can also occur in networks with a loop-free link topology (**linear routing loop**).

All datagram-forwarding protocols need some way of detecting and avoiding loops. Examples:

- Ethernet disallows loops in the underlying network topology (prevents **nonlinear routing loops**), and has no switches forwarding a packet back out the interface by which it arrived (prevents linear routing loops).
- IP provides a TTL (Time to Live) field in the header that is set by the sender and decremented by 1 at each router. The packet is discarded if TTL reaches 0.

In datagram routing, a switch is responsible only for the next hop to the ultimate destination. It may have a complete path in mind (A>B>C>D), but other switch downstream may consider a different path a better option (B>A>E>D), possibly leading to a routing loop.


### Congestion

It is caused when packets arrives to a switch faster than they can be sent out. Possible causes:

- The inbound interface has higher bandwidth than the outbound interface.
- Traffic arrives on multiple inputs, all destined for the same output.

If packets arrive for a given outbound interface faster than they can be sent, a queue will form for that interface. Once that queue is full, packets will be dropped (most common strategy). 

Congestion may refer to the point where the queue starts to build up (knee, contention), or where the queue is full and packets are lost (cliff).

In Internet, most packet losses are due to congestion. Other type of losses (corruption…) are insignificant in comparison.

In real-time networks we want to keep losses to an absolute minimum. One way to do it is to limit the acceptance of new connections unless sufficient resources are available.


### LANs and Ethernet

**LAN** (Local Area Network) **components:**

- Physical links (serial lines)
- Common interfacing hardware (connects hosts to links)
- Protocols (make everything work together)

Every LAN node can usually communicate with every other LAN node, but sometimes it requires the cooperations of intermediate nodes acting as switches.

**Ethernet** (1976) is by far the most common type of wired LAN. Today, it operates between 100 Mbps and 1 gigabit. It’s widely used in server rooms. **Wireless (Wi-Fi)** LANs are popular between end-users.

Many early Ethernet installations were unswitched. Each host simply tapped in to a single primary cable that wound through the building. Two stations could then transmit at the same time, rendering the data unintelligible (**collision**). However, Ethernet has several design features for minimizing the bandwidth wasted on collisions (transmit when the line is idle, detection of collision during transmission, random backoff if collision is detected…).

In unswitched Ethernets every packet is received by every host, and each host (its network card) must determine if the packet is address to him. This poses a security threat: password sniffers eavesdropping.

For privacy and efficiency, almost all Ethernets today are fully switched, which ensures that each packet is delivered only to the host to which it is addressed. It eliminates collisions, but introduces the queuing issue (but queues seldom fill up). It also prevents eavesdropping (though encryption could be a better solution).

**Ethernet addresses** are 6 bytes long (first 3 are assigned to the manufactures, next 3 are a serial number assigned by the manufacturer). Each Ethernet card (or **network interface**) is assigned a (supposedly) unique address at the time of manufacture, burned into the card’s ROM, and it’s called the **physical** address, or **hardware** address, or **MAC** address (Media Access Control). 

**IP addresses** are assigned administratively by the local site. 

The network interface continually monitors all arriving packets. If it sees any packet containing a destination address that matches its own physical address, it grabs the packet and forwards it to the attached CPU (via a CPU interrupt).

Ethernet also has a designated **broadcast address**. If a switch receives a broadcast packet on one port, it forwards the packet out every other port. This allows host A to contact host B when A doesn’t yet know B’s physical address. It may be used for asking for B’s physical address.

Traffic addressed to a particular host (i.e., not broadcast) is called **unicast**.

Ethernet addresses are assigned by the hardware, so they don’t provide any direct indication of where that address is located in the network. In switched Ethernet, the switches must thus have a **forwarding-table** record for each individual Ethernet address in the network. However, this becomes unwieldy for extremely large networks. Ethernet doesn’t scale well to “large” sizes, but works well for networks with 10.000-100.000 nodes.

Traditionally, Ethernet switches get all the active destination addresses locations in the LAN using a passive **learning algorithm**: a host physical address is entered into a switch’s forwarding table when a packet from that host is first received (IP, in turn, use “active” protocols). If a given destination address is not yet in the forwarding table, Ethernet switches may use the **flooding** option: forwarding the packet to everyone (like the broadcast address), which is generally used for just one packet (minimizing excessive traffic and eavesdropping).

The <host, interface> forwarding table can be thought as <host, next_hop>, where the next_hop is any switch or host at the immediate end of the link connecting to the given interface. In a fully switched network, each link connects only two interfaces.


### IETF and OSI

The **IETF** (Internet Engineering Task Force), guided by the **IAB** (Internet Architecture Board), guided by the **ISOC** (Internet Society), publishes RFC (Request For Comment) documents containing all the Internet standards (including the 5-layer model). RFC standards sometimes allow modest flexibility; that’s why RFC 2119 declares official definitions for MUST (absolute requirement) and SHOULD (can be ignored in particular circumstances).

- 1969 – DARPA (US Defense Advanced Research Projects Agency) puts ARPANET network online.
- 1977- ISO (International Organization for Standardization) founds OSI project (Open System Interconnection).
- 1986 – NSF (National Science Foundation) begins NSFNet, which replaces ARPANET.
- 1991 – Operation of NSFNet is turned over to ANSNet, a private corporation.
- 1992 – ISOC is founded. 

**OSI** tries to create networking standards independent of any individual government. It created the 7-layer model, though it is not necessary since the 2 new layers aren’t true layers.

- **7-layer model** (due to OSI): Physical LAN – Logical LAN – Internetwork – Transport – Session – Presentation – Application
  - **Presentation:** It handles things like defining universal data formats, compression, encryption, etc.
  - **Session layer:** It handles “sessions” between applications.

OSI has its own version of IP (CLNP) and TCP (TP4), and others (TP0, TP3…). However, OSI protocols have failed in the marketplace due to bureaucracy, completion, and rigid specifications.

In turn, IETF has a “two working implementation” rule for a protocol to become a “Draft Standard” (RFC 2026): only specifications with at least two independent and interoperable implementations may be elevated to the “Draft Standard” level. This facilitates the discovery of protocol design weaknesses early.

Trying to fit protocols into specific layers is often useless. A more successful approach to understand layers is to view them as parts of a **protocol graph**.

<br>![networking image](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/resources/net_3.jpg)


### LANs

#### - Wi-Fi

Wi-Fi is a trademark of the Wi-Fi Alliance denoting any of several IEEE wireless-networking protocols. Like classic Ethernet, Wi-Fi must deal with **collisions**; but unlike Ethernet, it’s unable to detect collisions in progress, complicating the backoff and retransmission algorithms.

In addition to normal data packets, Wi-Fi uses **control** and **management** packets that exist only in the Wi-Fi LAN layer. They are used to compensate for some infelicities of the radio environment (lack of collision detection, …).

Wi-Fi is designed to interoperate freely with Ethernet at the logical LAN layer. Wi-Fi MAC has the same size, same internal structure, and share same namespace (all addresses are different), than any Ethernet MAC. Therefore, data packets can be forwarded by switches between Ethernet and Wi-Fi.

IEEE stablish which ISM band (Industrial, Scientific, and Medical) is used by Wi-Fi. The Wi-Fi 6 (802.11ax) version uses the 5 GHz ISM band (previously, 2.5 GHz), which has reduced ability to penetrate walls, but provides more channels than lower frequencies. Wi-Fi radio spectrum is usually unlicensed (no permission needed to transmit), so others may be trying to use the same band simultaneously. Wi-Fi 6 has a channel width of 20-160 MHz, and a maximum bit rate up to 1200 Mbps. The effective bit rate takes into account the time spent in the collision-handling mechanism. In practice, the bit rate is reduced up to tenfold (or more) in environments with higher error rates (distance, obstructions, competing transmissions, radio noise). By international agreement, the ISM bands are divided into channels of 5 MHz (almost 200 5 MHz channels in the 5 GHz band, and 14 in the 2.5 GHz band). The more channels available, the faster Wi-Fi runs. Support for aditional frequency bands (6-7 GHz range) is awaiting FCC approval (in USA).

Wi-Fi designers use some techniques to improve throughput: improve radio modulation techniques, improve error-correcting codes, smaller guard intervals between symbols, increase channel width, allow multiple spatial streams via multiple antennas.

#### - Virtual Private Networks (VPN)

A **VPN** supports the creation of **virtual links** that join farflung nodes via the Internet. 

Your workplace has a security policy that doesn’t allow outside IP addresses to access essential internal resources, which prevent you from working from home. This ca be solved by connecting your computer (via TCP or UDP) to a workplace **VPN server** (IP-layer packet encapsulation can also be used, avoiding timeout problems sometimes created by sending TCP packets within another TCP stream). Each end of the connection is typically associated with a software-created **virtual network interface**, each one with its own IP address. When send a packet along the virtual link, it is sent through Internet to the VPN server (**tunneling**). The virtual link behaves like any other physical link. These packets are often encrypted and encapsulated. At workplace side, the virtual network interface in the VPN server is attached to a router or switch. At home user’s end, the virtual network interface can now be assigned an internal workplace IP address, making this computer part of the internal workplace network.

<br>![networking image](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/resources/net_4.jpg)

The user’s regular Internet connection is via hardware interface eth0. To connect to site A’s VPN server, a virtual interface tun0 (with its own site-A IP address) is created on user’s machine, which looks like a direct link to the VPN server. But, in fact, packets sent via tun0 interface travel via eth0 through Internet. The home host’s tun0 interface will appear to be locally connected to site A. The home host’s forwarding table would route site A’s private addresses via interface tun0.

Some VPN uses:

- Work from home (connecting home computer to workplace VPN server).
- To connect entire remote offices to headquarters (the office end of the tunnel will be the office’s local router).
- To appear geographically to be at another location to firewall rules blocking specific TCP or UDP ports.
- To improve security by using the VPN connection as the default route for all traffic (except that needed to maintain the VPN itsef). This may require a **host-specific** forwarding-table entry at the residential (or remote-office) end to allow the packets that carry the VPN tunnel traffic to be routed via eth0. This way, intruders cannot access the residential host (and thus, the workplace internal network) through the original residential Internet access. If the home worker downloads a file from a non-workplace site, it will travel first to the workplace, then back to Internet via the VPN connection, and the arrive at home.

To improve congestion response, IP packets are sometimes marked by routers experiencing congestion.

#### - Carrier Ethernet

It is a leased-line point-to-point link between two sites, where the subscriber interface at each end of the line looks like Ethernet (in some flavor). The physical path in between sites could be implemented however the carrier wishes (need not to do anything to with Ethernet). It will be, or appear to be, full-duplex, collision-free, and its length may exceed the maximum permitted by any IEEE Ethernet standard (IEEE: Institute of Electrical and Electronics engineers). It provides a layer of abstraction between customers (they only need to install a commodity Ethernet interface) and the provider (he can upgrade the link implementation (bandwidth…) at will without requiring changes at customer end).

The link technologies may not look aything like Ethernet, but the interface will. It’s similar to DSL and cable routers with an Ethernet interface for customer interconnection.

It looks like a virtual VPN link, but runs on top of the provider’s internal network rather than Internet at large. It often provides the primary Internet connectivity for one endpoint, unlike Internet VPNs which assume both edpoints already have full Internet connectivity.

#### - Token ring

Stations are connected in a ring (A>B>C>D>E>F>A) and packets are transmitted in one direction. Stations froward most packets around the ring, though they can remove a packet. When the network is idle, they forward a special, small packet (**token**). If station A wishes to transmit, it waits for the token to arrive at A, then forwards its packet instead of the token, it travels around the network and then it is removed by A. At that point (sometimes, when A finishes transmitting its packet), A forwards the token.

In a small ring network, the ring circumference may be a small fraction of one packet and the entire packet cannot be in transit.

It is a simple **multiple-access** method where all stations get an equal number of changes to transmit (**fairness**), and no bandwidth is wasted on collision (**collision-free**). Different implementations: FDDI (Fiber-Distributed Data Interface), IBM Token Ring, etc.

When stations are powered off it’s essential that the packets continue forwarding. Usually, this is addressed by configuring the default circuit to keep the loop closed.

Some station has to watch out in case the token disappears or a duplicate token appears.

IBM Token Ring was once considered the premium LAN mechanism. Later, Ethernet won out due to lower hardware costs and higher bit-rates (even taking collisions into account).

#### - Virtual circuits

It is an alternative to datagram switching, where routers know about end-to-end connections (instead of next_hop), and packets are addressed by a connection ID (instead of a destination). It’s considered the road not taken by IP. 

Before sending a data packet, a connection is stablished by computing the route and assigning a connection ID (**VCI**, Virtual Circuit Identifier) to each link along the path.

Packets arrive at (and depart from) switches via one of several ports. Switches maintain a **connection table** indexed by <VCI, port> pairs, which has a record of every connection through that switch at that particular moment (unlike forwarding tables). As a packet arrives, its inbound VCIin and inbound portin are looked up in this table; this yields an outbound <VCIout , portout> pair. The VCI field of the packet is then rewritten to VCIout, and the packet is sent via portout.

Typically, there is no source address information included in the packet. Packets are identified by connection, not destination. Any node along the path, including endpoints, could look up the connection and figure out the endpoints.

Each switch must rewrite the VCI. Each switch must rewrite the VCI (datagrams switches never rewrite addresses, but they update hopcount/TTL fields, and don’t use packet’s arrival interface).

Virtual-circuit switching advantages:

- Connections can get quality-of-service guarantees, because the switches are aware of connections and can reserve capacity at the time the connection is made.
- Headers are smaller, allowing:
  - Faster throughput.
  - Efficient support for very small packet sizes (optimal for voice connections).

Data forwarding advantages:

- Routers have less state information to manage.
- Router crashes and partial connection state loss are not a problem.
- If a router or link is disabled, rerouting is easy and doesn’t affect any connection state.
- Per-connection billing is very difficult.

#### - Asynchronous Transfer Mode (ATM)

ATM is a network mechanism intended to accommodate real-time traffic and bulk data transfer. It is sometimes used as a LAN layer, transmitting IP packets over ATM. It has a small packet size because it was originally intended to support voice. A significant source of delay in voice traffic is the packet **fill time**. Smaller packets reduce the fill time and thus the delay: when voice is sent over IP (VoIP), one common method is to send 160 bytes every 20 ms. But ATM packets (**cells**) have 48 bytes of data, plus 5 bytes of header (IP packets of such size would consume more than 50% of the bandwidth on headers, if the LAN header is included). To manage such a small header, virtual-circuit routing is a necessity 

Small cells advantages:

- Reduced fill time.
- Reduced store-and-forward delay.
- Minimal queuing delay (at least for high-priority traffic, since this traffic is never allowed to interrupt transmission already begun of a low-priority packet).

ATM requires **fixed-size cells**, simplifying hardware design and making easier to design for parallelism.

ATM mandates **no cell reordering**, so cells can use a smaller sequence-number field, but makes parallel switches much harder to build.

ATM cells content:

- Data: 48 bytes
- Header: 5 bytes
  - VCI information: 28 bits
  - Type: 3 bits
  - CLP (Cell-loss priority): 1 bit
  - Checksum: 8 bits

Forwarding is by full switching only, and there is no mechanism for physical (LAN) broadcast.

Due to the small packet size, ATM defines its own mechanisms (**ATM adaptation layers**) for **segmentation** and **reassembly** of larger packets. These mechanisms are called **ATM adaptation layers** (AALs), and there are 4 of them AALs 1, 2, 3/4 and 5 (1 and 2 are used only for voice-type traffic).


### Network software

#### Protocol hierarchies

To reduce design complexity, most networks are organized as a stack of **layers** (or levels), each one built upong the one below it. Each layer offers certain services to the higher layers while shielding those layers from the details of how these services are actually implemented.

- **Protocol:** Agreement between the communicating parties on how communication is to proceed (i.e., the rules and conventions used for layer n in a machine A for having a conversation with layer n in another machine).
- **Peers:** Entities that communicate by using the protocol to talk to each other. Entities (software processes, hardware devices, or human beings) comprising the corresponding layers on different machines.

<br>![networking image](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/resources/net_5.jpg)

In reality, no data are directly transferred from layer n on one machine to layer n on another machine. Instead, each layer passes data and control information to the layer immediately below it, until the lowes layer is reached. Actual communication occurs through the **physical medium**. Virtual communication is shown by dotted lines, and physical communication by solid lines.

- **Interface:** It defines what primitive operations and services the lower layer makes available to the upper one. Different hosts may use different implementations of the same protocol, but the other layers won't notice it.
- **Network architecture:** Set of layers and protocols. Neither the details of the implementation nor the specification of the interfaces is part of the architecture because they are hidden. It's not even necessary that the interfaces on all machines in a network be the same, provided that each machine can correctly use all the protocols.
- **Protocol stack:** List of the protocols used by a certain system (one protocol per layer).

Example: Phylosopher A, who speaks french, wants to send a message to phylosopher B, who speaks german (layer 3). Phylosopher A sends the message to translator A (layer 2), which in turn translates it to english and sends it to secretary A (layer 1). Secretary A sends the message by email to secretary B, which sends it to translator B, which translates it to german and sends it to phylosopher B. Each protocol is independent of the others as long as the interfaces doesn't change (translators can switch from english to chineses provided that they both agree and doesn't change their interface with layer 3 or 1) (secretaries can switch from email to telephone without other layers noticing it). 

A message M is produced by an application process running in layer 5 and given to layer 4 for transmission. Layer 4 puts a **header** in front of the message and passes the result to layer 3. In many networks, the message size has no limit in the layer 4 protocol, but a limit is nearly always imposed by the layer 3 protocol, so it breaks the incoming messages into smaller units (**packets**), preprends a header to each one, and pass them layer 2. Layer 2 add a header and a trailer and passes them to alyer 1 for physical transmission. At the receiving machine the message moves upward, from layer to layer, with headers being stripped of as it progresses. None of the headers for layers below n are passed up to layer n. The lower layers of a protocol hierarchy are frequently implemented in hardware or firmware.

- **Header:** Data put in front of the message by the layer. It includes control information like addresses (to allow the same layer in the destination deliver the message), sequences of numbers (in case the lower layer doesn't preserve message order), sizes, and times.

#### Design issues for the layers

...




### Connection-oriented and connectionless networks

**Data communication network:** Telecommunication network that allows two or more computers to send and receive data across the same or distinct networks.

Based on transmission, we can cathegorize networks in 2 groups: Connection-oriented and connectionless communication.

#### - Connection-oriented service

This is a network service where an end-to-end connection is established between the sender and the receiver before delivering data over the same or separate networks. It is a reliable network service. It is similar to the telephone system.

Packets are forwarded to the receiver in the same sequence as they were sent by the sender.

Before sending the data, the sender sends a request packet (SYN packet) to the receiver. Then, the receiver, answers the sender by sending him another packet (SYN-ACK). This serves as a “handshake” that confirms that the communication between the sender and the receiver can begin. Now, the sender can send the data to the receiver. Similarly, the receiver can react or send data to the sender.

To terminate the connection, the sender has to send a signal to the receiver. Connection-oriented communication takes place on the same transmission channel.

Example of connection-oriented protocol: TCP (Transmission Control Protocol).

**TCP (Transmission Control Protocol):** Connection-oriented protocol that allows two or more computers to communicate by creating connections in the same or separate networks. It is widely used over the internet protocol (that’s why it is also called TCP/IP). It guarantees that the transfer succeeds.

Advantages:
- Reliable connection (it assures that packets are received)
- Packets are received in the same sequence as they were transmitted
- No congestion (end-to-end link)

Disadvantages:
- Slower
- Requires more bandwidth
- Requires authentication before sending packets

#### - Connectionless service

This is a network service where data is send from one end to the other without establishing a connection. A sender can deliver any data to the recipient without first establishing a connection. It is similar to a postal system.

It doesn’t guarantee that the packets will be delivered to the receiver since they don’t follow a predefined path, and data may be lost due to congestion. These packets can arrive in any sequence. It is an unreliable network service.

Connectionless communication doesn’t necessarily take place on the same transmission channel. Transmissions are independently routed, and perhaps re-assembled in some order at the other end.

Examples of connectionless protocols: UDP (User Datagram Protocol), IP (Internet Protocol), ICMP (Internet Control Message Protocol).

**UDP (User Datagram Protocol):** Connectionless protocol that allows two or more computers to communicate without creating a connection. The sender simply sends packets to the receiver without establishing a connection. It doesn’t guarantee that the transfer succeeds, and doesn’t acknowledge the data.

Advantages:
- Faster
- Requires very low bandwidth
- Doesn’t require authentication before sending packets

Disadvantages:
- Unreliable connection (it doesn’t assure that packets are received)
- Not guarantee that packets are received in the same sequence as they were transmitted
- Congestion may occur (no end-to-end link)

#### - Quality of service

A protocol may sacrifice some reliability in exchange for greater speed. Sometimes, a handshake is necessary; but others the performance hit is unacceptable (like streaming video). Not all applications require connections. No protocol is superior to others. Sometimes, it’s not even necessary to ensure that a message gets sent, so long as the chance of it being received is high enough (like spammers).








