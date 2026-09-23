---
title: "Dọn dẹp tài nguyên "
weight: 11
pre: " <b> 4.11 </b> "
---

# DỌN DẸP TÀI NGUYÊN (CLEAN-UP)

## Mục tiêu
Loại bỏ toàn bộ các tài nguyên và dịch vụ đã khởi tạo trên AWS trong suốt quá trình thực hành. Đảm bảo môi trường đám mây được dọn sạch hoàn toàn nhằm đáp ứng tiêu chí Tối ưu hóa: Tránh phát sinh chi phí (Zero-cost) sau khi dự án kết thúc.

## Tổng quan
Trong môi trường điện toán đám mây, các dịch vụ lưu trữ (như S3, DynamoDB) sẽ tiếp tục tính phí dựa trên dung lượng lưu trữ ngay cả khi bạn không còn chạy ứng dụng. Do đó, việc dọn dẹp tài nguyên (Clean-up) là một kỹ năng bắt buộc đối với mọi Kỹ sư Cloud.

Để việc xóa diễn ra suôn sẻ và không bị hệ thống chặn do ràng buộc dữ liệu, chúng ta sẽ tiến hành xóa theo quy tắc tuần tự: Phải làm rỗng dữ liệu bên trong kho lưu trữ trước rồi mới xóa vỏ kho, tiếp theo là xóa máy chủ tính toán, cơ sở dữ liệu, nhật ký hoạt động và cuối cùng là dọn dẹp các nhóm quyền bảo mật.

## Các bước thực hiện chi tiết

### Bước 1: Xóa các kho lưu trữ Amazon S3 (Rất quan trọng)
*Lưu ý: AWS không cho phép xóa một kho S3 nếu bên trong nó vẫn còn chứa bất kỳ file nào. Bạn bắt buộc phải "Empty" (Làm rỗng) trước khi "Delete" (Xóa).*
1. Truy cập dịch vụ S3, đánh dấu tích chọn kho `kho-anh-goc-cua-toi-1`.
2. Nhấn nút **Empty** ở menu trên cùng, gõ chữ `permanently delete` để xác nhận xóa toàn bộ ảnh gốc bên trong.

![alt text](/Workshop/images/4/4.11/image1.png)

3. Trở lại danh sách, tiếp tục chọn kho `kho-anh-goc-cua-toi-1` và nhấn nút **Delete**, gõ tên kho để xác nhận xóa vĩnh viễn cái vỏ kho.
![alt text](/Workshop/images/4/4.11/image2.png)
4. Lặp lại thao tác Empty và Delete tương tự cho 2 kho còn lại: `kho-anh-nho-cua-toi-1` (Kho Output) và `trang-web-xu-ly-anh-cua-toi` (Kho Website tĩnh).
![alt text](/Workshop/images/4/4.11/image3.png)

### Bước 2: Xóa bảng cơ sở dữ liệu Amazon DynamoDB
1. Truy cập dịch vụ DynamoDB, chọn **Tables** ở menu bên trái.
2. Đánh dấu tích vào bảng `ThongTinAnh`.
3. Nhấn nút **Delete**, gõ chữ `confirm` để xác nhận xóa toàn bộ dữ liệu lịch sử metadata.
![alt text](/Workshop/images/4/4.11/image4.png)

### Bước 3: Xóa hàm xử lý AWS Lambda
1. Truy cập dịch vụ Lambda, chọn tab **Functions**.
2. Đánh dấu tích vào hàm `HamXuLyAnh12`
3. Nhấn **Actions** $\rightarrow$ Chọn **Delete**, gõ chữ `delete` để xác nhận xóa mã nguồn Python.
![alt text](/Workshop/images/4/4.11/image5.png)
![alt text](/Workshop/images/4/4.11/image6.png)
### Bước 4: Xóa nhật ký Amazon CloudWatch Logs
1. Truy cập dịch vụ CloudWatch, tìm mục **Logs** $\rightarrow$ **Log Management** ở menu bên trái.
2. Tìm và tích chọn nhóm log có tên `/aws/lambda/HamXuLyAnh12` (hoặc tương ứng).
3. Nhấn **Actions** $\rightarrow$ **Delete log group** và xác nhận.

![alt text](/Workshop/images/4/4.11/image7.png)

### Bước 5: Xóa danh tính bảo mật AWS IAM
1. Truy cập dịch vụ IAM, vào mục **Roles**.
2. Tìm "Thẻ nhân viên" `RoleChoLambda`, đánh dấu tích và nhấn **Delete**.
![alt text](/Workshop/images/4/4.11/image8.png)
3. Chuyển sang mục **Users**, chọn tài khoản IAM User mà bạn đã tạo ở Chương 2, tiến hành vô hiệu hóa (**Deactivate**) phần Access Key, xóa Key và sau đó xóa luôn IAM User này.

![alt text](/Workshop/images/4/4.11/image9.png)

## Kết quả mong đợi
* Toàn bộ ảnh gốc, ảnh nén, lịch sử cơ sở dữ liệu và mã nguồn web tĩnh đã được gỡ bỏ hoàn toàn khỏi hệ thống.
* Môi trường AWS Learner Lab trở về trạng thái sạch sẽ ban đầu.
* Đảm bảo không có bất kỳ khoản phí lưu trữ hoặc vận hành nào bị trừ ngầm trong tương lai.