---
title: "Cấu hình hạ tầng lưu trữ (Tạo kho Amazon S3 Input và Output)"
weight: 3
pre: " <b> 4.3 </b> "
---

## Mục tiêu
Khởi tạo hai kho lưu trữ đối tượng (Object Storage) độc lập trên nền tảng đám mây AWS. Đảm bảo thiết lập đúng khu vực (Region) và định danh (Bucket Name) để mã nguồn Frontend có thể tải ảnh lên kho Input và đọc ảnh thu nhỏ từ kho Output một cách trơn tru.

## Tổng quan
Trong kiến trúc Hệ thống xử lý ảnh tự động Serverless, Amazon S3 (Simple Storage Service) đóng vai trò là nơi lưu trữ vật lý cho các tệp tin đồ họa.

Thay vì lưu chung tất cả vào một nơi, hệ thống được thiết kế tách biệt thành 2 kho:

* **Input Bucket (Kho gốc):** Nơi tiếp nhận các bức ảnh nguyên bản có dung lượng lớn do trình duyệt của người dùng đẩy lên. Việc có file mới xuất hiện tại đây chính là "phát súng" (Trigger) kích hoạt hàm AWS Lambda hoạt động.
* **Output Bucket (Kho đích):** Nơi chỉ chứa các bức ảnh đã được Lambda nén siêu nhẹ, dùng để trả về và hiển thị trên giao diện Web (thông qua Pre-signed URL) nhằm tiết kiệm băng thông.

## Nội dung thực hành
Phần thực hành này bao gồm hai quy trình chính:

* Khởi tạo kho S3 Input (`kho-anh-goc-cua-toi-1`) tại khu vực `us-east-1`.
* Khởi tạo kho S3 Output (`kho-anh-nho-cua-toi-1`) tại cùng khu vực `us-east-1`.

## Kết quả mong đợi
* Hai kho S3 được tạo thành công trên hệ thống.
* Tên của hai kho hoàn toàn khớp với hằng số `INPUT_BUCKET` và `OUTPUT_BUCKET` đã được khai báo trong file `index.html`.
* Các kho được triển khai đúng khu vực, sẵn sàng để tích hợp luồng sự kiện (Event Notification) ở các chương tiếp theo.