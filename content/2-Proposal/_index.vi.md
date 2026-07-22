---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

<!-- {{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}} -->

<!-- Tại phần này, bạn cần tóm tắt các nội dung trong workshop mà bạn **dự tính** sẽ làm. -->

# Nền tảng Thương mại Điện tử Thời trang (Fashion E-commerce Platform)

## Giải pháp kiến trúc AWS hợp nhất tối ưu hóa chi phí và đảm bảo tính sẵn sàng cao

### 1. Tóm tắt điều hành

Dự án Nền tảng Thương mại Điện tử Thời trang được thiết kế nhằm cung cấp trải nghiệm mua sắm trực tuyến chuyên nghiệp, bảo mật và có khả năng mở rộng cao, đáp ứng lưu lượng truy cập lớn trong các đợt cao điểm mua sắm. Hệ thống sử dụng **React** cho giao diện người dùng và **Spring Boot** cho phía máy chủ. Kiến trúc được triển khai theo tiêu chuẩn **Sẵn sàng cao (Multi-AZ)**, tích hợp các kỹ thuật mạng nâng cao như **VPC Endpoints** để loại bỏ hoàn toàn các dịch vụ tốn kém như NAT Gateway, đảm bảo hiệu quả chi phí tối ưu cho môi trường đám mây.

### 2. Tuyên bố vấn đề

#### Vấn đề là gì?

Các hệ thống thương mại điện tử truyền thống khi triển khai trên môi trường đám mây thường phải đối mặt với thách thức lớn về chi phí hạ tầng mạng — đặc biệt là phí NAT Gateway đắt đỏ — và thiếu tính sẵn sàng cao nếu không được thiết kế theo tiêu chuẩn Multi-AZ. Ngoài ra, việc vận hành các luồng CI/CD và truyền tải tài sản đa phương tiện thường làm tăng độ trễ và chi phí duy trì.

#### Giải pháp

Nền tảng sử dụng **Amazon CloudFront** để tối ưu hóa trải nghiệm người dùng toàn cầu. Hệ thống triển khai kiến trúc **Multi-AZ** với nhóm tự động mở rộng (**Auto Scaling Group**) cho EC2, sử dụng **Amazon ElastiCache** và **RDS PostgreSQL** theo mô hình Cache-Aside để giảm tải cho cơ sở dữ liệu. Quan trọng hơn, thay vì sử dụng NAT Gateway tốn kém, hệ thống tận dụng **VPC Gateway Endpoints** cho S3 và **Interface Endpoints** cho các dịch vụ CI/CD, đảm bảo truyền tải dữ liệu nội bộ bảo mật, tốc độ cao và miễn phí.

#### Lợi ích và Tỷ suất hoàn vốn (ROI)

Giải pháp tạo nền tảng vững chắc, sẵn sàng cho việc mở rộng tính năng trong tương lai. Việc tối ưu hóa mạng lưới giúp giảm đáng kể chi phí duy trì hàng tháng so với các kiến trúc thông thường. Nền tảng giảm thiểu rủi ro vận hành nhờ khả năng tự động chuyển đổi dự phòng (failover) của RDS và ElastiCache, đồng thời tự động hóa hoàn toàn quy trình triển khai bằng các pipeline CI/CD gốc trên AWS.

### 3. Kiến trúc giải pháp

Kiến trúc tập trung vào sự đơn giản trong thiết kế mạng nhưng tối đa hóa tính sẵn sàng. Toàn bộ máy chủ backend được cách ly trong các Private Subnet, chỉ tiếp nhận lưu lượng đã được lọc qua ALB. Kiến trúc chi tiết được thể hiện bên dưới:

![Fashion E-commerce Architecture](/images/2-Proposal/Proposal.png)

#### Các dịch vụ AWS được sử dụng

- **Tầng Biên & Mạng (Edge & Network Layer)**: Amazon CloudFront, AWS WAF, ALB, VPC Endpoints.
- **Tầng Tính toán (Compute Layer)**: Amazon EC2 (Auto Scaling Group), Spring Boot.
- **Tầng Dữ liệu & Lưu trữ (Data & Storage Layer)**: Amazon RDS (PostgreSQL Multi-AZ), Amazon ElastiCache (Redis Multi-AZ), Amazon S3.
- **Tầng CI/CD**: GitHub, AWS CodePipeline, AWS CodeDeploy.
- **Dịch vụ dùng chung (Shared Services)**: AWS IAM, AWS Key Management Service (KMS), Amazon CloudWatch.

#### Thiết kế thành phần

- **Tầng Giao diện (Frontend Layer)**: Giao diện ReactJS phân phối qua CloudFront/S3.
- **Tầng Định tuyến (Routing Layer)**: ALB đặt tại Public Subnet, điều hướng lưu lượng đến các instance EC2 Backend trong Private Subnet.
- **Tầng Dữ liệu (Data Layer)**: Cơ sở dữ liệu và Cache lưu trữ trong các subnet chuyên biệt hỗ trợ đồng bộ chéo giữa các Availability Zone (Cross-AZ).
- **Tầng Lưu trữ ảnh (Image Storage Layer)**: Sử dụng S3 thông qua VPC Gateway Endpoints để đảm bảo xử lý hình ảnh sản phẩm nội bộ và bảo mật.

### 4. Triển khai kỹ thuật

#### Các giai đoạn triển khai

- **Giai đoạn 1 (Tháng 1)**: Phân tích yêu cầu, thiết kế cơ sở dữ liệu, lập kế hoạch kiến trúc hệ thống và phát triển các API cốt lõi bằng Spring Boot.
- **Giai đoạn 2 (Tháng 2)**: Phát triển giao diện ReactJS, thiết lập VPC, subnet, security group, Internet Gateway, cùng với việc triển khai Amazon RDS PostgreSQL và máy chủ backend trên EC2.
- **Giai đoạn 3 (Tháng 3)**: Tích hợp Amazon S3, CloudFront, thiết lập CI/CD qua CodePipeline và CodeDeploy, cấu hình CloudWatch, kiểm thử bảo mật và hệ thống.

#### Yêu cầu kỹ thuật

- Thành thạo ReactJS (UI/UX) và Spring Boot (RESTful APIs).
- Hiểu biết sâu sắc về định tuyến VPC, chuyển đổi dự phòng Multi-AZ và Tối ưu hóa chi phí AWS.
- Kỹ năng DevOps: Cấu hình pipeline, tự động hóa CI/CD và quản lý Secrets Manager.

### 5. Lộ trình & Mốc triển khai

#### Lộ trình dự án

- **Thời gian thực tập (Tháng 1-3)**: Tổng cộng 3 tháng triển khai.
  - Tháng 1: Thiết kế & API Backend cốt lõi.
  - Tháng 2: Thiết lập Frontend, Mạng & Tích hợp tính toán.
  - Tháng 3: Pipeline CI/CD, Giám sát & Kiểm thử.
- **Sau khi ra mắt**: Tiếp tục tối ưu hóa và bảo trì hệ thống.

### 6. Ước tính ngân sách

Được ước tính dựa trên việc sử dụng trong hạn mức Free Tier và loại bỏ hoàn toàn chi phí NAT Gateway.

#### Chi phí hạ tầng

- **Amazon EC2 (2 t3.micro)**: 18,00 USD/tháng (Máy chủ ứng dụng, Auto Scaling Group).
- **Application Load Balancer (ALB)**: 8,00 USD/tháng (Cân bằng tải và định tuyến lưu lượng).
- **Amazon RDS PostgreSQL**: 15,00 USD/tháng (DB đơn cho môi trường Demo).
- **Amazon ElastiCache Redis**: 10,00 USD/tháng (Lưu trữ cache, giảm tải cho database).
- **Amazon S3 Standard**: 2,00 USD/tháng (Lưu trữ ảnh sản phẩm và tài nguyên tĩnh).
- **Amazon CloudFront**: 2,00 USD/tháng (Phân phối nội dung CDN).
- **AWS CodePipeline & CodeDeploy**: 0,00 USD/tháng (Trong giới hạn Free Tier).
- **Amazon CloudWatch, IAM, Secrets Manager & VPC Endpoint**: 2,00 USD/tháng.
- **Tổng cộng**: 57,00 USD/tháng, tương đương khoảng 684,00 USD/năm.

### 7. Đánh giá rủi ro

#### Ma trận rủi ro

- **Sự cố mạng**: Tác động trung bình, xác suất trung bình.
- **Biến động chi phí**: Tác động trung bình, xác suất thấp.
- **Lỗ hổng bảo mật**: Tác động cao, xác suất thấp.

#### Chiến lược giảm thiểu

- **Mạng**: Triển khai Multi-AZ để đảm bảo tính sẵn sàng cao và hỗ trợ chuyển đổi dự phòng.
- **Chi phí**: Cấu hình cảnh báo hóa đơn (CloudWatch billing alarms) để theo dõi các chi phí phát sinh bất thường.
- **Bảo mật**: Sử dụng IAM Permissions Boundary, WAF và Secrets Manager để bảo vệ thông tin xác thực và quyền truy cập database.

### 8. Kết quả kỳ vọng

#### Cải tiến kỹ thuật:

- Triển khai thành công hệ thống thương mại điện tử thời trang đa tầng trên AWS.
- Xây dựng hoàn chỉnh pipeline CI/CD tự động sử dụng AWS CodePipeline và CodeDeploy để phát hành phiên bản mới nhanh chóng.
- Tăng cường bảo mật tận dụng Private Subnet, IAM, Security Groups, Secrets Manager và VPC Endpoints.

#### Giá trị dài hạn:

- Dễ dàng mở rộng để tích hợp các dịch vụ AWS khác như hệ thống gợi ý AI/ML hoặc phân tích dữ liệu.
- Mẫu kiến trúc có thể tái sử dụng cho các dự án web quy mô tương tự, giúp rút ngắn thời gian đưa sản phẩm ra thị trường và giảm chi phí phát triển.
