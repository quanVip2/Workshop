---
title: "Cấu hình Xác thực định danh (Amazon Cognito)"
weight: 3
pre: " <b> 4.3 </b> "
---

## Mục tiêu
Khởi tạo và cấu hình dịch vụ Amazon Cognito thông qua giao diện thiết lập nhanh (Setup resources for your application). Đây là bước thiết lập lớp bảo mật (Security Layer) để quản lý tài khoản người dùng và cấp phát chuẩn JWT Token cho toàn bộ hệ thống.

## Tổng quan
Trong kiến trúc Hệ thống xử lý ảnh Enterprise, thay vì lưu trữ mật khẩu thủ công hoặc để người dùng vô danh tải ảnh tự do, chúng ta sử dụng **Amazon Cognito**. 

Giao diện mới của AWS Cognito cho phép chúng ta cấu hình đồng thời các thành phần cốt lõi:
* **User Directory:** Lưu trữ thông tin định danh và xác thực người dùng qua Email.
* **Application Integration:** Tích hợp trực tiếp với ứng dụng Web thông qua App Client (hỗ trợ xác thực qua các SDK như `amazon-cognito-identity-js`).

## Nội dung thực hành
Phần thực hành này được chia thành 2 bước chính tương ứng với các thư mục con:
* **4.3.1 Cấu hình ứng dụng và phương thức đăng nhập:** Thiết lập loại ứng dụng, tên định danh và thuộc tính định danh người dùng (Email).
* **4.3.2 Hoàn tất khởi tạo và lấy thông số định danh:** Tạo User Directory, lấy User Pool ID và Client ID để nhúng vào mã nguồn Frontend.

![Giao diện khởi tạo Amazon Cognito User Pool](/Workshop/images/4/4.3/2.1.png)
*Chú thích ảnh: Giao diện quản lý của Amazon Cognito trên AWS Console.*

## Kết quả mong đợi
* Khởi tạo thành công User Directory trên Amazon Cognito tại khu vực `us-east-1`.
* Thu thập thành công 2 thông số quan trọng: **User Pool ID** và **Client ID** phục vụ cho quá trình tích hợp mã nguồn Frontend ở các bước tiếp theo.