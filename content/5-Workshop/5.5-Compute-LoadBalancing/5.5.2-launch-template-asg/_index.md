---
title: "Launch Templates & ASG"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.5.2. </b> "
---

In this section, we will set up EC2 Launch Templates and Auto Scaling Groups (ASG) to manage the backend compute capacity dynamically for the **Fashion E-commerce Platform**.

#### 1. Setting Up EC2 Launch Templates

- **Blueprint Configuration:** Defines the foundational configuration for backend EC2 instances, specifying the AMI, instance type (`t3.medium`), IAM instance profile, and dedicated security groups.
- **User Data Automation:** Embeds startup scripts (User Data) to automatically pull, configure, and launch the Spring Boot application upon instance boot.

![EC2 Launch Template Setup](/images/5-Workshop/5.5-compute/launch-template.png)
_*Figure: EC2 Launch Template configuration for the backend application servers.*_

#### 2. Configuring Auto Scaling Groups (ASG) & Scaling Policies

- **Multi-AZ Deployment:** Deploys backend instances across the private subnets spanning multiple Availability Zones to ensure high availability and fault tolerance.
- **ALB Integration:** Directly attaches the ASG to the Target Group created in Section 5.5.1, enabling automated instance registration and health monitoring.
- **Dynamic Scaling Policies:** Establishes CPU utilization-based scaling policies to automatically scale out instances during peak shopping surges and scale in during off-peak hours.

![Auto Scaling Group Setup](/images/5-Workshop/5.5-compute/asg-scaling.png)
_*Figure: Auto Scaling Group and scaling policy configuration.*_
