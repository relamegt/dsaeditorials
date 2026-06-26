# Transport Layer in OSI Model

## Introduction

The **Transport Layer** is the **fourth layer (Layer 4)** of the OSI reference model. It is responsible for providing reliable, efficient, and end-to-end communication between applications running on different hosts. Unlike the Network Layer, which delivers packets from one host to another, the Transport Layer ensures that data reaches the correct application process in the proper order and without errors.

The Transport Layer provides services such as segmentation, error recovery, flow control, sequencing, multiplexing, and connection management. It uses protocols like **Transmission Control Protocol (TCP)**, **User Datagram Protocol (UDP)**, and **Stream Control Transmission Protocol (SCTP)** to meet different communication requirements.

### Key Features

- Operates at Layer 4 of the OSI model.
- Provides process-to-process communication.
- Uses port numbers to identify applications.
- Ensures reliable and ordered data delivery.
- Performs flow control and error recovery.
- Supports multiple transport protocols.

# Functions of the Transport Layer

The Transport Layer performs several important functions to ensure reliable communication between applications.

## 1. End-to-End Data Delivery

Provides communication between applications running on different hosts regardless of the underlying network.

---

## 2. Reliable Data Transfer

Ensures that transmitted data reaches the destination completely and in the correct order.

---

## 3. Error Detection and Recovery

Detects transmission errors and retransmits lost or corrupted segments.

---

## 4. Flow Control

Regulates the transmission rate so that the receiver is not overwhelmed with incoming data.

---

## 5. Multiplexing and Demultiplexing

Uses port numbers to allow multiple applications to share the same network connection.

# Working of the Transport Layer

The Transport Layer establishes logical communication between applications on different devices.

### Working Steps

1. Receives data from the Application Layer.
2. Divides the data into smaller segments or datagrams.
3. Adds Transport Layer headers.
4. Assigns source and destination port numbers.
5. Performs sequencing and error detection.
6. Passes the segments to the Network Layer.
7. At the receiver, removes Transport Layer headers.
8. Reassembles the original data.
9. Delivers the data to the appropriate application.

### Characteristics

- Implemented only in end devices.
- Uses port numbers for process identification.
- Supports multiplexing and demultiplexing.
- Coordinates with the Network Layer for packet delivery.
- Performs segmentation and reassembly.
- Supports reliable and unreliable communication.

# TCP Three-Way Handshake

The **Three-Way Handshake** is the connection establishment process used by TCP before data transmission begins.

## Step 1: SYN

The client sends a TCP segment with the SYN flag set to request a connection.

### Purpose

- Initiates communication.
- Sends the client's Initial Sequence Number (ISN).

---

## Step 2: SYN-ACK

The server replies with both SYN and ACK flags set.

### Purpose

- Acknowledges the client's request.
- Sends the server's Initial Sequence Number.
- Requests synchronization.

---

## Step 3: ACK

The client acknowledges the server's response.

### Purpose

- Confirms synchronization.
- Completes connection establishment.
- Both devices enter the **ESTABLISHED** state.

# Why Three Steps Are Required

A third acknowledgment ensures that both the client and server know the connection has been successfully established before data transfer begins.

Without the final acknowledgment, either side could incorrectly assume that communication is ready.

# Transport Layer Protocols

Several protocols operate at the Transport Layer.

- TCP
- UDP
- SCTP

# 1. Transmission Control Protocol (TCP)

TCP is a **connection-oriented** transport protocol that provides reliable communication.

### Characteristics

- Reliable communication.
- Connection-oriented.
- Ordered data delivery.
- Error recovery through retransmission.
- Flow control.
- Congestion control.

### Advantages

- Reliable transmission.
- No data loss.
- Correct packet ordering.
- Error detection and correction.

### Limitations

- Higher overhead.
- Slower than UDP.
- Larger header size.

# 2. User Datagram Protocol (UDP)

UDP is a **connectionless** transport protocol designed for fast communication.

### Characteristics

- Connectionless communication.
- No acknowledgment.
- No retransmission.
- Low latency.
- Small header size.

### Advantages

- High speed.
- Low overhead.
- Suitable for real-time applications.
- Efficient bandwidth usage.

### Limitations

- No reliability.
- No packet ordering.
- No congestion control.
- Lost packets are not recovered.

# 3. Stream Control Transmission Protocol (SCTP)

SCTP combines several features of both TCP and UDP.

### Characteristics

- Reliable communication.
- Message-oriented transmission.
- Multi-stream communication.
- Multi-homing support.
- Error recovery.

### Advantages

- Higher reliability.
- Better fault tolerance.
- Supports multiple communication streams.
- Improved performance for signaling applications.

### Limitations

- More complex implementation.
- Limited deployment compared to TCP and UDP.
- Not universally supported.

# Difference Between TCP and UDP

| Feature | TCP | UDP |
| --- | --- | --- |
| Connection | Connection-Oriented | Connectionless |
| Reliability | Reliable | Unreliable |
| Packet Ordering | Guaranteed | Not Guaranteed |
| Error Recovery | Supported | Not Supported |
| Acknowledgment | Yes | No |
| Retransmission | Yes | No |
| Header Size | 20–60 Bytes | 8 Bytes |
| Speed | Slower | Faster |
| Flow Control | Available | Not Available |
| Congestion Control | Available | Not Available |
| Best Used For | File Transfer, Email, Web Browsing | Streaming, Gaming, VoIP, DNS |

# Advantages of the Transport Layer

- Provides end-to-end communication.
- Ensures reliable data delivery.
- Supports error detection and recovery.
- Maintains packet sequencing.
- Performs flow control.
- Enables process-to-process communication.
- Supports multiple simultaneous applications.

# Limitations of the Transport Layer

- Adds protocol overhead.
- Reliable protocols increase communication delay.
- Error recovery consumes additional bandwidth.
- Complex connection management.
- High processing requirements for reliable communication.

# Applications of the Transport Layer

- Web browsing.
- File transfer.
- Email communication.
- Video conferencing.
- Voice over IP (VoIP).
- Online gaming.
- Live streaming.
- Domain Name System (DNS).

# Summary

The **Transport Layer** is the fourth layer of the OSI model responsible for reliable, efficient, and process-to-process communication between applications on different hosts. It performs segmentation, sequencing, error recovery, flow control, multiplexing, and connection management. Protocols such as **TCP**, **UDP**, and **SCTP** provide different communication services depending on application requirements. While TCP offers reliable and ordered communication, UDP prioritizes speed and low overhead, making the Transport Layer a critical component of modern computer networks.




