# Dynamic Host Configuration Protocol (DHCP)

## Introduction

The **Dynamic Host Configuration Protocol (DHCP)** is an Application Layer protocol that automatically assigns IP addresses and other network configuration parameters to devices connected to a network. It eliminates manual configuration, simplifies network administration, and ensures seamless connectivity.

## Key Features

- Automatically assigns unique IP addresses.
- Provides subnet mask information.
- Configures the default gateway.
- Supplies DNS server addresses.
- Reduces manual network configuration.
- Prevents IP address conflicts.

# Components of DHCP

## 1. DHCP Server

The DHCP Server manages IP address allocation and network configuration.

### Features

- Maintains the IP address pool.
- Assigns IP addresses to clients.
- Stores lease information.
- Provides network configuration parameters.

---

## 2. DHCP Relay

A DHCP Relay forwards DHCP messages between different subnets.

### Features

- Connects clients and servers across networks.
- Forwards DHCP requests and replies.
- Eliminates the need for a DHCP server in every subnet.

---

## 3. DHCP Client

A DHCP Client requests configuration from the DHCP server.

### Features

- Requests an IP address automatically.
- Receives network configuration.
- Renews lease periodically.

---

## 4. IP Address Pool

A collection of available IP addresses.

### Features

- Contains assignable IP addresses.
- May include exclusions and reservations.
- Allocates addresses dynamically.

---

## 5. Lease

A Lease defines how long a client can use an assigned IP address.

### Features

- Temporary assignment.
- Renewable before expiration.
- Returned after release.

---

## 6. DHCP Options

Additional configuration values supplied by the DHCP server.

### Examples

- DNS Servers
- Domain Name
- NTP Servers
- Boot Server
- Lease Time

---

## 7. Default Gateway

The router address used to communicate outside the local network.

### Features

- Enables internet access.
- Allows communication with other networks.

---

## 8. DNS Server

Provides domain name resolution.

### Features

- Converts domain names into IP addresses.
- Assigned automatically through DHCP.

---

## 9. DHCP Renewal

Lease renewal process.

### Features

- Extends lease duration.
- Prevents address expiration.
- Happens automatically.

---

## 10. DHCP Failover

Provides backup DHCP services.

### Features

- Uses two DHCP servers.
- Prevents service interruption.
- Improves availability.

---

## 11. Dynamic Updates

Automatically updates DNS records.

### Features

- Updates A and PTR records.
- Keeps DNS synchronized.
- Reduces manual administration.

---

## 12. Audit Logging

Maintains DHCP activity logs.

### Features

- Records lease events.
- Helps troubleshooting.
- Supports auditing.

# DHCP Packet Format

The DHCP packet contains several fields required for communication.

## Fields

- Hardware Length
- Hop Count
- Transaction ID
- Seconds Elapsed
- Flags
- Client IP Address
- Your IP Address
- Server IP Address
- Gateway IP Address
- Client Hardware Address
- Server Name
- Boot Filename
- Options

# Working of DHCP (DORA Process)

DHCP follows the **DORA** process.

## 1. DHCP Discover

The client searches for available DHCP servers.

### Features

- Broadcast message.
- Sent when the device starts.
- Requests network configuration.

---

## 2. DHCP Offer

The server offers an available IP address.

### Features

- Contains offered IP address.
- Includes subnet mask.
- Includes gateway.
- Includes DNS server.
- Includes lease time.

---

## 3. DHCP Request

The client accepts one server's offer.

### Features

- Requests the offered IP.
- Identifies the selected server.
- Rejects other offers.

---

## 4. DHCP ACK

The server confirms the assignment.

### Features

- Officially assigns the IP.
- Sends final configuration.
- Client starts communication.

---

## 5. DHCP NAK

The server rejects the client's request.

### Features

- Invalid requested IP.
- Address already allocated.
- Client moved to another network.
- Client restarts DHCP process.

---

## 6. DHCP Decline

Sent when the client detects an IP conflict.

### Features

- Reports duplicate IP.
- Server marks the address unavailable.
- Another address is assigned later.

---

## 7. DHCP Release

Client returns its assigned IP address.

### Features

- Frees the address.
- Makes it available for reuse.
- Sent during shutdown or disconnect.

---

## 8. DHCP Inform

Used when the client already has a static IP.

### Features

- Requests additional configuration.
- Receives DNS and other settings.
- Does not request a new IP address.

# DHCP Message Flow

```Code
Client
   │
   │ DHCP Discover
   ▼
DHCP Server
   │
   │ DHCP Offer
   ▼
Client
   │
   │ DHCP Request
   ▼
DHCP Server
   │
   │ DHCP ACK
   ▼
Client receives IP configuration
```

# Security Concerns

## DHCP Starvation Attack

- Floods DHCP requests.
- Exhausts available IP addresses.
- Prevents legitimate users from obtaining addresses.

---

## Rogue DHCP Server

- Fake DHCP server.
- Provides incorrect configuration.
- Redirects user traffic.

---

## Man-in-the-Middle Attack

- Supplies malicious gateway.
- Intercepts network traffic.
- Alters transmitted data.

---

## DNS Misuse

- Assigns malicious DNS servers.
- Redirects users to fake websites.
- Enables phishing attacks.

# Protection Against DHCP Attacks

- Enable DHCP Snooping.
- Configure trusted switch ports.
- Use Port Security.
- Apply rate limiting.
- Monitor DHCP logs.
- Filter unauthorized MAC addresses.

# Advantages of DHCP

- Automatic IP assignment.
- Eliminates manual configuration.
- Prevents duplicate IP addresses.
- Simplifies network management.
- Supports large networks.
- Saves administrative effort.

# Limitations of DHCP

- Depends on DHCP server availability.
- Vulnerable to rogue DHCP attacks.
- Lease expiration may temporarily interrupt connectivity.
- Requires additional security mechanisms.

# Summary

The **Dynamic Host Configuration Protocol (DHCP)** automatically assigns IP addresses and network configuration settings using the **DORA (Discover, Offer, Request, Acknowledge)** process. It simplifies network administration, prevents configuration errors, and supports efficient management of modern computer networks while requiring proper security measures to defend against DHCP-based attacks.




