---
title : "Các bước chuẩn bị"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

#### IAM Permissions
Để triển khai hệ thống theo nguyên tắc **Least Privilege** (Quyền tối thiểu), hãy gắn Policy dưới đây cho tài khoản AWS User dùng để deploy. Policy này tập trung vào các dịch vụ cần thiết cho E-commerce (EC2, RDS, S3, CodePipeline) và lược bỏ các dịch vụ VPN/Transit Gateway không cần thiết.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "EcommerceDeploymentPermissions",
            "Effect": "Allow",
            "Action": [
                "ec2:CreateVpc", "ec2:CreateSubnet", "ec2:CreateVpcEndpoint",
                "ec2:RunInstances", "rds:CreateDBInstance", "elasticache:CreateCacheCluster",
                "s3:CreateBucket", "codepipeline:*", "codedeploy:*",
                "iam:PassRole", "logs:CreateLogGroup", "secretsmanager:GetSecretValue"
            ],
            "Resource": "*"
        }
    ]
}

