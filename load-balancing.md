# AZ-700 Study Notes - Azure Load Balancing Services

**Study Date:** End of Day Review

## Topics Covered

- Azure Load Balancer
- Azure Application Gateway
- Azure Front Door
- Azure Traffic Manager

---

# Quick Reference Cheat Sheet

| Service | Layer | Primary Purpose |
|----------|---------|----------------|
| Azure Load Balancer | Layer 4 | TCP/UDP traffic distribution |
| Azure Application Gateway | Layer 7 | Web application load balancing |
| Azure Front Door | Layer 7 (Global) | Global web application acceleration and routing |
| Azure Traffic Manager | DNS | DNS-based traffic routing |

---

# Azure Load Balancer

## Purpose

Distributes incoming TCP or UDP traffic across multiple backend resources.

## Key Features

- Layer 4 Load Balancing
- Supports TCP and UDP
- Internal or Public Load Balancer
- Health Probes
- Load Balancing Rules
- HA Ports
- Zone-redundant support (Standard SKU)

## Use Cases

✅ SQL Servers

✅ Custom TCP applications

✅ UDP applications

✅ VM load balancing

✅ Internal application load balancing

## Exam Triggers

If the question mentions:

- TCP
- UDP
- Custom application ports
- Database traffic
- Layer 4

**Answer is usually Azure Load Balancer.**

## Common Trap

If the requirement includes:

- URL inspection
- SSL termination
- Path-based routing

**It is NOT Azure Load Balancer.**

---

# Azure Application Gateway

## Purpose

Layer 7 load balancing for web applications.

## Key Features

- HTTP/HTTPS only
- URL Path Routing
- Host-Based Routing
- SSL Offload
- Session Affinity
- Web Application Firewall (WAF)

## Example

```text
/api      -> Backend Pool A
/images   -> Backend Pool B
```

## Use Cases

✅ Internal web applications

✅ Public web applications

✅ URL-based routing

✅ Host-based routing

✅ OWASP protection

✅ SSL termination

## Exam Triggers

If a question mentions:

- URL routing
- Hostnames
- Web traffic inspection
- SSL offloading
- WAF

**Answer is usually Application Gateway.**

## Common Trap

Application Gateway is:

✅ Regional

❌ Global

---

# Azure Front Door

## Purpose

Global Layer 7 entry point for web applications.

## Key Features

- Global Load Balancing
- Anycast Routing
- Edge Network Acceleration
- SSL Offload
- Web Application Firewall
- Fast Regional Failover

## Typical Architecture

```text
Users
   ↓
Front Door
   ↓
East US
West US
Europe
```

## Use Cases

✅ Global web applications

✅ Multi-region deployments

✅ Fast failover

✅ Global WAF

✅ Reduced latency for worldwide users

## Exam Triggers

If a question mentions:

- Global application
- Lowest latency worldwide
- Edge locations
- Microsoft global edge network
- Global WAF

**Answer is usually Front Door.**

## Common Trap

Front Door is:

✅ Layer 7

❌ TCP/UDP Load Balancer

---

# Azure Traffic Manager

## Purpose

DNS-based traffic distribution.

## Important Concept

Traffic Manager does NOT proxy traffic.

Traffic Manager answers DNS queries and directs clients to an endpoint.

### Traffic Flow

```text
Client
   ↓ DNS Request
Traffic Manager
   ↓ DNS Response
Chosen Endpoint
```

---

# Traffic Manager Routing Methods

## Priority

Primary/Secondary failover.

### Example

```text
East US
   ↓
West US (Backup)
```

### Use Case

Disaster Recovery

---

## Geographic

Routes users according to geographic location.

### Example

```text
US Users -> US Endpoint
EU Users -> EU Endpoint
```

### Use Case

Data residency requirements

Regional compliance

---

## Subnet

Routes traffic according to client IP address ranges.

### Use Case

Different networks require different destinations.

---

## Multivalue

Returns multiple healthy endpoints in DNS responses.

### Use Case

Client-side failover

Reduce impact of DNS caching

### Exam Trigger

When a client application:

- Receives a list of endpoints
- Tries another endpoint if the first fails

Think:

**Multivalue Routing**

---

# Traffic Manager Endpoint Types

## Azure Endpoint

Traffic directed to Azure resources.

### Examples

- Azure App Service
- Azure Public Load Balancer

---

## External Endpoint

Traffic directed to public resources outside Azure.

### Examples

- AWS workloads
- On-premises web servers
- Third-party hosted applications

---

## Nested Endpoint

Traffic Manager profile inside another Traffic Manager profile.

### Example

```text
Global Traffic Manager
        ↓
Regional Traffic Manager
        ↓
Azure Resources
```

### Use Cases

- Hierarchical routing
- Large-scale deployments
- Combining routing methods

---

# Service Selection Matrix

## Requirement → Service

### Custom TCP Application

✅ Azure Load Balancer

---

### URL Path Routing

✅ Azure Application Gateway

---

### Host-Based Routing

✅ Azure Application Gateway

---

### SQL Injection/XSS Protection

✅ Application Gateway WAF

✅ Front Door WAF

---

### Multi-Region Web Application

✅ Azure Front Door

✅ Azure Traffic Manager

---

### DNS-Based Traffic Distribution

✅ Azure Traffic Manager

---

### Application Acceleration Through Edge Locations

✅ Azure Front Door

---

### Disaster Recovery Failover

✅ Traffic Manager (Priority Routing)

---

### Closest Regional Endpoint

✅ Traffic Manager

---

# High-Value Exam Traps

## Trap #1

Requirement:

> Route based on URL paths

Wrong Answer:

❌ Load Balancer

Correct Answer:

✅ Application Gateway

---

## Trap #2

Requirement:

> Custom TCP application

Wrong Answer:

❌ Application Gateway

Correct Answer:

✅ Load Balancer

---

## Trap #3

Requirement:

> Global web application

Wrong Answer:

❌ Application Gateway

Correct Answer:

✅ Front Door

---

## Trap #4

Requirement:

> DNS-based failover

Wrong Answer:

❌ Front Door

Correct Answer:

✅ Traffic Manager

---

## Trap #5

Requirement:

> Microsoft Global Edge Network

Correct Answer:

✅ Azure Front Door

---

# Morning Review Quiz

## Question 1

You need to distribute TCP 1433 traffic across several SQL Servers.

A. Front Door  
B. Application Gateway  
C. Load Balancer  
D. Traffic Manager

---

## Question 2

You need URL path routing for:

```text
/api
/images
```

Which service?

A. Application Gateway  
B. Load Balancer  
C. Traffic Manager  
D. NAT Gateway

---

## Question 3

A global web application requires WAF protection and Microsoft's edge network.

A. Application Gateway  
B. Front Door  
C. Traffic Manager  
D. Load Balancer

---

## Question 4

Which service is DNS-based?

A. Front Door  
B. Load Balancer  
C. Application Gateway  
D. Traffic Manager

---

## Question 5

A company needs an active/passive disaster recovery setup.

Which Traffic Manager routing method should be used?

A. Geographic  
B. Priority  
C. Subnet  
D. Multivalue

---

## Question 6

Users should connect to different endpoints based on country.

A. Priority  
B. Multivalue  
C. Geographic  
D. Subnet

---

## Question 7

A company hosts an application in AWS and wants it included in a Traffic Manager profile.

Which endpoint type should be used?

A. Azure Endpoint  
B. Nested Endpoint  
C. External Endpoint  
D. Geographic Endpoint

---

## Question 8

Traffic Manager should return multiple healthy endpoints so the client can perform failover.

A. Subnet  
B. Geographic  
C. Multivalue  
D. Priority

---

## Question 9

An administrator wants SQL Injection and XSS protection for a single-region web application.

A. Application Gateway WAF  
B. Load Balancer  
C. Traffic Manager  
D. NAT Gateway

---

## Question 10

Which service proxies HTTP/HTTPS traffic through Microsoft's global edge network?

A. Traffic Manager  
B. Front Door  
C. Load Balancer  
D. Route Server

---

# Quiz Answers

1. C
2. A
3. B
4. D
5. B
6. C
7. C
8. C
9. A
10. B

---

# One-Sentence Memory Hook

> Azure Load Balancer handles TCP/UDP traffic, Application Gateway handles web applications, Front Door handles global web applications, and Traffic Manager handles DNS-based routing.
