---
title: "Cấu hình ứng dụng và đăng nhập"
weight: 1
pre: " <b> 4.3.1 </b> "
---

## Các bước thực hiện theo giao diện mới của AWS Cognito

**Bước 1:** Từ thanh tìm kiếm của AWS Management Console, tìm và truy cập dịch vụ **Amazon Cognito**. 

**Bước 2: Define your application (Xác định loại ứng dụng)**[cite: 12]
* Tại mục **Application type**, hệ thống cung cấp các tùy chọn giao diện[cite: 12]. Vì chúng ta xây dựng ứng dụng trang đơn chạy trên trình duyệt web, hãy chọn **Single-page application (SPA)**.
* Tại ô **Name your application**, đặt tên cho ứng dụng của bạn (ví dụ: `image-processor-web` hoặc giữ nguyên tên mặc định AWS sinh sẵn như `My web app - ...`)[cite: 12].

![Cấu hình loại ứng dụng SPA trong bảng điều khiển Cognito](/Workshop/images/4/4.3/2.2.png)


**Bước 3: Configure options (Cấu hình tùy chọn định danh)**[cite: 13]
* Kéo xuống phần **Options for sign-in identifiers**, tại mục tùy chọn thuộc tính đăng nhập, tích chọn vào ô **Email** (Đảm bảo người dùng sử dụng địa chỉ email để đăng ký và đăng nhập)[cite: 13].
* Tại mục **Self-registration**, giữ nguyên dấu tích chọn **Enable self-registration** để cho phép người dùng tự động đăng ký tài khoản mới qua giao diện Web[cite: 13].
* Mục **Required attributes for sign-in**: Có thể để trống hoặc chọn tùy chọn nếu cần[cite: 13].

![Cấu hình loại ứng dụng SPA trong bảng điều khiển Cognito](/Workshop/images/4/4.3/2.3.png)

**Bước 4: Add a return URL (Cấu hình đường dẫn phản hồi)**[cite: 13]
* Mục **Return URL**: Đây là URL chuyển hướng sau khi đăng nhập thành công. Vì chúng ta chạy file cục bộ trên máy tính hoặc trên môi trường test, bạn có thể điền tạm `https://localhost` hoặc `http://localhost` (hoặc đường dẫn Netlify sau khi deploy)[cite: 13]. 
*(Lưu ý: Bạn hoàn toàn có thể thay đổi lại thông số này sau khi triển khai thực tế).*

![Cấu hình loại ứng dụng SPA trong bảng điều khiển Cognito](/Workshop/images/4/4.3/2.4.png)
