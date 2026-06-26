# Sliding Window Protocol

## Introduction

The **Sliding Window Protocol** is a flow control and error control mechanism used in computer networks to improve data transmission efficiency. Instead of waiting for an acknowledgment after sending every packet, the sender is allowed to transmit multiple packets continuously before acknowledgments are received.

This protocol keeps several packets "in transit" at the same time, making better use of the communication channel and significantly increasing throughput, especially in networks with high bandwidth or long propagation delays.

Sliding Window Protocol is widely used in the **Data Link Layer** and the **Transport Layer**, including the **Transmission Control Protocol (TCP)**.

### Key Features

- Allows multiple packets to be transmitted before receiving acknowledgments.
- Improves channel utilization and throughput.
- Supports reliable and ordered packet delivery.
- Uses sender and receiver windows to manage communication.
- Reduces idle waiting time during transmission.

# Important Terminologies

Understanding the following terms makes it easier to analyze the performance of Sliding Window Protocol.

## 1. Transmission Delay (Tt)

Transmission Delay is the time required to place all bits of a packet onto the communication channel.

### Formula

```text
Transmission Delay (Tt) = Data Size (D) / Bandwidth (B)
```

Where:

- **D** = Packet Size (bits)
- **B** = Bandwidth (bits per second)

### Characteristics

- Depends on packet size.
- Depends on available bandwidth.
- Independent of communication distance.

---

## 2. Propagation Delay (Tp)

Propagation Delay is the time required for the first transmitted bit to travel from the sender to the receiver through the communication medium.

### Formula

```text
Propagation Delay (Tp) = Distance (d) / Signal Speed (s)
```

Where:

- **d** = Distance between devices
- **s** = Signal propagation speed

### Characteristics

- Depends on physical distance.
- Depends on transmission medium.
- Independent of packet size.

---

## 3. Protocol Efficiency

Efficiency represents the proportion of useful transmission time compared to the total communication cycle.

For the Stop-and-Wait protocol:

```text
Total Cycle Time = Tt + 2Tp
```

Ignoring acknowledgment transmission time,

```text
Efficiency = Tt / (Tt + 2Tp)
```

If

```text
a = Tp / Tt
```

then,

```text
Efficiency = 1 / (1 + 2a)
```

Higher efficiency indicates better utilization of the communication channel.

---

## 4. Effective Bandwidth (Throughput)

Effective Bandwidth represents the actual number of useful bits transmitted successfully per second.

### Formula

```text
Throughput = Efficiency × Bandwidth
```

or

```text
Throughput = (1 / (1 + 2a)) × B
```

Where:

- **B** = Channel Bandwidth

---

## 5. Link Capacity

Link Capacity is the maximum amount of data that can exist within a communication link at any given instant.

### Formula

```text
Capacity = Bandwidth × Propagation Delay
```

For a full-duplex communication channel,

```text
Capacity = 2 × Bandwidth × Propagation Delay
```

# Concept of Pipelining

In Stop-and-Wait ARQ, the sender remains idle while waiting for acknowledgments. This wastes valuable communication time.

Sliding Window Protocol introduces **pipelining**, allowing multiple packets to be transmitted consecutively before acknowledgments arrive.

As a result:

- The communication channel remains active.
- Multiple packets travel simultaneously.
- Overall throughput increases significantly.

# Maximum Packets in One Communication Cycle

The communication cycle is:

```text
Cycle Time = Tt + 2Tp
```

Using

```text
a = Tp / Tt
```

the maximum number of packets that can remain in transit during one communication cycle is

```text
Maximum Packets = 1 + 2a
```

This value determines the ideal sender window size for maximum channel utilization.

# Example

Suppose:

- Transmission Delay = **1 ms**
- Propagation Delay = **2 ms**

Then,

```text
a = 2 / 1 = 2
```

Maximum packets that may remain in transit:

```text
1 + 2a

= 1 + (2 × 2)

= 5 packets
```

Instead of sending only one packet and waiting, the sender can continuously transmit several packets, improving communication efficiency.

# Sender Window Size

The sender maintains a window containing packets that have been transmitted but are not yet acknowledged.

For maximum utilization,

```text
Window Size = 1 + 2a
```

Each packet inside the sender window receives a unique sequence number.

# Minimum Number of Sequence Bits

If the sender window size is **Ws**, then the minimum number of bits required for sequence numbering is

```text
Bits = ⌈log₂(Ws)⌉
```

If the protocol header allocates **N** bits for sequence numbers, the maximum available sequence numbers become

```text
2ᴺ
```

Therefore,

```text
Window Size = min(1 + 2a, 2ᴺ)
```

and

```text
Required Bits = ⌈log₂(Window Size)⌉
```

# Types of Sliding Window Protocol

Sliding Window Protocol is mainly implemented using two Automatic Repeat Request (ARQ) protocols.

## 1. Go-Back-N ARQ

Go-Back-N allows the sender to transmit multiple frames continuously.

### Characteristics

- Multiple outstanding frames are allowed.
- Receiver accepts only the expected frame.
- Uses cumulative acknowledgments.
- Lost frames cause retransmission of the lost frame and all following frames.

### Advantages

- High throughput.
- Simple receiver implementation.
- Efficient under low error conditions.

### Limitations

- Retransmits correctly received frames.
- Wastes bandwidth when errors occur frequently.

---

## 2. Selective Repeat ARQ

Selective Repeat improves communication by retransmitting only the frames that are actually lost or corrupted.

### Characteristics

- Receiver stores out-of-order frames.
- Individual acknowledgments are used.
- Only erroneous frames are retransmitted.

### Advantages

- Better bandwidth utilization.
- Fewer retransmissions.
- Higher performance on unreliable channels.

### Limitations

- More complex implementation.
- Requires additional memory for buffering frames.

# Advantages of Sliding Window Protocol

- Better utilization of available bandwidth.
- Increased throughput.
- Supports pipelined transmission.
- Improves communication efficiency.
- Suitable for long-distance networks.
- Reliable data transfer through acknowledgments and retransmissions.

# Limitations of Sliding Window Protocol

- More complex than Stop-and-Wait ARQ.
- Requires sequence number management.
- Sender and receiver windows must remain synchronized.
- Large windows increase implementation complexity.

# Comparison of Stop-and-Wait and Sliding Window

| Feature | Stop-and-Wait | Sliding Window |
| --- | --- | --- |
| Outstanding Packets | One | Multiple |
| Channel Utilization | Low | High |
| Throughput | Low | High |
| Communication Speed | Slower | Faster |
| Suitable For | Small Networks | High-Speed Networks |
| Complexity | Simple | Moderate to High |

# Applications

Sliding Window Protocol is commonly used in:

- TCP (Transmission Control Protocol)
- Reliable Data Link Layer protocols
- High-speed Local Area Networks
- Wide Area Networks
- Satellite communication systems
- Wireless communication networks

# Summary

The Sliding Window Protocol is an efficient communication mechanism that allows multiple packets to remain in transit simultaneously, significantly improving network throughput and bandwidth utilization. By introducing pipelining, sender and receiver windows, acknowledgments, and sequence numbers, it overcomes the limitations of Stop-and-Wait ARQ. Modern networking protocols such as **Go-Back-N ARQ**, **Selective Repeat ARQ**, and **TCP** rely on Sliding Window concepts to provide reliable, efficient, and high-speed data transmission across computer networks.




