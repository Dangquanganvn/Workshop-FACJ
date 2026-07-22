---
title: "Amazon RDS Multi-AZ"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

In this section, we will provision a highly available relational database for the **Fashion E-commerce Platform** using Amazon RDS.

#### 1. Deploying Amazon RDS PostgreSQL (Multi-AZ)

- **Purpose**: Stores persistent relational data such as user accounts, product catalogs, order history, and transactions.
- **High Availability**: We configure the RDS instance with **Multi-AZ deployment**, which automatically provisions a synchronous standby replica in a different Availability Zone. If the primary database fails, AWS automatically fails over to the standby.
- **Subnet Group & Security**: The database is placed inside the dedicated **DB Subnets** created in Section 5.3, protected by the Database Security Group allowing connections solely from the backend application servers.

![RDS Multi-AZ Setup](/images/5-Workshop/5.4-data-layer/rds-multi-az2.png)
![RDS Multi-AZ Setup](/images/5-Workshop/5.4-data-layer/rds-multi-az.png)
_*Figure: Amazon RDS Multi-AZ primary and standby database configuration.*_
