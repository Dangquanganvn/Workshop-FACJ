---
title: "Các bước chuẩn bị"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

#### 1. Tài khoản AWS và Lựa chọn Region

Trong workshop này, chúng ta sẽ **tự tay triển khai hạ tầng (manual deployment)** thay vì dùng code tự động. Vui lòng đảm bảo bạn có quyền truy cập vào tài khoản AWS.

Chúng ta sẽ thống nhất sử dụng **Region Singapore (ap-southeast-1)** cho toàn bộ hệ thống e-commerce này.

1. Đăng nhập vào [AWS Management Console](https://console.aws.amazon.com/).
2. Ở góc trên cùng bên phải, nhấp vào menu thả xuống chọn Region.
3. Chọn **Asia Pacific (Singapore) ap-southeast-1**.

#### 2. Phân quyền IAM (IAM permissions)

Để có thể tạo và xóa tài nguyên một cách trơn tru trong lab này (bao gồm VPC, EC2, ALB, Auto Scaling, RDS, ElastiCache và S3), tài khoản IAM của bạn cần được cấp quyền phù hợp.

Nếu bạn không sử dụng tài khoản có quyền Quản trị viên (AdministratorAccess), hãy thêm chính sách (policy) dạng JSON sau vào user của bạn:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "ec2:CreateVpc",
                "ec2:DeleteVpc",
                "ec2:DescribeVpcs",
                "ec2:ModifyVpcAttribute",
                "ec2:CreateSubnet",
                "ec2:DeleteSubnet",
                "ec2:DescribeSubnets",
                "ec2:CreateRouteTable",
                "ec2:DeleteRouteTable",
                "ec2:DescribeRouteTables",
                "ec2:AssociateRouteTable",
                "ec2:CreateInternetGateway",
                "ec2:DeleteInternetGateway",
                "ec2:AttachInternetGateway",
                "ec2:DetachInternetGateway",
                "ec2:CreateSecurityGroup",
                "ec2:DeleteSecurityGroup",
                "ec2:DescribeSecurityGroups",
                "ec2:AuthorizeSecurityGroupIngress",
                "ec2:AuthorizeSecurityGroupEgress",
                "ec2:RunInstances",
                "ec2:StopInstances",
                "ec2:TerminateInstances",
                "ec2:DescribeInstances",
                "rds:CreateDBInstance",
                "rds:DeleteDBInstance",
                "rds:DescribeDBInstances",
                "rds:CreateDBSubnetGroup",
                "elasticache:CreateCacheCluster",
                "elasticache:DeleteCacheCluster",
                "elasticache:DescribeCacheClusters",
                "s3:CreateBucket",
                "s3:DeleteBucket",
                "s3:PutObject",
                "s3:GetObject",
                "s3:ListBucket",
                "ec2:CreateVpcEndpoint",
                "ec2:DeleteVpcEndpoints",
                "ec2:DescribeVpcEndpoints",
                "codedeploy:*",
                "logs:CreateLogGroup",
                "logs:PutRetentionPolicy",
                "iam:PassRole"
            ],
            "Resource": "*"
        }
    ]
}

```
