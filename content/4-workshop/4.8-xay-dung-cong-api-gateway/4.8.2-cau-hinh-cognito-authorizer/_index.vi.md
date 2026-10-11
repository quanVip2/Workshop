---
title: "2. Cấu hình Cognito JWT Authorizer"
weight: 2
pre: " <b> 4.8.2 </b> "
---

## Tích hợp Lớp Bảo Vệ bằng Cognito

Đây là bước cực kỳ quan trọng giúp API Gateway biết cách "đọc" Token mà người dùng gửi lên để xác định xem họ đã đăng nhập hợp lệ hay chưa.

**Các bước thực hiện:**
1. Tại trang quản lý API của bạn (`ImageProcessorAPI`), nhìn sang menu bên trái, chọn **Authorization** (Bảo mật).
2. Chuyển sang tab **Manage authorizers** và nhấn **Create**.
3. Cấu hình các thông số sau:
   * **Authorizer type:** Chọn **JWT**.
   * **Name:** Nhập tên `CognitoAuth`.
   * **Identity source:** Nhập `$request.header.Authorization` (Trình duyệt sẽ gửi Token vào Header này).
   * **Issuer URL:** Dán đường dẫn định danh User Pool của bạn. Định dạng chuẩn là: 
     `https://cognito-idp.us-east-1.amazonaws.com/<USER_POOL_ID_CỦA_BẠN>` 
     *(Thay thế đoạn mã ID bạn đã copy ở bài 4.3 vào đây)*.
   * **Audience:** Dán chuỗi **Client ID** (App Client) bạn đã copy ở bài 4.3 vào đây.
4. Nhấn **Create** để lưu lại lớp bảo vệ này.

![Tạo JWT Authorizer liên kết với Amazon Cognito](/Workshop/images/4/4.8/2.2.png)
