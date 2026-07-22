---
title: "Networking & Security"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

In this section, we will manually build the network foundation for the **Fashion E-commerce Platform** in the Singapore region (`ap-southeast-1`), ensuring high security and clear tier separation.

#### 5.3.1. Creating VPC and 8 Multi-AZ Subnets

We will provision a centralized VPC and divide it into 8 subnets spread evenly across 2 Availability Zones (AZs), including: Public Subnets (for ALB), Private Subnets (for Backend EC2), DB Subnets (for RDS), and Cache Subnets (for Redis).

- **Execution Steps on AWS Console:** Go to the **VPC** service > **Your VPCs** > Create VPC with the appropriate CIDR block. Continue to create 8 subnets according to the architecture design.
- **Result Image:**
  ![Create VPC and 8 Subnets](/images/5-Workshop/5.3-networking/vpc-subnets.png)
  _*Figure: Completed initialization of 1 VPC and 8 Multi-AZ subnets.*_

#### 5.3.2. Configuring Internet Gateway (IGW) and Route Tables

To allow Public Subnets to communicate with the external Internet (enabling users to access the e-commerce system), we need to create an Internet Gateway and associate it with route tables.

- **Result Image:**
  ![Create Internet Gateway](/images/5-Workshop/5.3-networking/igw-routing.png)
  _*Figure: Attaching Internet Gateway to VPC and configuring Route Tables.*_

#### 5.3.3. Setting Up 3 Security Group Tiers

Security is a core element of the e-commerce platform. We will create 3 security groups to isolate each tier:

1. **ALB Security Group:** Allows HTTP/HTTPS access from all sources (`0.0.0.0/0`).
2. **Application Security Group:** Only allows incoming traffic originating from the ALB.
3. **Database & Cache Security Group:** Only allows internal connections from the Application EC2 instances.

- **Result Image:**
  ![Create Security Groups](/images/5-Workshop/5.3-networking/security-groups.png)
  _*Figure: Setting up 3 security group tiers protecting the system.*_

#### 5.3.4. Configuring VPC Gateway Endpoint for Amazon S3

To allow Backend servers in Private Subnets to securely access or download product images on **Amazon S3** without incurring expensive NAT Gateway charges, we configure a VPC Gateway Endpoint.

- **Result Image:**
  ![Create VPC Endpoint](/images/5-Workshop/5.3-networking/vpc-endpoint.png)
  _*Figure: Configuring VPC Gateway Endpoint for direct private connection to S3.*_
