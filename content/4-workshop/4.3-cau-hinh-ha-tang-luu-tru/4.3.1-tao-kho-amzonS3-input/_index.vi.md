---
title: "Tạo kho Amazon S3 Input (Kho chứa ảnh gốc)"
weight: 1
pre: " <b> 4.3.1 </b> "
---



## Hướng dẫn chi tiết cách làm:

**Bước 1: Truy cập dịch vụ S3**
1. Tại thanh tìm kiếm trên cùng của giao diện AWS Management Console, gõ **S3** và chọn dịch vụ S3 
2. Nhấn nút màu cam **Create bucket** (Tạo nhóm) ở góc bên phải màn hình.

![alt text](/Workshop/images/4/image1.png)
**Bước 2: Cấu hình thông tin kho Input**
1. **AWS Region:** Đảm bảo chọn đúng **US East (N. Virginia) us-east-1**. Điều này rất quan trọng để kho S3 nằm cùng một trung tâm dữ liệu với hàm Lambda, giúp tốc độ truyền file diễn ra nhanh nhất.
2. **Bucket name (Tên nhóm):** Nhập chính xác tên `kho-anh-goc-cua-toi-1`. 
![alt text](/Workshop/images/4/image2.png)

**Bước 3: Thiết lập quyền truy cập cơ bản**
1. Cuộn xuống phần **Object Ownership** (Quyền sở hữu đối tượng), giữ nguyên mặc định là **ACLs disabled**.
2. Cuộn xuống phần **Block Public Access settings for this bucket**. Giữ nguyên dấu tích ở ô **Block all public access** (Chặn tất cả quyền truy cập công cộng). 
3. Cuộn xuống dưới cùng và nhấn nút **Create bucket**.
![alt text](/Workshop/images/4/image3.png)
![alt text](/Workshop/images/4/image4.png)