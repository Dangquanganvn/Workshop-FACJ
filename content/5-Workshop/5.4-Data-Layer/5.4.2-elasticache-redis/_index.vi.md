---
title: "Amazon ElastiCache Redis"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

Trong phần này, chúng ta sẽ triển khai tầng caching trong bộ nhớ bằng Amazon ElastiCache để tối ưu hiệu năng cho hệ thống **Fashion E-commerce Platform**.

#### 1. Triển khai cụm Amazon ElastiCache Redis

- **Mục đích**: Quản lý phiên giỏ hàng, token xác thực người dùng và cache các chi tiết sản phẩm được truy cập thường xuyên nhằm giảm tải cho cơ sở dữ liệu chính.
- **Hiệu năng cao**: Kho lưu trữ dữ liệu trong bộ nhớ mang lại thời gian phản hồi dưới một mili-giây cho các hoạt động thương mại điện tử thời gian thực.
- **Subnet Group & Bảo mật**: Cụm Redis được triển khai bên trong các **Cache Subnets** chuyên dụng và được bảo mật bằng Cache Security Group chỉ giới hạn quyền truy cập độc quyền từ tầng tính toán backend.

![ElastiCache Redis Setup](/images/5-Workshop/5.4-data-layer/elasticache-redis.png)
![ElastiCache Redis Setup](/images/5-Workshop/5.4-data-layer/elasticache-redis2.png)
_*Hình: Cấu hình cụm Amazon ElastiCache Redis.*_
