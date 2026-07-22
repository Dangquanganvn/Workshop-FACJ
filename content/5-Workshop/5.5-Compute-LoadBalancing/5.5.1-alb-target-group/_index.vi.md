---
title: "ALB & Target Group"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.5.1. </b> "
---

Trong phần này, chúng ta sẽ cấu hình Application Load Balancer (ALB) và các Target Group để định tuyến lưu lượng bên ngoài vào các máy chủ ứng dụng backend.

#### 1. Cấu hình Application Load Balancer và Target Groups

- **ALB hướng ngoại (Public-Facing):** Được triển khai trải rộng trên các **Public Subnets** để đóng vai trò là điểm entry duy nhất cho mọi yêu cầu HTTP/HTTPS của khách hàng vào nền tảng e-commerce.
- **Target Groups:** Định tuyến các request đến các instance Spring Boot backend nằm trong private subnets, sử dụng các tiêu chuẩn kiểm tra sức khỏe nghiêm ngặt để chuyển hướng lưu lượng hiệu quả.
- **Tích hợp Bảo mật:** Được liên kết với ALB Security Group cho phép lưu lượng truy cập từ internet đi vào đồng thời thực thi các giao thức truyền thông bảo mật.

![ALB and Target Group Setup](/images/5-Workshop/5.5-compute/alb-target-group.png)
_*Hình: Cấu hình định tuyến của Application Load Balancer và Target Group.*_

#### 2. Cấu hình Health Check của Target Group

- **Đường dẫn Health Check:** Được cấu hình với một endpoint cụ thể (như `/actuator/health`) để giám sát liên tục trạng thái hoạt động của các node ứng dụng backend.
- **Ngưỡng & Khoảng thời gian:** Thiết lập thời gian timeout, ngưỡng đánh giá healthy/unhealthy và mã phản hồi thành công (`200`) phù hợp để đảm bảo lưu lượng chỉ được phân phối độc quyền tới các máy chủ đang hoạt động tốt, tránh gián đoạn dịch vụ khi triển khai hoặc xảy ra sự cố.

![Target Group Health Check Configuration](/images/5-Workshop/5.5-compute/target-group-health-check.png)
_*Hình: Cấu hình health check của Target Group đảm bảo tính sẵn sàng cho các node backend.*_
