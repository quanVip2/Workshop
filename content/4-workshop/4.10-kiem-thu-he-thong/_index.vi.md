---
title: "Kiểm thử hệ thống "
weight: 10
pre: " <b> 4.10 </b> "
---

## Mục tiêu
Đánh giá toàn diện hoạt động của dự án từ đầu cuối (End-to-End). Kiểm chứng khả năng tự động hóa của luồng sự kiện (S3 Trigger Lambda) và đặc biệt là kiểm tra tính năng cách ly dữ liệu người dùng (Multi-user isolation) thông qua kỹ thuật định danh ngầm.

## Tổng quan
Để giải quyết bài toán "Mỗi thiết bị một lịch sử khác nhau" mà không cần phải xây dựng hệ thống Đăng ký/Đăng nhập phức tạp (như Amazon Cognito), dự án này áp dụng một thủ thuật thông minh ở phía Frontend: Sử dụng LocalStorage.

Khi một trình duyệt truy cập Web, nó tự động sinh ra một mã số định danh ẩn (Ví dụ: `user_123xyz`). Mã này được tự động gắn vào tên file khi đẩy lên S3, đi qua Lambda và lưu vào DynamoDB. Khi giao diện gọi dữ liệu về, nó dùng bộ lọc (Filter) để chỉ lấy những bản ghi thuộc về mã định danh đó, tạo ra ảo giác về những "không gian cá nhân" hoàn toàn độc lập và bảo mật.

## Kết quả mong đợi
* Ứng dụng tải ảnh gốc lên S3 và lấy về ảnh đã nén thành công trong khoảng 8 giây.
* Lịch sử thao tác trên hai trình duyệt web khác nhau (ví dụ: Google Chrome và Cốc Cốc) hoàn toàn tách biệt, không bị nhìn thấy dữ liệu của nhau.
* Chức năng tải ảnh về (Download) và Xóa ảnh khỏi lịch sử (Delete) hoạt động trơn tru.

---

## Các bước kiểm thử chi tiết

### Bước 1: Trải nghiệm trên thiết bị thứ nhất (Ví dụ: Google Chrome)
1. Mở đường link Static Website S3 bằng trình duyệt Google Chrome.

![alt text](/images/4/4.10/image1.png)

2. Nhấn vào khu vực tải ảnh, chọn một tấm ảnh dung lượng lớn từ máy tính.

![alt text](/images/4/4.10/image2.png)

3. Nhấn **TẢI ẢNH LÊN HỆ THỐNG**.

![alt text](/images/4/4.10/image3.png)

4. Quan sát dòng trạng thái: Chuyển từ *"Đang đẩy ảnh lên kho S3 gốc..."* sang *"Đang chờ hệ thống nén ảnh (8s)..."* và cuối cùng là *"Hoàn tất!"*.

![alt text](/images/4/4.10/image4.png)

5. Bức ảnh thu nhỏ hiện ra, bạn nhấn **Mở / Tải ảnh này xuống** để kiểm tra chất lượng và xem dung lượng thực tế đã được giảm đi bao nhiêu so với ảnh 
gốc.

![alt text](/images/4/4.10/image5.png)

6. Kéo xuống phần Lịch sử Dữ liệu, bạn sẽ thấy thông tin bức ảnh vừa tải (Đã được cắt bỏ tiền tố định danh để giao diện hiển thị tên gốc đẹp mắt).

![alt text](/images/4/4.10/image6.png)

### Bước 2: Kiểm chứng không gian độc lập trên thiết bị thứ hai (Ví dụ: Cốc Cốc)
1. Giữ nguyên trang web bên Chrome, bạn mở thêm trình duyệt Cốc Cốc (hoặc mở Tab Ẩn danh).
2. Dán đường link website vào Cốc Cốc.
3. Kéo xuống phần Lịch sử Dữ liệu, bạn sẽ thấy dòng chữ: *"Bạn chưa tải lên tấm ảnh nào"*. Mặc dù bạn vừa tải ảnh bên Chrome, nhưng Cốc Cốc hoàn toàn không nhìn thấy nhờ cơ chế định danh LocalStorage.

![alt text](/images/4/4.10/image7.png)

4. Thử tải một bức ảnh khác (Ví dụ: Ảnh B) trên Cốc Cốc. Lúc này lịch sử bên Cốc Cốc hiện Ảnh B, còn lịch sử bên Chrome (sau khi bấm nút Làm mới) vẫn chỉ hiện Ảnh A. 
   
![alt text](/images/4/4.10/image8.png)

$$\rightarrow \text{Tính năng Multi-user hoạt động thành công xuất sắc!}$$

### Bước 3: Kiểm thử tính năng Xóa
1. Quay lại Chrome, bấm nút 🗑️ **Xóa** ở bức ảnh trong bảng lịch sử.
2. Một bảng xác nhận hiện lên, chọn **OK**.
![alt text](/images/4/4.10/image9.png)
3. Giao diện tự động tải lại và bức ảnh biến mất khỏi lịch sử (Lệnh `deleteItem` của DynamoDB đã được thực thi).

![alt text](/images/4/4.10/image10.png)

# CÁC DỊCH VỤ AWS ĐƯỢC SỬ DỤNG

Trong quá trình kiểm thử ứng dụng, nền tảng đã tích hợp các dịch vụ AWS sau:

| Dịch vụ AWS | Mục đích |
| :--- | :--- |
| **Amazon S3** | Lưu trữ giao diện web tĩnh, hình ảnh gốc và ảnh sau khi nén |
| **AWS Lambda** | Cung cấp môi trường tính toán phi máy chủ để tự động xử lý và nén ảnh |
| **Amazon DynamoDB** | Lưu trữ dữ liệu lịch sử thao tác (metadata) của người dùng |
| **AWS IAM** | Cấp quyền truy cập bảo mật cho mã nguồn Frontend và các dịch vụ nội bộ |
| **Amazon CloudWatch** | Giám sát tình trạng hoạt động của ứng dụng, ghi nhận lỗi và nhật ký hệ thống |

Việc tất cả các giao diện hoạt động thành công chứng minh rằng ứng dụng Hệ thống Xử lý Ảnh Tự động đã được triển khai hoàn chỉnh và vận hành ổn định trên hạ tầng điện toán đám mây AWS.