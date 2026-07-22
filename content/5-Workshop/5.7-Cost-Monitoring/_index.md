---
title: "Cost Monitoring & Cleanup"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

# Cost Monitoring & Resource Cleanup

In this final section, we will cover how to monitor cloud expenditures for the **Fashion E-commerce Platform** using native AWS financial tools and outline the essential steps to clean up resources to prevent unexpected charges.

### 1. Monitoring AWS Costs and Setting Budgets

Keeping track of cloud resources in the Singapore region (`ap-southeast-1`) is crucial during development and workshops.

- **AWS Budgets:** Configured to track monthly spending limits and send alerts when expenditures exceed specific thresholds.

![AWS Budgets Dashboard](/images/5-Workshop/5.7-cost/budgets.png)
_*Figure: AWS Budgets overview tracking spending limits and health status.*_

- **AWS Cost Explorer:** Used to analyze historical spending patterns, breakdown costs by service (EC2, RDS, ElastiCache, S3, ALB), and forecast future expenses.

![AWS Cost Explorer Breakdown](/images/5-Workshop/5.7-cost/cost-explorer.png)
_*Figure: AWS Cost Explorer analyzing cost comparison and usage drivers.*_

### 2. Resource Cleanup & Deletion Strategy

To avoid ongoing charges after completing the workshop, resources must be terminated or deleted in the correct reverse-dependency order:

1. **Compute & Load Balancing:** Delete the Application Load Balancer (ALB), terminate the Auto Scaling Group (ASG), and remove Launch Templates.
2. **Data Layer:** Delete the Amazon RDS PostgreSQL Multi-AZ instance and the Amazon ElastiCache Redis cluster.
3. **Storage:** Empty and delete the S3 bucket used for frontend static hosting.
4. **Networking & Security:** Delete custom VPCs, subnets, internet gateways, NAT gateways, and security groups created during Section 5.3.
