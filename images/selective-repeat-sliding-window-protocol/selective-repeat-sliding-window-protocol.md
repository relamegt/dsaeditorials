# Selective Repeat Sliding Window Protocol

## Introduction

The **Selective Repeat Sliding Window Protocol (SRP)** is an advanced **Automatic Repeat reQuest (ARQ)** protocol used for reliable data transmission in computer networks. Unlike Go-Back-N ARQ, where multiple frames may be retransmitted after an error, Selective Repeat retransmits **only the frames that are lost or corrupted**.

This selective retransmission minimizes unnecessary network traffic, improves bandwidth utilization, and delivers better performance over communication channels that experience transmission errors.

### Key Features

- Retransmits only missing or damaged frames.
- Sender and receiver maintain windows of equal size.
- Receiver accepts and stores out-of-order frames.
- Uses acknowledgments and optional negative acknowledgments (NAKs).
- Provides higher efficiency than Go-Back-N on unreliable communication links.
- Reduces unnecessary retransmissions.

# Characteristics of Selective Repeat Protocol

Selective Repeat uses sender and receiver windows to manage multiple outstanding frames while maintaining reliable communication.

## Sender Window

The sender is allowed to transmit multiple frames without waiting for acknowledgments.

### Characteristics

- Sender window size is **N**.
- Multiple frames can remain in transit.
- Every transmitted frame has an independent timer.
- Only unacknowledged frames are retransmitted.

---

## Receiver Window

Unlike Go-Back-N, the receiver can temporarily store frames that arrive out of sequence.

### Characteristics

- Receiver window size equals sender window size.
- Out-of-order frames are accepted.
- Correct frames are buffered.
- Buffered frames are delivered in proper order after missing frames arrive.

# Working of Selective Repeat Protocol

The communication process follows these steps:

1. Sender transmits multiple frames within its current window.
2. Receiver accepts every correctly received frame.
3. If a frame is missing, the receiver stores subsequent frames instead of discarding them.
4. Receiver acknowledges each correctly received frame individually.
5. Sender retransmits only the missing or damaged frame after receiving a timeout or a Negative Acknowledgment (NAK).
6. Once the missing frame arrives, the receiver rearranges buffered frames into the correct sequence and forwards them to the upper layer.

This approach avoids retransmitting frames that have already been received successfully.

# Retransmission Mechanism

Selective Repeat retransmits only frames that require recovery.

## Timeout

If an acknowledgment is not received within the timeout interval, only that specific frame is retransmitted.

## Negative Acknowledgment (NAK)

Some implementations allow the receiver to send a **Negative Acknowledgment (NAK)** whenever a frame is missing or corrupted.

The sender immediately retransmits only the requested frame without waiting for the timeout period.

# Efficiency of Selective Repeat Protocol

Ignoring processing delay, queueing delay, and acknowledgment transmission delay, protocol efficiency is

```formula
Efficiency = N / (1 + 2a)
```

Where:

- **N** = Window Size
- **a = Tp / Tt**
- **Tp** = Propagation Delay
- **Tt** = Transmission Delay

---

Considering additional delays,

```formula
Efficiency =
Tt /
(Tt + 2Tp + Tq + Tpro + Tack)
```

Where:

- **Tt** = Transmission Delay
- **Tp** = Propagation Delay
- **Tq** = Queueing Delay
- **Tpro** = Processing Delay
- **Tack** = ACK Transmission Delay

Because only erroneous frames are retransmitted, Selective Repeat generally provides better practical bandwidth utilization than Go-Back-N on unreliable communication channels.

# Importance of Window Size

The sender and receiver windows must satisfy an important condition to avoid ambiguity caused by sequence number reuse.

If the sequence number field contains **m bits**, then

```formula
Window Size ≤ 2^(m-1)
```

This restriction ensures that old retransmitted frames are never mistaken for newly transmitted frames after sequence numbers wrap around.

Using a larger window than this limit may result in duplicate frames being accepted incorrectly.

# Buffers Required

Selective Repeat requires buffering at both communication endpoints.

## Sender Buffer

The sender stores every transmitted frame until its acknowledgment is received.

Required Buffers:

```formula
N Buffers
```

---

## Receiver Buffer

The receiver stores out-of-order frames until missing frames are received.

Required Buffers:

```formula
N Buffers
```

Therefore,

```formula
Total Buffers Required = 2N
```

# Sequence Numbers

Each transmitted frame is assigned a unique sequence number.

The total sequence number space should be large enough to distinguish between new frames and previously transmitted frames.

For Selective Repeat,

```formula
Total Sequence Numbers = 2N
```

This prevents confusion when sequence numbers are reused.

# Advantages of Selective Repeat

- Retransmits only lost or corrupted frames.
- Improves bandwidth utilization.
- Supports higher throughput on unreliable networks.
- Receiver stores correctly received out-of-order frames.
- Reduces unnecessary network traffic.
- Better performance than Go-Back-N when transmission errors are frequent.

# Limitations of Selective Repeat

- More complex implementation.
- Requires buffering at both sender and receiver.
- Needs independent timers for every outstanding frame.
- Sequence number management is more complicated.
- Higher memory requirements.

# Selective Repeat vs Go-Back-N

| Feature | Selective Repeat | Go-Back-N |
| --- | --- | --- |
| Receiver Window Size | N | 1 |
| Out-of-Order Frames | Accepted and Buffered | Discarded |
| Retransmission | Only Lost Frames | Lost Frame and All Following Frames |
| Acknowledgment | Individual ACKs | Cumulative ACK |
| Buffer Requirement | Sender and Receiver | Mainly Sender |
| Bandwidth Utilization | Higher | Lower during errors |
| Complexity | Higher | Lower |

# Applications

Selective Repeat Protocol is commonly used in:

- High-speed computer networks.
- Wireless communication systems.
- Satellite communication.
- Error-prone communication channels.
- Reliable data transmission systems.

# Summary

Selective Repeat Sliding Window Protocol is a reliable ARQ technique that improves communication efficiency by retransmitting **only the frames that are actually lost or corrupted**. Unlike Go-Back-N, the receiver buffers out-of-order frames and acknowledges each frame individually, resulting in fewer unnecessary retransmissions and better bandwidth utilization. Although the protocol requires additional memory, buffering, and implementation complexity, it provides significantly better performance on unreliable networks where transmission errors occur frequently.




