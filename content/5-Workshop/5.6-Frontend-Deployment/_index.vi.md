---
title: "Triển khai Frontend"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

# Triển khai Frontend lên Amazon S3

Trong phần này, chúng ta sẽ tiến hành host giao diện frontend tĩnh của hệ thống **Fashion E-commerce Platform** bằng dịch vụ **Amazon S3 Static Website Hosting**. Ứng dụng frontend được build cục bộ bằng React thành các tài nguyên tĩnh tối ưu sẵn sàng cho môi trường production và sau đó được tải lên trực tiếp vào một S3 bucket đã cấu hình tính năng web hosting.

### Tổng quan Kiến trúc & Các bước Triển khai

1. **Build Ứng dụng React cho Production:**
   - Thực thi các script build production (ví dụ: `npm run build`) để đóng gói ứng dụng React thành các file tĩnh hiệu năng cao (`HTML`, `CSS` và các bundle JavaScript đã được tối ưu thu gọn).

2. **Khởi tạo S3 Bucket & Cấu hình Static Website Hosting:**
   - Tạo một S3 bucket , điều chỉnh cấu hình chặn quyền truy cập công cộng (block public access) phù hợp cho việc host website và bật tính năng **Static website hosting** với các tài liệu trang chủ và trang lỗi được chỉ định (ví dụ: `index.html`).

![S3 Static Website Hosting Configuration](/images/5-Workshop/5.6-frontend/s3-website-hosting.png)
_*Hình: Cấu hình S3 bucket và các thiết lập static website hosting.*_

1. **Tải lên các tệp Build & Xác thực Giao diện:**
   - Tải các tệp build production của React lên thư mục gốc của S3 bucket, thiết lập thành công giao diện người dùng công khai cho nền tảng thương mại điện tử.

![Frontend Website Deployed on S3](/images/5-Workshop/5.6-frontend/frontend-deployed.png)
_*Hình: Giao diện website frontend React sau khi deploy thành công và chạy trên Amazon S3 static hosting.*_
