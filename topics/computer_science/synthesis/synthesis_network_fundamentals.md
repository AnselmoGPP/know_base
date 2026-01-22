# Network fundamentals

## Table of Contents
+ [Resources](#resources)
+ [Introduction](#introduction)
+ [Network types](#network-types)
+ [Cabling devices](#cabling-devices)
+ [The OSI model](#the-osi-model)

## Resources

- Network direction (2023) _**Network fundamentals**_ (playlist). YouTube. Retrieved from [here](https://www.youtube.com/playlist?list=PLDQaRcbiSnqF5U8ffMgZzS7fq1rHUI3Q8)

## Introduction

**Network:** System that allows multiple devices to communicate to one another.
**Switch:** Device used to connect multiple devices together through cables.
**Wireless Access Point:** Device used to connect multiple devices together wirelessly.
**Hub:** Old devices not used anymore. Today, they've been replaced by switches.
**Router:** Device used to connect to the Internet.

Often, a router, switch and Access point are integrated into a single device.

Example: A computer in a lab may be connected to a **wall socket**, which is connected to another cable that goes through the wall and is connected to a port in a **patch pannel** that is somewhere else, which in turn connects all its ports directly into the **switch**. At home, devices are usually connected to the switch directly.

We can connect a switch and a WAP through a cable and make both part of the same network. This gives us more connection options (we can connect a laptop to the switch while working on a desk, and connect it to Wi-Fi for making a presentation in the meeting room).

**Protocol:** Devices that communicate information between each other have to speak the same "language". They agree on the process of how to handle that information (how data is sent, how it's received, how it's organized, and how it's handled). There're many protocols with different uses (Ethernet, TCP, HTTP, SMTP...). Network software and hardware are designed with these protocols in mind. Many protocols work together to get a common task done.


## Network types

- **Network equipment:** Switch, Router, etc.
- **Endpoints (or hosts):** Devices connected to the network equipment (computers, servers, printers...).

Network types (size):
- **SOHO (Small Office, Home Office):** It involves a few connected devices (couple of computers + printer + few phones + tablet...). Some are connected to Wi-Fi and others cabled to a switch.
- **Small to Medium business (SMB):** Similar to an Enterprise network, but using cheaper networking equipment.
- **Enterprise network:** It may involve hundred of devices (large corporations like banks). It may cover several floors in a building, or several office buildings around the country.
- **Internet/Service Provider (ISP) Network:** Very large network. It provides Internet. It also offers services to connect their customers together (it may provide links, or network connectivity, between all the branches of a bank)

Network types (distribution):
- **Local Area Network (LAN):** Big or small network that is confined to a single location. A SMB network may involve a bunch of LANs connected together. An Enterprise network may involve one LAN for a building, or one LAN per floor, all of them connected together.
- **Wide Area Network (WAN):** Network covering a wide area (like offices in different cities, which are likely connected together by an ISP).


## Cabling devices

Devices can be connected using **wired** or **wireless** connections.

**Cables** are can be made of:
- **Copper:** Cheaper. Used for short distances. Data transferred with electrical signals, so they can be affected by outside interference.
- **Fiber:** Expensive. Used for long distances. Data transferred with pulsing light, so it cannot be affected by outside interference. Made of strands of glass (pipe, core). 

**Ethernet:** Protocol used by physical links (like a wired LAN). It has different parts:
- Physical rules: Type of cabling and speed.
- Media Access Control: How data should be formatted and sent.
- etc.
This make different devices with different cables and speeds be able to communicate. Example: a computer with a slow connection formats a message accordingly and sends it to a server with a fast connection. The server decodes the message at the physical layer and obtains the same message that the first computer had.

**IEEE** has created many standards for different technologies, such as Ethernet protocol. Each standard have a code. Examples:
- 802: LAN technologies
- 802.3: [Ethernet](https://en.wikipedia.org/wiki/IEEE_802.3) cables.
	- 802.3i = 10 Mbps
	- 802.3u = 100 Mbps
	- 802.3ab = 1 Gbps
	- 802.3an = 10 Gbps

These codes have easier to remember versions. Example:
802.3an = 10GBASE-T =   10GBASE-T = 10 Gigabits/s + Baseband (cable) + UTP (cable type)

Electrical cables use electrical signals (patterns of 1s & 0s). The pattern (encoding scheme) is decoded by the receiver.

**UTP (Unshielded Twisted Pair):** Most common type of copper cable. It usually has 4 pairs of wires, each pair forming a circuit. One pair can cause interference on another pair. Electricity in one pair cause a magnetic field that can affect the signal on another pair (**crosstalk**). Most crosstalk is eliminated by twisting together each pair. Each pair is color-coded. 

There're also **cable standards**, depending on the number of pairs, wire thickness, how tightly they're twisted, etc (cat2, Cat5e, Cat6, Cat6a, Cat7...). Newer standards support better speeds over longer distances, and is backward compatible with older technologies. Examples:
- 100Mb network -> You can use a CAT5 cable
- 1Gbps -> At least CAT5e.
- 10Gbps -> CAT6 (up to 55m) or CAT6a (up to 100m)

**Connectors:** Cables have a connector at both ends.

- **rj45:** Copper connector that you connect to the network card or switch port. It has 8 color-coded pins. There're different color schemes (568b...). Some pairs transmit data (TX) and others receive it (RX). 

  - **Straight Through cable:** Standard UTP cables match the pins at both ends. This type of cable connects a host to a switch. The host uses pair 1 as TX and 2 as RX, while the switch do the opposite (pair 1 as RX and pair 2 as TX). 

  - **Crossover cable:** To connect a host to a non-switch device (host, router...), or one switch to another, we use a cable that swaps the pairs at one end.

  - **Auto MDI-X technology:** A device supporting this can detect if the wrong cable is used and then logically switch the functions of the pins. The 100BASE and newer standards support this.

  - At 1000BASE it's different. It requires MDI-X support. The 1000BASE-TX uses 2 pairs as TX and 2 as RX (requires CAT6 or higher). The 1000BASE-T uses all 4 ports for sending and receiving (requires CAT5e or higher).

**Duplex:** It depends on the capabilities of the device at both ends and the software configuration.

- **Full duplex:** Both ends of the cable can send and receive at the same time (UTP cables can). 

- **Half duplex:** One end sends while the other receives. Both ends exchange roles regularly.

**Fiber cables:** Often used between networking devices (routers, switches...), or even servers. If it's bended too much, attenuation happens (degraded/lost signal), so check the bend radius. Types of cables it can use:

- **Single core:** One core. Half duplex. ISPs often use this.
- **Dual core:** Two cores. Full duplex. Enterprise networks mostly use this between switches, routers, and servers.

Types of fibre based on the type of light used:

- **Single mode fibre (SMF):** Expensive. Laser light. For >2kms.
- **Multi mode fibre (MMF):** Cheaper. LED light. For <500m.

Fiber cables can use many connectors (fibre is not only used for networking). For data networking, we often use:

- **SC:** Larger and older. 
- **LC:** Smaller. Usually used on switches and routers. It can be dual core or single core.

Some switches have special port/s for installing a **transceiver module**, which can be use for mixing and matching the top of cabling you use. Different transceivers support a different cable type (based on single/multi mode, speed, cable length, etc.). This way you can mix and match which transceivers you use for the job. There is a rj45 transceiver for using UTP copper cable. 

**Wireless (Wi-Fi) communication:** It doesn't use cabling, but access points, which are like a switch for wireless networks. Access points can connect to a wired network, making wired and wireless devices be in the same network. Access points are good for connecting end-user devices, but rarely for servers or routers. Code:
- 802.11 = Wireless (WiFi). This standard describes how microwaves format and encode information.

**Network addresses:** Every device on a network has a 2 unique addresses:
- **MAC:** Each network card from each device has one. It is assigned during manufacture and cannot change. It's used within the same LAN segment.
- IP: Chosen by us, network administrators. It's used within a segment, and to pass traffic to a different segment.

Two networks (**LAN segments**) can be joined together with a **router**. This router is part of both segments, and its job is to pass network traffic from one segment to another. If a device in one network wants to communicate with a printer in another network it sends to the router the message with the printer's IP and routerS's MAC. The router replaces the MAC in the message with the printer's MAC and forwards the message to the printer.

If, within a SOHO network, one device (computer) wants to communicate with another (printer), it can send a message to all the devices in the network. This happens sometimes, but if this happens everytime, it would be inefficient, insecure, and imprecise. 

## The OSI model
 
**OSI model:** Model of all the steps done for stablishing communications. It's not about specific technologies but rather how they fit into the network stack. Each layer can only communicate with the layer above and below. OSI model layers:

1. **Application:** Where apps (web brosing...) and network APIs (FTP...) live.
2. **Presentation:** Data has to be in an understandable format (image, video...).
3. **Session:** It tracks application processes (remote procedure calls, service requests...). It's like building a session between a local application and a remote one.
4. **Transport:** The data is divided into chunks and sent chunk by chunk. Different applications can take turns sending chunks (multiplexing) rather than one app hogging the hosts resources.
5. **Network:** Some information is added to the chunk as a header (destination address...) or trailer.
6. **Data link:**
7. **Physical:** Data is transmitted over cable or wireless to the remote host. Then, the data flow is reversed and each layer removes headers and trailers, modifying the data until it is in a form understood by the app at the application layer.

Layers 1, 2, 3 work with large pieces of information. The other layers work with small pieces (so connection interruptions don't make us start the whole transfer again or make other applications wait). Each chunk gets bigger and bigger as it moves through the network stack.








