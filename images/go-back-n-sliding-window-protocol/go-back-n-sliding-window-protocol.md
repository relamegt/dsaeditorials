# Go-Back-N Sliding Window Protocol

## Introduction

**Go-Back-N (GBN)** is a reliable **Sliding Window Automatic Repeat reQuest (ARQ)** protocol used at the **Data Link Layer** to improve data transmission efficiency. Unlike Stop-and-Wait ARQ, where the sender waits after transmitting every frame, Go-Back-N allows multiple frames to be transmitted continuously before acknowledgments are received.

If a frame is lost or damaged during transmission, the receiver discards that frame and every frame received after it. The sender then retransmits the lost frame along with all subsequent frames in the current transmission window.

### Key Features

- Allows transmission of multiple frames without waiting for individual acknowledgments.
- Uses a sliding window mechanism for efficient communication.
- Employs cumulative acknowledgments.
- Receiver accepts only the next expected frame.
- Improves throughput compared to Stop-and-Wait ARQ.
- Suitable for communication channels with moderate propagation delays.

# Characteristics of Go-Back-N Protocol

The Go-Back-N protocol relies on sender and receiver windows to control communication.

## Sender Window Size (Ws)

The sender is allowed to transmit multiple frames before waiting for acknowledgments.

### Characteristics

- Sender window size is **N**.
- Up to **N** frames may remain unacknowledged.
- Multiple frames can be transmitted continuously.
- Window advances whenever acknowledgments are received.

If:

```text
N = 1
```

the protocol behaves exactly like **Stop-and-Wait ARQ**.

# Efficiency of Go-Back-N Protocol

When processing delay, queueing delay, and acknowledgment transmission delay are ignored, protocol efficiency is:

```text
Efficiency = N / (1 + 2a)
```

Where:

- **N** = Sender Window Size
- **a = Tp / Tt**
- **Tp** = Propagation Delay
- **Tt** = Transmission Delay

---

When additional delays are considered:

```text
Efficiency =
(N × Tt) /
(Tt + 2Tp + Pr + Pq + Tack)
```

Where:

- **Tt** = Transmission Delay
- **Tp** = Propagation Delay
- **Pr** = Processing Delay
- **Pq** = Queueing Delay
- **Tack** = ACK Transmission Delay

---

If channel bandwidth is represented by **B**, then:

```text
Throughput = Efficiency × B
```

For the ideal case:

```text
Throughput =
(N / (1 + 2a)) × B
```

# Receiver Window Size (WR)

Unlike the sender, the receiver always maintains a window size of **1**.

### Characteristics

- Receiver accepts only the expected frame.
- Out-of-order frames are discarded.
- Duplicate frames are ignored.
- No buffering of unexpected frames.

# Acknowledgments in Go-Back-N

Acknowledgments notify the sender about successfully received frames.

## Cumulative Acknowledgment

A cumulative acknowledgment confirms that every frame up to a particular sequence number has been received successfully.

### Advantages

- Reduces acknowledgment traffic.
- Improves communication efficiency.
- Simplifies acknowledgment handling.

### Limitation

If one acknowledgment is lost, multiple frames may need retransmission.

---

## Independent Acknowledgment

Each received frame is acknowledged separately.

### Characteristics

- One acknowledgment for every frame.
- Used by Selective Repeat ARQ.
- Eliminates unnecessary retransmissions.
- Produces higher acknowledgment overhead.

# Working of Go-Back-N Protocol

## Sender Operation

The sender performs the following steps:

1. Maintains a sliding window containing **N** frames.
2. Continuously transmits frames while the window is not full.
3. Starts timers for transmitted frames.
4. Slides the window forward whenever cumulative acknowledgments arrive.
5. Retransmits all unacknowledged frames after a timeout.

---

## Receiver Operation

The receiver follows these steps:

1. Waits for the expected frame.
2. Accepts only correctly received frames in sequence.
3. Sends a cumulative acknowledgment.
4. Discards all out-of-order frames.
5. Repeats the acknowledgment for the last correctly received frame whenever necessary.

# Relationship Between Window Size and Sequence Numbers

The sender window, receiver window, and available sequence numbers must satisfy the following condition:

```text
Ws + Wr ≤ ASN
```

Where:

- **Ws** = Sender Window Size
- **Wr** = Receiver Window Size
- **ASN** = Available Sequence Numbers

Since:

```text
Wr = 1
```

the condition becomes:

```text
Ws + 1 ≤ ASN
```

If the sender window size is **N**, then:

```text
Minimum Sequence Numbers = N + 1
```

The number of bits required to represent sequence numbers is:

```text
Bits Required = ⌈log₂(N + 1)⌉
```

The additional sequence number prevents ambiguity when old sequence numbers are reused.

# Example of Go-Back-N Protocol

Suppose the sender window size is **4**.

The sender transmits:

```text
Frame 0
Frame 1
Frame 2
Frame 3
```

Assume **Frame 2** is lost during transmission.

The receiver:

- Accepts Frame 0.
- Accepts Frame 1.
- Expects Frame 2.
- Discards Frame 3 because Frame 2 is missing.
- Sends the acknowledgment for the last correctly received frame.

After the timeout expires, the sender retransmits:

```text
Frame 2
Frame 3
```

This process ensures reliable communication but may result in retransmitting correctly received frames.

# Advantages of Go-Back-N

- Higher throughput than Stop-and-Wait ARQ.
- Supports pipelined transmission.
- Simple receiver implementation.
- Uses cumulative acknowledgments.
- Suitable for networks with low error rates.

# Limitations of Go-Back-N

- Retransmits multiple frames even if only one frame is lost.
- Wastes bandwidth during retransmissions.
- Receiver cannot store out-of-order frames.
- Performance decreases on highly unreliable communication channels.

# Go-Back-N vs Stop-and-Wait ARQ

| Feature | Stop-and-Wait ARQ | Go-Back-N ARQ |
| --- | --- | --- |
| Frames in Transit | One | Multiple |
| Sender Window Size | 1 | N |
| Receiver Window Size | 1 | 1 |
| Throughput | Low | High |
| Acknowledgment Type | Individual | Cumulative |
| Retransmission | One Frame | Lost Frame and All Following Frames |
| Channel Utilization | Low | Better |

# Applications

Go-Back-N is commonly used in:

- Reliable Data Link Layer communication.
- Wireless communication systems.
- Satellite communication.
- Medium-speed computer networks.
- Protocols requiring pipelined transmission.

# Summary

Go-Back-N Sliding Window Protocol improves communication efficiency by allowing multiple frames to be transmitted before acknowledgments are received. It uses a sender window of size **N**, a receiver window of size **1**, and cumulative acknowledgments to achieve reliable communication. Whenever a frame is lost, the sender retransmits the missing frame along with all subsequent unacknowledged frames. Although this approach provides better throughput than Stop-and-Wait ARQ, unnecessary retransmissions can reduce efficiency in networks with high error rates.




