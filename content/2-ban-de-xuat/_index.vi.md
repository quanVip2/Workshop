---
title: "Đề xuất"
weight: 2
pre: " <b> 2. </b> "
---

# HỆ THỐNG TỰ ĐỘNG XỬ LÝ HÌNH ẢNH SERVERLESS TÍCH HỢP AI (ENTERPRISE SERVERLESS IMAGE PROCESSOR)

## 1. Thông tin chung (General Information)

* **Tên đề tài (Project Title):** Xây dựng hệ thống tự động xử lý hình ảnh phi máy chủ tích hợp AI và bảo mật định danh trên AWS.
* **Thành viên thực hiện (Author):** Nguyễn Hồng Quân
* **Bối cảnh (Context):** Trong các ứng dụng web và nền tảng SaaS hiện đại, việc quản lý tài sản kỹ thuật số (hình ảnh) đòi hỏi khắt khe về tốc độ tải, bảo mật dữ liệu người dùng và khả năng phân tích thông minh. Đề tài này xây dựng một giải pháp hoàn chỉnh (End-to-End) ứng dụng mô hình hướng sự kiện (Event-driven), xác thực người dùng an toàn và phân tích Trí tuệ nhân tạo (AI) hoàn toàn trên nền tảng đám mây AWS.

## 2. Bài toán và Mục tiêu (Problem Statement & Objectives)

### 2.1. Bối cảnh và Bài toán (Context & Problem)
* **Hệ thống dùng để làm gì?** Hệ thống cung cấp nền tảng quản lý hình ảnh cá nhân hóa. Người dùng sau khi đăng nhập an toàn có thể tải ảnh lên. Hệ thống tự động nén, chuyển đổi định dạng (JPEG), trích xuất từ khóa bằng AI (Rekognition), và lưu trữ lịch sử dữ liệu riêng biệt cho từng tài khoản cùng bảng thống kê dung lượng tiết kiệm.
* **Đối tượng sử dụng (Target Users):** Các nền tảng thương mại điện tử, hệ thống quản lý nội dung (CMS), hoặc các ứng dụng SaaS cần một luồng xử lý ảnh đa người dùng (Multi-tenant) bảo mật tuyệt đối.
* **Vấn đề giải quyết (Problem Solved):** Loại bỏ chi phí duy trì máy chủ truyền thống, giải quyết bài toán lộ lọt dữ liệu qua việc cấp quyền truy cập tạm thời (Presigned URL), và tự động hóa khâu phân loại hình ảnh bằng AI thay vì gắn thẻ thủ công.

### 2.2. Mục tiêu cụ thể (Specific Objectives)
* **Output mong muốn:**
  * Hệ thống xác thực người dùng và bảo vệ API bằng JWT Token.
  * Cụm 4 hàm AWS Lambda đảm nhiệm các vai trò vi dịch vụ độc lập (Microservices).
  * Ứng dụng AI để tự động gắn nhãn nội dung (Labels) cho ảnh.
  * Bảng điều khiển (Dashboard) thống kê lịch sử và hiệu quả tối ưu dung lượng của từng cá nhân.
* **Tiêu chí đánh giá thành công (Success Criteria):**
  * Quá trình xác thực, cấp quyền, nén ảnh và phân tích AI diễn ra tự động hoàn toàn dưới 5 giây.
  * 100% kho lưu trữ S3 được khóa kín (Block Public Access), người dùng chỉ tải/xem ảnh thông qua chữ ký bảo mật hợp lệ.
  * Thông tin của tài khoản nào chỉ được phép truy xuất và hiển thị cho chính tài khoản đó.

## 3. Kiến trúc và Thiết kế Kỹ thuật (Architecture & Technical Design)

### Sơ đồ kiến trúc (Architecture Diagram)
![Sơ đồ kiến trúc Hệ thống Tự động xử lý hình ảnh Serverless](/Workshop/images/so_do.png)

### 3.1. Các dịch vụ AWS sử dụng (AWS Services Selection)
* **Amazon Cognito:** Quản lý định danh, đăng ký/đăng nhập và cấp phát JWT Token bảo mật.
* **Amazon API Gateway:** Cổng giao tiếp REST API trung tâm, kết hợp JWT Authorizer để chặn các truy cập trái phép.
* **AWS Lambda:** Đóng vai trò lõi xử lý với 4 hàm độc lập: Cấp quyền Upload (`GenerateUploadUrl`), Cấp quyền Download (`GenerateDownloadUrl`), Truy vấn Lịch sử (`GetUserHistory`) và Xử lý ảnh tự động (`HamXuLyAnh`).
* **Amazon Rekognition (AI):** Dịch vụ Trí tuệ nhân tạo (Machine Learning) tự động phân tích thị giác và trích xuất nhãn dán (Tags) từ bức ảnh tải lên.
* **Amazon S3 (Simple Storage Service):** Lưu trữ Frontend (Static Web Hosting), Input Bucket (Ảnh gốc) và Output Bucket (Ảnh JPEG đã nén).
* **Amazon DynamoDB:** Cơ sở dữ liệu NoSQL hiệu năng cao lưu trữ metadata, email sở hữu, dung lượng nén và từ khóa AI.
* **Amazon CloudWatch:** Giám sát, thu thập log và đo lường hiệu suất toàn hệ thống.

### 3.2. Bảo mật và Nguyên tắc Least Privilege (Security & IAM)
* **Bảo mật Frontend - Backend:** Không sử dụng Access Key tĩnh trong mã nguồn. Mọi luồng truy cập file đều sử dụng **Presigned URL** (URL có thời hạn 5 phút).
* **Quản lý quyền IAM:** Tách biệt Roles cho từng hàm Lambda tuân thủ nguyên tắc Least Privilege (VD: Hàm `GenerateUploadUrl` chỉ có quyền S3 PutObject, không có quyền xóa hay đọc DB).

## 4. Rủi ro Tiềm ẩn và Hướng giải quyết (Potential Risks & Mitigation)

* **Rủi ro 1: Tấn công trực tiếp vào kho lưu trữ S3 (Direct Access Data Breach)**
  * *Hướng giải quyết:* Cấu hình S3 Block Public Access toàn cục. Mọi hành động Tải lên/Tải xuống bắt buộc phải đi qua cụm API Gateway + Lambda để xin chữ ký tạm thời (Presigned URL) dựa trên Token của Cognito.
* **Rủi ro 2: Lỗi định dạng và ký tự đặc biệt khi Upload**
  * *Hướng giải quyết:* Lambda tạo link Upload tự động cắt bỏ tên gốc chứa ký tự nhạy cảm, thay thế bằng UUID kết hợp Email (VD: `user---upload_id.jpg`) để định danh người dùng và ngăn chặn lỗi HTTP 403 Signature.
* **Rủi ro 3: Lỗi vòng lặp sự kiện (Infinite Loop Event Trigger)**
  * *Hướng giải quyết:* Tách biệt 2 Bucket (Input Bucket riêng và Output Bucket riêng). Đảm bảo hàm `HamXuLyAnh` chỉ được Trigger từ Input, và trả kết quả sang Output.

## 5. Kế hoạch Triển khai Lab (Implementation Lab Steps)

Dự án được triển khai qua các bước chuẩn hóa end-to-end:
* **Bước 1:** Khởi tạo Amazon Cognito User Pool để quản lý tài khoản.
* **Bước 2:** Xây dựng kho lưu trữ Amazon S3 (Input, Output, Static Web) và bảng DynamoDB.
* **Bước 3:** Cấu hình IAM Policies & Roles chi tiết cho các dịch vụ.
* **Bước 4:** Lập trình cụm 4 hàm AWS Lambda xử lý logic (Python) kết hợp thư viện Pillow (Xử lý đồ họa) và Boto3.
* **Bước 5:** Xây dựng Amazon API Gateway, tích hợp Cognito Authorizer và cấu hình CORS an toàn.
* **Bước 6:** Tích hợp tính năng AI Amazon Rekognition vào luồng xử lý ảnh tự động (S3 Trigger).
* **Bước 7:** Tích hợp mã nguồn Frontend (HTML/JS) gọi API, kiểm thử phân luồng đa người dùng (Multi-tenant) và Dashboard thống kê.

## 6. Đóng góp Cá nhân và Sáng tạo (Personal Contributions & Innovations)

Khác với các bài lab cơ bản, dự án này đã được nâng cấp với các tính năng mang tính sáng tạo cao:
* **Tích hợp Trí tuệ nhân tạo (AI):** Tự động nhận diện chủ thể bức ảnh và gán nhãn thông minh bằng Machine Learning (Amazon Rekognition).
* **Kiến trúc Đa người dùng (Multi-tenant):** Hệ thống có khả năng nhận diện email chủ sở hữu, lưu trữ lịch sử tách biệt và bảo mật quyền riêng tư cho từng cá nhân.
* **Bảng điều khiển Thống kê (Analytics Dashboard):** Frontend tự động tính toán tổng số ảnh, dung lượng gốc, dung lượng nén và tỷ lệ phần trăm băng thông/lưu trữ đã tiết kiệm được nhờ Cloud.
* **Cơ chế cấp quyền ký tự động (Presigned Security Workflow):** Giấu kín hoàn toàn kiến trúc lưu trữ S3 nội bộ khỏi môi trường Internet, tạo ra một tiêu chuẩn bảo mật mức Doanh nghiệp.