---
title: "Triển khai cụm Vi dịch vụ (Lambda Functions)"
weight: 7
pre: " <b> 4.7 </b> "
---

## Mục tiêu
Thiết lập và lập trình toàn bộ cụm **4 hàm AWS Lambda** hoạt động dưới dạng các vi dịch vụ độc lập (Microservices). Cụm hàm này đóng vai trò xử lý toàn bộ logic nghiệp vụ của hệ thống: từ việc cấp phát Presigned URL an toàn, nén ảnh tự động tích hợp AI Rekognition, cho đến việc truy vấn lịch sử cá nhân hóa theo chuẩn bảo mật đa người dùng (Multi-tenant).

## Tổng quan kiến trúc Vi dịch vụ
Thay vì dồn mọi xử lý vào một hàm duy nhất, hệ thống tách rời thành 4 chức năng chuyên biệt:
* **4.7.1 Hàm `GenerateUploadUrl`:** Nhận request từ API Gateway, tạo chữ ký tạm thời để Frontend upload trực tiếp lên S3 Input an toàn.
* **4.7.2 Hàm `HamXuLyAnh`:** Lắng nghe sự kiện S3, tự động nén ảnh bằng Pillow, gọi **Amazon Rekognition** để phân tích AI và ghi metadata xuống DynamoDB.
* **4.7.3 Hàm `GetUserHistory`:** Truy vấn bảng DynamoDB theo Email người dùng, lọc dữ liệu, xử lý kiểu số (Decimal) và trả về danh sách lịch sử kèm thống kê dung lượng.
* **4.7.4 Hàm `GenerateDownloadUrl`:** Cấp phát chữ ký tạm thời để người dùng xem/tải ảnh thành phẩm từ S3 Output.

![Cụm 4 vi dịch vụ Lambda trong hệ thống](/Workshop/images/4/4.7/2.1.png)
