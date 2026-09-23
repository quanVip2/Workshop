---
title: "Triển khai logic xử lý"
weight: 5
pre: " <b> 4.6 </b> "
---


## Mục tiêu
Xây dựng "bộ não" của hệ thống xử lý ảnh bằng dịch vụ tính toán phi máy chủ (Serverless Compute). Đảm bảo hàm AWS Lambda được cấu hình đúng môi trường Python 3.12, tích hợp thành công thư viện đồ họa Pillow thông qua Lambda Layer, thiết lập đủ tài nguyên RAM/Timeout và triển khai mã nguồn xử lý thành công.

## Tổng quan
AWS Lambda đóng vai trò là lõi xử lý trung tâm trong mô hình Event-driven. Khi có ảnh mới đẩy lên S3, Lambda sẽ được đánh thức để làm việc.

Tuy nhiên, môi trường Python mặc định của Lambda rất tinh gọn và không có sẵn các thư viện xử lý đồ họa (như PIL/Pillow). Thay vì phải đóng gói mã nguồn và thư viện thành một file ZIP phức tạp (dễ sinh lỗi môi trường giữa Windows và Linux), workshop này áp dụng giải pháp Lambda Layers bằng cách sử dụng kho lưu trữ mã nguồn mở Klayers để "nhúng" trực tiếp thư viện Pillow vào hàm. Ngoài ra, việc xử lý đồ họa đòi hỏi nhiều sức mạnh tính toán, do đó việc tinh chỉnh thông số Memory (RAM) và Timeout là bắt buộc để tránh tình trạng hệ thống bị Crash.

## Nội dung thực hành
Phần thực hành này bao gồm ba quy trình chính:

* Khởi tạo hàm AWS Lambda và gắn thẻ định danh (IAM Role) đã tạo ở phần trước.
* Cấu hình Lambda Layer (Pillow) tương thích với môi trường Python 3.12 tại khu vực `us-east-1`.
* Cập nhật mã nguồn Python, cấu hình tài nguyên hệ thống (512MB RAM, 15s Timeout) và Deploy.

## Kết quả mong đợi
* Hàm Lambda được khởi tạo với Runtime Python 3.12.
* Thư viện Pillow được thêm vào thành công qua chỉ định ARN mà không gặp lỗi "The resource you requested does not exist".
* Mã nguồn nén ảnh (giảm dung lượng, ép định dạng JPEG) được triển khai và lưu lại trên máy chủ.
* Tài nguyên cấp phát cho hàm được nâng cấp thành 512MB RAM để xử lý các file ảnh nặng.