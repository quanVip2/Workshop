---
title: "Workshop"
weight: 4
pre: " <b> 4. </b> "
---

## TRIỂN KHAI HỆ THỐNG XỬ LÝ ẢNH TỰ ĐỘNG (SERVERLESS) TRÊN AWS

### Tổng quan
Trong workshop này, chúng ta sẽ xây dựng và triển khai Hệ thống xử lý ảnh tự động (Thumbnail Generator) bằng kiến trúc Serverless Event-driven trên AWS.

Giải pháp sử dụng các dịch vụ cốt lõi của AWS như Amazon S3 (để lưu trữ ảnh gốc, ảnh đầu ra và lưu trữ giao diện web tĩnh), AWS Lambda (để xử lý đồ họa, nén ảnh bằng Python 3.12 và Pillow Layer), Amazon DynamoDB (để lưu trữ metadata, lịch sử xử lý) và AWS IAM (để quản lý quyền truy cập bảo mật), nhằm xây dựng một nền tảng có khả năng mở rộng tự động, không cần quản lý máy chủ và tối ưu hóa chi phí.

Trong suốt workshop này, bạn sẽ chuẩn bị môi trường tài khoản AWS Learner Lab, cấu hình các kho lưu trữ đám mây, thiết lập cơ sở dữ liệu NoSQL, lập trình hàm xử lý phi máy chủ tích hợp thư viện bên ngoài (Layer), thiết lập luồng kích hoạt sự kiện (Event Trigger) giữa S3 và Lambda, triển khai giao diện người dùng lên máy chủ web tĩnh (Static Website Hosting), thực hiện kiểm thử toàn bộ ứng dụng với nhiều thiết bị độc lập và cuối cùng dọn dẹp tất cả tài nguyên AWS đã tạo.

---

### Nội dung

1.[Tổng quan Workshop](4.1-tong-quan-workshop/)

2.[Điều kiện chuẩn bị](4.2-dieu-kien-chuan-bi/)

3.[Cấu hình hạ tầng lưu trữ ](4.3-cau-hinh-ha-tang-luu-tru/)

4.[Thiết lập Cơ sở dữ liệu NoSQL](4.4-thiet-lap-co-so-du-lieu-nosl/)

5.[Cấp quyền truy cập hệ thống](4.5-cap-quyen-truy-cap-he-thong/)

6.[Triển khai logic xử lý](4.6-trien-khai-logic-xu-ly/)

7.[Cấu hình luồng sự kiện](4.7-cau-hinh-luong-su-kien/)

8.[Cấu hình tên miền và Web Hosting](4.8-cau-hinh-ten-mien/)

9.[Giám sát hệ thống](4.9-giam-sat-he-thong/)

10.[Kiểm thử hệ thống](4.10-kiem-thu-he-thong/)

11.[Dọn dẹp tài nguyên](4.11-don-dep-tai-nguyen/)