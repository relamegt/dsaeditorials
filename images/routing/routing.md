# Routing

## Introduction

Routing is the process of selecting the best path for data packets to travel from a source device to a destination across one or more interconnected networks. Routers perform routing by examining destination IP addresses and forwarding packets through the most efficient path. Routing plays a vital role in packet-switched networks such as the Internet by ensuring reliable, efficient, and timely data delivery.

## Router

A **Router** is a networking device that forwards data packets between different networks based on destination IP addresses.

### Key Features

- Operates at Layer 3 (Network Layer) of the OSI model.
- Forwards packets between different networks.
- Selects the best available route.
- Uses routing tables for forwarding decisions.

## Working of Routing

Routing takes place through the following steps:

1. The sender creates a data packet containing the destination IP address.
2. The nearest router receives the packet.
3. The router checks its routing table.
4. The router selects the best available path.
5. The packet is forwarded through one or more intermediate routers (hops).
6. The process repeats until the destination is reached.
7. The destination reassembles the received packets and verifies their integrity.

**Note:** Every packet has a maximum hop count. If the hop count exceeds the limit, the packet is discarded.

# Types of Routing

## 1. Static Routing

Static routing is a routing method in which routes are manually configured by the network administrator.

### Features

- Routes are manually configured.
- Full administrator control.
- Simple implementation.
- Best suited for small networks.

### Advantages

- Easy to understand.
- No routing update traffic.
- High security.
- Predictable routing.

### Disadvantages

- Difficult to manage in large networks.
- Does not adapt to network failures.
- Requires manual updates.

---

## 2. Dynamic Routing

Dynamic routing automatically discovers and updates network routes using routing algorithms.

### Features

- Automatic route updates.
- Adapts to topology changes.
- Suitable for large networks.
- Uses routing protocols.

### Advantages

- Automatically adapts to failures.
- Reduces manual configuration.
- Highly scalable.
- Efficient path selection.

### Disadvantages

- Consumes bandwidth for routing updates.
- Requires more processing power.
- More complex configuration.

---

## 3. Default Routing

Default routing forwards packets to a predefined gateway whenever no specific route exists.

### Features

- Used when no matching route exists.
- Simple configuration.
- Common in small networks.
- Uses the default route:

**Default Route**

```Code
0.0.0.0/0
```

### Advantages

- Easy to configure.
- Reduces routing table size.
- Suitable for single-exit networks.

### Disadvantages

- May create inefficient routing.
- Depends entirely on the default gateway.

# Main Routing Protocols

## 1. Routing Information Protocol (RIP)

### Features

- Distance Vector protocol.
- Uses hop count.
- Suitable for small networks.

## 2. Open Shortest Path First (OSPF)

### Features

- Link State protocol.
- Uses Dijkstra's Algorithm.
- Supports large networks.

## 3. Enhanced Interior Gateway Routing Protocol (EIGRP)

### Features

- Hybrid routing protocol.
- Fast convergence.
- Efficient route calculation.

## 4. Border Gateway Protocol (BGP)

### Features

- Path Vector protocol.
- Used between autonomous systems.
- Standard Internet routing protocol.

## 5. Intermediate System to Intermediate System (IS-IS)

### Features

- Link State protocol.
- Used by Internet Service Providers.
- Suitable for large-scale networks.

# Routing Algorithms

## 1. Distance Vector Routing

Distance Vector Routing shares routing tables with neighboring routers periodically.

### Features

- Uses neighboring router information.
- Periodic routing updates.
- Uses fixed-length subnetting.
- Suitable for smaller networks.

### Algorithm Used

- Bellman-Ford Algorithm

---

## 2. Link State Routing

Link State Routing shares network topology information whenever changes occur.

### Features

- Sends updates only after topology changes.
- Uses Variable Length Subnet Mask (VLSM).
- Faster convergence.
- Better scalability.

### Algorithm Used

- Dijkstra's Algorithm

# Routing Metrics

Routing protocols use several metrics to determine the best path.

## Hop Count

- Number of routers crossed by a packet.
- Lower hop count is preferred.

## Bandwidth

- Available transmission capacity.
- Higher bandwidth is preferred.

## Delay

- Time required for packet delivery.
- Lower delay is preferred.

## Load

- Current traffic on a network path.
- Lower load is preferred.

## Reliability

- Stability and availability of a network path.
- More reliable paths are preferred.

# Advantages of Routing

- Selects efficient communication paths.
- Supports automatic route selection.
- Scales well for large networks.
- Supports load balancing.
- Improves overall network performance.

# Disadvantages of Routing

- Static routing is difficult to maintain in large networks.
- Dynamic routing consumes additional bandwidth.
- Dynamic routing requires more CPU and memory.
- Incorrect default routing may lead to communication failures.

# Summary

Routing is the process of forwarding data packets from a source to a destination through the best available network path. Routers perform routing using routing tables and routing protocols. Routing can be Static, Dynamic, or Default, depending on how routes are determined. Common routing protocols include RIP, OSPF, EIGRP, BGP, and IS-IS, while routing decisions are based on metrics such as hop count, bandwidth, delay, load, and reliability.




