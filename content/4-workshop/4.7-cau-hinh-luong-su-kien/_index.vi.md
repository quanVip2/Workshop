---
title: "Cấu hình luồng sự kiện (Thiết lập S3 Event Notification kích hoạt Lambda)"
weight: 7
pre: " <b> 4.7 </b> "
---

## Mục tiêu
Tự động hóa hoàn toàn quy trình xử lý ảnh bằng cách thiết lập luồng sự kiện (Event Trigger). Đảm bảo rằng ngay khoảnh khắc một bức ảnh gốc được người dùng (qua giao diện Web) đẩy lên kho S3 Input, hàm AWS Lambda sẽ lập tức được "đánh thức" để thực hiện việc nén ảnh và ghi lịch sử vào cơ sở dữ liệu.

## Tổng quan
Đặc trưng mạnh mẽ và tinh tế nhất của kiến trúc Serverless Hướng sự kiện (Event-driven Architecture) chính là sự tự động hóa thụ động.

Thay vì phải duy trì một máy chủ ảo hoạt động 24/7 chỉ để liên tục quét (polling) xem có file ảnh mới nào được tải lên hay không (gây lãng phí tài nguyên lớn), chúng ta sẽ sử dụng tính năng S3 Event Notifications. Tính năng này cho phép kho Amazon S3 đóng vai trò như một "người canh gác", chủ động gửi tín hiệu kích hoạt (Trigger) trực tiếp đến hàm AWS Lambda ngay khi có một tệp (Object) vừa được tạo mới. Nhờ đó, hệ thống đạt được độ trễ cực thấp và chi phí vận hành bằng 0 khi rảnh rỗi.

## Nội dung thực hành
Phần thực hành này bao gồm hai quy trình chính:

* Truy cập kho lưu trữ ảnh gốc (`kho-anh-goc-cua-toi-1`) để tạo luồng thông báo sự kiện.
* Cấu hình loại sự kiện kích hoạt (`ObjectCreated`) và chỉ định đích đến (Destination) chính là hàm Lambda xử lý ảnh.

## Kết quả mong đợi
* Luồng sự kiện `s3:ObjectCreated:*` được thiết lập thành công trên kho S3 Input.
* Kho S3 Input và hàm AWS Lambda được liên kết với nhau thành một luồng dữ liệu thông suốt (Data Pipeline).
* Bất kỳ file nào được đưa vào kho Input đều sẽ tự động chạy qua mã nguồn Python của Lambda mà không cần thao tác thủ công.