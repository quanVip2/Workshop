---
title: "Hoàn tất và Lấy thông số"
weight: 2
pre: " <b> 4.3.2 </b> "
---

## Các bước hoàn tất khởi tạo và trích xuất thông số

**Bước 5: Tạo Thư mục người dùng (User Directory)**[cite: 13]
* Kiểm tra lại toàn bộ thông tin cấu hình ở các bước trên.
* Kéo xuống dưới cùng màn hình và nhấn vào nút màu cam **Create user directory**[cite: 13].

![Nhấn nút tạo thư mục người dùng](/Workshop/images/4/4.3/2.5.png)

**Bước 6: Trích xuất thông số User Pool ID và Client ID**
* Sau khi hệ thống khởi tạo thành công (mất khoảng vài giây), bạn sẽ được chuyển hướng về trang tổng quan của User Pool vừa tạo.
* **Checkpoint 1 (User Pool ID):** Nhìn lên phần đầu của trang tổng quan, sao chép lại giá trị **User Pool ID** (Có định dạng dạng `us-east-1_XXXXXXXXX`).
* **Checkpoint 2 (Client ID):** Cuộn xuống phía dưới trang tổng quan hoặc bấm vào tab **App Clients** , tìm đến phần danh sách App client để sao chép chuỗi **Client ID** của ứng dụng SPA vừa tạo.

![User Pool ID](/Workshop/images/4/4.3/2.6.png)
![Client ID](/Workshop/images/4/4.3/2.7.png)

Sau khi hoàn tất bước này, chúng ta đã sẵn sàng chuyển sang xây dựng hạ tầng lưu trữ S3 ở bài tiếp theo!