---
title: "Data Layer Setup"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

# Comprehensive Architecture of the Data & Caching Tier

In this section, we will deploy the high-availability persistence and caching layers for the **Fashion E-commerce Platform** in the Singapore region . A robust, scalable, and secure data tier is critical for handling concurrent user transactions, maintaining session integrity, and delivering ultra-low latency product catalog searches during peak shopping events.

### Architectural Overview

The data and caching tier is partitioned into two primary components, strictly isolated within dedicated private subnets to maximize security and minimize performance bottlenecks:

1. **Transactional Database Tier (Amazon RDS PostgreSQL Multi-AZ):**
   - **Persistence & Integrity:** Acts as the primary source of truth for the entire e-commerce ecosystem, securely storing relational data such as user credentials, product inventories, detailed pricing, order history, and payment transactions.
   - **High Availability & Disaster Recovery:** Deployed across multiple Availability Zones with a synchronous standby instance. This ensures automatic failover capabilities, eliminating single points of failure and guaranteeing business continuity even during underlying hardware degradation or zone-level outages.

2. **In-Memory Caching & Session Tier (Amazon ElastiCache Redis):**
   - **Session Management:** Offloads high-frequency session reads and writes (such as shopping cart states and authentication tokens) from the primary relational database.
   - **Catalog Acceleration:** Caches hot product attributes and promotional flash-sale data to deliver sub-millisecond response times, drastically lowering database CPU utilization and ensuring a smooth user experience under high traffic loads.

### Subnet & Security Alignment

- **Network Isolation:** Both RDS and ElastiCache instances reside entirely inside non-routable **DB Subnets** and **Cache Subnets** established during the network provisioning phase. They lack public IP addresses and cannot be accessed directly from the public internet.
- **Strict Access Control:** Protected by dedicated security groups that only permit ingress traffic originating exclusively from the backend application compute instances.
