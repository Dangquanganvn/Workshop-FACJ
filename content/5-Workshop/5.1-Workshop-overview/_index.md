---
title: "Workshop Overview"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

#### Introduction to VPC Endpoints in Fashion E-commerce Architecture

- **VPC endpoints** are virtual devices. They are horizontally scaled, redundant, and highly available VPC components. They allow communication between your compute resources and AWS services without imposing availability risks.
- In the **Fashion E-commerce Platform** architecture, compute resources (Spring Boot backend running on EC2 instances within Private Subnets) can securely access **Amazon S3** (for product images) using a Gateway endpoint, and AWS services for CI/CD via Interface Endpoints (PrivateLink) completely bypassing the need for an expensive NAT Gateway.

#### Workshop Overview

In this workshop, you will deploy and test the core components of the Fashion E-commerce infrastructure:

- **"VPC Cloud"**: Houses the cloud resources including the application servers (EC2 in Private Subnet), Application Load Balancer (ALB), and VPC Endpoints for secure, cost-optimized internal data transfer.
- **"Data & Storage Layer"**: Integrates Amazon RDS PostgreSQL (Multi-AZ) and Amazon ElastiCache (Redis) to ensure high performance and high availability (Cross-AZ Sync) for the e-commerce application.
- **"Automation & Monitoring"**: Implements secure automated deployments via AWS CodeDeploy/CodePipeline using VPC Interface Endpoints and configures CloudWatch for system logging and billing alerts.

![overview](/images/5-Workshop/5.1-Workshop-overview/VPC_Gateway_Endpoint.png)
