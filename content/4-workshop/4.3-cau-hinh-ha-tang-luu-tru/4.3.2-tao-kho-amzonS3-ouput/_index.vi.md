---
title: "Tạo kho Amazon S3 Output (Kho chứa ảnh thu nhỏ)"
weight: 3
pre: " <b> 4.3.2 </b> "
---


## Hướng dẫn chi tiết cách làm:
Tương tự như luồng tạo kho Input, chúng ta sẽ tạo một không gian riêng biệt để chứa kết quả do AWS Lambda trả về. Việc tách riêng kho Output giúp hệ thống tránh bị vòng lặp vô hạn (Infinite Loop) – lỗi kinh điển khi Lambda lưu đè file mới vào kho cũ và liên tục tự kích hoạt lại chính nó.

**Bước 1: Bắt đầu tạo kho Output**
1. Trở lại giao diện danh sách Buckets của dịch vụ S3.
2. Tiếp tục nhấn nút **Create bucket**.
![alt text](/Workshop/images/4/image1.png)

**Bước 2: Cấu hình thông tin kho Output**
1. **AWS Region:** Chọn **US East (N. Virginia) us-east-1**.
2. **Bucket name (Tên nhóm):** Nhập chính xác tên `kho-anh-nho-cua-toi-1`.
![alt text](/Workshop/images/4/image5.png)
**Bước 3: Hoàn tất cấu hình**
1. Tương tự kho Input, giữ nguyên thiết lập chặn truy cập công cộng (**Block all public access**). Khi ứng dụng Web cần tải ảnh thu nhỏ, hệ thống sẽ sử dụng tính năng Pre-signed URL (URL có chữ ký hết hạn sau 300 giây) để hiển thị ảnh một cách an toàn.
2. Cuộn xuống dưới cùng, kiểm tra lại thông tin và nhấn **Create bucket**.
![alt text](/Workshop/images/4/image3.png)
![alt text](/Workshop/images/4/image6.png)