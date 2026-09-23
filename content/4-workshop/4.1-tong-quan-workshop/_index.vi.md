---
title: "Tổng quan Workshop"
weight: 1
pre: " <b> 4.1 </b> "
---

## Mục tiêu
Workshop này hướng dẫn triển khai ứng dụng Hệ thống Xử lý Ảnh Tự động (Thumbnail Generator) trên nền tảng AWS bằng cách sử dụng kiến trúc phi máy chủ (Serverless), các dịch vụ được quản lý (Managed Services), và luồng xử lý theo sự kiện (Event-driven Architecture). Sau khi hoàn thành workshop, bạn sẽ có thể triển khai một ứng dụng web xử lý đồ họa hoàn chỉnh với khả năng tự động mở rộng, tối ưu chi phí (Zero-cost lúc nhàn rỗi) và quản lý không gian làm việc độc lập cho nhiều người dùng.

## 1. Giới thiệu bài toán và giải pháp
Hệ thống Xử lý Ảnh Tự động là một ứng dụng web mô phỏng lại luồng làm việc ngầm (Background Job) của các nền tảng lớn (như Facebook, Shopee), nơi người dùng tải ảnh gốc lên và hệ thống tự động tạo ra một phiên bản thu nhỏ để tối ưu hóa tốc độ tải trang. Hệ thống hỗ trợ các chức năng như tải lên hình ảnh, tự động nén kích thước (sử dụng thư viện Pillow), quản lý lịch sử xử lý, tải/xem ảnh đã nén và cấp phát không gian dữ liệu độc lập cho từng thiết bị.

Thay vì triển khai ứng dụng trên một máy chủ truyền thống (EC2) hoạt động 24/7 gây lãng phí tài nguyên, workshop này áp dụng kiến trúc Serverless trên AWS. Giao diện tĩnh của ứng dụng được lưu trữ và phân phối bởi Amazon S3 (Static Website Hosting). Hình ảnh gốc và hình ảnh thu nhỏ cũng được lưu trữ an toàn trong các kho Amazon S3 độc lập.

Quy trình nén ảnh được thực thi bởi hàm AWS Lambda (Python 3.12) kết hợp với Lambda Layer (Klayers) để nạp thư viện đồ họa Pillow, đảm bảo khả năng tính toán mạnh mẽ mà không cần quản lý máy chủ. Mọi dữ liệu về lịch sử xử lý (Metadata) được ghi chép tự động vào cơ sở dữ liệu NoSQL Amazon DynamoDB. Hệ thống được giám sát thông qua Amazon CloudWatch và quản lý quyền hạn truy cập nghiêm ngặt bằng AWS IAM.

## 2. Kiến trúc hệ thống
Kiến trúc của hệ thống bao gồm các thành phần chính sau:

* Người dùng (Client Browser)
* Web Hosting tĩnh (Trình diễn giao diện)
* Dịch vụ lưu trữ Object (Input & Output)
* Dịch vụ tính toán phi máy chủ (Serverless Compute)
* Cơ sở dữ liệu NoSQL (Ghi chú lịch sử)
* Quản lý danh tính và quyền hạn
* Giám sát hệ thống

![Hình 1 – Kiến trúc hệ thống Xử lý ảnh tự động](/images/architecture-diagram.png)
*Hình 1 – Kiến trúc hệ thống Xử lý ảnh tự động (Lưu ý: Hãy đảm bảo bạn đã lưu ảnh sơ đồ kiến trúc vào thư mục `/images/architecture-diagram.png`)*

## 3. Quy trình hoạt động của hệ thống
Luồng xử lý chính của hệ thống diễn ra theo các bước sau:

1. Người dùng truy cập website thông qua đường dẫn được cung cấp bởi tính năng S3 Static Website Hosting.
2. Trình duyệt web sinh ra một mã định danh ngầm (Device ID) bằng LocalStorage, tự động gắn mã này vào tiền tố của bức ảnh và đẩy trực tiếp lên kho Amazon S3 (Input Bucket) thông qua AWS SDK.
3. Sự kiện `s3:ObjectCreated` từ Input Bucket ngay lập tức kích hoạt (trigger) hàm AWS Lambda.
4. Hàm AWS Lambda (được cấp RAM 512MB và Timeout 15s) tải ảnh gốc vào bộ nhớ, sử dụng thư viện Pillow (từ Lambda Layer) để giảm độ phân giải, ép chất lượng xuống 50% và chuyển đổi sang định dạng JPEG.
5. AWS Lambda đẩy bức ảnh đã nén siêu nhẹ sang kho Amazon S3 (Output Bucket).
6. Đồng thời, AWS Lambda ghi nhận thông tin (Tên file, kích thước mới, thời gian xử lý) vào cơ sở dữ liệu Amazon DynamoDB.
7. Trình duyệt web của người dùng liên tục lắng nghe, lấy ảnh thu nhỏ từ S3 Output (thông qua Pre-signed URL) để hiển thị.
8. Trình duyệt gọi API truy vấn Amazon DynamoDB, sử dụng logic bộ lọc (Filter) để chỉ lấy và hiển thị lịch sử xử lý hình ảnh thuộc về đúng thiết bị của người dùng đó.
9. Nhật ký hoạt động (Logs) và các lỗi thực thi của hàm Lambda (nếu có) được gửi đến Amazon CloudWatch để phục vụ việc giám sát và khắc phục sự cố (Troubleshooting).

## 4. Các dịch vụ được sử dụng
Workshop sử dụng các dịch vụ AWS sau:

* **Dịch vụ tính toán (Compute)**
  * AWS Lambda
  * AWS Lambda Layers
* **Lưu trữ (Storage)**
  * Amazon S3 (Object Storage & Static Website)
  * Amazon DynamoDB (NoSQL Database)
* **Bảo mật & Quản lý (Security & Management)**
  * AWS Identity and Access Management (IAM)
* **Giám sát (Monitoring)**
  * Amazon CloudWatch

## 5. Kết quả đạt được
Sau khi hoàn thành workshop, bạn sẽ có thể:

* Lập trình và cấu hình giao diện web tĩnh giao tiếp trực tiếp với AWS mà không cần máy chủ Backend (thông qua AWS SDK for JavaScript).
* Triển khai giải pháp lưu trữ hình ảnh và website tĩnh (Static Website Hosting) trên Amazon S3.
* Thiết kế bảng cơ sở dữ liệu phi quan hệ (NoSQL) với Amazon DynamoDB để ghi nhận Log/Metadata.
* Tích hợp các thư viện bên thứ ba (C-compiled modules như Pillow) vào môi trường AWS Lambda thông qua tính năng Lambda Layers.
* Xây dựng luồng tự động hóa theo sự kiện (Event-driven): dùng sự kiện thêm file của S3 để kích hoạt Lambda.
* Cấu hình sức mạnh tính toán (Memory, Timeout) cho Lambda để xử lý các tác vụ đồ họa nặng.
* Phân tích lỗi hệ thống và giám sát hoạt động của kiến trúc thông qua Amazon CloudWatch Logs.
* Xóa toàn bộ tài nguyên AWS sau khi hoàn thành workshop để tránh phát sinh chi phí.