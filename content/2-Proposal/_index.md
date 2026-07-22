---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

<!-- In this section, you need to summarize the contents of the workshop that you **plan** to conduct. -->

# Fashion E-commerce Platform

## A Unified AWS Architecture for High Availability and Cost Optimization

### 1. Executive Summary

The Fashion E-commerce Platform is designed to provide a professional, secure, and highly scalable online shopping experience capable of handling high traffic loads during peak shopping events. The system utilizes **React** for the frontend and **Spring Boot** for the backend. The architecture is deployed following **High Availability (Multi-AZ)** standards, integrating advanced networking techniques such as **VPC Endpoints** to completely eliminate expensive services like NAT Gateway, ensuring high cost-efficiency for the cloud environment.

### 2. Problem Statement

#### What’s the Problem?

Traditional E-commerce systems deployed on Cloud environments often face major infrastructure cost challenges—especially regarding expensive NAT Gateway fees—and lack high availability if not designed following Multi-AZ standards. Additionally, handling CI/CD pipelines and media asset transmissions often introduces latency and high maintenance costs.

#### The Solution

The platform utilizes **Amazon CloudFront** to optimize global user experience. The system implements a **Multi-AZ** architecture with an **Auto Scaling Group** for EC2, utilizing **Amazon ElastiCache** and **RDS PostgreSQL** with a Cache-Aside pattern to reduce database load. Crucially, instead of using costly NAT Gateways, the system uses **VPC Gateway Endpoints** for S3 and **Interface Endpoints** for CI/CD services, ensuring secure, high-speed, and cost-free internal data transfers.

#### Benefits and Return on Investment

The solution establishes a solid foundation ready for future feature expansions. Network optimization significantly lowers monthly maintenance costs compared to conventional architectures. The platform minimizes operational risks thanks to automatic failover capabilities in RDS and ElastiCache, while fully automating deployment workflows using native AWS CI/CD pipelines.

### 3. Solution Architecture

The architecture focuses on structural simplicity in network design while maximizing availability. All backend servers are isolated within Private Subnets, accepting only filtered traffic routed through the ALB. The architecture is detailed below:

![Fashion E-commerce Architecture](/images/2-Proposal/Proposal.png)

#### AWS Services Used

- **Edge & Network Layer**: Amazon CloudFront, AWS WAF, ALB, VPC Endpoints.
- **Compute Layer**: Amazon EC2 (Auto Scaling Group), Spring Boot.
- **Data & Storage Layer**: Amazon RDS (PostgreSQL Multi-AZ), Amazon ElastiCache (Redis Multi-AZ), Amazon S3.
- **CI/CD Layer**: GitHub, AWS CodePipeline, AWS CodeDeploy.
- **Shared Services**: AWS IAM, AWS Key Management Service (KMS), Amazon CloudWatch.

#### Component Design

- **Frontend Layer**: ReactJS frontend distributed via CloudFront/S3.
- **Routing Layer**: ALB located in the Public Subnet, routing traffic to Backend EC2 instances in the Private Subnet.
- **Data Layer**: Database and Cache hosted in dedicated subnets supporting Cross-AZ synchronization.
- **Image Storage Layer**: Utilizes S3 via VPC Gateway Endpoints to ensure internal, secure handling of product images.

### 4. Technical Implementation

#### Implementation Phases

- **Phase 1 (Month 1)**: Requirements analysis, database design, system architecture planning, and core API development using Spring Boot.
- **Phase 2 (Month 2)**: ReactJS frontend development, VPC, subnet, security group, and Internet Gateway setup, alongside Amazon RDS PostgreSQL and backend compute deployment on EC2.
- **Phase 3 (Month 3)**: Integration of Amazon S3, CloudFront, setting up CI/CD via CodePipeline and CodeDeploy, configuring CloudWatch, and performing security and system testing.

#### Technical Requirements

- Proficiency in ReactJS (UI/UX) and Spring Boot (RESTful APIs).
- In-depth knowledge of VPC routing, Multi-AZ failover, and AWS Cost Optimization.
- DevOps skills: Pipeline configuration, automated CI/CD, and Secrets Manager management.

### 5. Timeline & Milestones

#### Project Timeline

- **Internship (Months 1-3)**: 3 months total implementation.
  - Month 1: Design & Core Backend API.
  - Month 2: Frontend & Network Setup, Compute Integration.
  - Month 3: CI/CD Pipeline, Monitoring & Testing.
- **Post-Launch**: Ongoing optimization and system maintenance.

### 6. Budget Estimation

Estimated based on Free Tier utilization and the complete elimination of NAT Gateway costs.

#### Infrastructure Costs

- **Amazon EC2 (2 t3.micro)**: $18.00/month (Application Server, Auto Scaling Group).
- **Application Load Balancer (ALB)**: $8.00/month (Load balancing and traffic routing).
- **Amazon RDS PostgreSQL**: $15.00/month (Single DB for Demo environment).
- **Amazon ElastiCache Redis**: $10.00/month (Data caching, reducing database load).
- **Amazon S3 Standard**: $2.00/month (Product image storage and static assets).
- **Amazon CloudFront**: $2.00/month (CDN content delivery).
- **AWS CodePipeline & CodeDeploy**: $0.00/month (Within Free Tier limits).
- **Amazon CloudWatch, IAM, Secrets Manager & VPC Endpoint**: $2.00/month.
- **Total**: $57.00/month, approximately $684.00/year.

### 7. Risk Assessment

#### Risk Matrix

- **Network Outages**: Medium impact, medium probability.
- **Cost Surges**: Medium impact, low probability.
- **Security Vulnerabilities**: High impact, low probability.

#### Mitigation Strategies

- **Network**: Multi-AZ deployment to guarantee high availability and failover support.
- **Cost**: CloudWatch billing alarms to monitor unexpected spikes.
- **Security**: IAM Permissions Boundary, WAF, and Secrets Manager to protect credentials and database access.

### 8. Expected Outcomes

#### Technical Improvements:

- Successful implementation of a multi-tier fashion E-commerce system on AWS.
- Fully automated CI/CD pipeline using AWS CodePipeline and CodeDeploy for rapid version releases.
- Enhanced security leveraging Private Subnets, IAM, Security Groups, Secrets Manager, and VPC Endpoints.

#### Long-term Value:

- Easily extensible for integrating additional AWS services such as AI/ML recommendation engines or data analytics.
- Reusable architecture template for similar web scale projects, reducing time-to-market and development costs.
