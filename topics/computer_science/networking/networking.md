# Networking

<br>![networking image](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/resources/networking.jpg)


## Table of Content

+ [Communications & Networking](#communications-and-networking)
  + [References](#references)
  + [Introduction to Communication and Networks](#introduction-to-communication-and-networks)
  + [The physical layer and Transmission media](#the-physical-layer-and-transmission-media)
  + [Data link layer](#data-link-layer)
  + [Network layer](#network-layer)
  + [Transport layer](#transport-layer)
  + [Session layer and Presentation layer](#session-layer-and-presentation-layer)
  + [The Application layer and Network security](#the-application-layer-and-network-security)
  + [Introduction to next-generation communication technologies](#introduction-to-next-generation-communication-technologies)
+ [Advanced networking & Data security](#advanced-networking-and-data-security)
  + [Introduction to Advanced network components](#introduction-to-advanced-network-components)
  + [Network protocols](#network-protocols)
  + [Multimedia and Real-time applications](#multimedia-and-real-time-applications)
  + [Computer network operations](#computer-network-operations)
  + [Future broadband networking trends and topics](#future-broadband-networking-trends-and-topics)
  + [Virtualization, Secure storage, and Grid computing](#virtualization,-secure-storage,-and-grid-computing)
  + [Broadband wireless networking](#broadband-wireless-networking)
  + [Network security fundamentals](#network-security-fundamentals)


## Communications and Networking


### References

- Peter L. Dordal (2023). _**Introduction to Computer Networks**_. 2nd edition. Loyola University. Chicago. Retrieved from [here](http://intronetworks.cs.luc.edu/current2/html/index.html).
- Mitra, R., Brown, G., Huffman, M., & Zhu, H. (n.d.). _**Telecommunications and networking**_. Pressbooks. Retrieved from [here](https://utsa.pressbooks.pub/networking/).

- Synthesis:
  - [1_Communications_and_networking](https://github.com/AnselmoGPP/know_base/master/topics/computer_science/others/1_Communications_and_networking.md)
  - [Network_fundamentals](https://github.com/AnselmoGPP/know_base/master/topics/computer_science/others/network_fundamentals.md)


### Introduction to Communication and Networks

#### References

- _Introduction to Computer Networks_ (2023)

  1. An overview of networks
    1.1. Layers
    1.2. Data rate, Throughput, and Bandwidth
    1.3. Packets
    1.4. Datagram forwarding
    1.5. Topology
    1.9. LANs and Ethernet
  5. Other LANs
    5.5. Asynchronous Transfer Mode: ATM
  7. Packets
    7.1. Packet delay
    7.2. Packet delay variability
    7.3. Packet size

- _Telecommunications and networking_ (n.d.)

  2. The growth of the Internet
    - Early computing
    - Evolving technologies
    - The digital divide
  3. Overview of network models
    - Network system models
    - Network reference models

- Videos

  - CertBros. (2020, Apr 21). _**TCP/IP Model Explained | Cisco CCNA 200-301**_ [Video](https://youtu.be/OTwp3xtd4dg). YouTube.
  - Code-exe. (2020, OCT 10). _**Networks - Episode 2 | LAN, WAN & PAN**_ [Video](https://youtu.be/IXkMgGhUcgE). YouTube.
  - IT-Made-Easy. (2021, July 5). _**OSI Model animated, what is OSI model in networking? 7 OSI layers explained**_ [Video](https://youtu.be/Ca1jnqwqzg0). YouTube.
  - Make It Easy Education. (2021, Apr 7). _**Computer Networks Topology || MESH, BUS, STAR, RING AND HYBRID TECHNOLOGY**_ [Video](https://youtu.be/mpFWIZ318eQ). YouTube. 
  - Quick Learn. (2020, June 15). Introduction to Data Communication and Networking [Video](https://youtu.be/OmYHJShD_QM). YouTube.

#### Synthesis

**Layers**: Each layer communicates directly only with the two layers immediately above and below it.

  - __Application__ layer (application): An application hands off a chunk of data to TCP.
  - __Transport__ layer (TCP): It makes calls to the IP.
  - __Internetwork__ layer (IP): It calls the LAN.
  - __Link__ layer (LAN): It delivers the data. It can be subdivided into:
    - __Physical LAN__: LAN hardware.
    - __Logical LAN__: Kernel software interface.

**Four-layer model**: Application > Link > Internetwork > Transport.

**Five-layer model**: Application > Transport > Internetwork > Logical LAN > Physical LAN.

**Data rate**: Rate at which bits are transmitted on a network connection.

**Throughput**: Overall effective transmission rate, taking into account different factors (account transmission overhead, protocol inefficiencies, competing traffic...). Usually measured at a higher network layer than the data rate.

**Bandwidth**: 











### The physical layer and Transmission media

#### References

- _Introduction to Computer Networks_ (2023)

  6. Links
    6.2. Time division multiplexing

- _Telecommunications and networking_ (n.d.)

  4. The physical layer
    - Connecting hosts through physical media
    - Bit rates
    - Encoding and modulation
    - Common networking hardware devices

- javatpoint (n.d.) _**Difference between synchronous and asynchronous transmission**_. T point Tech. Retrieved from [here](https://www.tpointtech.com/synchronous-vs-asynchronous-transmission).

- Videos

  - Ankit Verma (2021) _**Types of multiplexing | FDM TDM WDM | Analog digital | Computer networks**_. YouTube. Retrieved from [here](https://youtu.be/WXof7bg_Zys).
  - Business courses (2022) _**NRZ-L (Non-Return to Zero Level), NRZ-I (Non-Return to Zero Inverted), Manchester Encoding**_. YouTube. Retrieved from [here](https://youtu.be/gwe3S_AFLEo).
  - Esoteric ray (2021). _**Differential Manchester encoding tutorial**_. YouTube. Retrieved from [here](https://youtu.be/7BaJyQmXVbc).
  - Future electronics (2021) _**Microchip's Manchester code**_. YouTube. Retrieved from [here](https://youtu.be/3OndfNWAH3g).
  - Practical networking (2020). _**Hub, bridge, switch, router - Network devices - Networking fundamentals - Lesson 1b**_. YouTube. Retrieved from [here](https://youtu.be/H7-NR3Q3BeI).

#### Synthesis

…


### Data link layer

#### References

- _Introduction to Computer Networks_ (2023)

  7. Packets
    7.4. Error detection

- _Telecommunications and networking_ (n.d.)

  5. The Data Link layer
    - Introduction
    - Framing
    - Recovering from Transmission errors
    - Reliable data transfer on top of an imperfect link
    - Protocols associated with the Data link layer

- Videos

  - Engineering Funda. (2023, May 14). _**Examples on Selective Repeat ARQ Protocol in Computer Network**_. YouTube. Retrieved from [here](https://youtu.be/-qOfQym-TVo).
  - Neso Academy. (2020, May 1). _**Ethernet**_. YouTube. Retrieved from [here](https://youtu.be/MzhiVE6OuQA).
  - Neso Academy. (2020, March 18). _**High-Level Data Link Control (HDLC)**_. YouTube. Retrieved from [here](https://youtu.be/N2tgsPUPEBE).
  - Neso Academy. (2020, March 21). _**Point-to-Point Protocol (PPP)**_. YouTube. Retrieved from [here](https://youtu.be/kKCwkRT_U8I).
  - PowerCert Animated Videos. (2019, January 13). _**CSMA/CD and CSMA/CA Explained**_. YouTube. Retrieved from [here](https://youtu.be/iKn0GzF5-IU).
  - Sudhakar Atchala. (2021, May 11). _**Hamming code || Error Detection and Error Correction**_. YouTube. Retrieved from [here](https://youtu.be/cb0T4UE0c4w).

#### Synthesis

…


### Network layer

#### References

- _Introduction to Computer Networks_ (2023)

  9. IP version 4
    9.1. The IPv4 header
    9.2. Interfaces
    9.3. Special addresses
    9.4. Fragmentation
    9.5. The classless IP delivery algorithm
    9.6. IPv4 subnets
  11. IPv6
    11.1. The IPv6 header
    11.2. IPv6 addresses
    11.3. Network prefixes
    11.4. IPv6 multicast
    11.5. IPv6 extension headers
    11.6. Neighbor discovery
    11.7. IPv6 host address assignment
  13. Routing update algorithms
    13.1. Distance-vector routing-update algorithm
    13.2. Distance-vector slow-convergence algorithm
    13.5. Link-state routing-update algorithm
  15. Border gateway protocol (BGP)
    15.4. Filtering and routing policies
    15.5. BGP table size
    15.6. BGP path attributes
    15.7. BGP and traffic engineering
    15.8. BGP and anycast
    15.9. BGP for interior routing
    15.10. BGP relationships
    15.11. Examples of BGP instability
    15.12. BGP security and route registries

- _Telecommunications and networking_ (n.d.)

  6. The Network Layer I | Addressing
    - IPv4 addressing
    - IP subnetting
    - Constructing an IP network addressing scheme
    - The IPv6 address
  7. The Network Layer II | Routing
    - Routers
    - Routing in IP networks
    - Interdomain routing: BGP

- Videos

  - Engineering Wing. (2022, May 11). _**Lec05-Open Loop and closed Loop congestion control | Network layer performance-part 3**_. YouTube. Retrieved from [here](https://youtu.be/KCTQmtWg82Q).
  - Neso Academy. (2022, June 1). _**Classful Addressing (Part 1)**_. YouTube. Retrieved from [here](https://youtu.be/VkgfyLf1raY).
  - Neso Academy. (2022, July 1). _**Classless Addressing (Part 2)**_. YouTube. Retrieved from [here](https://youtu.be/PGwtar-BZzs).

#### Synthesis

…


### Transport layer

#### References

- _Introduction to Computer Networks_ (2023)

  16. UDP transport
    16.1. User Datagram Protocol - UDP
    16.3. Fundamental transport issues
    16.5. Remote Procedure Call (RPC)
  17. TCP transport basics
    17.2. TCP header
    17.3. TCP connection establishment
    17.8. TCP state diagram
  18. TCP issues and alternatives
    18.3. The three-way handshake revisited
    18.7. TCP sliding windows
    18.10. TCP flow control
    18.14. TCP timers
  19. TCP Reno and Congestion management
    19.1. Basics of TCP congestion management
    19.2. Slow start
    19.6. Selective acknowledgments (SACKS)
    19.8. Single packet losses
    19.9. TCP assumptions and scalability
    19.10. TCP parameters

- _Telecommunications and networking_ (n.d.)

  8. The Transport layer
    - The Transport layer
    - Transport layer protocols
    - Connectionless service
    - Reliability and congestion control
    - The connection-oriented service
    - Phases of the connection-oriented service

- Videos

  - JimKurose. (2022, January 15). _**3.6 Principles of congestion control**_. YouTube. Retrieved from [here](https://youtu.be/Fm92xvIp6JY).

#### Synthesis

…


### Session layer and Presentation layer

#### References

- Musa, S. M. (2018). _**Network Security and Cryptography**_. Mercury Learning & Information. Retrieved from [here](https://dokumen.pub/network-security-and-cryptography-a-self-teaching-introduction-1942270836-9781942270836.html).

  3. Overview of cryptography
    3.6. Symmetric (or conventional) encryption model (pp. 123-126)
  6. Modern symmetric ciphers
    6.5. Data Encryption Standards (DES) (pp. 219-231)
    6.8. International Data Encryption Algorithm (IDEA) (pp. 262-274)
  7. Public key cryptography for data confidentiality
    7.4. RSA algorithm (pp. 292-300)
    7.7. Elliptic Curve Cryptography (ECC) (pp. 308-312)
  8. Authentication schemes
      8.3.3. Message Authentication Cde (MAC) (PP. 342)
    8.4. Application modes of digital signatures (pp. 349-352)
    8.8. Digital signature schemes (pp. 376-388)
  12. Internet security services
    12.7. Secure Socket Layer/Transport Layer Security (SSL/TLS) (pp. 444-448)

- Mulder, V., Mermoud, A., Lenders, V., & Tellenbach, B. (Eds.). (2023). _**Trends in Data Protection and Encryption Technologies**_. Springer. Retrieved from [here](https://link.springer.com/book/10.1007/978-3-031-33386-6).

  - Part I: Encryption foundations
    - Section 3: Asymmetric encryption (pp. 11-15)
  - Part II: Low level applications
    - Section 11: Functional encryption (pp. 55-59)

- Videos

  - Prof. Saleh Oqeili Lectures. (2020, June 2). _**Data Compression Techniques**_. YouTube. Retrieved from [here](https://youtu.be/3hIdN-wZowM).

#### Synthesis

…


### The Application layer and Network security

#### References

- _Introduction to Computer Networks_ (2023)

  26. Network management and SNMP
    26.2. SNMP basics
    26.3. SNMP naming and OIDs
    26.7. SNMP tables
    26.8. SNMP operations
    26.14. SNMP alternatives
  27. SNMP versions 2 and 3
    27.1. SNMPv2
    27.2. Table row creation
    27.3. SNMPv3

- _Telecommunications and networking_ (n.d.)

  7. The Application layer
    - Introduction
    - Application Layer Protocols
    - Hypertext Transfer Protocol Secure (HTTPS) 
    - The Domain Name System (DNS) 
    - Dynamic Host Configuration (DHCP)
    - RDP
    - Telnet
    - LDAP
    - IMAP/POP3
    - SMTP 
    - NTP 
    - FTP 
    - SNMP
    - SSH 
    - TLS(SSL)

- Videos

  - WIT Solapur - Professional Learning Community. (2021, April 28). _**Electronic Mail**_. YouTube. Retrieved from [here](https://youtu.be/chzCgHdr6G4).
  - Instrumentation Tools. (2022, November 13). _**Intrusion Detection System (IDS) and Intrusion Prevention System (IPS)**_. YouTube. Retrieved from [here](https://youtu.be/0H502fmj5IY).

#### Synthesis

…


### Introduction to next-generation communication technologies

#### References

- Bhushan, B., Sharma, S. K., Kumar, R., & Priyadarshini, I. (Eds.). (2023). _**5g and beyond**_. Springer. Retrieved from [here](https://link.springer.com/book/10.1007/978-981-99-3668-7).

  1. Evolution of next-generation communication technology (pp. 1-19)

- Mishra, V. K. (2018). _**Software Defined Networks**_. Momentum Press. Retrieved from [here]().

  3. History of software-defined networking
    3.1. Early Approaches to Programmable Data Plane (DP) (pp.17-21)  
    3.2. Early approaches to Control Plane (CP) and Data Plane (DP) (pp.21-24) 
    3.3. Early Approaches to Network Function Virtualization (NFV) (pp.24-25) 
    3.4. Early Approaches to Network Operating System (NOS) (pp.25-26) 
  4. An overview of software defined networking
    4.1. High-Level SDN Architecture (pp.27-28) 
    4.2. Data Plane (DP) (pp.28-29) 
    4.3. Control Plane (CP) (pp.29-32) 
    4.4. Application Management Plane (AMP) (pp.32-34) 
    4.5. Role of Orchestration in SDN (pp.34-35) 
    4.6. SDN Security (pp.35-36) 

- Zhang, Y. (2018). _**Network Function Virtualization: Concepts And Applicability in 5g Networks**_. John Wiley & Sons, Incorporated. Retrieved from [here]().

  3. Network Function Virtualization  
    3.1. NFV Architecture (pp. 38-42) 
    3.2. NFV Use Cases and Examples (pp. 42-45) 
    3.3. BFV Challenges (pp. 45-46) 
    3.4. NFV Orchestration (pp. 46-47) 
    3.5. NFV Performance Characterization (pp. 47-49) 
    3.6. NFV Performance Improvements (pp. 49-50) 
    3.7. NFV Example (pp. 50-52)

- Kapoor, A. (2019). _**Hands-On Artificial Intelligence for IoT: Expert Machine Learning and Deep Learning Techniques for Developing Smarter IoT Systems**_. Packt Publishing, Limited. Retrieved from [here]().

  1. Principles and Foundations of IoT and AI  
    1.1. What is IoT 101? (pp. 7-13) 
  9. Personal and Home IoT 
    9.1. Personal IoT (pp. 274-283) 
    9.2. IoT and Smart Homes (pp. 284-295) 
  10. AI for the Industrial IoT 
    10.1. Introduction to AI Powered Industrial IoT (pp. 297-299) 
    10.2. Predictive Maintenance using AI (pp. 300-315) 
  11. AI for Smart Cities IoT 
    11.1. Why do we need Smart Cities? (pp. 321-328) 
    11.2. Adapting IoT for Smart Cities and the necessary steps (pp. 328-336) 

- Robinson, D. (2017). _**Content Delivery Networks: Fundamentals, Design, and Evolution**_. John Wiley & Sons, Incorporated. Retrieved from [here]().

  2. Context and Orientation 
    2.5. What is a CDN: A Simple Model (pp. 63-70) 

- Boeira, Felipe. _**Authentic Communication and Trustworthy Location in Mobile Networks**_, Linkopings University, 2023. ProQuest Ebook Central. Retrieved from [here]().

  2. Background  
    2.4. Cellular Networks (pp. 25-29) 
  5. Uncovering Threats in Cellular Networks 
    5.1. Security Analysis of Lawful Interception in 5G (pp. 68-70) 
    5.2. Threat Scenario Case Studies (pp.71-75) 

- Videos

  - Unriddle Tech. (2021, May 10). _**Software Defined Networking | SDN**_. YouTube. Retrieved from [here](https://youtu.be/lfqQhRkL4Vo).
  - alantalkstech. (2021, January 26). _**Network Functions Virtualization (NFV)**_. YouTube. Retrieved from [here](https://youtu.be/NtvoD0Lfzxc).
  - Great Learning. (2020, July 17). _**Internet of Things (IoT) in 10 minutes | What is IoT and how it works | Great learning**_. YouTube. Retrieved from [here](https://youtu.be/Fj02iTrWUx0).
  - Honest Marg. (2023, May 6). _**What is a Content Delivery Network (CDN)? | How do CDNs work? What are the benefits of using a CDN?**_. YouTube. Retrieved from [here](https://youtu.be/vNLQo13e20c).
  - Sunny Classroom. (2023, March 7). _**How does cellular network work?**_. YouTube. Retrieved from [here](https://youtu.be/cUWl_EhuNHg).

#### Synthesis

…


## Advanced networking & Data security

### Resources

- Ivan Marsic (2013) _**Computer networks: Performance and quality of service**_. Rutgers University. New Jersey. Retrieved from [here](https://www.ece.rutgers.edu/~marsic/books/CN/book-CN_marsic.pdf).
- Mell, P. & Grance, T. (2011, September). _**The NIST definition of cloud computing**_. National Institute of Standards and Technology. NIST Special Publication 800-145. Retrieved from [here](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwi56pfj7p2EAxWXSaQEHfxKAoUQFnoECA4QAQ&url=https%3A%2F%2Fnvlpubs.nist.gov%2Fnistpubs%2Flegacy%2Fsp%2Fnistspecialpublication800-145.pdf&usg=AOvVaw3eDW_Nq66d7NUNBEv7FTeg&opi=89978449).
- Smart Grid & Cyber Security for Energy Assurance (2010, October). _**Planning Elements for Consideration in States’ Energy Assurance Plans**_. Final Draft Report. Electric Power Research Institute (EPRI). Retrieved from [here](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwiIp4m0752EAxU-UqQEHUFwCr4QFnoECBEQAQ&url=https%3A%2F%2Fwww.researchgate.net%2Fprofile%2FMohamed-Mourad-Lafifi%2Fpost%2FCan_anybody_please_suggest_me_some_cyber_related_data_for_the_energy_delivery_systems_or_smart_grid%2Fattachment%2F5de5033e3843b0938393f852%2FAS%253A831639273869318%25401575289662750%2Fdownload%2FNASEO_Smart_Grid_and_Cyber_Security_for_Energy_Assurance_rev_November_2011.pdf&usg=AOvVaw2-6E3Uvbm-LKN4ERqTJR4K&opi=89978449).
- NIST Special Publication 800-125 (2011). Guide to Security for Full Virtualization Technologies. Retrieved from [here](https://csrc.nist.gov/pubs/sp/800/125/final). 
- K. Ahmad (2004). _**Grid Architectures and Technologies Lecture**_.
- Vint Cert (2010) _**Comments on Cloud Computing**_. Retrieved from [InfoWorld](https://www.infoworld.com/article/2629245/cerf-urges-standards-for-cloud-computing.html) and [The Guardian](https://www.theguardian.com/technology/blog/2010/feb/05/google-cloud-computing-intercloud-cerf).
- Federal Communications Commission (FCC) (2010). _**Connecting America: The National Broadband Plan**_. Retrieved from [here](https://transition.fcc.gov/national-broadband-plan/national-broadband-plan.pdf).
- Beyer, D. (2002). _**Wireless Mesh Networks for Residential Broadband**_.
- Hoebeke, J. (2006). _**An Overview of Mobile Ad Hoc Networks: Applications and Challenges**_. INTC Ghent University. Retrieved from [here](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwiXstOd-52EAxVIUKQEHYbIB-8QFnoECA4QAQ&url=https%3A%2F%2Fwww-di.inf.puc-rio.br%2F~endler%2Fcourses%2FMobile%2Fpapers%2FMANET-Challenges.pdf&usg=AOvVaw01eehm0MYKldHGGX1aw2T_&opi=89978449).
- Andrews, J. (2008). _**3G and 4G Cellular Standards**_. Wireless Networking Communications Group (WNCG). Retrieved from [here](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwiQlqnB-52EAxXrSKQEHZwQDtsQFnoECBkQAQ&url=https%3A%2F%2Fwww.cosmocom.gr%2Fwp-content%2Fuploads%2F2013%2F05%2FWirelessStandardsSummary.pdf&usg=AOvVaw3HVE0WP7pmXZV4lRIn4lJ4&opi=89978449).
- NIST SP 800-127 (2010). _**Guide to Securing WiMAX Wireless Communications**_. Retrieved from [here](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjpnI-B_J2EAxVdcKQEHbxuBpsQFnoECA4QAQ&url=https%3A%2F%2Fnvlpubs.nist.gov%2Fnistpubs%2Flegacy%2Fsp%2Fnistspecialpublication800-127.pdf&usg=AOvVaw21ljz2KbeGXrXEPW7ARpRB&opi=89978449).
- NIST SP 800-97 (2007). _**Establishing Wireless Robust Security Networks: A Guide to IEEE 802.11i**_. Retrieved from [here](https://csrc.nist.gov/pubs/sp/800/97/final)
- Ogletree, T, (2006). _**Upgrading and Repairing Networks**_. Retrieved from [here](https://web.archive.org/web/20111018214712/http://freeopenbook.com/upgrading-repairing-networks/ch44.html).
- NIST Special Publication 800-100 (2006). _**Information Security Handbook: A Guide for Managers**_. Retrieved from [here](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-100.pdf).
- NIST Special Publication 800-53 (2010). _**Recommended Security Controls for Federal Information Systems and Organizations**_. Retrieved from [here](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-53r3.pdf).
- _**Cloud Security Alliance Cloud Controls Matrix (CSA CCM)**_. Retrieved from [here](https://cloudsecurityalliance.org/research/working-groups/cloud-controls-matrix#_overview).
- _**DHS Top 20 Security Controls**_ (Department of Homeland Security).

### Introduction to Advanced network components

- _Computer networks: Performance and quality of service_ (2013)
  - 1 Introduction to Computer networks

### Network protocols

- _Computer networks: Performance and quality of service_ (2013)
  - 2 Transmission Control Protocol (TCP)
  - 9 Internet protocols

### Multimedia and Real-time applications

- _Computer networks: Performance and quality of service_ (2013)
  - 3 Multimedia and Real-time applications

### Computer network operations

- _Computer networks: Performance and quality of service_ (2013)
  - 4 Switching and queuing delay models
  - 5 Mechanisms for quality-of-service

### Future broadband networking trends and topics

- _The NIST definition of cloud computing_ (2011)
- _Planning Elements for Consideration in States’ Energy Assurance Plans_ (2010, pages 1-10)

### Virtualization, Secure storage, and Grid computing

- _Guide to Security for Full Virtualization Technologies_ (2011, sections: 2, 3, 4, 5)
- _Grid Architectures and Technologies Lecture_ (2004)
- _The NIST definition of cloud computing_ (2011)
- _Comments on Cloud computing_ (2010)

### Broadband wireless networking

- _Computer networks: Performance and quality of service_ (2013)
  - 6 Wireless networks
- _Connecting America: The National Broadband Plan_ (2010) (chapter 5)
- _Wireless Mesh Networks for Residential Broadband_ (2002) (pages 13-24)
- _An Overview of Mobile Ad Hoc Networks: Applications and Challenges_ (2006)
- _3G and 4G Cellular Standards_ (2008)
- _Guide to Securing WiMAX Wireless Communications_ (2011) (chapters 2, 3, 4) (optional reading)
- _Establishing Wireless Robust Security Networks: A Guide to IEEE 802.11i_ (2007) (optional reading)

### Network security fundamentals

- _Upgrading and Repairing Networks_ (2006) (chapter 44, 45: Security Issues for Wide Area Networks)
- _Information Security Handbook: A Guide for Managers_ (2006) (chapters 2, 3, 6)
- _Recommended Security Controls for Federal Information Systems and Organizations_ (2010) (chapters 1, 2, 3)
- _Cloud Security Alliance Cloud Controls Matrix (CSA CCM)_
- _DHS Top 20 Security Controls_
