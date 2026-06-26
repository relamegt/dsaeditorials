# Distance Vector Routing (DVR) Protocol

## Introduction

Distance Vector Routing (DVR) is a dynamic routing protocol in which each router maintains a routing table containing the distance to every destination in the network. Routers periodically exchange their routing tables with neighboring routers and use the **Bellman-Ford Algorithm** to determine the shortest path for forwarding data packets.

## Key Features

- Dynamic routing protocol.
- Based on the Bellman-Ford Algorithm.
- Routers periodically exchange routing tables.
- Uses hop count or path cost as a routing metric.
- Automatically updates routes when network topology changes.
- Suitable for small and medium-sized networks.

## Bellman-Ford Basics

Each router maintains a **Distance Vector Table** containing the shortest known distance to every destination.

### Information Stored in the Distance Vector Table

- Router ID.
- Link cost to neighboring routers.
- Number of intermediate hops.
- Shortest known distance to every destination.

### Initialization

- Distance to itself = 0
- Distance to all other routers = ∞

# Working of Distance Vector Routing

## Step 1: Exchange Routing Tables

Each router periodically sends its distance vector table to all directly connected neighboring routers.

## Step 2: Receive Routing Information

When a router receives a neighbor's routing table:

- It stores the received information.
- It compares the received routes with its current routing table.
- If a shorter path is found, it updates its routing table.
- Routing tables are also updated whenever a network link fails.

## Step 3: Calculate Shortest Path

The shortest path is calculated using the Bellman-Ford equation.

### Bellman-Ford Formula

Dx(y)=min{ C(x,v)+D_v(y) }

Where:

- (D_x(y)) = Cost from router **x** to destination **y**
- (C(x,v)) = Cost from router **x** to neighboring router **v**
- (D_v(y)) = Cost from neighboring router **v** to destination **y**

## Example

Consider three routers:

- Router X
- Router Y
- Router Z

Router X shares its routing table with Router Y.

Router Y shares its routing table with Router X.

Router X applies the Bellman-Ford equation to calculate the shortest path to Router Z.

If the route through Router Y has a lower cost, Router X updates its routing table accordingly.

Similarly, Router Z updates its routing table after receiving information from neighboring routers.

Eventually, all routers maintain the shortest paths to every destination.

# Applications

## Computer Networks

- Used for routing data packets between routers.

## Telephone Networks

- Used in telephone switching systems.

## Military Networks

- Used in communication and missile routing systems.

# Advantages

- Finds the shortest available path.
- Easy to implement.
- Requires low computational resources.
- Suitable for LAN, MAN, and WAN.
- Automatically updates routing information.

# Disadvantages

- Slow convergence after topology changes.
- Suffers from the Count-to-Infinity problem.
- Generates periodic routing update traffic.
- Poor scalability for very large networks.
- Large routing tables increase bandwidth usage.

# Summary

Distance Vector Routing (DVR) is a dynamic routing protocol based on the Bellman-Ford Algorithm. Each router maintains a routing table and periodically exchanges routing information with neighboring routers to determine the shortest path. DVR is simple to implement and widely used in small and medium-sized networks, but its slow convergence and Count-to-Infinity problem make it less suitable for very large networks.




