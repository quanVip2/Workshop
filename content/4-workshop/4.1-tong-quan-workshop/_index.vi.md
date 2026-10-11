---
title: "Tổng quan Workshop"
weight: 1
pre: " <b> 4.1 </b> "
---

## Mục tiêu
Workshop này hướng dẫn triển khai ứng dụng **Hệ thống Xử lý Ảnh Tự động tích hợp AI (Enterprise Serverless Image Processor)** trên nền tảng đám mây AWS. 

Bằng cách kết hợp kiến trúc phi máy chủ (Serverless), các dịch vụ được quản lý (Managed Services), phân tích Machine Learning và mô hình hướng sự kiện (Event-driven Architecture), workshop sẽ giúp bạn xây dựng một giải pháp hoàn chỉnh (End-to-End). Sau khi hoàn thành, bạn sẽ sở hữu một hệ thống web có khả năng tự động mở rộng, tối ưu chi phí, nhận diện hình ảnh thông minh bằng Trí tuệ nhân tạo, và bảo mật định danh đa người dùng ở cấp độ doanh nghiệp.

## 1. Giới thiệu bài toán và giải pháp
Trong các hệ thống phần mềm hiện đại (như CMS, Thương mại điện tử), việc quản lý và tối ưu hóa tài sản kỹ thuật số là yêu cầu bắt buộc. Tuy nhiên, việc tự xây dựng máy chủ (EC2) để xử lý ảnh không chỉ lãng phí tài nguyên lúc nhàn rỗi mà còn tiềm ẩn rủi ro bảo mật dữ liệu.

Workshop này giải quyết bài toán trên bằng cách ứng dụng toàn diện hệ sinh thái AWS Serverless. Giao diện người dùng được lưu trữ trên Amazon S3 tĩnh hoặc Netlify. Dữ liệu định danh được quản lý chặt chẽ bởi **Amazon Cognito**, kết hợp cùng **Amazon API Gateway** để tạo thành một lớp lá chắn bảo vệ API vững chắc (API Protection).

Trái tim của hệ thống là cụm 4 hàm vi dịch vụ (Microservices) chạy trên **AWS Lambda** (Python 3.12). Khi có sự kiện ảnh được tải lên, Lambda sử dụng thư viện đồ họa Pillow để chuẩn hóa ảnh sang JPEG siêu nhẹ, đồng thời gọi dịch vụ **Amazon Rekognition** để dùng AI trích xuất các nhãn dán nội dung (AI Tags). Toàn bộ dữ liệu, bao gồm cả các chỉ số đo lường dung lượng gốc và dung lượng nén, được lưu vào cơ sở dữ liệu NoSQL **Amazon DynamoDB** để xuất ra Bảng thống kê (Dashboard) phân tích hiệu quả cho từng người dùng riêng biệt.

## 2. Kiến trúc hệ thống
Kiến trúc của hệ thống bao gồm các lớp thành phần chính sau:

* **Lớp Trình diễn (Presentation Layer):** Giao diện Web Frontend.
* **Lớp Xác thực & Bảo mật (Security Layer):** Quản lý người dùng, cấp Token và kiểm soát truy cập API.
* **Lớp Giao tiếp (API Layer):** Cổng REST API định tuyến request.
* **Lớp Tính toán phi máy chủ (Compute Layer):** Cụm 4 hàm Lambda (Upload, Download, History, Xử lý ảnh).
* **Lớp Trí tuệ nhân tạo (AI Layer):** Phân tích hình ảnh bằng Machine Learning.
* **Lớp Lưu trữ (Storage & Database Layer):** Lưu trữ File tĩnh và dữ liệu Metadata.
* **Lớp Giám sát (Monitoring):** Quản trị log và hiệu suất.

![Hình 1 – Kiến trúc hệ thống Xử lý ảnh tự động tích hợp AI](/Workshop/images/so_do.png)

## 3. Quy trình hoạt động của hệ thống
Luồng xử lý chính của hệ thống diễn ra theo 10 bước khép kín và bảo mật:

1. Người dùng truy cập website thông qua Frontend tĩnh.
2. Người dùng Đăng ký/Đăng nhập qua **Amazon Cognito**. Nếu thành công, Cognito cấp một **JWT Token** hợp lệ.
3. Trình duyệt gửi Request đính kèm JWT Token lên **Amazon API Gateway**. API Gateway kiểm tra tính hợp lệ của Token trước khi cho phép đi tiếp.
4. Hệ thống gọi hàm Lambda `GenerateUploadUrl` để xin cấp quyền. Lambda trả về một chữ ký bảo mật (**Presigned URL**). Trình duyệt dùng URL này đẩy ảnh trực tiếp lên S3 Input Bucket.
5. Sự kiện `s3:ObjectCreated` từ Input Bucket ngay lập tức kích hoạt (Trigger) hàm Lambda lõi `HamXuLyAnh`.
6. Hàm Lambda xử lý đồ họa: Tự động đổi định dạng mọi loại ảnh về chuẩn `.jpg`, thu nhỏ và nén kích thước.
7. Hàm Lambda gửi ảnh vừa nén qua **Amazon Rekognition** để AI phân tích và trích xuất các từ khóa (Tags).
8. Lambda lưu ảnh thành phẩm sang S3 Output Bucket; đồng thời ghi toàn bộ thông tin (Email sở hữu, Dung lượng gốc, Dung lượng nén, Nhãn dán AI) vào **Amazon DynamoDB**.
9. Trình duyệt người dùng gọi hàm Lambda `GetUserHistory` thông qua API Gateway để lấy dữ liệu. Hàm này chỉ truy vấn DynamoDB các bản ghi khớp với Email của người dùng hiện tại, tính toán tỷ lệ tiết kiệm dung lượng và đổ ra Bảng Dashboard thống kê.
10. Khi người dùng bấm "Xem", API Gateway tiếp tục gọi hàm Lambda `GenerateDownloadUrl` để cấp thêm một Presigned URL tạm thời, giúp người dùng tải/xem bức ảnh từ S3 Output một cách an toàn tuyệt đối.

![alt text](/Workshop/images/123.png)

## 4. Các dịch vụ AWS được sử dụng
Workshop ứng dụng một hệ sinh thái AWS Serverless toàn diện, bao gồm:

* **Tính toán & Trí tuệ nhân tạo (Compute & Machine Learning)**
  * AWS Lambda
  * Amazon Rekognition
* **Bảo mật & Phân phối API (Security & Network)**
  * Amazon Cognito (User Pools)
  * Amazon API Gateway
  * AWS Identity and Access Management (IAM)
* **Lưu trữ (Storage & Database)**
  * Amazon S3 (Object Storage & Block Public Access)
  * Amazon DynamoDB (NoSQL Database)
* **Giám sát (Monitoring)**
  * Amazon CloudWatch

## 5. Kết quả đạt được
Sau khi hoàn thành workshop, bạn sẽ làm chủ các kỹ năng đám mây nâng cao:

* Tích hợp hệ thống xác thực người dùng an toàn với Amazon Cognito User Pools và quản lý phiên đăng nhập qua chuẩn JWT.
* Bảo vệ REST API bằng cơ chế Amazon API Gateway Authorizer, ngăn chặn hoàn toàn các truy cập trái phép.
* Xây dựng luồng giao tiếp dữ liệu an toàn bằng kỹ thuật "chữ ký tạm thời" (Presigned URLs), loại bỏ rủi ro lộ khóa Access Key tĩnh.
* Triển khai kiến trúc vi dịch vụ (Microservices) bằng AWS Lambda để bóc tách các tác vụ: Cấp quyền Upload, Download, Lấy lịch sử và Xử lý ngầm.
* Ứng dụng mô hình Event-driven Architecture để kích hoạt quy trình nén ảnh tự động ngay khi có file mới.
* Tích hợp dịch vụ Machine Learning (Amazon Rekognition) vào hệ thống xử lý để tự động gán nhãn dán cho hình ảnh bằng AI.
* Thiết kế cơ sở dữ liệu NoSQL đa người dùng (Multi-tenant) với Amazon DynamoDB, phục vụ cho việc xây dựng Bảng thống kê Analytics Dashboard trực quan.
* Dọn dẹp và quản lý tài nguyên AWS theo thực hành tốt nhất (Best Practices) để tối ưu hóa chi phí.

![Ảnh các Lambda đã tạo(trừ hàm NoteHandler là của bạn em)](/Workshop/images/4/4.1/2.1.png)