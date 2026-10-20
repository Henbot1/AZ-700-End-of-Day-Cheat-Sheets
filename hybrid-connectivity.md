# AZ-700 Study Notes - Azure Virtual WAN, VPN Gateway, and ExpressRoute

**Study Date:** End of Day Review

## Topics Covered

- Azure Virtual WAN (vWAN)
- Azure VPN Gateway
- Site-to-Site VPN
- Point-to-Site VPN
- ExpressRoute
- Virtual Hubs
- Hub-and-Spoke Architecture
- Transit Routing

---

# Quick Reference Cheat Sheet

| Service | Purpose | Uses Internet? |
|----------|----------|----------|
| VPN Gateway | Connect Azure to remote networks | ✅ Yes |
| Site-to-Site VPN | Office ↔ Azure | ✅ Yes |
| Point-to-Site VPN | User Laptop ↔ Azure | ✅ Yes |
| ExpressRoute | Private connectivity to Azure | ❌ No |
| Virtual WAN | Microsoft-managed networking hub | Depends on attachment |
| Virtual Hub | Managed routing hub inside vWAN | N/A |

---

# Traditional Hub-and-Spoke

## What It Looks Like

```text
Branch Office
      ↓
VPN Gateway
      ↓
Hub VNet
   ↙     ↘
Spoke1   Spoke2
```

## What You Manage

- VPN Gateway
- ExpressRoute Gateway
- VNet Peerings
- Route Tables
- Cross-region transit
- Gateway availability

## Benefits

✅ Full control

✅ Custom architecture

✅ Supports IPv6

## Drawbacks

❌ Operational overhead

❌ Complex at scale

❌ Must build routing yourself

---

# Azure Virtual WAN (vWAN)

## What It Is

A Microsoft-managed networking service that combines:

- Connectivity
- Routing
- Security

Into a managed hub architecture.

## Key Idea

With Virtual WAN:

```text
You attach resources.

Microsoft manages the hub.
```

---

## Architecture

```text
Virtual WAN
      ↓
Virtual Hub
      ↓
Attachments
      ↓
Routing
```

Attachments may include:

- VNets
- Branch offices
- VPN connections
- ExpressRoute circuits
- Remote users

---

# Why Virtual WAN Exists

Without vWAN:

```text
Spokes
    ↔
Hub
    ↔
VPN
    ↔
ExpressRoute
```

You manage everything.

With vWAN:

```text
Spokes
    ↓
Virtual Hub
    ↓
Microsoft-managed routing
```

---

# Virtual WAN Benefits

## Managed Hub Per Region

Microsoft creates and maintains:

- Hub infrastructure
- Routing
- Connectivity

---

## Transit Routing Included

Allows:

```text
Spoke A
    ↓
Virtual Hub
    ↓
Spoke B
```

Without manually configuring transit.

---

## Consolidated Connectivity

Single location for:

- Site-to-Site VPN
- Point-to-Site VPN
- ExpressRoute
- Branch offices

---

## Hub-to-Hub Connectivity

Microsoft automatically provides:

```text
Hub East US
      ↓
Hub West US
```

No need to design inter-region routing.

---

# When to Use Virtual WAN

Choose vWAN when:

✅ Many branch offices

✅ Many spokes

✅ Multiple regions

✅ Shared networking platform

✅ Simplified operations

### Exam Trigger

If the question says:

> 50 branch offices

> 30 spoke VNets

> Reduce management overhead

The answer is often:

✅ Azure Virtual WAN

---

# What Can Live Inside a Virtual Hub

## Supported

✅ VPN Gateway

✅ ExpressRoute Gateway

✅ Azure Firewall

✅ Route Tables

✅ SD-WAN Partner Appliances

---

## NOT Supported

❌ Virtual Machines

❌ Azure Bastion

❌ DNS Servers

❌ General Shared Services

These belong in spokes.

### Exam Tip

Virtual Hub is not a place to deploy workloads.

Think:

> Connectivity and Routing Only

---

# Virtual Hub Rules

## Put These In The Hub

```text
VPN Gateway
ExpressRoute Gateway
Azure Firewall
Route Tables
```

---

## Put These In A Spoke

```text
Virtual Machines
Azure Bastion
DNS Servers
Application Services
Management Tools
```

---

# Azure VPN Gateway

## What It Does

Provides encrypted connectivity between Azure and external networks.

---

# Site-to-Site VPN (S2S)

## Purpose

Connects entire locations together.

```text
Branch Office
      ↔
Azure VPN Gateway
```

### Characteristics

✅ IPsec/IKE

✅ Always-on tunnel

✅ Connects networks

✅ Requires VPN device

### Exam Trigger

> Connect company headquarters to Azure

Answer:

✅ Site-to-Site VPN

---

# Point-to-Site VPN (P2S)

## Purpose

Connects individual users.

```text
User Laptop
      ↔
Azure VPN Gateway
```

### Characteristics

✅ Remote workers

✅ Developer access

✅ Single device connection

✅ Can use Microsoft Entra ID authentication

### Exam Trigger

> Remote user access

Answer:

✅ Point-to-Site VPN

---

# VPN Gateway vs ExpressRoute

| Feature | VPN Gateway | ExpressRoute |
|----------|----------|----------|
| Uses Internet | Yes | No |
| Encrypted | Yes | Optional |
| Cost | Lower | Higher |
| Speed | Lower | Higher |
| SLA | Lower | Higher |
| Latency | Higher | Lower |

---

# ExpressRoute

## What It Is

Dedicated private connection between your network and Microsoft.

Traffic does NOT traverse the public Internet.

---

## Benefits

✅ Predictable latency

✅ Higher throughput

✅ Greater reliability

✅ Private connectivity

✅ Enterprise-grade connectivity

---

## Exam Trigger

The answer is usually ExpressRoute if requirements include:

- Private connection
- Regulatory compliance
- Consistent low latency
- High bandwidth
- Enterprise connectivity

---

# Common Exam Scenario

## Question Clue

"We cannot send traffic over the public Internet."

Answer:

✅ ExpressRoute

---

# ExpressRoute Fast Facts

## Uses A Dedicated Circuit

```text
Datacenter
      ↓
Connectivity Provider
      ↓
Microsoft Edge
      ↓
Azure
```

---

## Common Use Cases

✅ Large Enterprise

✅ Datacenter Migration

✅ Hybrid Cloud

✅ Compliance Requirements

✅ Financial Institutions

---

# Virtual WAN + ExpressRoute

A Virtual Hub may contain:

```text
ExpressRoute Gateway
```

This allows:

```text
On-Premises
      ↓
ExpressRoute
      ↓
Virtual Hub
      ↓
Spokes
```

---

# Service Selection Matrix

## Requirement → Service

### Connect Entire Office To Azure

✅ Site-to-Site VPN

---

### Connect Remote Worker To Azure

✅ Point-to-Site VPN

---

### Private Connectivity

✅ ExpressRoute

---

### Lowest Latency

✅ ExpressRoute

---

### Highest Reliability

✅ ExpressRoute

---

### Many Branch Offices

✅ Virtual WAN

---

### Reduce Networking Administration

✅ Virtual WAN

---

### Many Regions

✅ Virtual WAN

---

### Need Azure Firewall In Managed Hub

✅ Virtual WAN

---

# High-Value Exam Traps

## Trap #1

Requirement:

> Individual users need remote access.

Wrong Answer:

❌ Site-to-Site VPN

Correct Answer:

✅ Point-to-Site VPN

---

## Trap #2

Requirement:

> Entire branch office connectivity.

Wrong Answer:

❌ Point-to-Site VPN

Correct Answer:

✅ Site-to-Site VPN

---

## Trap #3

Requirement:

> Traffic must not traverse the Internet.

Wrong Answer:

❌ VPN Gateway

Correct Answer:

✅ ExpressRoute

---

## Trap #4

Requirement:

> Reduce hub-and-spoke management overhead.

Wrong Answer:

❌ Build another hub

Correct Answer:

✅ Virtual WAN

---

## Trap #5

Requirement:

> Deploy a VM in a Virtual Hub.

Correct Answer:

❌ Not Supported

Deploy it in a Spoke instead.

---

# Morning Review Quiz

## Question 1

A company wants private connectivity between its datacenter and Azure. Traffic must not traverse the public Internet.

A. Site-to-Site VPN

B. Point-to-Site VPN

C. ExpressRoute

D. Azure Front Door

---

## Question 2

A remote employee needs secure access to Azure resources from a laptop.

A. ExpressRoute

B. Point-to-Site VPN

C. Site-to-Site VPN

D. Virtual WAN

---

## Question 3

A company has 50 branch offices and 40 spoke VNets. Administrators want Microsoft to manage routing and connectivity.

A. Hub-and-Spoke VNet

B. Azure Route Server

C. Virtual WAN

D. Application Gateway

---

## Question 4

Which resource can be deployed inside a Virtual Hub?

A. DNS Server

B. Virtual Machine

C. ExpressRoute Gateway

D. Azure Bastion

---

## Question 5

Which VPN type connects an entire office network to Azure?

A. Point-to-Site

B. Site-to-Site

C. User VPN

D. Bastion

---

## Question 6

Which service automatically provides transit routing between spokes?

A. Application Gateway

B. Load Balancer

C. Virtual WAN

D. NAT Gateway

---

## Question 7

A company needs the lowest latency and highest reliability possible for hybrid connectivity.

A. Point-to-Site VPN

B. Site-to-Site VPN

C. ExpressRoute

D. Azure Bastion

---

## Question 8

Where should Azure Bastion be deployed when using Virtual WAN?

A. Virtual Hub

B. VPN Gateway

C. ExpressRoute Gateway

D. Spoke VNet

---

## Question 9

Which Virtual WAN component is Microsoft-managed?

A. VPN Appliance

B. Virtual Hub

C. User VM

D. Domain Controller

---

## Question 10

A company wants an always-on encrypted tunnel between headquarters and Azure.

A. Point-to-Site VPN

B. ExpressRoute

C. Site-to-Site VPN

D. Azure Firewall

---

# Quiz Answers

1. C
2. B
3. C
4. C
5. B
6. C
7. C
8. D
9. B
10. C

---

# One-Sentence Memory Hook

> VPN Gateway connects users and sites over the Internet, ExpressRoute provides private enterprise connectivity, and Virtual WAN is Microsoft's managed hub that simplifies routing, branch connectivity, and multi-region networking at scale.
