---
title: "Thiết lập Tầng Dữ liệu"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

# Tổng quan Chi tiết về Tầng Dữ liệu & Caching

Trong phần này, chúng ta sẽ triển khai tầng lưu trữ dữ liệu bền vững và caching có tính sẵn sàng cao cho hệ thống **Fashion E-commerce Platform** . Một tầng dữ liệu mạnh mẽ, khả năng mở rộng cao và bảo mật chặt chẽ đóng vai trò cốt lõi trong việc xử lý các giao dịch đồng thời của người dùng, duy trì tính toàn vẹn của phiên đăng nhập và mang lại tốc độ truy vấn danh mục sản phẩm cực nhanh trong các đợt cao điểm mua sắm.

### Tổng quan Kiến trúc

Tầng dữ liệu và caching được phân tách thành hai thành phần chính, được cô lập hoàn toàn bên trong các private subnet chuyên dụng nhằm tối đa hóa bảo mật và hạn chế tối đa các điểm nghẽn về hiệu năng:

1. **Tầng Cơ sở dữ liệu Giao dịch (Amazon RDS PostgreSQL Multi-AZ):**
   - **Lưu trữ & Toàn vẹn dữ liệu:** Đóng vai trò là nguồn dữ liệu cốt lõi (Source of Truth) cho toàn bộ hệ sinh thái e-commerce, lưu trữ an toàn các dữ liệu quan hệ như tài khoản người dùng, kho hàng, bảng giá chi tiết, lịch sử đơn hàng và các giao dịch thanh toán.
   - **Tính sẵn sàng cao & Phục hồi thảm họa:** Được triển khai trải rộng trên nhiều Availability Zone với một thể hiện dự phòng đồng bộ (synchronous standby). Điều này đảm bảo khả năng chuyển đổi dự phòng tự động (failover), loại bỏ hoàn toàn điểm đơn lẻ gây lỗi (Single Point of Failure) và duy trì hoạt động kinh doanh liên tục ngay cả khi xảy ra sự cố hạ tầng ở cấp độ vùng.

2. **Tầng Caching & Quản lý Phiên (Amazon ElastiCache Redis):**
   - **Quản lý Phiên người dùng:** Giảm tải các tác vụ đọc/ghi tần suất cao (như trạng thái giỏ hàng và token xác thực) khỏi cơ sở dữ liệu quan hệ chính.
   - **Tăng tốc Danh mục sản phẩm:** Lưu cache các thuộc tính sản phẩm hot hoặc dữ liệu chương trình flash-sale để mang lại thời gian phản hồi dưới một mili-giây, qua đó giảm mạnh tải CPU của database và đảm bảo trải nghiệm mượt mà cho người dùng dưới tải truy cập lớn.

### Phân bổ Subnet & Bảo mật

- **Cô lập Mạng:** Cả hai dịch vụ RDS và ElastiCache đều nằm hoàn toàn bên trong các **DB Subnets** và **Cache Subnets** không định tuyến ra ngoài internet được thiết lập từ giai đoạn cấu hình mạng. Chúng hoàn toàn không có IP công cộng và không thể truy cập trực tiếp từ Internet.
- **Kiểm soát Truy cập Chặt chẽ:** Được bảo vệ bởi các security group riêng biệt, chỉ cho phép lưu lượng truy cập đi vào bắt nguồn độc quyền từ các máy chủ ứng dụng backend.
