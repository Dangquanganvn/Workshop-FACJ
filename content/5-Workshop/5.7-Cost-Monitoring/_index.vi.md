---
title: "Giám sát Chi phí & Dọn dẹp"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

# Giám sát Chi phí & Dọn dẹp Tài nguyên

Trong phần cuối cùng này, chúng ta sẽ tìm hiểu cách giám sát chi phí trên đám mây cho hệ thống **Fashion E-commerce Platform** bằng các công cụ tài chính nguyên bản của AWS, đồng thời thực hiện các bước quan trọng để dọn dẹp tài nguyên nhằm tránh phát sinh cước phí ngoài ý muốn.

### 1. Giám sát Chi phí AWS và Thiết lập Ngân sách (Budgets)

Việc theo dõi sát sao tài nguyên đám mây tại Region Singapore (`ap-southeast-1`) là rất quan trọng trong suốt quá trình phát triển và làm workshop.

- **AWS Budgets:** Được cấu hình để theo dõi hạn mức chi tiêu hàng tháng và gửi cảnh báo khi chi phí vượt qua các ngưỡng giới hạn cụ thể.

![AWS Budgets Dashboard](/images/5-Workshop/5.7-cost/budgets.png)
_*Hình: Bảng điều khiển AWS Budgets theo dõi hạn mức chi tiêu và trạng thái ngân sách.*_

- **AWS Cost Explorer:** Dùng để phân tích lịch sử chi tiêu, chi tiết hóa chi phí theo từng dịch vụ và theo dõi các yếu tố thay đổi chi phí.

![AWS Cost Explorer Breakdown](/images/5-Workshop/5.7-cost/cost-explorer.png)
_*Hình: AWS Cost Explorer phân tích tổng quan so sánh chi phí và các trình điều khiển sử dụng.*_

### 2. Chiến lược Dọn dẹp & Xóa Tài nguyên

Để tránh bị tính phí liên tục sau khi hoàn thành workshop, các tài nguyên cần phải được chấm dứt (terminate) hoặc xóa theo đúng thứ tự ngược lại với quá trình tạo:

1. **Tính toán & Cân bằng tải:** Xóa Application Load Balancer (ALB), dừng Auto Scaling Group (ASG) và xóa Launch Templates.
2. **Tầng Dữ liệu:** Xóa thể hiện Amazon RDS PostgreSQL Multi-AZ và cụm Amazon ElastiCache Redis.
3. **Lưu trữ:** Làm trống (empty) và xóa S3 bucket được dùng để host frontend tĩnh.
4. **Mạng & Bảo mật:** Xóa VPC tùy chỉnh, các subnet, internet gateway, NAT gateway và security group đã tạo ở Mục 5.3.
