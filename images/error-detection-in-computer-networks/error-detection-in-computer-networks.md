# Error Detection in Computer Networks

## Introduction

**Error Detection** is a technique used in computer networks to determine whether data has been altered during transmission. Noise, electromagnetic interference, signal attenuation, and other transmission problems can modify one or more bits of a data frame, resulting in corrupted information.

To detect such errors, the sender adds **redundant bits** to the original data before transmission. The receiver verifies these redundant bits after receiving the data. If the verification fails, the receiver concludes that the data has been corrupted and discards the frame or requests retransmission using an appropriate error control mechanism.

Error detection improves data integrity and ensures reliable communication between network devices.

### Key Features

- Detects errors introduced during transmission.
- Uses redundant bits for verification.
- Improves communication reliability.
- Maintains data integrity.
- Supports retransmission when errors are detected.
- Widely used in computer networks and communication protocols.

# Need for Error Detection

During data transmission, transmitted bits may change because of physical or environmental factors.

Error detection helps identify corrupted data before it is processed by the receiver.

### Benefits

- Detects transmission errors.
- Prevents corrupted data from being accepted.
- Improves communication reliability.
- Supports reliable data transfer.
- Maintains data accuracy.

# Types of Errors

Errors occurring during data transmission are generally classified into two categories.

- Single-Bit Error
- Burst Error

# 1. Single-Bit Error

A **Single-Bit Error** occurs when only one bit of the transmitted data changes during transmission.

### Example

Original Data

```text
10110110
```

Received Data

```text
10111110
```

Only one bit has changed, resulting in a single-bit error.

### Characteristics

- Only one bit is altered.
- Easy to detect.
- Less common in modern communication systems.
- Often caused by random electrical noise.

---

# 2. Burst Error

A **Burst Error** occurs when two or more consecutive bits are corrupted during transmission.

### Example

Original Data

```text
110010101011
```

Received Data

```text
110111001011
```

Multiple adjacent bits have changed.

### Characteristics

- Multiple consecutive bits are affected.
- More common than single-bit errors.
- Usually caused by transmission interference.
- Harder to detect than single-bit errors.

# Error Detection Methods

Several techniques are available to detect transmission errors.

- Simple Parity Check
- Two-Dimensional Parity Check
- Checksum
- Cyclic Redundancy Check (CRC)

# 1. Simple Parity Check

Simple Parity Check is the most basic error detection technique. A single **parity bit** is appended to every data unit before transmission.

The receiver recalculates the parity and compares it with the received parity bit.

If both values differ, an error is detected.

## Types of Parity

### Even Parity

The parity bit is selected so that the total number of **1s** becomes even.

### Odd Parity

The parity bit is selected so that the total number of **1s** becomes odd.

### Advantages

- Very simple implementation.
- Detects all single-bit errors.
- Requires only one additional parity bit.
- Fast error detection.

### Limitations

- Cannot detect all multiple-bit errors.
- Fails when an even number of bits change.
- Not suitable for noisy communication channels.

# 2. Two-Dimensional Parity Check

Two-Dimensional Parity Check extends the basic parity technique by calculating parity bits for both rows and columns of a data block.

At the receiver, row and column parity values are recalculated and compared with the received parity bits.

This method provides better error detection than Simple Parity Check.

### Advantages

- Detects all single-bit errors.
- Can identify the exact error position.
- Detects many multiple-bit errors.
- Better reliability than simple parity.

### Limitations

- Some multiple-bit error patterns remain undetected.
- Requires additional parity bits.
- Higher processing overhead.

# 3. Checksum

Checksum is a widely used software-based error detection technique.

The sender divides the data into fixed-size segments and computes a checksum using **1's complement arithmetic**.

The checksum is transmitted together with the original data.

The receiver performs the same calculation and verifies the checksum.

### Sender Operation

1. Divide data into equal-sized segments.
2. Add all segments using 1's complement arithmetic.
3. Compute the 1's complement of the sum.
4. Append the checksum to the transmitted data.

### Receiver Operation

1. Add all received segments including the checksum.
2. Verify the final result.

If the final result contains all **1s**, the data is accepted.

Otherwise, an error is detected.

### Advantages

- Detects many transmission errors.
- Better than parity checking.
- Easy software implementation.
- Used by TCP, UDP, and IP protocols.

### Limitations

- Does not correct errors.
- Some error combinations remain undetected.
- Less reliable than CRC.

# 4. Cyclic Redundancy Check (CRC)

**Cyclic Redundancy Check (CRC)** is one of the most reliable error detection techniques used in modern communication systems.

Instead of arithmetic addition, CRC uses **binary polynomial division**.

The sender appends CRC bits to the original message before transmission.

The receiver performs the same division using the identical generator polynomial.

If the remainder becomes zero, the frame is accepted.

Otherwise, the receiver detects an error.

### CRC Working

Step 1: Append **(k − 1)** zeros to the original data.

Step 2: Perform modulo-2 binary division using the generator polynomial.

Step 3: Obtain the remainder.

Step 4: Append the remainder to the original message to create the codeword.

### Important Points

```formula
CRC Bits = k - 1
```

```formula
Codeword Length = n + k - 1
```

Where:

- **n** = Length of the original data.
- **k** = Length of the generator polynomial.

### Advantages

- Detects single-bit errors.
- Detects multiple-bit errors.
- Highly effective against burst errors.
- Very reliable.
- Widely used in Ethernet, USB, HDLC, and storage devices.

### Limitations

- Performs only error detection.
- More computationally complex.
- Requires polynomial division.

# Comparison of Error Detection Techniques

| Technique | Detects Single-Bit Errors | Detects Burst Errors | Error Correction | Complexity |
| --- | --- | --- | --- | --- |
| Simple Parity Check | Yes | Limited | No | Very Low |
| Two-Dimensional Parity | Yes | Moderate | Single-Bit Only | Low |
| Checksum | Yes | Good | No | Medium |
| Cyclic Redundancy Check (CRC) | Yes | Excellent | No | High |

# Applications of Error Detection

Error detection techniques are widely used in modern communication systems.

- Computer networks.
- Ethernet communication.
- Wireless communication.
- USB communication.
- Hard disk storage.
- Satellite communication.
- Mobile networks.
- Data Link Layer protocols.
- Transport Layer protocols.

# Summary

Error Detection is an essential mechanism that ensures data integrity during communication by identifying corrupted data before it reaches the application layer. Techniques such as **Simple Parity Check**, **Two-Dimensional Parity Check**, **Checksum**, and **Cyclic Redundancy Check (CRC)** provide different levels of reliability and complexity. Among these methods, **CRC** offers the highest error detection capability and is widely used in modern networking protocols because of its ability to detect single-bit, multiple-bit, and burst errors with high accuracy.:::




