# Introduction to Classful IP Addressing

## Introduction

**Classful IP Addressing** is an early IPv4 addressing scheme that was used to organize and allocate IP addresses across computer networks. Introduced during the early development of the Internet, this method divides the entire IPv4 address space into fixed address classes based on the leading bits of the first octet.

Each class defines a fixed boundary between the **Network ID** and the **Host ID**, allowing networks of different sizes to be created. Although Classful Addressing played an important role in the growth of the Internet, it was later replaced by **Classless Inter-Domain Routing (CIDR)** due to inefficient utilization of IP addresses.

### Key Features

- Divides IPv4 addresses into five fixed classes.
- Determines the class using the leading bits of the first octet.
- Classes A, B, and C are used for unicast communication.
- Class D is reserved for multicast communication.
- Class E is reserved for experimental and research purposes.
- Uses fixed network and host boundaries.

# Dotted Decimal Notation

IPv4 addresses are commonly represented using **Dotted Decimal Notation**, a human-readable format in which the 32-bit binary address is divided into four groups of eight bits called **octets**.

Each octet is converted into its decimal equivalent and separated by periods (dots), making IP addresses easier to read and remember.

### Characteristics

- Consists of four decimal numbers.
- Each octet ranges from **0 to 255**.
- Octets are separated by dots.
- Leading zeros are not used.
- Most widely used representation of IPv4 addresses.

### Example

```text
192.168.10.25
```

# Binary Representation

Internally, every IPv4 address is stored as a **32-bit binary number**.

For example, the previous IP address is represented as:

```text
11000000.10101000.00001010.00011001
```

# Hexadecimal Notation

Another way to represent an IPv4 address is **Hexadecimal Notation**. In this format, each 8-bit octet is converted into a two-digit hexadecimal value.

Although hexadecimal notation is less common in everyday networking, it provides a compact representation and is frequently used in networking software, debugging tools, and protocol analysis.

### Characteristics

- Uses hexadecimal digits **0–9** and **A–F**.
- Every octet is represented using two hexadecimal digits.
- Shorter than binary notation.
- Useful in low-level networking and programming.

### Example

```text
C0.A8.0A.19
```

# Need for Classful IP Addressing

When the Internet was first developed, there was a need for a structured method to allocate IP addresses to organizations of different sizes.

Classful Addressing provided a simple solution by dividing IPv4 addresses into predefined classes based on network size.

### Why It Was Introduced

- Simplified IP address allocation.
- Allowed networks of different sizes to receive appropriate address ranges.
- Enabled routers to identify address classes quickly.
- Reduced routing complexity during the early stages of the Internet.
- Simplified network management without requiring variable subnet masks.

# Types of Classful IP Addresses

Classful Addressing divides the IPv4 address space into five classes.

- Class A
- Class B
- Class C
- Class D
- Class E

Each class has its own address range, network size, host capacity, and intended purpose.

# Important Notes

- IPv4 addresses are **32 bits** long.
- IP address allocation is managed globally by organizations such as the **Internet Assigned Numbers Authority (IANA)** and **Regional Internet Registries (RIRs)**.
- The **first address** in every network represents the **Network Address**.
- The **last address** represents the **Broadcast Address**.
- These two addresses cannot be assigned to hosts.

# Address Space Occupation

In Classful Addressing, different classes occupy different portions of the IPv4 address space.

- Class A occupies the smallest number of networks but supports the largest number of hosts.
- Class B provides a balance between networks and hosts.
- Class C supports a very large number of networks with fewer hosts in each network.
- Class D is reserved for multicast communication.
- Class E is reserved for experimental purposes.

# Classes of Classful IP Addressing

The IPv4 address space is divided into **five different classes** based on the leading bits of the first octet. Each class is designed for a specific type of network and provides a fixed division between the **Network ID** and the **Host ID**.

# Class A

**Class A** addresses are designed for organizations that require a very large number of hosts.

The first bit of the first octet is always **0**, while the remaining bits identify the network.

### Characteristics

- Leading bit: **0**
- Network ID: **8 bits**
- Host ID: **24 bits**
- Default Subnet Mask: **255.0.0.0**
- Suitable for very large networks.

### Number of Networks

```formula
2^7 = 128 Networks
```

> Note: One network is reserved, so **127 usable Class A networks** are available.

### Number of Usable Hosts Per Network

```formula
2^24 - 2 = 16,777,214 Hosts
```

### IP Address Range

```text
0.0.0.0 to 127.255.255.255
```

---

# Class B

**Class B** addresses are intended for medium to large-sized organizations.

The first two bits of the first octet are always **10**.

### Characteristics

- Leading bits: **10**
- Network ID: **16 bits**
- Host ID: **16 bits**
- Default Subnet Mask: **255.255.0.0**
- Suitable for medium and large networks.

### Number of Networks

```formula
2^14 = 16,384 Networks
```

### Number of Usable Hosts Per Network

```formula
2^16 - 2 = 65,534 Hosts
```

### IP Address Range

```text
128.0.0.0 to 191.255.255.255
```

---

# Class C

**Class C** addresses are primarily used for small-sized networks.

The first three bits of the first octet are always **110**.

### Characteristics

- Leading bits: **110**
- Network ID: **24 bits**
- Host ID: **8 bits**
- Default Subnet Mask: **255.255.255.0**
- Suitable for small networks.

### Number of Networks

```formula
2^21 = 2,097,152 Networks
```

### Number of Usable Hosts Per Network

```formula
2^8 - 2 = 254 Hosts
```

### IP Address Range

```text
192.0.0.0 to 223.255.255.255
```

---

# Class D

**Class D** addresses are reserved for **multicast communication**, where a single sender transmits data to multiple receivers simultaneously.

Unlike Classes A, B, and C, Class D addresses do not contain separate Network ID and Host ID fields.

### Characteristics

- Leading bits: **1110**
- Used for multicast communication.
- No Network ID.
- No Host ID.
- No default subnet mask.

### IP Address Range

```text
224.0.0.0 to 239.255.255.255
```

---

# Class E

**Class E** addresses are reserved for **experimental and research purposes**.

These addresses are generally not assigned to hosts in normal computer networks.

### Characteristics

- Leading bits: **1111**
- Reserved for experiments.
- No Network ID.
- No Host ID.
- No default subnet mask.

### IP Address Range

```text
240.0.0.0 to 255.255.255.255
```

# Comparison of Classful Address Types

| Class | Leading Bits | Network ID | Host ID | Default Subnet Mask | Primary Purpose |
| --- | --- | --- | --- | --- | --- |
| A | 0 | 8 Bits | 24 Bits | 255.0.0.0 | Very Large Networks |
| B | 10 | 16 Bits | 16 Bits | 255.255.0.0 | Medium Networks |
| C | 110 | 24 Bits | 8 Bits | 255.255.255.0 | Small Networks |
| D | 1110 | — | — | Not Applicable | Multicast Communication |
| E | 1111 | — | — | Not Applicable | Experimental Purposes |

# Special IP Address Ranges

Some IPv4 address ranges are reserved for specific networking purposes and cannot be assigned as ordinary host addresses.

## 1. Link-Local Address Range

Link-local addresses are automatically assigned when a device cannot obtain an IP address from a DHCP server.

### Address Range

```text
169.254.0.0 - 169.254.255.255
```

### Uses

- Automatic IP address assignment.
- Communication within a local network.
- Troubleshooting DHCP failures.

---

## 2. Loopback Address Range

Loopback addresses allow a device to communicate with itself for testing and diagnostic purposes.

### Address Range

```text
127.0.0.0 - 127.255.255.255
```

### Uses

- Local host testing.
- Software debugging.
- Network diagnostics.

---

## 3. Current Network Address Range

This range is used during system initialization before a valid IP address is assigned.

### Address Range

```text
0.0.0.0 - 0.255.255.255
```

### Uses

- Indicates an unknown source address.
- Used during network startup.
- Temporary addressing before DHCP assignment.

# Rules for Assigning Host ID

A **Host ID** uniquely identifies a device within a network. Every host connected to the same network must have a different Host ID.

## Rule 1: Host IDs Must Be Unique

Every host within a network must have a unique Host ID.

### Reason

This prevents address conflicts and ensures that packets are delivered to the correct device.

---

## Rule 2: All-Zero Host ID Is Reserved

A Host ID containing all binary zeros cannot be assigned to a device.

### Reason

It represents the **Network Address**.

---

## Rule 3: All-One Host ID Is Reserved

A Host ID containing all binary ones cannot be assigned to a device.

### Reason

It represents the **Broadcast Address**, which is used to send packets to every host on the network.

# Rules for Assigning Network ID

The **Network ID** identifies an entire network. Devices belonging to the same network share the same Network ID.

## Rule 1: Network IDs Must Be Unique

Every network should have a unique Network ID.

### Reason

Unique Network IDs prevent routing conflicts.

---

## Rule 2: Network IDs Starting with 127 Are Reserved

Any Network ID beginning with **127** cannot be assigned to a network.

### Reason

The entire **127.x.x.x** range is reserved for loopback communication.

---

## Rule 3: All-One Network ID Is Reserved

A Network ID containing all binary ones is reserved.

### Reason

It is used for broadcast-related operations.

---

## Rule 4: All-Zero Network ID Is Reserved

A Network ID containing all binary zeros is also reserved.

### Reason

It represents the current network and is not used as a normal network identifier.

# Structure of Classful Addressing

The following table summarizes the characteristics of all five address classes.

| Class | Leading Bits | Network ID Bits | Host ID Bits | Number of Networks | Usable Hosts per Network | Start Address | End Address |
| --- | --- | --- | --- | --- | --- | --- | --- |
| A | 0 | 8 | 24 | 128* | 16,777,214 | 0.0.0.0 | 127.255.255.255 |
| B | 10 | 16 | 16 | 16,384 | 65,534 | 128.0.0.0 | 191.255.255.255 |
| C | 110 | 24 | 8 | 2,097,152 | 254 | 192.0.0.0 | 223.255.255.255 |
| D | 1110 | — | — | — | — | 224.0.0.0 | 239.255.255.255 |
| E | 1111 | — | — | — | — | 240.0.0.0 | 255.255.255.255 |

> **Note:** Although the theoretical number of Class A networks is **128**, one network is reserved, leaving **127 usable Class A networks**.

# Important Points to Remember

- IPv4 addresses contain **32 bits**.
- Classes A, B, and C are used for **unicast communication**.
- Class D is used for **multicast communication**.
- Class E is reserved for **experimental purposes**.
- The first address of a network is the **Network Address**.
- The last address of a network is the **Broadcast Address**.
- These reserved addresses cannot be assigned to hosts.

# Problems with Classful Addressing

Although Classful IP Addressing was simple to understand and implement, it introduced several limitations as the Internet expanded. The fixed division between the Network ID and Host ID often resulted in inefficient utilization of IPv4 addresses and increased routing complexity.

## 1. IP Address Wastage

Since each class has a fixed number of host addresses, organizations often received far more addresses than they actually required.

### Example

A company requiring only 500 hosts could not use a Class C network because it supports only 254 hosts. Instead, it had to obtain a Class B network containing **65,534** host addresses, leaving most of the addresses unused.

---

## 2. Fixed Network and Host Boundaries

The network and host portions were predefined for each class.

### Limitations

- No flexibility in address allocation.
- Difficult to allocate addresses based on actual requirements.
- Large organizations and small organizations often received inefficient address blocks.

---

## 3. No Variable Length Subnet Mask (VLSM)

Classful Addressing does not support variable subnet masks.

### Result

- Network administrators cannot create subnets of different sizes.
- Address utilization becomes inefficient.

---

## 4. Poor Scalability

As more devices joined the Internet, the fixed address classes became insufficient for efficient address allocation.

### Result

- Increased IPv4 address exhaustion.
- Difficult network expansion.

---

## 5. Large Routing Tables

Every network had to be stored separately in routing tables.

### Result

- Increased memory usage.
- Slower routing decisions.
- Higher processing overhead.

---

## 6. Inefficient Address Allocation

Organizations frequently received address blocks much larger than their actual requirements.

### Result

- Significant waste of IPv4 address space.
- Faster depletion of available addresses.

# Classful Addressing vs Classless Addressing (CIDR)

| Feature | Classful Addressing | Classless Addressing (CIDR) |
| --- | --- | --- |
| Address Allocation | Fixed address classes | Variable-length prefixes |
| Network Division | Fixed Network ID and Host ID | Flexible network prefix |
| Address Utilization | Less efficient | Highly efficient |
| Subnetting | Limited | Fully supported |
| VLSM Support | Not Supported | Supported |
| Route Aggregation | Not Supported | Supported |
| Routing Tables | Larger | Smaller through route aggregation |
| Scalability | Limited | Highly scalable |
| Flexibility | Low | High |
| IPv4 Utilization | Wastes addresses | Conserves addresses |
| Modern Usage | Obsolete | Widely used |

# Why CIDR Replaced Classful Addressing

Classless Inter-Domain Routing (CIDR) was introduced to overcome the limitations of Classful Addressing.

### Advantages of CIDR

- Allocates addresses according to actual requirements.
- Supports Variable Length Subnet Masks (VLSM).
- Reduces IPv4 address wastage.
- Supports route aggregation.
- Decreases routing table size.
- Improves routing efficiency.
- Provides greater flexibility and scalability.

# Key Points

- IPv4 addresses contain **32 bits**.
- Classful Addressing divides IPv4 addresses into **five fixed classes**.
- Classes **A**, **B**, and **C** support unicast communication.
- **Class D** is reserved for multicast communication.
- **Class E** is reserved for experimental and research purposes.
- Every network reserves one address as the **Network Address** and another as the **Broadcast Address**.
- Modern computer networks use **CIDR** instead of Classful Addressing because it provides better flexibility and efficient address allocation.

# Summary

Classful IP Addressing was one of the earliest IPv4 addressing methods and divided the address space into five predefined classes based on fixed Network ID and Host ID boundaries. Classes A, B, and C were designed for networks of different sizes, while Class D supported multicast communication and Class E was reserved for experimental use. Although this approach simplified address allocation during the early development of the Internet, it suffered from poor address utilization, limited scalability, and the inability to support Variable Length Subnet Masks (VLSM). These limitations led to the adoption of **Classless Inter-Domain Routing (CIDR)**, which provides flexible prefix lengths, efficient IP address allocation, smaller routing tables, and better scalability for modern computer networks.




