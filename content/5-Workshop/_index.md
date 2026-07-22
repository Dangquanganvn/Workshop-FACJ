---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Manual AWS Infrastructure Deployment for Fashion E-commerce Platform

#### Overview

In this workshop section, you will learn how to manually build and configure a production-ready, highly available Multi-AZ network and compute infrastructure for the **Fashion E-commerce Platform** in the **Singapore region (ap-southeast-1)**.

By avoiding complex automated tools, you will gain hands-on experience with core AWS components:

- **Networking & Security** - Provisioning a custom VPC, 8 multi-tier subnets across 2 Availability Zones, Internet Gateway, Route Tables, and VPC Endpoints for secure private communication.
- **Data & Caching Layer** - Setting up Amazon RDS Multi-AZ for relational database persistence and Amazon ElastiCache (Redis) for high-performance session and data caching.
- **Compute & Load Balancing** - Configuring Application Load Balancers (ALB), Target Groups, EC2 Launch Templates, and Auto Scaling Groups (ASG) to handle high-traffic shopping events.
- **Frontend & Storage** - Deploying static web assets to Amazon S3.

#### Contents

1. [Workshop Overview](5.1-workshop-overview)
2. [Prerequisites](5.2-prerequisite)
3. [Networking & Security](5.3-networking-security)
4. [Data Layer Setup](5.4-data-layer)
5. [Compute & Load Balancing](5.5-compute-load-balancing)
6. [Frontend Deployment](5.6-frontend-deployment)
7. [Cost Optimization & Monitoring](5.7-cost-monitoring)
