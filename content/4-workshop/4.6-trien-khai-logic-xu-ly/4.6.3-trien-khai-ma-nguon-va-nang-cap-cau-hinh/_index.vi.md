---
title: "Triển khai mã nguồn và nâng cấp cấu hình máy chủ"
weight: 3
pre: " <b> 4.6.3 </b> "
---

# TRIỂN KHAI MÃ NGUỒN VÀ NÂNG CẤP CẤU HÌNH MÁY CHỦ

## Hướng dẫn chi tiết cách làm:

**Bước 1: Tăng cường sức mạnh tính toán (Optimize Performance)**
Mặc định Lambda chỉ cấp 128MB RAM và 3 giây xử lý. Thông số này không đủ để thư viện Pillow nén ảnh, gây ra lỗi Crash (Timeout).
1. Chuyển sang thẻ **Configuration** (Cấu hình) ➔ Chọn **General configuration** (Cấu hình chung) ở menu trái.
![alt text](/Workshop/images/4/4.5/image8.png)
2. Nhấn nút **Edit** 
3. Tăng **Memory (RAM)** lên **512 MB**.
4. Tăng **Timeout (Thời gian chờ)** lên **15 giây**.
5. Nhấn **Save** 
![alt text](/Workshop/images/4/4.5/image9.png)

**Bước 2: Triển khai mã nguồn Python (Code Deploy)**
1. Quay lại thẻ **Code**.
2. Trong khung soạn thảo **Code source** (Mã nguồn), xóa toàn bộ đoạn code mặc định và dán đoạn mã xử lý vào.
![alt text](/Workshop/images/4/4.5/image10.png)
**Bước 3: Lưu và Cập nhật (Cực kỳ quan trọng)**
1. Nhấn nút **Deploy** (Triển khai) màu xám nhạt ở phía trên vùng soạn thảo mã.
2. *Lưu ý:* Nếu bỏ qua thao tác này, AWS Lambda sẽ không lưu cấu hình mã mới mà vẫn chạy đoạn code mẫu mặc định, dẫn đến hệ thống không phản hồi. Đợi dòng thông báo màu xanh lá "Successfully updated the function" xuất hiện là hoàn tất.

![alt text](/Workshop/images/4/4.5/image11.png)