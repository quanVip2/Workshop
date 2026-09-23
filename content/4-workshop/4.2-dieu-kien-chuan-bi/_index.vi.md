---
title: "Điều kiện chuẩn bị"
weight: 2
pre: " <b> 4.2 </b> "
---

## Mục tiêu
Đảm bảo người đọc có thể truy cập hệ thống AWS Management Console, thiết lập tài khoản IAM với các quyền bảo mật phù hợp để lấy bộ khóa truy cập (Access Keys), và chuẩn bị sẵn mã nguồn giao diện Web trước khi bắt đầu triển khai các dịch vụ cốt lõi.

## 1. Công cụ cần chuẩn bị
Khác với các ứng dụng truyền thống, dự án này áp dụng kiến trúc Serverless 100%, do đó không yêu cầu cài đặt phần mềm máy chủ, Node.js hay Docker trên máy cá nhân. Mọi cấu hình hạ tầng đều được thực hiện trực tiếp trên AWS Management Console.

Bạn chỉ cần chuẩn bị:

* **Tài khoản AWS:** Có quyền truy cập vào AWS Management Console.
* **Trình duyệt Web (Browser):** Khuyến nghị sử dụng Google Chrome, Cốc Cốc hoặc Microsoft Edge để chạy và kiểm thử giao diện.
* **Trình soạn thảo mã (Code Editor):** Visual Studio Code (hoặc Notepad++) dùng để chỉnh sửa thông số trong mã nguồn.
* **Mã nguồn dự án:** File `index.html` chứa bộ khung giao diện Web tĩnh và logic kết nối AWS SDK (có sẵn trong phụ lục).

## 2. Các bước thực hiện

**Bước 1: Đăng nhập AWS Console và kiểm tra Region**
1. Đăng nhập vào AWS Management Console.
2. **Checkpoint:** Quan sát góc trên cùng bên phải màn hình, đảm bảo Region (Khu vực) đang được chọn là **us-east-1 (N. Virginia)**. Toàn bộ tài nguyên lưu trữ và tính toán của workshop này sẽ được gom chung tại khu vực này để tối ưu tốc độ và tránh lỗi khác Region.

**Bước 2: Tạo khóa truy cập (IAM Access Key) cho ứng dụng Web**
Để giao diện Web (chạy trên trình duyệt của người dùng) có thể kết nối với kho S3 và cơ sở dữ liệu DynamoDB một cách an toàn, chúng ta cần cấp cho nó một bộ chìa khóa định danh.

1. Từ thanh tìm kiếm của AWS Console, truy cập dịch vụ **IAM (Identity and Access Management)**.
2. Điều hướng đến mục **Users** và chọn người dùng bạn muốn cấp quyền là `WebUser`
3. Chuyển sang thẻ **Security credentials** (Thông tin xác thực bảo mật).
4. Kéo xuống phần **Access keys**, nhấn nút **Create access key**.
5. Bấm tải về file CSV hoặc sao chép cẩn thận 2 chuỗi ký tự: `Access key ID` và `Secret access key`.
![Tạo Access Key](/images/4/4.2/image2.png)

**Bước 3: Tích hợp khóa bảo mật vào mã nguồn**
1. Mở file `index.html` bằng Visual Studio Code.
2. Tìm đến khối mã cấu hình AWS SDK (ở phần `<script>`) và điền 2 giá trị Key vừa lấy được ở Bước 2 vào đúng vị trí.
 ![cấu hình](/images/4/4.2/image3.png)
3. **Checkpoint:** Lưu file `index.html` thành công. Lúc này file mã nguồn đã sẵn sàng kết nối với hạ tầng đám mây.

## 3. Kết quả mong đợi
* Đăng nhập thành công vào AWS Management Console tại khu vực `us-east-1`.
* Khởi tạo và lưu trữ an toàn bộ khóa truy cập định danh (Access Key ID & Secret Access Key) từ dịch vụ IAM.
* Mã nguồn dự án (`index.html`) đã được cập nhật thành công khóa bảo mật, sẵn sàng cho các bước triển khai tài nguyên ở chương tiếp theo.