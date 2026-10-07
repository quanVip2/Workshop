---
title: "1. Cấu hình Xác thực (Cognito UI)"
weight: 1
pre: " <b> 4.11.1 </b> "
---

## Nhúng thông số Amazon Cognito vào mã nguồn

Để biểu mẫu Đăng nhập/Đăng ký trên web có thể giao tiếp với User Pool đã tạo ở bài 4.3, chúng ta cần khai báo thông số.

**Các bước thực hiện:**
1. Mở file `index.html` của dự án bằng phần mềm Visual Studio Code.
2. Tìm đến đầu đoạn thẻ `<script>`, bạn sẽ thấy khu vực khai báo Cấu hình Cognito.
3. Thay thế các giá trị trống bằng thông số bạn đã lưu lại:
   * `POOL_ID`: Nhập giá trị **User Pool ID** (Ví dụ: `us-east-1_xxxxxxxxx`).
   * `CLIENT_ID`: Nhập giá trị **App Client ID** (Ví dụ: `3abc123...`).
   * `REGION`: Khai báo `'us-east-1'`.

**Giao diện Form động (Dynamic Form):**
Hệ thống Frontend đã được lập trình sẵn hàm `toggleAuth()` để tự động đổi tiêu đề `<h1>` thành *"Đăng Nhập"* hoặc *"Đăng Ký Tài Khoản"* tùy thuộc vào hành động của người dùng, mang lại trải nghiệm mượt mà.

![alt text](/Workshop/images/4/4.11/2.2.png)
*Chú thích ảnh: Khai báo thông số Amazon Cognito vào Frontend.*

![alt text](/Workshop/images/4/4.11/2.3.png)
*Chú thích ảnh: Giao diện đăng ký tài khoản xác thực qua Cognito.*