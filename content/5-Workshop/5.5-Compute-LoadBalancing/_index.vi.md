---
title: "Tính toán & Cân bằng tải"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

# Tổng quan Tầng Tính toán & Cân bằng tải

Trong phần này, chúng ta sẽ triển khai hạ tầng tính toán và cân bằng tải có tính sẵn sàng cao cho hệ thống **Fashion E-commerce Platform** tại Region Singapore . Tầng này đảm bảo lưu lượng truy cập của khách hàng được phân phối hiệu quả, xử lý bảo mật và tự động mở rộng quy mô để đáp ứng khối lượng công việc biến động trong các đợt mua sắm cao điểm.

### Tổng quan Kiến trúc

Tầng tính toán và cân bằng tải tích hợp hai thành phần cốt lõi để đạt được khả năng chịu lỗi và mở rộng:

1. **Tầng Phân phối Tải (Application Load Balancer & Target Groups):**
   - **Quản lý Lưu lượng:** Định tuyến các yêu cầu HTTP/HTTPS công cộng từ client qua public subnet đến các máy chủ ứng dụng backend nằm an toàn trong private subnet.
   - **Kiểm tra Sức khỏe & Định tuyến:** Liên tục giám sát tình trạng của các instance backend, đảm bảo lưu lượng chỉ được chuyển đến các máy chủ đang hoạt động tốt.

2. **Tầng Tính toán & Tự động mở rộng (Launch Templates & Auto Scaling Groups):**
   - **Khởi tạo Tự động:** Sử dụng EC2 Launch Templates chứa môi trường ứng dụng Spring Boot đã được cấu hình sẵn.
   - **Khả năng co giãn (ASG):** Tự động điều chỉnh số lượng EC2 instance dựa trên mức sử dụng CPU hoặc tải yêu cầu, đảm bảo tính sẵn sàng cao trải dài trên nhiều Availability Zones.
