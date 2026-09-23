---
title: "Đề xuất "
weight: 2
pre: " <b> 2. </b> "
---

# HỆ THỐNG TỰ ĐỘNG XỬ LÝ HÌNH ẢNH SERVERLESS (SERVERLESS IMAGE THUMBNAIL GENERATOR)

## 1. Thông tin chung (General Information)

* **Tên đề tài (Project Title):** Xây dựng hệ thống tự động xử lý tạo ảnh thu nhỏ phi máy chủ trên AWS (Serverless Image Thumbnail Generation System on AWS).
* **Thành viên thực hiện (Author):** Nguyễn Hồng Quân
* **Bối cảnh (Context):** Trong các ứng dụng web hiện đại, việc tối ưu hóa hình ảnh tải lên là bắt buộc để giảm băng thông và tăng tốc độ trải nghiệm cho người dùng. Đề tài này xây dựng một giải pháp hoàn toàn tự động, ứng dụng mô hình hướng sự kiện (Event-driven) trên nền tảng đám mây AWS.

## 2. Bài toán và Mục tiêu (Problem Statement & Objectives)

### 2.1. Bối cảnh và Bài toán (Context & Problem)
* **Hệ thống dùng để làm gì?** Hệ thống tự động nhận diện tệp hình ảnh khi người dùng tải lên, tiến hành xử lý tạo bản thu nhỏ (thumbnail) và lưu trữ lại, đồng thời ghi nhận metadata vào cơ sở dữ liệu.
* **Đối tượng sử dụng (Target Users):** Quản trị viên hệ thống, nhà phát triển ứng dụng web thương mại điện tử hoặc blog cá nhân.
* **Vấn đề giải quyết (Problem Solved):** Khắc phục tình trạng tốn kém tài nguyên máy chủ truyền thống (EC2 chạy 24/7), loại bỏ độ trễ do xử lý thủ công và tối ưu chi phí vận hành bằng kiến trúc Serverless.

### 2.2. Mục tiêu cụ thể (Specific Objectives)
* **Output mong muốn:**
  * Hai phân vùng lưu trữ ảnh riêng biệt (Kho ảnh gốc và Kho ảnh đã xử lý).
  * Hàm xử lý tự động kích hoạt qua sự kiện S3 Event.
  * Bảng lưu trữ thông tin kích thước và thời gian xử lý trên cơ sở dữ liệu NoSQL.
  * Hệ thống log giám sát hoạt động theo thời gian thực.
* **Tiêu chí đánh giá thành công (Success Criteria):**
  * Tải ảnh lên kho gốc sang Ảnh thu nhỏ xuất hiện tự động ở kho đích trong vòng dưới 3 giây.
  * Thông tin hình ảnh được ghi nhận đầy đủ vào cơ sở dữ liệu mà không cần can thiệp thủ công.

## 3. Kiến trúc và Thiết kế Kỹ thuật (Architecture & Technical Design)

## Sơ đồ kiến trúc (Architecture Diagram)
![Sơ đồ kiến trúc Hệ thống Tự động xử lý hình ảnh Serverless](/Workshop/images/sodo.jpg)

### 3.1. Các dịch vụ AWS sử dụng (AWS Services Selection)
* **Amazon S3 (Simple Storage Service):** Dùng để lưu trữ tệp (chia làm Input Bucket và Output Bucket) với ưu điểm độ bền cao, chi phí rẻ, hỗ trợ tính năng sinh sự kiện (Event Notification).
* **AWS Lambda:** Dịch vụ tính toán Serverless. Được lựa chọn vì không cần quản trị hệ thống phần cứng, chỉ tính phí theo số lượng request thực tế và tự động co giãn theo tải.
* **Amazon DynamoDB:** Cơ sở dữ liệu NoSQL hiệu năng cao, quản lý toàn bộ dữ liệu cấu trúc nhẹ của tệp hình ảnh.
* **Amazon CloudWatch:** Giám sát, thu thập log và đo lường hiệu suất hoạt động của hàm Lambda.

### 3.2. Bảo mật và Nguyên tắc Least Privilege (Security & IAM)
* Hệ thống cấu hình IAM Role riêng biệt cho AWS Lambda.
* Tuân thủ tuyệt đối nguyên tắc Least Privilege (Quyền tối thiểu): Hàm Lambda chỉ có quyền GetObject trên kho gốc, PutObject trên kho đích, quyền ghi log vào CloudWatch và quyền ghi dữ liệu vào bảng DynamoDB định sẵn. Không sử dụng quyền quản trị toàn cục (AdministratorAccess).

## 4. Rủi ro Tiềm ẩn và Hướng giải quyết (Potential Risks & Mitigation)

* **Rủi ro 1: Lỗi vòng lặp vô hạn (Infinite Loop Event Trigger)**
  * *Mô tả:* Nếu hàm Lambda ghi file kết quả trả về đúng vào Input Bucket (nơi kích hoạt sự kiện), nó sẽ tạo ra một vòng lặp sự kiện vô tận, dẫn đến cạn kiệt tài nguyên và phát sinh chi phí lớn.
  * *Hướng giải quyết:* Thiết kế kiến trúc tách biệt hoàn toàn 2 Bucket (Input Bucket riêng và Output Bucket riêng). Đảm bảo hàm Lambda chỉ lắng nghe sự kiện từ Input Bucket và ghi file kết quả sang Output Bucket với tên tiền tố định danh khác (`resized_`).
* **Rủi ro 2: Lỗi phân quyền bảo mật (IAM Permission Denied)**
  * *Mô tả:* Hàm Lambda không có quyền đọc/ghi bucket hoặc không thể kết nối vào bảng DynamoDB do cấu hình IAM Role sai.
  * *Hướng giải quyết:* Kiểm tra kỹ cấu hình ARN của tài nguyên trong IAM Policy, đồng thời sử dụng Amazon CloudWatch Logs để truy vết mã lỗi chính xác ngay khi gặp sự cố thực thi.
* **Rủi ro 3: Phát sinh chi phí ngoài ý muốn (Cost Overruns)**
  * *Mô tả:* Quên dọn dẹp các tài nguyên sau khi thử nghiệm làm phát sinh chi phí vượt định mức Free Tier.
  * *Hướng giải quyết:* Xây dựng sẵn quy trình dọn dẹp tài nguyên (Clean-up steps) sau khi hoàn tất lab và kiểm tra định kỳ trên bảng điều khiển AWS Billing.

## 5. Kế hoạch Triển khai Lab (Implementation Lab Steps)

Dự án được triển khai qua các bước chuẩn hóa end-to-end:
* **Bước 1:** Khởi tạo 2 Amazon S3 Bucket (Input và Output).
* **Bước 2:** Tạo bảng Amazon DynamoDB để lưu vết metadata hình ảnh.
* **Bước 3:** Thiết lập IAM Policy và IAM Role tuân thủ nguyên tắc Least Privilege.
* **Bước 4:** Xây dựng hàm AWS Lambda (Python) xử lý logic sao chép và ghi dữ liệu.
* **Bước 5:** Cấu hình S3 Event Trigger để kích hoạt tự động hàm Lambda khi có tệp mới.
* **Bước 6:** Kiểm thử (Test), xác thực kết quả trên DynamoDB và kiểm tra CloudWatch Logs.
* **Bước 7:** Thực hiện dọn dẹp tài nguyên (Clean-up) để tối ưu chi phí.

## 6. Đóng góp Cá nhân và Sáng tạo (Personal Contributions & Customization)

* **Tùy biến mở rộng:** Không chỉ dừng lại ở việc sao chép tệp đơn thuần, hệ thống tích hợp thêm Amazon DynamoDB để tự động trích xuất, định hình và lưu trữ thông tin chi tiết (tên tệp, dung lượng, thời gian xử lý), phục vụ cho việc thống kê báo cáo.
* **Định hướng phát triển tương lai:** Tích hợp thêm giao diện web tĩnh (Static Web Front-end) trên S3 kết hợp chính sách CORS để người dùng cuối có thể thao tác trực tiếp qua trình duyệt web một cách trực quan.