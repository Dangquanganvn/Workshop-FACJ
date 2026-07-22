---
title: "Amazon ElastiCache Redis"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

In this section, we will deploy an in-memory caching layer using Amazon ElastiCache to optimize performance for the **Fashion E-commerce Platform**.

#### 1. Deploying Amazon ElastiCache Redis Cluster

- **Purpose**: Manages shopping cart sessions, user authentication tokens, and caches frequently accessed product details to reduce database load.
- **High Performance**: In-memory data store providing sub-millisecond response times for real-time e-commerce operations.
- **Subnet Group & Security**: The Redis cluster is deployed inside the dedicated **Cache Subnets** and secured using a Cache Security Group that restricts access exclusively to the backend compute tier.

![ElastiCache Redis Setup](/images/5-Workshop/5.4-data-layer/elasticache-redis.png)
![ElastiCache Redis Setup](/images/5-Workshop/5.4-data-layer/elasticache-redis2.png)
_*Figure: Amazon ElastiCache Redis cluster configuration.*_
