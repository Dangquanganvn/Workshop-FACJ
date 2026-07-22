---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---


# Multi-AZ hay Read Replica? Mình cũng từng nhầm!

Khi mới học về Amazon RDS, mình từng nhầm lẫn giữa Multi-AZ và Read Replica, và mình nghĩ đây cũng là điều khá nhiều bạn mới học AWS gặp phải. Hai tính năng này đều tạo thêm bản sao của database nhưng mục đích sử dụng hoàn toàn khác nhau. Trong bài viết này, mình sẽ tóm tắt những điểm khác biệt quan trọng để mọi người dễ ghi nhớ.

Các điểm chính cần nắm:

* Multi-AZ
  * Mục tiêu : High Availability (HA).
  * Đồng bộ dữ liệu Synchronous.
  * Có Standby DB ở AZ khác.
  * Tự động Failover khi Primary gặp sự cố.
  * Không xử lý truy vấn đọc, không giúp tăng hiệu năng. 

* Read Replica
  * Mục tiêu : Read Scaling.
  * Động bộ dữ liệu Asynchronous.
  * Xử lý các truy vấn SELECT để giảm tải cho Primary/
  * Có thể xảy ra độ trễ dữ liệu (Replication Lag).
  * Không tự động Failover khi Primary gặp sự cố. 

* Kết luận nhanh
  *  Multi-AZ = Chống sập hệ thống (HA).
  *  Read Replica = Tăng khả năng đọc (Read Scaling).
  *  Trong các hệ thống production, hai tính năng này thường được kết hợp với nhau để vừa đảm bảo tính sẵn sàng vừa cải thiện hiệu năng.
![Ảnh Blog](/images/3-BlogsPosted/Blog1.png)

[Link Blog](https://www.facebook.com/groups/660548818043427/user/100022580752820)

