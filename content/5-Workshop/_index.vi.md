---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Triển khai Hạ tầng AWS Thủ công cho Nền tảng E-commerce Thời trang

#### Tổng quan

Trong phần workshop này, bạn sẽ học cách tự tay xây dựng và cấu hình một hạ tầng mạng và tính toán Multi-AZ sẵn sàng cho môi trường production đối với hệ thống **Fashion E-commerce Platform** tại **Region Singapore (ap-southeast-1)**.

Thông qua việc tự thực hiện từng bước thủ công, bạn sẽ nắm vững các thành phần lõi của AWS:

- **Mạng & Bảo mật (Networking & Security)** - Khởi tạo VPC tùy chỉnh, 8 subnet đa phân lớp trên 2 Availability Zones, Internet Gateway, Route Tables và VPC Endpoints nhằm bảo mật đường truyền nội bộ.
- **Tầng Dữ liệu & Cache (Data & Caching Layer)** - Thiết lập Amazon RDS Multi-AZ cho cơ sở dữ liệu quan hệ và Amazon ElastiCache (Redis) để tối ưu hiệu năng xử lý phiên người dùng.
- **Tầng Tính toán & Cân bằng tải (Compute & Load Balancing)** - Cấu hình Application Load Balancer (ALB), Target Groups, EC2 Launch Templates và Auto Scaling Groups (ASG) để đáp ứng lượng truy cập mua sắm lớn.
- **Frontend & Lưu trữ (Frontend & Storage)** - Đưa giao diện tĩnh lên dịch vụ Amazon S3.

#### Nội dung

1. [Tổng quan Workshop](5.1-workshop-overview)
2. [Các bước chuẩn bị](5.2-prerequisite)
3. [Mạng & Bảo mật](5.3-networking-security)
4. [Thiết lập Tầng Dữ liệu](5.4-data-layer)
5. [Tính toán & Cân bằng tải](5.5-compute-load-balancing)
6. [Triển khai Frontend](5.6-frontend-deployment)
7. [Tối ưu chi phí & Giám sát](5.7-cost-monitoring)
