---
title: "Compute & Load Balancing"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

# Architecture of Compute & Load Balancing Tier

In this section, we will deploy the high-availability compute and load balancing infrastructure for the **Fashion E-commerce Platform** in the Singapore region . This tier ensures that incoming customer traffic is efficiently distributed, securely processed, and automatically scaled to handle varying workloads during high-traffic shopping events.

### Architectural Overview

The compute and load balancing tier integrates two core components to achieve fault tolerance and scalability:

1. **Load Distribution Tier (Application Load Balancer & Target Groups):**
   - **Traffic Management:** Routes incoming public HTTP/HTTPS requests from clients across the public subnets to backend application servers securely located in private subnets.
   - **Health Checks & Routing:** Continuously monitors backend instance health, ensuring traffic is only routed to responsive servers.

2. **Compute & Auto-Scaling Tier (Launch Templates & Auto Scaling Groups):**
   - **Automated Provisioning:** Uses EC2 Launch Templates containing the pre-configured Spring Boot application environment.
   - **Elasticity (ASG):** Dynamically adjusts the number of EC2 instances based on CPU utilization or request loads, ensuring high availability across multiple Availability Zones.
