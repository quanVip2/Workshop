---
title: "Kiểm tra kết nối (Kiểm thử cấu trúc)"
weight: 2
pre: " <b> 4.7.2 </b> "
---

# KIỂM TRA KẾT NỐI (KIỂM THỬ CẤU TRÚC)

## Hướng dẫn chi tiết cách làm:
Để chắc chắn rằng việc liên kết giữa Storage (S3) và Compute (Lambda) đã thành công, chúng ta cần kiểm tra lại sơ đồ kiến trúc tự động của hàm.

1. Quay trở lại dịch vụ **Lambda** trên AWS Console.
2. Mở hàm `HamXuLyAnh12` 
3. Nhìn vào phần **Function overview** (Sơ đồ tổng quan chức năng) ở ngay trên cùng.
4. Nếu kết nối thành công, bạn sẽ thấy biểu tượng **Amazon S3** xuất hiện ở bên trái (đóng vai trò Trigger), chỉ mũi tên vào hàm Lambda ở giữa.

![alt text](/images/4/4.7/image7.png)