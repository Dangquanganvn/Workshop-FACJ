---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

In this section, I summarize the objectives, scope, and AWS infrastructure architecture proposed for the Fashion E-commerce project.

# Fashion E-commerce Platform

**A cost-optimized and highly available fashion e-commerce solution on AWS**

## 1. Executive Summary

The **Fashion E-commerce Platform** is designed to provide a professional online shopping system with high scalability, strong security, and cost-efficient cloud operations. The application uses **React** for the frontend and **Spring Boot** for the backend. The infrastructure follows a **High Availability (Multi-AZ)** architecture and leverages **VPC Endpoints** to eliminate the need for costly **NAT Gateways**, making it an economical solution for demonstration and educational environments.

## 2. Problem Statement

### Current Challenges

Traditional cloud-based e-commerce systems often face significant challenges related to infrastructure costs, especially the high expense of **NAT Gateways**, as well as limited availability when they are not designed using a **Multi-AZ** architecture. In addition, CI/CD pipelines and image delivery frequently increase both latency and operational costs.

### Proposed Solution

The platform utilizes **Amazon CloudFront** to optimize content delivery for users worldwide. The infrastructure adopts a **Multi-AZ architecture** with **Amazon EC2 Auto Scaling Groups**, **Amazon ElastiCache**, and **Amazon RDS PostgreSQL** using the **Cache-Aside** pattern to reduce database workload.

Instead of using NAT Gateways, the solution employs **Amazon VPC Gateway Endpoints** for Amazon S3 and **Interface Endpoints** for CI/CD services, enabling secure, high-speed, and cost-effective internal communication.

### Benefits and Return on Investment (ROI)

The proposed architecture provides a reliable foundation for future expansion while significantly reducing monthly operational costs compared to traditional cloud deployments. Automatic failover capabilities provided by Amazon RDS and Amazon ElastiCache minimize service interruptions, while AWS-native CI/CD services fully automate software deployment.

## 3. Solution Architecture

The architecture emphasizes simplicity in networking while maximizing availability. All backend services are deployed inside **Private Subnets** and only receive traffic that has been validated by the **Application Load Balancer (ALB)**.

![Architecture Diagram](/images/2-Proposal/Proposal.png)

### AWS Services

- **Edge & Networking:** Amazon CloudFront, AWS WAF, Application Load Balancer (ALB), Amazon VPC Endpoints.
- **Compute:** Amazon EC2 (Auto Scaling Group), Spring Boot.
- **Data & Storage:** Amazon RDS PostgreSQL (Multi-AZ), Amazon ElastiCache for Redis (Multi-AZ), Amazon S3.
- **CI/CD:** GitHub, AWS CodePipeline, AWS CodeDeploy.
- **Shared Services:** AWS IAM, AWS Secrets Manager, Amazon CloudWatch.

### Component Design

- **Presentation Layer:** React frontend hosted on Amazon S3 and distributed through Amazon CloudFront.
- **Routing Layer:** The Application Load Balancer is deployed in Public Subnets and routes incoming requests to backend EC2 instances running in Private Subnets.
- **Data Layer:** Database and cache services are deployed in separate subnet groups with cross-AZ synchronization for high availability.
- **Image Storage:** Product images are stored in Amazon S3 and accessed through a VPC Gateway Endpoint, ensuring secure internal traffic.

## 4. Technical Implementation

### Deployment Phases

1. Configure the networking infrastructure, including the VPC, Public and Private Subnets, Internet Gateway, and VPC Endpoints.
2. Deploy the data layer by provisioning Amazon RDS PostgreSQL and Amazon ElastiCache in a Multi-AZ configuration.
3. Deploy the application layer by creating EC2 AMIs, configuring Auto Scaling Groups, and integrating the Application Load Balancer.
4. Configure security, monitoring, and CI/CD using GitHub, AWS CodePipeline, CodeDeploy, IAM, Secrets Manager, and Amazon CloudWatch.

### Technical Requirements

- Proficiency in ReactJS for frontend development.
- Experience with Spring Boot for RESTful API development.
- Strong understanding of Amazon VPC routing, Multi-AZ failover, and AWS cost optimization strategies.
- DevOps skills for building CI/CD pipelines and managing AWS Secrets Manager.

## 5. Project Roadmap

### Phase 1 (Weeks 1–2)

- Analyze system requirements.
- Design the database.
- Build the system architecture.
- Develop core REST APIs using Spring Boot.

### Phase 2 (Weeks 3–4)

- Develop the React frontend.
- Configure the Amazon VPC, Subnets, Security Groups, and Internet Gateway.
- Deploy Amazon RDS PostgreSQL.

### Phase 3 (Weeks 5–6)

- Deploy backend services to Amazon EC2 using Auto Scaling Groups.
- Configure the Application Load Balancer.
- Integrate Amazon S3 and Amazon CloudFront.

### Phase 4 (Weeks 7–8)

- Build CI/CD pipelines with AWS CodePipeline and CodeDeploy.
- Configure Amazon CloudWatch monitoring.
- Perform performance testing, security testing, and high availability validation.

## 6. Estimated Budget

The following cost estimate assumes Free Tier eligibility where applicable and completely eliminates NAT Gateway expenses.

| AWS Service | Estimated Monthly Cost | Purpose |
|-------------|----------------------:|---------|
| Amazon EC2 (2 × t3.micro) | **USD 18.00** | Application servers with Auto Scaling |
| Application Load Balancer | **USD 8.00** | Load balancing and request routing |
| Amazon RDS PostgreSQL | **USD 15.00** | Database for the demo environment |
| Amazon ElastiCache for Redis | **USD 10.00** | Database caching |
| Amazon S3 Standard | **USD 2.00** | Product image and static asset storage |
| Amazon CloudFront | **USD 2.00** | Content Delivery Network (CDN) |
| AWS CodePipeline & CodeDeploy | **USD 0.00** | Within AWS Free Tier limits |
| Amazon CloudWatch, IAM, Secrets Manager, and VPC Endpoints | **USD 2.00** | Monitoring and security services |

**Total Estimated Cost:** **USD 57.00 per month**, or approximately **USD 684.00 per year**.

## 7. Risk Assessment

- **Network Risk:** Inter-AZ connectivity failures, mitigated through Multi-AZ deployment.
- **Cost Risk:** Unexpected traffic spikes, mitigated by CloudWatch Billing Alarms.
- **Security Risk:** Exposure of database credentials, mitigated using IAM permission boundaries and AWS Secrets Manager.

## 8. Expected Outcomes

### Technical Improvements

- Successfully deploy a fashion e-commerce platform using a Multi-tier AWS architecture.
- Implement a fully automated CI/CD pipeline with AWS CodePipeline and CodeDeploy.
- Strengthen infrastructure security through Private Subnets, IAM, Security Groups, Secrets Manager, and VPC Endpoints.
- Establish a highly automated software deployment process.

### Long-Term Value

- Provide a scalable foundation for integrating future AWS services such as AI/ML, recommendation systems, analytics, and online payment solutions.
- Reuse the architecture for other e-commerce or web-based applications, reducing development time and deployment costs.
- Build a cloud-native infrastructure capable of scaling with increasing user traffic and business growth.
