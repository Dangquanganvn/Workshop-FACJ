---
title: "Tổng quan Workshop"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

#### Giới thiệu về VPC Endpoint trong kiến trúc Fashion E-commerce

- **Điểm cuối VPC (VPC endpoints)** là các thiết bị ảo. Chúng là các thành phần VPC có khả năng mở rộng theo chiều ngang, dự phòng và có tính sẵn sàng cao. Chúng cho phép giao tiếp giữa tài nguyên điện toán của bạn và các dịch vụ AWS mà không gây ra rủi ro về tính sẵn sàng.
- Trong kiến trúc hệ thống **Fashion E-commerce Platform**, các tài nguyên điện toán (Spring Boot backend chạy trên EC2 instance trong Private Subnet) có thể truy cập an toàn vào **Amazon S3** (lưu trữ ảnh sản phẩm) bằng điểm cuối Gateway, và kết nối với các dịch vụ CI/CD qua Interface Endpoint (PrivateLink) mà hoàn toàn không cần sử dụng NAT Gateway tốn kém.

#### Tổng quan về Workshop

Trong workshop này, bạn sẽ tiến hành triển khai và kiểm thử các thành phần cốt lõi của hạ tầng thương mại điện tử thời trang:

- **"VPC Cloud"**: Nơi chứa các tài nguyên trên cloud bao gồm máy chủ ứng dụng (EC2 trong Private Subnet), Application Load Balancer (ALB), và các VPC Endpoints giúp truyền tải dữ liệu nội bộ bảo mật, tối ưu chi phí.
- **"Tầng Dữ liệu & Lưu trữ (Data Layer)"**: Tích hợp Amazon RDS PostgreSQL (Multi-AZ) và Amazon ElastiCache (Redis) nhằm đảm bảo hiệu năng cao và tính sẵn sàng cao (Đồng bộ chéo Cross-AZ) cho ứng dụng bán hàng.
- **"Tự động hóa & Giám sát (CI/CD & Monitoring)"**: Thiết lập quy trình deploy tự động, bảo mật thông qua AWS CodeDeploy/CodePipeline sử dụng VPC Interface Endpoint, đồng thời cấu hình CloudWatch để theo dõi log ứng dụng và cảnh báo chi phí.
  ![overview](/images/5-Workshop/5.1-Workshop-overview/VPC_Gateway_Endpoint.png)
