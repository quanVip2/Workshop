---
title: "4. Cấu hình CORS và Hoàn tất"
weight: 4
pre: " <b> 4.8.4 </b> "
---

## Mở khóa giao tiếp (CORS) và Lấy URL API

Vì giao diện Web (Frontend) và API Gateway (Backend) nằm ở hai tên miền khác nhau, trình duyệt mặc định sẽ chặn kết nối. Chúng ta phải cấu hình CORS để cho phép luồng dữ liệu đi qua.

**Bước 1: Cấu hình CORS**
1. Nhìn menu bên trái, phần *Develop*, chọn **CORS**.
2. Nhấn **Configure** và nhập các thông số sau:
   * **Access-Control-Allow-Origins:** Nhập `*` (hoặc tên miền website của bạn) -> Nhấn Add.
   * **Access-Control-Allow-Headers:** Nhập `*` hoặc `Authorization, Content-Type` -> Nhấn Add.
   * **Access-Control-Allow-Methods:** Nhập `*` hoặc chọn `GET, OPTIONS` -> Nhấn Add.
   * **Access-Control-Expose-Headers:** Để trống.
   * **Max-age:** Nhập `300`.
3. Nhấn **Save** để lưu lại.

 [Cấu hình CORS cho phép Frontend giao tiếp API](/Workshop/images/4/4.8/2.5.png)

**Bước 2: Lấy URL để cấu hình Frontend**
1. Chọn menu **API: ImageProcessorAPI** (nhấp vào dòng chữ trên cùng bên trái để quay ra trang tổng quan API).
2. Dưới mục **Invoke URL**, bạn sẽ thấy một đường dẫn có dạng:
   `https://xxxxxxxxx.execute-api.us-east-1.amazonaws.com`
3. Hãy sao chép (Copy) đường dẫn này. Đây chính là xương sống để kết nối giao diện của bạn với toàn bộ hệ thống AWS. Bạn sẽ dùng link này gán vào biến `API_GATEWAY_URL` và `API_HISTORY_URL` trong mã nguồn Javascript ở các phần sau.

 [Sao chép Invoke URL để gắn vào Frontend](/Workshop/images/4/4.8/2.6.png)
