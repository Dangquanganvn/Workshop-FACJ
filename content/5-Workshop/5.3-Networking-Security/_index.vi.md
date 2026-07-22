---
title: "Mạng & Bảo mật"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

Trong phần này, chúng ta sẽ tự tay xây dựng nền móng hạ tầng mạng cho hệ thống **Fashion E-commerce Platform** tại Region Singapore (`ap-southeast-1`), đảm bảo tính bảo mật cao và phân tách rõ ràng các tầng kiến trúc.

#### 5.3.1. Tạo VPC và Hệ thống 8 Subnet đa vùng

Chúng ta sẽ khởi tạo 1 VPC tập trung và chia nhỏ thành 8 Subnet trải đều trên 2 Availability Zones (AZs), bao gồm: Public Subnets (cho ALB), Private Subnets (cho Backend EC2), DB Subnets (cho RDS) và Cache Subnets (cho Redis).

- **Bước thực hiện trên AWS Console:** Vào dịch vụ **VPC** > **Your VPCs** > Tạo VPC với dải CIDR phù hợp. Tiếp tục tạo 8 Subnet phân bổ theo sơ đồ thiết kế.
- **Hình ảnh kết quả:**
  ![Tạo VPC và 8 Subnet](/images/5-Workshop/5.3-networking/vpc-subnets1.png)
  _*Hình: Hoàn tất khởi tạo 1 VPC và 8 Subnet đa vùng.*_

#### 5.3.2. Cấu hình Internet Gateway (IGW) và Route Tables

Để các Public Subnet có thể giao tiếp ra Internet bên ngoài (phục vụ người dùng truy cập vào hệ thống e-commerce), chúng ta cần tạo Internet Gateway và liên kết với các bảng định tuyến (Route Tables).

- **Hình ảnh kết quả:**
  ![Tạo Internet Gateway](/images/5-Workshop/5.3-networking/igw-routing.png)

  _*Hình: Gắn Internet Gateway vào VPC và cấu hình Route Table.*_

#### 5.3.3. Thiết lập 3 Security Groups phân lớp

Bảo mật là yếu tố cốt lõi của nền tảng thương mại điện tử. Chúng ta sẽ tạo 3 nhóm an ninh (Security Groups) để cô lập từng tầng:

1. **ALB Security Group:** Cho phép truy cập HTTP/HTTPS từ mọi nguồn (`0.0.0.0/0`).
2. **Application Security Group:** Chỉ cho phép nhận traffic bắt nguồn từ ALB.
3. **Database & Cache Security Group:** Chỉ cho phép kết nối nội bộ từ Application EC2.

- **Hình ảnh kết quả:**
  ![Tạo Security Groups](/images/5-Workshop/5.3-networking/security-groups.png)
  _*Hình: Thiết lập 3 phân lớp Security Groups bảo vệ hệ thống.*_

#### 5.3.4. Cấu hình VPC Gateway Endpoint cho Amazon S3

Để các máy chủ Backend trong Private Subnet có thể tải hoặc truy cập hình ảnh sản phẩm thời trang trên **Amazon S3** một cách bảo mật mà không tốn chi phí NAT Gateway, chúng ta cấu hình VPC Gateway Endpoint.

- **Hình ảnh kết quả:**
  ![Tạo VPC Endpoint](/images/5-Workshop/5.3-networking/vpc-endpoint.png)
  _*Hình: Cấu hình VPC Gateway Endpoint kết nối trực tiếp tới S3.*_
