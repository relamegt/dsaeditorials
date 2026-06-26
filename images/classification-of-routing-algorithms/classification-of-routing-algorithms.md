# Classification of Routing Algorithms

## Introduction

Routing is the process of determining the path that data packets follow from a source device to a destination device in a network. Routers use routing algorithms to identify efficient paths and maintain routing tables that store routing information. Routing algorithms improve network performance by selecting suitable paths based on factors such as distance, traffic, and network topology.

## Classification of Routing Algorithms

Routing algorithms are broadly classified into:

- Adaptive Algorithms
- Non-Adaptive Algorithms
- Hybrid Algorithms

## 1. Adaptive Algorithms

Adaptive routing algorithms modify routing decisions whenever network topology or traffic conditions change. They are also known as **Dynamic Routing Algorithms** and use current network information to determine the best path.

### Features

- Automatically adapts to topology changes.
- Uses dynamic network information.
- Optimizes routing based on distance, delay, load, and hop count.
- Suitable for large and complex networks.

### Types of Adaptive Algorithms

#### Isolated Routing

Each node makes routing decisions independently using only its own information.

##### Features

- No information exchange with neighboring nodes.
- Simple implementation.
- May route packets through congested paths.

##### Examples

- Hot Potato Routing
- Backward Learning

#### Centralized Routing

A central controller maintains complete network information and determines routing paths.

##### Features

- Central node maintains the entire network topology.
- Provides accurate routing decisions.
- Failure of the central node affects the entire network.

##### Example

- Link-State Algorithm

#### Distributed Routing

Each router exchanges routing information with neighboring routers before making routing decisions.

##### Features

- Uses information from neighboring routers.
- No central controller required.
- Supports decentralized routing.
- May experience temporary routing delays after topology changes.

---

## 2. Non-Adaptive Algorithms

Non-Adaptive routing algorithms use predefined routes that do not change after configuration. They are also called **Static Routing Algorithms**.

### Features

- Routes remain fixed.
- No response to traffic or topology changes.
- Simple implementation.
- Suitable for small networks.

### Types of Non-Adaptive Algorithms

#### Flooding

Every incoming packet is forwarded through every outgoing link except the incoming link.

##### Features

- No routing table required.
- Always delivers through the shortest available path.
- Produces duplicate packets.
- High network traffic.

#### Random Walk

Packets are forwarded randomly to one of the neighboring nodes.

##### Features

- Simple routing method.
- Highly robust.
- Often selects the least congested link.
- Does not guarantee the shortest path.

---

## 3. Hybrid Algorithms

Hybrid routing algorithms combine both adaptive and non-adaptive routing techniques. Different regions of a network may use different routing methods.

### Features

- Combines advantages of static and dynamic routing.
- Suitable for large enterprise networks.
- Provides flexibility and scalability.

### Types of Hybrid Algorithms

#### Link-State Routing

Each router builds a complete map of the network and shares it with all routers.

##### Features

- Complete network topology.
- Accurate routing decisions.
- Fast convergence.
- High memory requirement.

#### Distance Vector Routing

Each router maintains a routing table containing distance and direction information for every destination.

##### Features

- Exchanges routing tables with neighboring routers.
- Simple implementation.
- May create routing loops.
- Suitable for medium-sized networks.

# Difference Between Adaptive and Non-Adaptive Routing

| Adaptive Routing | Non-Adaptive Routing |
| --- | --- |
| Dynamic routing | Static routing |
| Routes change automatically | Routes remain fixed |
| Responds to topology changes | Does not respond to topology changes |
| Uses current network information | Uses predefined routing information |
| Suitable for large networks | Suitable for small networks |
| Higher complexity | Lower complexity |
| Better performance in changing networks | Better for stable networks |

# Routing Protocols

## 1. Routing Information Protocol (RIP)

Routing Information Protocol (RIP) is one of the earliest Interior Gateway Protocols that determines routes using hop count.

### Features

- Distance vector protocol.
- Uses hop count metric.
- Suitable for LANs and small WANs.
- Simple configuration.

## 2. Interior Gateway Routing Protocol (IGRP)

Interior Gateway Routing Protocol (IGRP) is a Cisco-developed distance vector routing protocol.

### Features

- Supports up to 100 hops.
- Uses bandwidth, delay, reliability, and load.
- Automatically updates routes.
- Prevents routing loops.

## 3. Exterior Gateway Protocol (EGP)

Exterior Gateway Protocol (EGP) exchanges routing information between different autonomous systems.

### Features

- Used between autonomous systems.
- Supports inter-domain routing.
- Exchanges routing information across gateways.

## 4. Enhanced Interior Gateway Routing Protocol (EIGRP)

Enhanced Interior Gateway Routing Protocol (EIGRP) is an advanced Cisco routing protocol.

### Features

- Classless protocol.
- Distance vector protocol.
- Uses Diffusing Update Algorithm (DUAL).
- Supports fast convergence.
- Shares routing information with neighboring routers.

## 5. Open Shortest Path First (OSPF)

Open Shortest Path First (OSPF) is a link-state routing protocol that uses the Shortest Path First algorithm.

### Features

- Link-state protocol.
- Uses Dijkstra's algorithm.
- Supports authentication.
- Scalable for small and large networks.
- Maintains topology databases.

## 6. Border Gateway Protocol (BGP)

Border Gateway Protocol (BGP) is the standard routing protocol used between autonomous systems on the Internet.

### Features

- Exterior Gateway Protocol.
- Path vector protocol.
- Uses best path selection.
- Supports Internet-scale routing.
- Uses Autonomous System Numbers (ASN).

# Difference Between Routing and Flooding

| Routing | Flooding |
| --- | --- |
| Requires routing table | No routing table required |
| May provide shortest path | Always provides shortest path |
| Less reliable | More reliable |
| Low network traffic | High network traffic |
| No duplicate packets | Duplicate packets are generated |

# Advantages of Routing Algorithms

- Select optimal network paths.
- Improve network efficiency.
- Reduce transmission delay.
- Support scalable communication.
- Adapt to changing network conditions.

# Limitations of Routing Algorithms

- Dynamic routing increases complexity.
- Routing updates consume bandwidth.
- Some algorithms create routing loops.
- Large routing tables require more memory.

# Summary

Routing algorithms determine the best path for transmitting data across computer networks. They are classified into Adaptive, Non-Adaptive, and Hybrid algorithms based on how routing decisions are made. Popular routing protocols such as RIP, IGRP, EIGRP, OSPF, and BGP implement different routing techniques depending on network size, complexity, and performance requirements.




