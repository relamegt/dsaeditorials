# Computer Networks Cheat Sheet — Final Interview Edition

## 1. Basic Terminology

| Term | Full Form / Meaning |
| --- | --- |
| CN | Computer Network — interconnected devices that share resources and data |
| NIC | Network Interface Card — hardware enabling a device to connect to a network |
| IP | Internet Protocol — addressing scheme for routing packets |
| MAC | Media Access Control — 48-bit hardware address burned into the NIC |
| ISP | Internet Service Provider |
| Node | Any device connected to the network (computer, router, printer) |
| Router | Device that forwards packets between different networks based on IP address |
| Switch | Device that forwards frames within the same network based on MAC address |

## 2. Types of Networks (By Scale)

- **PAN (Personal Area Network)** — covers a few meters (e.g., Bluetooth between phone and earbuds).
- **LAN (Local Area Network)** — covers a building/campus; high speed, privately owned.
- **MAN (Metropolitan Area Network)** — covers a city; connects multiple LANs.
- **WAN (Wide Area Network)** — covers countries/continents; the Internet is the largest WAN.

## 3. Network Topologies — How Each Works

- **Bus Topology**: All devices connect to a single shared cable (the "bus"); data sent by one node travels along the cable and is read by all, but only the intended recipient accepts it. Cheap but a single cable break kills the whole network.
- **Star Topology**: Every device connects individually to a central hub/switch. Data between two nodes actually passes through the hub. Easy to manage and isolate faults, but the hub is a single point of failure.
- **Ring Topology**: Each device connects to exactly two neighbors, forming a closed loop; data travels around the ring node by node until it reaches its destination. A single broken link can disrupt the entire ring (unless dual-ring).
- **Mesh Topology**: Every device connects directly to every other device. Highly fault-tolerant (multiple paths) but expensive due to the large number of cables needed.
- **Hybrid Topology**: Combination of two or more topologies (e.g., star-bus) to balance cost and reliability.

## 4. OSI Model — 7 Layers (How Data Flows)

**OSI = Open Systems Interconnection.** Data moves down through the sender's layers (each adding a header) and up through the receiver's layers (each stripping its header) — this is called encapsulation/decapsulation.

| Layer | Name | Function | Example Protocols/Devices |
| --- | --- | --- | --- |
| 7 | Application | Interfaces directly with user software, provides network services | HTTP, FTP, SMTP |
| 6 | Presentation | Translates, encrypts, and compresses data between formats | SSL/TLS, JPEG |
| 5 | Session | Establishes, manages, and terminates connections/sessions | NetBIOS, PPTP |
| 4 | Transport | Ensures reliable/unreliable end-to-end delivery, segments data | TCP, UDP |
| 3 | Network | Handles logical addressing and routing between networks | IP, ICMP, Router |
| 2 | Data Link | Handles physical addressing (MAC) and error detection within one network | Ethernet, Switch |
| 1 | Physical | Transmits raw bits over the physical medium | Cables, Hubs |

## 5. TCP/IP Model — 4 Layers

**How it works:** A simplified, practically-used model that combines OSI's top three layers into one Application layer, and OSI's bottom two into one Network Access layer.

| Layer | Corresponds to OSI | Role |
| --- | --- | --- |
| Application | Application + Presentation + Session | User-facing protocols (HTTP, FTP, DNS) |
| Transport | Transport | End-to-end communication (TCP, UDP) |
| Internet | Network | Logical addressing and routing (IP) |
| Network Access | Data Link + Physical | Physical transmission and framing |

## 6. TCP vs UDP — How Each Works

**TCP (Transmission Control Protocol)**
How it works: Before sending data, TCP performs a **three-way handshake** (SYN → SYN-ACK → ACK) to establish a connection. Data is broken into segments, each numbered; the receiver acknowledges (ACKs) received segments, and TCP retransmits any that are lost or corrupted. It also uses flow control and congestion control to avoid overwhelming the network.
Trait: Reliable, ordered, connection-oriented — but slower due to overhead. Used for web browsing (HTTP), email, file transfer.

**UDP (User Datagram Protocol)**
How it works: Sends data as independent datagrams with no handshake, no acknowledgment, and no guaranteed order or delivery — it just fires packets and hopes they arrive.
Trait: Connectionless, fast, low overhead — but unreliable. Used for video streaming, DNS queries, online gaming (VoIP).

## 7. Three-Way Handshake (TCP Connection Setup)

1. **SYN** — client sends a synchronize request with an initial sequence number.
2. **SYN-ACK** — server acknowledges and sends its own synchronize request back.
3. **ACK** — client acknowledges the server's request, and the connection is now established.

## 8. IP Addressing

- **IPv4**: 32-bit address, written as four decimal octets (e.g., 192.168.1.1); ~4.3 billion addresses.
- **IPv6**: 128-bit address, written in hexadecimal groups (e.g., 2001:db8::1); designed to solve IPv4 exhaustion.
- **Classes of IPv4** (historical): Class A (large networks), B (medium), C (small), D (multicast), E (experimental).
- **Public IP**: globally unique, routable on the internet.
- **Private IP**: used within local networks (e.g., 192.168.x.x), not routable on the internet directly.
- **Static IP**: manually assigned, doesn't change.
- **Dynamic IP**: assigned automatically by DHCP, can change over time.

## 9. Subnetting

**How it works**: A subnet mask splits an IP address into a network portion and a host portion, allowing a large network to be divided into smaller, manageable sub-networks. The number after the slash (CIDR notation) indicates how many bits are used for the network portion.

| CIDR | Subnet Mask | Usable Hosts |
| --- | --- | --- |
| /24 | 255.255.255.0 | 254 |
| /25 | 255.255.255.128 | 126 |
| /26 | 255.255.255.192 | 62 |
| /30 | 255.255.255.252 | 2 |

## 10. Key Protocols — How Each Works

**DNS (Domain Name System)**
How it works: Translates human-readable domain names (google.com) into IP addresses by querying a hierarchy of DNS servers (root → TLD → authoritative) until it finds the matching IP, which is then cached for faster future lookups. Runs on port 53.

**DHCP (Dynamic Host Configuration Protocol)**
How it works: Automatically assigns IP addresses to devices joining a network using a 4-step process — **DORA**: Discover (client broadcasts a request), Offer (server offers an IP), Request (client requests that IP), Acknowledge (server confirms the lease). Uses UDP ports 67/68.

**ARP (Address Resolution Protocol)**
How it works: Since devices communicate at the hardware level using MAC addresses, ARP resolves a known IP address to its corresponding MAC address by broadcasting a request ("who has this IP?") on the LAN; the owning device replies with its MAC address.

**NAT (Network Address Translation)**
How it works: Allows many devices on a private network to share a single public IP address; the router rewrites the source IP/port of outgoing packets to its own public IP, and maps incoming replies back to the correct internal device using a translation table.

**ICMP (Internet Control Message Protocol)**
How it works: Used for diagnostic and error-reporting messages (e.g., "destination unreachable," "time exceeded"). The `ping` command uses ICMP echo request/reply to test reachability, and `traceroute` uses ICMP with increasing TTL values to map the path packets take.

**HTTP/HTTPS (HyperText Transfer Protocol / Secure)**
How it works: HTTP is a stateless request-response protocol where a client requests a resource and the server responds with data (port 80). HTTPS adds a TLS/SSL encryption layer on top, encrypting the data in transit (port 443).

**FTP (File Transfer Protocol)**
How it works: Uses two separate connections — a control connection (port 21) for commands and a data connection (port 20) for actual file transfer.

**SMTP (Simple Mail Transfer Protocol)**
How it works: Used to send email from client to server or between mail servers; runs on port 25.

## 11. Common Port Numbers

| Protocol | Port |
| --- | --- |
| FTP | 20, 21 |
| SSH | 22 |
| SMTP | 25 |
| DNS | 53 |
| DHCP | 67, 68 |
| HTTP | 80 |
| HTTPS | 443 |
| SNMP | 161 |
| OSPF | 89 |
| BGP | 179 |

## 12. Routing — How It Works

**How routing works**: A router examines a packet's destination IP, consults its routing table (a list of network destinations and the next-hop to reach them), and forwards the packet to the best next-hop toward its destination — repeating hop-by-hop until it arrives.

- **Static Routing**: Routes are manually configured by an admin; doesn't adapt to network changes.
- **Dynamic Routing**: Routers automatically exchange information and adjust routes using protocols:
- **RIP (Routing Information Protocol)**: Uses hop count as its metric; simple but doesn't scale well.
- **OSPF (Open Shortest Path First)**: Uses link-state information and calculates the shortest path using Dijkstra's algorithm; fast convergence, used within large enterprise networks.
- **BGP (Border Gateway Protocol)**: The protocol that routes traffic between different autonomous systems (ISPs) across the entire internet.

## 13. Switching Techniques

- **Circuit Switching**: A dedicated physical path is established for the entire duration of the communication before data transfer begins (e.g., traditional telephone calls). Guarantees bandwidth but wastes resources when idle.
- **Packet Switching**: Data is broken into packets, each routed independently and possibly via different paths, then reassembled at the destination. Efficient resource use; basis of the modern internet.
- **Message Switching**: Entire message is stored at each intermediate node before being forwarded (store-and-forward) — largely obsolete.

## 14. Multiplexing

**How it works**: Combines multiple signals to travel over a single shared communication channel, then separates them at the receiving end.

- **FDM (Frequency Division Multiplexing)**: Splits the channel's bandwidth into separate frequency bands, one per signal.
- **TDM (Time Division Multiplexing)**: Splits transmission time into slots, each signal gets a turn in its assigned slot.
- **WDM (Wavelength Division Multiplexing)**: Used in fiber optics; multiple signals sent as different light wavelengths over one fiber.

## 15. Error Detection & Flow Control

- **Checksum**: Sender computes a value from the data and sends it along; receiver recomputes and compares to detect corruption.
- **CRC (Cyclic Redundancy Check)**: A more robust polynomial-division-based error-detection code appended to data frames.
- **Flow Control**: Prevents a fast sender from overwhelming a slow receiver.
- **Stop-and-Wait**: Sender sends one frame, waits for ACK before sending the next.
- **Sliding Window**: Sender can send multiple frames up to a window size before requiring an ACK, improving throughput.

## 16. Collision Handling

- **CSMA/CD (Carrier Sense Multiple Access with Collision Detection)**: Used in wired Ethernet — a device listens before transmitting; if a collision is detected during transmission, it stops, waits a random backoff time, and retries.
- **CSMA/CA (Collision Avoidance)**: Used in wireless (Wi-Fi) networks — since collisions are hard to detect over radio, devices try to avoid them by sensing the channel and using request-to-send/clear-to-send signaling before transmitting.

## 17. Network Devices

| Device | OSI Layer | Function |
| --- | --- | --- |
| Hub | Physical | Broadcasts incoming data to all connected ports (no intelligence) |
| Switch | Data Link | Forwards frames only to the correct port based on MAC address table |
| Router | Network | Routes packets between different networks based on IP |
| Gateway | Application (or any) | Connects two dissimilar networks (protocol translation) |
| Repeater | Physical | Regenerates and amplifies weak signals to extend cable range |
| Bridge | Data Link | Connects two LAN segments, filtering traffic by MAC address |

## 18. Network Security Basics

- **Firewall**: Monitors and filters incoming/outgoing traffic based on defined security rules, blocking unauthorized access.
- **VPN (Virtual Private Network)**: Creates an encrypted tunnel over a public network so remote users can securely access a private network as if directly connected.
- **Encryption**: Symmetric (same key for encrypt/decrypt, faster) vs Asymmetric (public/private key pair, used in SSL/TLS handshakes).
- **DoS (Denial of Service)**: Attacker floods a server with traffic/requests to exhaust its resources and make it unavailable to legitimate users.
- **DMZ (Demilitarized Zone)**: A buffer subnet placed between a private internal network and the public internet, hosting public-facing services while isolating the internal network.

## 19. Transmission Media

- **Guided (Wired) Media**: Twisted Pair Cable (cheap, moderate speed), Coaxial Cable (better shielding), Fiber Optic Cable (light-based, highest speed and distance, immune to electromagnetic interference).
- **Unguided (Wireless) Media**: Radio waves, Microwaves, Infrared — signals travel through air without a physical conductor.

## 20. Quick Interview Traps

- OSI has 7 layers (conceptual model); TCP/IP has 4 layers (practically implemented model).
- TCP is reliable but slower (handshake + acknowledgments); UDP is fast but unreliable (no handshake).
- Switches use MAC addresses (Layer 2); routers use IP addresses (Layer 3).
- DNS resolves names to IPs; DHCP assigns IPs automatically; ARP resolves IP to MAC.
- CSMA/CD is for wired networks (can detect collisions); CSMA/CA is for wireless (avoids them since detection is hard).
- Public IP is unique globally; private IP is reused across different local networks via NAT.
- A /24 subnet gives 254 usable host addresses (256 minus network and broadcast addresses).

