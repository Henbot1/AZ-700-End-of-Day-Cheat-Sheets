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

Returns multiple
