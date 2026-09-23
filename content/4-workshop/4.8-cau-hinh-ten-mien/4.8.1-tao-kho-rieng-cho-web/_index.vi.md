---
title: "Tạo kho S3 riêng cho Website và Bật Hosting"
weight: 1
pre: " <b> 4.8.1 </b> "
---

**Bước 1: Tạo kho chứa Web**
1. Truy cập dịch vụ **S3** trên AWS Console.
2. Nhấn **Create bucket**.
3. **AWS Region:** Chọn `us-east-1` (N. Virginia).
4. **Bucket name:** Đặt một tên thật dễ nhớ (Ví dụ: `trang-web-xu-ly-anh-cua-toi`). Kho này sẽ hoàn toàn độc lập với kho Input và Output đã tạo trước đó.

![alt text](/images/4/4.8/image1.png)

5. Cuộn xuống phần **Block Public Access settings for this bucket**. Bỏ dấu tích (tắt) ở ô **Block all public access**.
6. Một cảnh báo màu vàng sẽ hiện ra, bạn đánh dấu tích vào ô *"I acknowledge that the current settings..."* để xác nhận bạn cố tình mở kho này ra công khai (vì nó là Web Public).

![alt text](/images/4/4.8/image2.png)

7. Cuộn xuống dưới cùng và nhấn **Create bucket**.


**Bước 2: Bật tính năng Web Server (Static website hosting)**
1. Trong danh sách Buckets, nhấp vào kho `trang-web-xu-ly-anh-cua-toi` vừa tạo.
2. Chuyển sang thẻ **Properties** (Thuộc tính).
3. Cuộn màn hình xuống dưới cùng, tìm mục **Static website hosting** và bấm **Edit** (Chỉnh sửa).
![alt text](/images/4/4.8/image3.png)
4. Chọn **Enable** (Bật).
5. Ở ô **Index document**, nhập chính xác tên file mã nguồn của bạn: `index.html`.
6. Nhấn **Save changes** (Lưu thay đổi).

![alt text](/images/4/4.8/image4.png)