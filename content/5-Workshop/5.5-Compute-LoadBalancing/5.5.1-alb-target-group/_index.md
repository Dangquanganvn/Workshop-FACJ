---
title: "ALB & Target Group"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.5.1. </b> "
---

In this section, we will configure the Application Load Balancer (ALB) and Target Groups to route external traffic to our backend application servers.

#### 1. Configuring Application Load Balancer and Target Groups

- **Public-Facing ALB:** Deployed across the **Public Subnets** to act as the single point of entry for all customer HTTP/HTTPS requests coming into the e-commerce platform.
- **Target Groups:** Routes requests to the backend Spring Boot instances residing in the private subnets, utilizing strict health checks to route traffic effectively.
- **Security Integration:** Bound to the ALB Security Group to allow inbound traffic from the internet while enforcing secure communication protocols.

![ALB and Target Group Setup](/images/5-Workshop/5.5-compute/alb-target-group.png)
_*Figure: Application Load Balancer and Target Group routing configuration.*_

#### 2. Target Group Health Check Configuration

- **Health Check Path:** Configured with a specific endpoint (such as `/actuator/health`) to actively monitor the operational status of the backend application nodes.
- **Thresholds & Intervals:** Sets appropriate response timeouts, healthy/unhealthy thresholds, and success codes (e.g., `200`) to ensure traffic is exclusively dispatched to responsive servers, preventing downtime during deployments or failures.

![Target Group Health Check Configuration](/images/5-Workshop/5.5-compute/target-group-health-check.png)
_*Figure: Target Group health check settings ensuring high availability of backend nodes.*_
