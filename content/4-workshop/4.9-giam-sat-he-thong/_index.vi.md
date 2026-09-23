---
title: "Giám sát hệ thống (Kiểm tra CloudWatch Logs và đo lường hiệu suất)"
weight: 9
pre: " <b> 4.9 </b> "
---


## Mục tiêu
Theo dõi quá trình hoạt động ngầm của hệ thống xử lý ảnh, đo lường thời gian thực thi thực tế (Duration), lượng RAM tiêu thụ (Max Memory Used) và phân tích lỗi (nếu có) thông qua dịch vụ Amazon CloudWatch.

## Tổng quan
Trong kiến trúc Serverless (phi máy chủ), bạn không có quyền truy cập vào hệ điều hành bên dưới để xem màn hình console hay file log truyền thống. Do đó, Amazon CloudWatch là "con mắt" duy nhất và mạnh mẽ nhất để giám sát hệ thống.

Nhờ việc chúng ta đã gắn quyền `AWSLambdaBasicExecutionRole` ở Chương 5.4, mỗi khi hàm AWS Lambda chạy, nó sẽ tự động đẩy toàn bộ nội dung lệnh `print()` và các thông số đo lường (Metrics) lên CloudWatch. Việc đọc hiểu các thông số này giúp chúng ta đánh giá xem cấu hình 512MB RAM và 15 giây Timeout đã thực sự tối ưu hay chưa, từ đó đáp ứng tiêu chí Kiểm thử và Đo lường của dự án.

## Nội dung thực hành
Phần thực hành này bao gồm hai quy trình chính:

* Điều hướng từ giao diện hàm AWS Lambda sang Amazon CloudWatch Log Groups.
* Đọc luồng dữ liệu nhật ký (Log stream) để phân tích các chỉ số `REPORT` về bộ nhớ và thời gian.

## Kết quả mong đợi
* Biết cách truy xuất nhật ký hoạt động của bất kỳ hàm Lambda nào.
* Đọc hiểu được các thông số cốt lõi trong dòng `REPORT` của CloudWatch.
* Xác nhận được việc nén ảnh bằng Pillow tiêu thụ bao nhiêu RAM thực tế, từ đó chứng minh quyết định nâng cấp RAM từ 128MB lên 512MB là hoàn toàn có cơ sở kỹ thuật.