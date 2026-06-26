# Stop-and-Wait ARQ

## Introduction

**Stop-and-Wait ARQ (Automatic Repeat reQuest)** is a reliable error-control protocol used at the **Data Link Layer** to ensure that data frames are delivered correctly between two communicating devices. In this protocol, the sender transmits only one frame at a time and waits for an acknowledgment (ACK) from the receiver before sending the next frame.

If the sender does not receive the acknowledgment within a specified timeout period, it assumes that the frame or acknowledgment was lost and retransmits the same frame. This mechanism provides reliable communication even when transmission errors occur.

### Key Features

- Sends only one frame at a time.
- Waits for an acknowledgment before transmitting the next frame.
- Uses timeout and retransmission for reliability.
- Employs one-bit sequence numbers (0 and 1).
- Provides both error control and flow control.
- Window size is always **1**, making it a special case of the Sliding Window Protocol.

# Important Terms

Before understanding the protocol, it is useful to know a few common networking terms.

## Propagation Delay

Propagation delay is the time required for a signal to travel from the sender to the receiver through the communication medium.

### Formula

```text
Propagation Delay = Distance / Signal Propagation Speed
```

### Factors Affecting Propagation Delay

- Distance between devices.
- Type of transmission medium.
- Signal propagation speed.

---

## Round Trip Time (RTT)

Round Trip Time (RTT) is the total time required for a data frame to reach the receiver and for its acknowledgment to return to the sender.

```text
RTT = Data Transmission Time + ACK Transmission Time
```

RTT is commonly used to determine an appropriate timeout value.

---

## Timeout

Timeout is the maximum period the sender waits for an acknowledgment after transmitting a frame.

If the timer expires before receiving an ACK, the sender retransmits the same frame.

```text
Timeout = Estimated RTT + Safety Margin
```

# Basic Stop-and-Wait Communication

The simplest form of Stop-and-Wait communication allows only one packet to be transmitted at a time.

## Sender Rules

- Send one frame.
- Start the timeout timer.
- Wait until an acknowledgment is received.
- Send the next frame only after receiving the ACK.

## Receiver Rules

- Receive the incoming frame.
- Verify whether the frame is valid.
- Deliver the frame to the upper layer.
- Send an acknowledgment to the sender.

# Problems in Simple Stop-and-Wait

Although simple Stop-and-Wait is easy to implement, several communication problems may occur.

## 1. Lost Data Frame

Sometimes a transmitted frame never reaches the receiver because of transmission errors or network failures.

### What Happens?

- Sender transmits a frame.
- Frame is lost.
- Receiver does not receive the frame.
- No acknowledgment is generated.
- Sender waits until timeout expires.
- Sender retransmits the same frame.

---

## 2. Lost Acknowledgment

In some situations, the receiver successfully receives the frame and sends an acknowledgment, but the ACK itself is lost.

### What Happens?

- Receiver successfully processes the frame.
- ACK is transmitted.
- ACK is lost during transmission.
- Sender assumes the frame was not delivered.
- Sender retransmits the same frame.

Without additional mechanisms, duplicate data may be delivered.

---

## 3. Delayed Frame or Delayed ACK

Network congestion may delay either the transmitted frame or its acknowledgment.

### What Happens?

- Sender transmits a frame.
- ACK arrives after the timeout period.
- Sender retransmits the frame.
- Receiver may receive duplicate frames.

To distinguish between original and duplicate frames, sequence numbers are required.

# Stop-and-Wait ARQ

Stop-and-Wait ARQ improves the basic Stop-and-Wait protocol by introducing **timeouts**, **sequence numbers**, and **acknowledgments**.

These mechanisms allow the sender and receiver to detect lost frames, duplicate frames, and delayed acknowledgments while maintaining reliable communication.

# Components of Stop-and-Wait ARQ

## 1. Timeout Mechanism

Whenever a frame is transmitted, the sender starts a timer.

### Working

- Timer starts immediately after transmission.
- ACK received before timeout → Send next frame.
- Timeout expires → Retransmit current frame.

This prevents communication from stopping permanently when a frame or ACK is lost.

---

## 2. Sequence Numbers for Data Frames

Every transmitted frame is assigned a sequence number.

Stop-and-Wait ARQ uses only **one-bit sequence numbers**, so only two sequence values are possible:

- Frame 0
- Frame 1

Sequence numbers allow the receiver to distinguish between new frames and duplicate retransmissions.

---

## 3. Sequence Numbers in ACKs

Acknowledgments also contain sequence numbers.

Instead of confirming the current frame, the ACK informs the sender about the **next expected frame**.

For example:

- ACK 1 indicates that Frame 0 has been received successfully and Frame 1 is expected next.
- ACK 0 indicates that Frame 1 has been received successfully and Frame 0 is expected next.

# Working of Stop-and-Wait ARQ

The communication process follows these steps:

1. Sender transmits **Frame 0**.
2. Sender starts the timeout timer.
3. Receiver receives Frame 0 successfully.
4. Receiver sends **ACK 1**.
5. Sender receives ACK 1.
6. Sender transmits **Frame 1**.
7. Receiver sends **ACK 0** after receiving Frame 1.
8. The communication continues by alternating sequence numbers 0 and 1.

Because only one frame is allowed in transit at any time, communication remains simple and reliable.

# Advantages of Stop-and-Wait ARQ

- Simple protocol implementation.
- Reliable data delivery.
- Detects lost frames.
- Handles lost acknowledgments.
- Prevents duplicate frame delivery using sequence numbers.
- Provides both flow control and error control.

# Limitations of Stop-and-Wait ARQ

- Very low channel utilization.
- Sender remains idle while waiting for acknowledgments.
- Poor performance over long-distance communication links.
- Low throughput when bandwidth-delay product is high.
- Not suitable for high-speed communication networks.

# Applications

Stop-and-Wait ARQ is commonly used in:

- Small Local Area Networks (LANs).
- Low-speed communication systems.
- Educational demonstrations of reliable communication.
- Networks where propagation delay is very small.

# Comparison with Sliding Window Protocol

| Feature | Stop-and-Wait ARQ | Sliding Window Protocol |
| --- | --- | --- |
| Window Size | 1 | Greater than 1 |
| Outstanding Frames | One | Multiple |
| Throughput | Low | High |
| Channel Utilization | Low | Better |
| Complexity | Simple | More Complex |
| Suitable For | Small Networks | High-Speed Networks |

# Summary

Stop-and-Wait ARQ is a reliable communication protocol that ensures error-free transmission by sending one frame at a time and waiting for an acknowledgment before continuing. It uses **timeouts**, **retransmissions**, and **one-bit sequence numbers** to detect lost or duplicate frames and maintain reliable communication. Although it is easy to implement, its performance decreases significantly on high-speed or long-distance networks because only one frame can remain in transit at any given time. More advanced protocols such as **Go-Back-N ARQ** and **Selective Repeat ARQ** overcome these limitations by allowing multiple outstanding frames.




