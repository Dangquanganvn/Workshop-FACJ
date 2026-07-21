---
title : "Giới thiệu"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Giới thiệu về VPC Endpoint trong kiến trúc E-commerce
Trong kiến trúc Fashion E-commerce, VPC Endpoint đóng vai trò là "cầu nối nội bộ" an toàn. Thay vì phụ thuộc vào NAT Gateway vốn tốn kém và yêu cầu cấu hình routing phức tạp cho luồng đi ra ngoài, VPC Endpoint cho phép các tài nguyên trong Private Subnet (như EC2 App Servers) giao tiếp trực tiếp với các dịch vụ AWS (S3, CodeDeploy) thông qua mạng nội bộ của AWS.

+ **Gateway Endpoint:** Được sử dụng cho Amazon S3, giúp EC2 truy cập S3 bucket lưu trữ ảnh sản phẩm với độ trễ thấp và hoàn toàn miễn phí.
+ **Interface Endpoint (AWS PrivateLink):** Được sử dụng cho các dịch vụ CI/CD, đảm bảo việc deploy code từ GitHub/CodePipeline vào Private EC2 không cần đi qua Internet công cộng.

#### Tổng quan về Workshop
Workshop này sẽ hướng dẫn bạn thiết lập hạ tầng thực tế cho hệ thống Fashion E-commerce trên AWS theo tiêu chuẩn Well-Architected:
+ **Tối ưu chi phí:** Loại bỏ NAT Gateway, tận dụng VPC Endpoints.
+ **High Availability:** Triển khai Multi-AZ với RDS và ElastiCache để đảm bảo hệ thống không bị gián đoạn.
+ **Automation:** Xây dựng luồng CI/CD bảo mật tuyệt đối cho Backend EC2.

![Architecture Overview](/images/5-Workshop/5.1-Workshop-overview/ecommerce_architecture.png)
*(Lưu ý: Thay thế bằng hình vẽ 10 luồng mà bạn đã hoàn thiện)*
