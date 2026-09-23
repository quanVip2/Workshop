---
title: "Cấp quyền truy cập hệ thống"
weight: 1
pre: " <b> 4.5.1 </b> "
---
# TẠO IAM ROLE

**Bước 1: Truy cập bảng điều khiển IAM**
1. Tại thanh tìm kiếm trên cùng của giao diện AWS Management Console, gõ **IAM** và chọn dịch vụ IAM (Manage access to AWS resources).
2. Ở menu điều hướng bên trái màn hình, nhấp vào mục **Roles** (Vai trò).

![alt text](/Workshop/images/4/4.4/image1.png)

**Bước 2: Bắt đầu khởi tạo Role**
1. Nhấn nút màu cam **Create role** (Tạo vai trò) nằm ở góc trên bên phải.
2. Hệ thống sẽ chuyển sang giao diện thiết lập Thực thể tin cậy (Select trusted entity). Đây là bước hệ thống AWS hỏi bạn: "Ai hoặc dịch vụ nào sẽ được phép sử dụng quyền này?".

![alt text](/Workshop/images/4/4.4/image2.png)


**Bước 3: Lựa chọn dịch vụ tin cậy**
1. Tại mục **Trusted entity type**, chọn ô **AWS service** (Dịch vụ AWS).
2. Tại mục **Use case** (Trường hợp sử dụng), chọn **Lambda** từ danh sách các dịch vụ phổ biến (hoặc tìm kiếm "Lambda" trong ô tìm kiếm).
3. Nhấn nút **Next** ở góc phải bên dưới để chuyển sang bước phân quyền.

![alt text](/Workshop/images/4/4.4/image3.png)