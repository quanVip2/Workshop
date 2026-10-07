---
title: "Triển khai Web Frontend & Dashboard Thống kê"
weight: 11
pre: " <b> 4.11 </b> "
---

## Mục tiêu
Tích hợp toàn bộ các dịch vụ Backend (Cognito, API Gateway) vào giao diện người dùng (Frontend). Triển khai hệ thống Bảng điều khiển (Analytics Dashboard) để hiển thị thống kê dữ liệu cá nhân, nhãn dán AI và cuối cùng là đưa website lên môi trường Internet công khai (Public URL).

## Tổng quan Giao diện
Ứng dụng Web của chúng ta được xây dựng dưới dạng **Single Page Application (SPA)** bằng HTML, CSS và JavaScript thuần (Vanilla JS), không cần cài đặt Node.js hay Webpack. 

Giao diện được chia làm 2 trạng thái (States) rõ rệt được bảo vệ nghiêm ngặt:
1. **Trạng thái Khách (Guest Mode):** Chỉ hiển thị form Đăng nhập / Đăng ký / Xác thực OTP. Hệ thống sẽ kết nối với thư viện `amazon-cognito-identity-js` để làm việc với AWS.
2. **Trạng thái Đăng nhập (Authenticated Mode):** Hiển thị khu vực tải ảnh (Upload), Bảng Dashboard thống kê dung lượng tiết kiệm, và Bảng lịch sử xử lý có chứa nhãn dán AI (Amazon Rekognition).

## Nội dung thực hành
Phần triển khai Frontend sẽ đi qua 3 bước cốt lõi:
* **4.10.1 Cấu hình Xác thực (Cognito UI):** Nhúng thông số User Pool và Client ID.
* **4.10.2 Tích hợp API & Dashboard:** Nhúng Invoke URL từ API Gateway, hiển thị thẻ AI và tính toán % dung lượng.
* **4.10.3 Deploy Website:** Triển khai mã nguồn lên nền tảng Netlify (hoặc S3 Static Hosting) để có đường link truy cập thực tế.

![alt text](/Workshop/images/4/4.11/2.1.png)
*Chú thích ảnh: Giao diện hoàn chỉnh của Hệ thống xử lý ảnh Enterprise.*