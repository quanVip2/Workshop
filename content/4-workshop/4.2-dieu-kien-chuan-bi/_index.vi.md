---
title: "Điều kiện chuẩn bị"
weight: 2
pre: " <b> 4.2 </b> "
---

## Mục tiêu
Đảm bảo bạn có đủ quyền truy cập vào AWS Management Console, thiết lập đúng khu vực (Region) triển khai và chuẩn bị sẵn sàng môi trường soạn thảo mã nguồn (Local Environment) trước khi bước vào xây dựng các dịch vụ cốt lõi.

## 1. Công cụ cần chuẩn bị
Dự án này áp dụng kiến trúc Serverless 100% kết hợp với Frontend tĩnh, do đó bạn không yêu cầu cài đặt phần mềm máy chủ ảo, Node.js hay Docker trên máy tính cá nhân. Mọi cấu hình hạ tầng backend đều được thực hiện trực tiếp trên AWS Management Console.

Bạn chỉ cần chuẩn bị:

* **Tài khoản AWS:** Có quyền truy cập vào AWS Management Console (Sử dụng tài khoản AWS Learner Lab hoặc tài khoản cá nhân).
* **Trình duyệt Web (Browser):** Khuyến nghị sử dụng Google Chrome, Cốc Cốc hoặc Microsoft Edge để chạy và kiểm thử giao diện giao tiếp với API.
* **Trình soạn thảo mã (Code Editor):** Visual Studio Code (hoặc Sublime Text, Notepad++) dùng để lập trình giao diện HTML/JS và cấu hình hàm Python.
* **Môi trường cục bộ:** Một thư mục trống trên máy tính để chứa mã nguồn Frontend dự án.

## 2. Các bước thực hiện

**Bước 1: Đăng nhập AWS Console và kiểm tra Region**
1. Đăng nhập vào AWS Management Console bằng tài khoản của bạn.
2. **Checkpoint:** Quan sát góc trên cùng bên phải màn hình, đảm bảo Region (Khu vực) đang được chọn là **US East (N. Virginia) `us-east-1`**. 
*Lý do:* Việc gom chung toàn bộ tài nguyên lưu trữ (S3), tính toán (Lambda), xác thực (Cognito) và AI (Rekognition) tại một khu vực sẽ tối ưu hóa tốc độ kết nối, tránh độ trễ và loại bỏ hoàn toàn các lỗi xung đột dịch vụ khác Region.
![Khu vực hiện thị](/Workshop/images/4/4.2/2.1.png)

**Bước 2: Chuẩn bị không gian làm việc (Workspace)**
1. Tạo một thư mục mới trên máy tính của bạn, đặt tên là `Enterprise_Image_Processor`.
2. Mở thư mục này bằng Visual Studio Code.
3. Tạo một file trống có tên là `index.html`. File này sẽ là nơi chúng ta lập trình toàn bộ giao diện Web, biểu mẫu Đăng nhập (Cognito) và Bảng điều khiển (Dashboard) ở các bước sau.

![Màn hình visual code](/Workshop/images/4/4.2/2.2.png)

---

### ⚠️ Lưu ý Bảo mật Tối quan trọng (Security Paradigm Shift)
Nếu bạn đã từng làm các bài Lab cơ bản trước đây, bạn thường được hướng dẫn tạo *IAM Access Key* và nhúng trực tiếp (hardcode) vào mã nguồn HTML/JS để kết nối với AWS SDK. **ĐÂY LÀ MỘT LỖ HỔNG BẢO MẬT NGHIÊM TRỌNG** trong môi trường thực tế, vì bất kỳ ai xem mã nguồn trang web (F12) đều có thể đánh cắp chìa khóa và kiểm soát tài khoản AWS của bạn.

Trong Workshop chuẩn Enterprise này, chúng ta **TUYỆT ĐỐI KHÔNG** sử dụng Access Key tĩnh trên Frontend. 
Thay vào đó, hệ thống của chúng ta sẽ sử dụng kiến trúc bảo mật nhiều lớp:
* Người dùng đăng nhập qua **Amazon Cognito** để lấy **JWT Token** (Chỉ có giá trị trong 1 giờ).
* Token này được gửi tới **Amazon API Gateway** để xác thực.
* Sau khi hợp lệ, AWS Lambda ở backend mới cấp một **Presigned URL** (Đường dẫn có chữ ký tạm thời sống trong 5 phút) để trình duyệt web có thể an toàn tải ảnh lên/xuống S3 mà không cần biết bất kỳ mật khẩu nào của hệ thống.

---

## 3. Kết quả mong đợi
* Bạn đã đăng nhập thành công vào AWS Management Console tại khu vực `us-east-1`.
* Đã khởi tạo thành công thư mục dự án và file `index.html` trên máy tính cá nhân.
* Nắm vững tư duy bảo mật mới: Không sử dụng và không nhúng IAM Access Key vào giao diện Frontend.