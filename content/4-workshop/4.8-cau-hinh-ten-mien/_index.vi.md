---
title: "Cấu hình tên miền và Web Hosting (Triển khai giao diện tĩnh trên S3)"
weight: 7
pre: " <b> 4.8 </b> "
---

## Mục tiêu
Đưa file mã nguồn Frontend (`index.html`) lên môi trường Internet để bất kỳ thiết bị nào cũng có thể truy cập thông qua một đường dẫn (Endpoint URL) duy nhất. Đảm bảo giao diện web hoạt động trơn tru 24/7 mà không cần phải thuê hay cấu hình máy chủ Web truyền thống.

## Tổng quan
Để biến bài thực hành thành một sản phẩm thực tế (Production-ready), người dùng không thể lúc nào cũng tải file `index.html` về máy tính để chạy. Trong các hệ thống thông thường, kỹ sư sẽ phải thuê máy chủ (như Amazon EC2), cài đặt Nginx/Apache, cấu hình tên miền... rất phức tạp và tốn kém.

Tuy nhiên, với kiến trúc Serverless, chúng ta sử dụng một tính năng tuyệt vời của Amazon S3 là **Static Website Hosting**. Tính năng này biến một kho S3 thông thường thành một máy chủ web tĩnh siêu tốc, chịu tải vô hạn và cấp phát sẵn một đường link public hoàn toàn miễn phí. Điều này giúp dự án đạt tiêu chí Tối ưu hóa chi phí ở mức tối đa.

## Nội dung thực hành
Phần thực hành này bao gồm ba quy trình chính:

* Tạo một kho S3 mới dành riêng cho giao diện web và bật tính năng Static Website Hosting.
* Thiết lập chính sách bảo mật (Bucket Policy) cho phép truy cập công khai (Public Access) để ai cũng có thể xem trang web.
* Tải file `index.html` lên hệ thống và lấy đường dẫn URL (tên miền mặc định của AWS) để sử dụng.

## Kết quả mong đợi
* Một kho S3 mới được khởi tạo với vai trò là máy chủ Web.
* Trang web xử lý ảnh có thể truy cập được từ bất kỳ đâu qua Internet (trên cả PC và Mobile) bằng Endpoint URL.
* Trình duyệt tải thành công giao diện và các tập lệnh Javascript AWS SDK để giao tiếp trực tiếp với hạ tầng backend.