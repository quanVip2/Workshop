---
title: "Tạo Event Notification trên kho S3 Input"
weight: 1
pre: " <b> 4.7.1 </b> "
---


**Bước 1: Truy cập cài đặt kho ảnh gốc**
1. Từ thanh tìm kiếm của AWS Console, mở lại dịch vụ **S3**.
2. Trong danh sách Buckets, nhấp chọn đúng kho `kho-anh-goc-cua-toi-1` (Kho Input). 
3. Chuyển sang thẻ **Properties** (Thuộc tính).
![alt text](/Workshop/images/4/4.7/image1.png)

**Bước 2: Cấu hình thông số sự kiện (Event Setup)**
1. Cuộn màn hình xuống tìm đến mục **Event notifications** (Thông báo sự kiện).
2. Nhấn nút **Create event notification** (Tạo thông báo sự kiện).
![alt text](/Workshop/images/4/4.7/image2.png)

3. **Event name (Tên sự kiện):** Đặt tên để dễ quản lý, ví dụ: `	
HamXuLyAnh`.
4. **Prefix (Tiền tố) / Suffix (Hậu tố):** Bỏ trống để áp dụng cho mọi file tải lên.
![alt text](/Workshop/images/4/4.7/image3.png)
**Bước 3: Chọn loại sự kiện kích hoạt (Event types)**
* Tại khu vực **Event types**, bạn tích chọn vào ô **All object create events** 
![alt text](/Workshop/images/4/4.7/image4.png)

**Bước 4: Chỉ định đích đến (Destination)**
1. Cuộn xuống dưới cùng tại mục **Destination** (Đích đến).
2. Chọn tùy chọn **Lambda function** (Hàm Lambda).
3. Tại ô thả xuống **Specify Lambda function** (Chỉ định hàm Lambda), hệ thống sẽ tự động liệt kê các hàm bạn đang có. Hãy chọn hàm `HamXuLyAnh12` mà bạn đã viết mã nguồn Python lúc nãy.
4. Nhấn nút **Save changes** (Lưu thay đổi) ở góc dưới cùng.

![alt text](/Workshop/images/4/4.7/image5.png)
![alt text](/Workshop/images/4/4.7/image6.png)