---
title: "Launch Templates & ASG"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.5.2. </b> "
---

Trong phần này, chúng ta sẽ thiết lập EC2 Launch Templates và Auto Scaling Groups (ASG) để quản lý năng lực tính toán backend một cách linh hoạt cho hệ thống **Fashion E-commerce Platform**.

#### 1. Thiết lập EC2 Launch Templates

- **Cấu hình Bản thiết kế (Blueprint):** Định nghĩa cấu hình nền tảng cho các EC2 instance backend, chỉ định AMI, loại instance free tier, IAM instance profile và các security group chuyên dụng.
- **Tự động hóa User Data:** Nhúng các script khởi động (User Data) để tự động tải, cấu hình và khởi chạy ứng dụng Spring Boot ngay khi instance khởi động.

![EC2 Launch Template Setup](/images/5-Workshop/5.5-compute/launch-template.png)
_*Hình: Cấu hình EC2 Launch Template cho các máy chủ ứng dụng backend.*_

#### 2. Cấu hình Auto Scaling Groups (ASG) & Chính sách Co giãn

- **Triển khai Đa Availability Zone:** Triển khai các instance backend bên trong các private subnet trải rộng trên nhiều Availability Zone nhằm đảm bảo tính sẵn sàng cao và khả năng chịu lỗi.
- **Tích hợp ALB:** Liên kết trực tiếp ASG với Target Group đã tạo ở Mục 5.5.1, cho phép tự động đăng ký instance và giám sát sức khỏe.
- **Chính sách Co giãn Động:** Thiết lập các chính sách co giãn dựa trên mức sử dụng CPU để tự động tăng số lượng instance (scale out) khi lượng truy cập mua sắm tăng cao và giảm bớt (scale in) trong giờ thấp điểm.

![Auto Scaling Group Setup](/images/5-Workshop/5.5-compute/asg-scaling.png)
_*Hình: Cấu hình Auto Scaling Group và chính sách co giãn tài nguyên.*_
