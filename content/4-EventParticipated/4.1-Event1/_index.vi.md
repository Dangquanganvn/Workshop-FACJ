---
title: "Meetup 1"
date: 2026-06-06
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---



# Buổi Meetup Ngày 6 tháng 6 năm 2026

### Mục Đích Của Sự Kiện

- Chia sẻ cách làm việc nhóm hiệu quả
- Chia sẻ hành trình tự học và lộ trình chuyển sang Cloud/DevOps
- Chia sẻ cách xây dựng ứng dụng GraphRAG bằng Amazon Bedrock và Amazon Neptune.
- Chia sẻ về cách Kết nối các Client Godot với AWS WebSockets
- Chia sẻ về cách sử dung Docker 
- Chia sẻ về Hệ thống phát hiện xâm nhập mạng (NIDS) dựa trên học máy trên AWS


### Danh Sách Diễn Giả

- Nguyễn Quốc Bảo - Chia sẻ về cách Kết nối các Client Godot với AWS WebSockets
- Huỳnh Nguyễn Quốc bảo - Chia sẻ về cách sử dung Docker 
- Lê Hoàng Gia Đại - Chia sẻ về Hệ thống phát hiện xâm nhập mạng (NIDS) dựa trên học máy trên AWS
- Trần Trung Vinh - Chia sẻ hành trình tự học và lộ trình chuyển sang Cloud/DevOps
- Việt Phát - Chia sẻ cách xây dựng ứng dụng GraphRAG bằng Amazon Bedrock và Amazon Neptune.
- Trương Huy Phước - Chia sẻ cách làm việc nhóm hiệu quả

### Nội Dung Nổi Bật
- Chia sẻ về cách sử dung Docker 

#### Các ảnh hưởng tiêu cực của kiến trúc ứng dụng cũ

- Copy code từ máy này qua máy khác → Mất thời gian 
- Dễ lỗi do thiếu thư viện 

#### Chuyển đổi sang kiến trúc ứng dụng mới 

- Containerization: Đóng gói ứng dụng cùng toàn bộ thư viện và môi trường chạy vào Container.
- Fast Deployment: Triển khai ứng dụng nhanh chóng, giảm thời gian cài đặt và cấu hình.
- Resource Optimization: Container sử dụng ít tài nguyên hơn so với máy ảo vì chia sẻ nhân hệ điều hành.
- Portability: Có thể di chuyển và chạy ứng dụng trên nhiều nền tảng khác nhau mà không cần thay đổi cấu hình.

#### Domain-Driven Design (DDD)

- Business Domain: Phân tích và hiểu rõ bài toán nghiệp vụ trước khi thiết kế hệ thống.
- Domain Events: Xác định các sự kiện quan trọng xảy ra trong quá trình xử lý nghiệp vụ.
- Bounded Context: Chia hệ thống thành nhiều miền chức năng độc lập để giảm sự phụ thuộc giữa các thành phần.
- Ubiquitous Language: Xây dựng ngôn ngữ chung giữa đội ngũ phát triển và bộ phận nghiệp vụ nhằm hạn chế hiểu sai yêu cầu.
- Event Storming: Phương pháp làm việc nhóm giúp xác định quy trình nghiệp vụ, các sự kiện và mối quan hệ giữa chúng trước khi triển khai hệ thống.
- Context Mapping: Xác định mối quan hệ và cách giao tiếp giữa các Bounded Context trong cùng một hệ thống.


#### Event-Driven Architecture

- Event Producer: Thành phần phát sinh sự kiện khi có một hành động hoặc thay đổi trạng thái xảy ra (ví dụ: đơn hàng được tạo, người dùng đăng ký).
- Event Router/Broker: Trung gian tiếp nhận và định tuyến sự kiện đến đúng nơi cần xử lý (ví dụ: Amazon EventBridge, Amazon SNS, Amazon SQS, Kafka).
- Event Consumer: Thành phần lắng nghe và xử lý sự kiện khi được gửi tới.

#### Compute Evolution

- Virtualization → Containerization: Từ mô hình máy ảo (mỗi VM có hệ điều hành riêng, nặng và tốn tài nguyên) chuyển sang container (chia sẻ chung Host OS, khởi động nhanh, nhẹ hơn nhiều).
- VM vs Container: VM cần hypervisor và guest OS riêng cho từng ứng dụng, boot mất vài phút; container chỉ cần container engine, boot chỉ mất vài mili-giây và cho hiệu năng gần như native.
- Mật độ triển khai: Một server vật lý có thể chạy 10-100 VM, nhưng có thể chạy đến 100-1000 container, giúp tận dụng tài nguyên hiệu quả hơn rất nhiều.


#### Amazon Q Developer

- **SDLC automation**: Từ planning đến maintenance
- **Code transformation**: Java upgrade, .NET modernization
- **AWS Transform agents**: VMware, Mainframe, .NET migration

### Những Gì Học Được

#### Tư Duy Thiết Kế

- So sánh trước khi chọn công nghệ: Hiểu rõ sự khác biệt giữa virtualization và containerization giúp đưa ra quyết định kiến trúc phù hợp với từng bài toán, thay vì mặc định dùng VM cho mọi trường hợp.
- Trade-off giữa isolation và hiệu năng: VM có tính cô lập và bảo mật cao hơn (fully isolated), trong khi container ưu tiên tốc độ và mật độ triển khai (process-level security) — cần cân nhắc tùy theo yêu cầu bảo mật của hệ thống.
- Tư duy "package everything": Đóng gói ứng dụng cùng toàn bộ môi trường chạy giúp loại bỏ vấn đề "chạy được trên máy tôi nhưng không chạy được trên máy bạn".

#### Kiến Trúc Kỹ Thuật

- Cấu trúc phân lớp của container: Kernel → Base Image → các Image trung gian (thêm package, thư viện) → Container writable layer trên cùng — hiểu rõ cơ chế này giúp tối ưu Dockerfile và kích thước image.
- Docker Engine nằm giữa Host OS và ứng dụng: Cho phép nhiều container cùng chia sẻ một Host OS nhưng vẫn chạy độc lập với nhau, khác hẳn với việc mỗi VM phải có Guest OS riêng.
- Dockerfile là "công thức" build image: Các chỉ thị như FROM, ARG, RUN, WORKDIR, COPY, CMD/ENTRYPOINT quyết định cách image được build và ứng dụng được khởi chạy.

#### Chiến Lược Hiện Đại Hóa

- Container hóa ứng dụng cũ: Đóng gói lại các ứng dụng legacy vào container giúp dễ dàng di chuyển (portability) sang nhiều môi trường khác nhau (physical, virtual, cloud) mà không cần thay đổi cấu hình.
- Tối ưu chi phí hạ tầng: Nhờ tính lightweight và khả năng chạy nhiều ứng dụng trên cùng một host, containerization giúp giảm chi phí infrastructure so với dùng nhiều VM riêng lẻ.
- Không vội vàng, thử nghiệm dần: Nên bắt đầu container hóa từ những service nhỏ, ít rủi ro trước khi áp dụng cho toàn bộ hệ thống.

### Ứng Dụng Vào Công Việc

- Container hóa các service hiện có: Đóng gói ứng dụng đang phát triển thành Docker image để đảm bảo môi trường chạy nhất quán giữa local, staging và production.
- Xây dựng CI/CD pipeline với Docker: Tận dụng Docker image làm đơn vị triển khai chuẩn hóa trong pipeline, giảm lỗi do khác biệt môi trường.
- Áp dụng cho kiến trúc microservices: Mỗi service chạy trong container riêng, dễ scale độc lập và triển khai nhanh hơn.
- Thử nghiệm Docker Compose: Quản lý nhiều container liên quan (ứng dụng + database + cache...) trong cùng một stack khai báo, thay vì chạy từng container thủ công.
- Tối ưu Dockerfile: Áp dụng hiểu biết về layer caching để viết Dockerfile hiệu quả hơn, giảm thời gian build.

### Trải nghiệm trong event

- Tham gia buổi meetup là một trải nghiệm rất bổ ích, đặc biệt với phần chia sẻ về Docker — một chủ đề tuy quen thuộc nhưng được trình bày theo hướng gần gũi, dễ hiểu và có phần hài hước.

#### Học hỏi từ các diễn giả có chuyên môn cao
- Diễn giả Huỳnh Nguyễn Quốc Bảo (Junior Cloud Native Developer tại Endava Vietnam, Founder ITea Lab) đã trình bày Docker theo hướng "a friendly intro", không đi sâu học thuật mà tập trung vào trực giác và ví dụ thực tế.
- Cách dẫn dắt từ vấn đề của virtualization (VM nặng, tốn tài nguyên) sang giải pháp containerization giúp người nghe dễ dàng thấy được lý do vì sao Docker ra đời và được ưa chuộng.

#### Trải nghiệm kỹ thuật thực tế
- Được xem trực tiếp phần demo Docker, từ việc build image bằng Dockerfile đến chạy container, giúp hình dung rõ hơn quy trình thực tế thay vì chỉ đọc lý thuyết.
- Hiểu sâu hơn về cơ chế layer caching: khi thay đổi một dòng trong Dockerfile, chỉ những layer từ đó trở đi mới bị rebuild, giúp tối ưu thời gian build trong thực tế.
- Nắm được bộ lệnh Docker CLI cơ bản (image, container lifecycle, network, volume, docker-compose) để có thể tự thao tác ngay sau buổi chia sẻ.

#### Ứng dụng công cụ hiện đại
- Trực tiếp tìm hiểu cách Docker đóng gói ứng dụng cùng toàn bộ dependency, giải quyết triệt để vấn đề "thiếu thư viện" hay "khác môi trường" từng gặp khi làm việc nhóm.
- Học được cách phân biệt khi nào nên dùng container thay vì VM truyền thống, dựa trên tiêu chí về hiệu năng, mật độ triển khai và mức độ cô lập cần thiết.

#### Kết nối và trao đổi
- Buổi chia sẻ được tổ chức theo phong cách **"relaxed, fun, and interactive"**, tạo không khí thoải mái để đặt câu hỏi và trao đổi trực tiếp với diễn giả.
- Có cơ hội trao đổi với các bạn cùng tham gia về kinh nghiệm sử dụng Docker trong các dự án cá nhân và công việc thực tế.

#### Bài học rút ra

- Việc chọn giữa VM và container không phải là "cái nào tốt hơn tuyệt đối" mà là **lựa chọn phù hợp với bài toán**: bảo mật/cô lập cao thì ưu tiên VM, cần nhẹ và mở rộng nhanh thì ưu tiên container.
- Docker không chỉ là công cụ dành cho DevOps chuyên sâu — với tư duy "friendly intro", ai cũng có thể bắt đầu thử nghiệm và áp dụng vào công việc hàng ngày.
- Việc hiểu cơ chế layer của Docker image giúp viết Dockerfile tối ưu hơn, tiết kiệm thời gian build và dung lượng image trong thực tế.

#### Một số hình ảnh khi tham gia sự kiện
* Thêm các hình ảnh của các bạn tại đây
> Tổng thể, sự kiện không chỉ cung cấp kiến thức kỹ thuật mà còn giúp tôi thay đổi cách tư duy về thiết kế ứng dụng, hiện đại hóa hệ thống và phối hợp hiệu quả hơn giữa các team.
