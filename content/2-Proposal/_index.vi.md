---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---


In this section, you need to summarize the contents of the workshop that you **plan** to conduct.
Tại phần này, em xin tóm tắt các nội dung, mục tiêu và phương án triển khai kiến trúc hạ tầng AWS cho dự án Fashion E-commerce.

# Fashion E-commerce Platform

Giải pháp sàn thương mại điện tử thời trang với kiến trúc tối ưu chi phí và High Availability

## 1. Tóm tắt điều hành

Dự án Fashion E-commerce Platform được thiết kế nhằm xây dựng hệ thống mua sắm trực tuyến chuyên nghiệp, có khả năng chịu tải cao trong các đợt cao điểm, bảo mật nghiêm ngặt và tối ưu hóa chi phí vận hành Cloud. Hệ thống sử dụng React cho Frontend và Spring Boot cho Backend. Kiến trúc được triển khai theo tiêu chuẩn High Availability (Multi-AZ), kết hợp các kỹ thuật tối ưu hóa mạng (VPC Endpoints) để loại bỏ hoàn toàn các dịch vụ tốn kém như NAT Gateway, đảm bảo tính kinh tế cao nhất cho môi trường Demo.

## 2. Tuyên bố vấn đề

### Vấn đề hiện tại
Các hệ thống E-commerce truyền thống khi triển khai trên Cloud thường gặp thách thức lớn về chi phí hạ tầng mạng (đặc biệt là NAT Gateway đắt đỏ) và tính sẵn sàng không cao nếu không thiết kế theo tiêu chuẩn Multi-AZ. Ngoài ra, việc quản lý luồng CI/CD và truyền tải dữ liệu ảnh thường làm tăng độ trễ và chi phí duy trì.

### Giải pháp
Nền tảng sử dụng **Amazon CloudFront** để tối ưu hóa trải nghiệm người dùng toàn cầu. Hệ thống triển khai kiến trúc **Multi-AZ** với **Auto Scaling Group** cho EC2, sử dụng **Amazon ElastiCache** và **RDS PostgreSQL** với mô hình Cache-Aside để giảm tải Database. Đặc biệt, thay vì dùng NAT Gateway tốn phí, hệ thống sử dụng **VPC Gateway Endpoint** cho S3 và **Interface Endpoints** cho dịch vụ CI/CD, giúp truyền tải dữ liệu nội bộ bảo mật, tốc độ cao và miễn phí.

### Lợi ích và hoàn vốn đầu tư (ROI)
Giải pháp tạo nền tảng vững chắc, sẵn sàng cho việc mở rộng tính năng. Việc tối ưu hóa mạng giúp chi phí duy trì hàng tháng thấp hơn đáng kể so với kiến trúc thông thường. Nền tảng giảm thiểu rủi ro vận hành nhờ tính năng tự động Failover của RDS và ElastiCache, đồng thời tự động hóa hoàn toàn quy trình triển khai bằng CI/CD pipeline nội bộ AWS.

## 3. Kiến trúc giải pháp

Kiến trúc tập trung vào sự tối giản trong hạ tầng mạng nhưng tối đa hóa tính sẵn sàng. Toàn bộ Backend được ẩn mình trong Private Subnet, chỉ tiếp nhận traffic đã qua kiểm duyệt từ ALB.

![Architecture Diagram](/images/2-Proposal/Proposal.png)

### Dịch vụ AWS sử dụng

- Tầng Edge & Network: Amazon CloudFront, AWS WAF, ALB, VPC Endpoints.
- Tầng Compute: Amazon EC2 (Auto Scaling Group), Spring Boot.
- Tầng Data & Storage: Amazon RDS (PostgreSQL Multi-AZ), Amazon ElastiCache (Redis Multi-AZ), Amazon S3.
- Tầng CI/CD: GitHub, AWS CodePipeline, AWS CodeDeploy.
- Dịch vụ dùng chung: AWS IAM, AWS Secrets Manager, Amazon CloudWatch.

### Thiết kế thành phần

- Tầng Giao diện: Frontend ReactJS phân phối qua CloudFront/S3.
- Tầng Định tuyến: ALB đặt tại Public Subnet, điều hướng traffic tới Backend EC2 trong Private Subnet.
- Tầng Dữ liệu: Database và Cache được đặt tại các subnet riêng biệt, hỗ trợ đồng bộ dữ liệu liên vùng (Cross-AZ Sync).
- Tầng Lưu trữ ảnh: Sử dụng S3 thông qua VPC Gateway Endpoint để đảm bảo luồng lưu trữ ảnh sản phẩm luôn nội bộ và bảo mật.

## 4. Triển khai kỹ thuật

### Các giai đoạn triển khai

1. Thiết lập Mạng: Khởi tạo VPC, Public/Private Subnets, cấu hình IGW và VPC Endpoints.
2. Triển khai Tầng Lưu trữ & Dữ liệu: Thiết lập RDS và ElastiCache với cấu hình Multi-AZ.
3. Triển khai Tầng Tính toán: Build AMI cho EC2, cấu hình ASG kết hợp ALB.
4. Tích hợp CI/CD & Bảo mật: Thiết lập Pipeline kéo code từ GitHub, cấu hình IAM Role/Policy và hệ thống giám sát CloudWatch.

### Yêu cầu kỹ thuật

- Thông thạo ReactJS (UI/UX) và Spring Boot (RESTful API).
- Kiến thức chuyên sâu về VPC Routing, Multi-AZ Failover, và tối ưu chi phí AWS (Cost Optimization).
- Kỹ năng DevOps: Cấu hình Pipeline, CI/CD tự động và quản lý Secrets Manager.

## 5. Lộ trình & Mốc triển khai

- Giai đoạn 1 (Tuần 1-2): Phân tích yêu cầu, thiết kế cơ sở dữ liệu, xây dựng kiến trúc hệ thống và phát triển các API cốt lõi bằng Spring Boot. 

- Giai đoạn 2 (Tuần 3-4): Phát triển giao diện ReactJS, thiết lập VPC, Subnet, Security Group, Internet Gateway và triển khai Amazon RDS PostgreSQL. 
- Giai đoạn 3 (Tuần 5-6): Triển khai Backend lên EC2 thông qua Auto Scaling Group, cấu hình Application Load Balancer, tích hợp Amazon S3 và CloudFront. 
- Giai đoạn 4 (Tuần 7-8): Thiết lập CI/CD bằng CodePipeline và CodeDeploy, cấu hình CloudWatch, kiểm thử hiệu năng, bảo mật và khả năng chịu lỗi. 

## 6. Ước tính ngân sách

Dựa trên việc sử dụng các dịch vụ trong Free Tier và loại bỏ hoàn toàn chi phí NAT Gateway.
Amazon EC2 (2 t3.micro): 18,00 USD/tháng (Application Server, Auto Scaling Group).
Application Load Balancer (ALB): 8,00 USD/tháng (Cân bằng tải và định tuyến lưu lượng).
Amazon RDS PostgreSQL: 15,00 USD/tháng (Single DB cho môi trường Demo).
Amazon ElastiCache Redis: 10,00 USD/tháng (Caching dữ liệu, giảm tải Database).
Amazon S3 Standard: 2,00 USD/tháng (Lưu trữ hình ảnh sản phẩm và tài nguyên tĩnh).
Amazon CloudFront: 2,00 USD/tháng (Phân phối nội dung CDN).
AWS CodePipeline & CodeDeploy: 0,00 USD/tháng (Trong giới hạn Free Tier).
Amazon CloudWatch, IAM, Secrets Manager và VPC Endpoint: 2,00 USD/tháng.
Tổng: 57,00 USD/tháng, tương đương khoảng 684,00 USD/năm.

## 7. Đánh giá rủi ro

- Rủi ro mạng: Mất kết nối liên vùng (giảm thiểu bằng cấu hình Multi-AZ).
- Rủi ro chi phí: Tăng đột biến do traffic ngoài dự kiến (giảm thiểu bằng CloudWatch Billing Alarms).
- Rủi ro bảo mật: Lộ lọt thông tin Database (giảm thiểu bằng IAM Permissions Boundary và Secrets Manager).

## 8. Kết quả kỳ vọng

### Cải tiến kỹ thuật 
-Xây dựng thành công hệ thống thương mại điện tử thời trang theo kiến trúc Multi-tier trên AWS. 
- Hoàn thiện quy trình CI/CD tự động bằng AWS CodePipeline và CodeDeploy, giúp rút ngắn thời gian triển khai phiên bản mới. 
- Tăng cường bảo mật với Private Subnet, IAM, Security Group, Secrets Manager và VPC Endpoint. 
- Xây dựng quy trình triển khai phần mềm tự động hóa cao.

### Giá trị dài hạn 
- Dễ dàng tích hợp các dịch vụ AWS khác như AI/ML, hệ thống gợi ý sản phẩm, phân tích dữ liệu và thanh toán trực tuyến trong tương lai. 
- Có thể tái sử dụng kiến trúc cho các dự án thương mại điện tử hoặc hệ thống web quy mô tương tự, góp phần giảm thời gian triển khai và chi phí phát triển các dự án sau. 
- Tạo nền tảng hạ tầng Cloud có khả năng mở rộng để phục vụ số lượng người dùng và đơn hàng ngày càng tăng. 
