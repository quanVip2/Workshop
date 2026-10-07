---
title: "Workshop"
weight: 4
pre: " <b> 4. </b> "
---

## TRIỂN KHAI HỆ THỐNG XỬ LÝ HÌNH ẢNH SERVERLESS TÍCH HỢP AI TRÊN AWS

### Tổng quan
Trong workshop này, chúng ta sẽ xây dựng và triển khai một Hệ thống xử lý ảnh tự động (Serverless Image Processor) theo chuẩn Doanh nghiệp (Enterprise). Hệ thống ứng dụng kiến trúc đa người dùng (Multi-tenant), bảo mật định danh và tích hợp Trí tuệ nhân tạo (AI) hoàn toàn trên nền tảng AWS.

Giải pháp sử dụng các dịch vụ cốt lõi của AWS bao gồm: 
* **Amazon Cognito:** Quản lý xác thực và cấp phát luồng token bảo mật (JWT).
* **Amazon API Gateway:** Xây dựng cổng giao tiếp REST API an toàn với kỹ thuật Presigned URL để không làm lộ cấu hình bảo mật ra Frontend.
* **AWS Lambda:** Triển khai cụm vi dịch vụ (Microservices) gồm 4 hàm xử lý nghiệp vụ độc lập bằng Python 3.12 (Cấp quyền, Nén ảnh, Truy vấn lịch sử).
* **Amazon Rekognition:** Ứng dụng Machine Learning để tự động phân tích và gán nhãn (AI Tags) cho hình ảnh.
* **Amazon S3 & DynamoDB:** Lưu trữ tệp tĩnh, metadata, và thống kê dung lượng tiết kiệm theo từng tài khoản cá nhân.
* **AWS IAM:** Quản lý quyền truy cập cực kỳ nghiêm ngặt theo nguyên tắc Least Privilege.

Trong suốt workshop này, bạn sẽ được hướng dẫn từ bước cấu hình môi trường bảo mật, thiết lập kho lưu trữ, lập trình cụm hàm phi máy chủ tích hợp AI, cấu hình luồng kích hoạt sự kiện (Event-driven), triển khai giao diện Website Frontend có tích hợp Dashboard Thống kê cá nhân, tiến hành kiểm thử phân luồng tài khoản độc lập và cuối cùng là dọn dẹp tài nguyên để tối ưu chi phí.

---

### Nội dung

1. [Tổng quan Workshop](4.1-tong-quan-workshop/)

2. [Điều kiện chuẩn bị](4.2-dieu-kien-chuan-bi/)

3. [Cấu hình Xác thực định danh với Amazon Cognito](4.3-cau-hinh-xac-thuc-cognito/) *(Mới bổ sung)*

4. [Cấu hình hạ tầng lưu trữ S3](4.4-cau-hinh-ha-tang-luu-tru/)

5. [Thiết lập Cơ sở dữ liệu NoSQL DynamoDB](4.5-thiet-lap-co-so-du-lieu-nosql/)

6. [Cấp quyền truy cập hệ thống (IAM)](4.6-cap-quyen-truy-cap-he-thong/)

7. [Triển khai cụm Vi dịch vụ (Lambda) & AI Rekognition](4.7-trien-khai-logic-xu-ly/) *(Cập nhật nội dung)*

8. [Xây dựng cổng REST API với Amazon API Gateway](4.8-xay-dung-cong-api-gateway/) *(Mới bổ sung)*

9. [Cấu hình luồng sự kiện tự động (S3 Trigger)](4.9-cau-hinh-ten-mien/)

9. [Cấu hình luồng sự kiện tự động (S3 Trigger)](4.10-cau-hinh-luong-su-kien/)

10. [Triển khai Web Frontend & Dashboard Thống kê](4.11-trien-khai-web-frontend/) *(Cập nhật nội dung)*

11. [Kiểm thử và Giám sát hệ thống (CloudWatch)](4.12-giam-sat-va-kiem-thu/)

12. [Dọn dẹp tài nguyên](4.13-don-dep-tai-nguyen/)