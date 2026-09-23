---
title: "Khởi tạo hàm AWS Lambda"
weight: 1
pre: " <b> 4.6.1 </b> "
---

# KHỞI TẠO HÀM AWS LAMBDA

**Bước 1: Tạo mới hàm Lambda**

* Từ AWS Management Console, tìm kiếm và truy cập dịch vụ **Lambda**. Đảm bảo Region đang ở `us-east-1`.
* Nhấn nút màu cam **Create function** (Tạo hàm).
* Chọn tùy chọn **Author from scratch** (Tạo từ đầu).

![alt text](/Workshop/images/4/4.5/image1.png)
**Bước 2: Thiết lập thông số cơ bản**

* **Function name (Tên hàm):** Đặt tên cho hàm, ví dụ: `HamXuLyAnh12`.
* **Runtime:** Chọn **Python 3.14** *(Lưu ý: Bắt buộc phải chọn đúng phiên bản này để tương thích với Layer Pillow ở bước sau)*.
* **Architecture:** Giữ nguyên `x86_64`.
![alt text](/Workshop/images/4/4.5/image2.png)
**Bước 3: Gắn quyền IAM (Execution Role)**

* Mở rộng mục **Additional settings** (Thay đổi vai trò thực thi mặc định).
* Chọn **Custom existing role** (Sử dụng vai trò hiện có).
* Tại ô tìm kiếm bên dưới, nhấp vào và chọn tên IAM Role mà bạn đã tạo ở phần trước , bấm save
![alt text](/Workshop/images/4/4.5/image3.png)
* Kéo xuống dưới và nhấn **Create function** để hệ thống khởi tạo máy chủ ảo.
![alt text](/Workshop/images/4/4.5/image4.png)