---
title: "Amazon RDS Multi-AZ"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

Trong phần này, chúng ta sẽ khởi tạo một cơ sở dữ liệu quan hệ có tính sẵn sàng cao cho hệ thống **Fashion E-commerce Platform** bằng sử dụng Amazon RDS.

#### 1. Triển khai Amazon RDS PostgreSQL (Multi-AZ)

- **Mục đích**: Lưu trữ dữ liệu quan hệ lâu dài như tài khoản người dùng, danh mục sản phẩm, lịch sử đơn hàng và các giao dịch.
- **Tính sẵn sàng cao**: Chúng ta cấu hình thể hiện RDS với **chế độ Multi-AZ**, tự động tạo một bản sao dự phòng đồng bộ (standby replica) ở một Availability Zone khác. Nếu cơ sở dữ liệu chính gặp sự cố, AWS sẽ tự động chuyển đổi dự phòng (failover) sang bản standby.
- **Subnet Group & Bảo mật**: Cơ sở dữ liệu được đặt bên trong các **DB Subnets** chuyên dụng đã tạo ở Mục 5.3, được bảo vệ bởi Database Security Group chỉ cho phép kết nối từ các máy chủ ứng dụng backend.
  ![RDS Multi-AZ Setup](/images/5-Workshop/5.4-data-layer/rds-multi-az2.png)
  ![RDS Multi-AZ Setup](/images/5-Workshop/5.4-data-layer/rds-multi-az.png)
  _*Hình: Cấu hình cơ sở dữ liệu chính và dự phòng của Amazon RDS Multi-AZ.*_
