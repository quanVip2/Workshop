---
title: "Kiểm thử và Giám sát hệ thống (CloudWatch)"
weight: 12
pre: " <b> 4.12 </b> "
---

## Mục tiêu
Đánh giá toàn diện luồng hoạt động của dự án từ đầu cuối (End-to-End). Kiểm chứng khả năng xác thực bảo mật đa người dùng (Amazon Cognito), luồng xử lý ảnh tự động tích hợp Trí tuệ nhân tạo (Amazon Rekognition), và khả năng giám sát, truy vết lỗi hệ thống thông qua Amazon CloudWatch.

## Tổng quan
Khác với các ứng dụng thử nghiệm sử dụng LocalStorage để tạo định danh ảo, hệ thống Enterprise này được bảo vệ nghiêm ngặt bằng Amazon Cognito và API Gateway. 

Mỗi người dùng khi truy cập đều phải có một tài khoản Email xác thực. Hệ thống sử dụng JWT Token để cấp quyền và định tuyến. Bất cứ khi nào trình duyệt yêu cầu tải ảnh lên hay lấy lịch sử, Token này sẽ được API Gateway giải mã để đối chiếu với bảng cơ sở dữ liệu DynamoDB, tạo ra một không gian làm việc (Workspace) hoàn toàn độc lập, bảo mật và cá nhân hóa cho từng người dùng. Mọi tiến trình xử lý ngầm đều được AWS lưu vết lại trên CloudWatch để quản trị viên dễ dàng theo dõi.

## Kết quả mong đợi
* Giao diện Đăng ký, gửi mã OTP và Đăng nhập bằng Email hoạt động mượt mà.
* Tải ảnh lên thành công, Bảng Dashboard thống kê tính toán chính xác % dung lượng tiết kiệm.
* Dịch vụ AI tự động trích xuất các nhãn dán (Tags) phù hợp với nội dung bức ảnh.
* Dữ liệu của tài khoản A không bị hiển thị chéo sang tài khoản B (Multi-tenant Isolation).
* Quản trị viên có thể xem chi tiết thời gian thực thi của hàm Lambda trên CloudWatch Logs.

---

## Các bước kiểm thử chi tiết

### Bước 1: Trải nghiệm Xác thực và Tính năng AI trên Tài khoản A
1. Mở đường link [website](https://trang-web-xu-ly-anh-cua-toi.s3.us-east-1.amazonaws.com/index.html) đã deploy trên  S3 bằng trình duyệt web.
2. Tại giao diện **Bảo Mật Hệ Thống**, nhấn vào "Chưa có tài khoản? Đăng ký". Nhập một Email thật và Mật khẩu (có chữ hoa, chữ thường, số, ký tự đặc biệt).
3. Kiểm tra Hộp thư đến (Email) để lấy mã OTP 6 số do Amazon Web Services gửi, nhập vào web để xác thực.
4. Sau khi đăng nhập thành công, tải một bức ảnh dung lượng lớn lên hệ thống.
5. Quan sát trạng thái xử lý. Sau vài giây, hệ thống trả về thông báo "Hoàn tất".
6. **Kiểm tra Bảng Dashboard & Lịch sử:**
   * Bảng Dashboard sẽ tự động cập nhật: Tổng số ảnh (1), Tổng dung lượng gốc (Ví dụ: 2MB), Dung lượng sau nén (Ví dụ: 150KB), và hiển thị Đã tiết kiệm (Ví dụ: 92%).
   * Cột **Nhãn dán AI 🤖** trong bảng lịch sử sẽ hiển thị các từ khóa bằng tiếng Anh (Ví dụ: *Person, Face, Electronics*) phản ánh đúng nội dung tấm hình.

![alt text](/Workshop/images/4/4.12/2.1.png)
*Chú thích ảnh: Giao diện cá nhân của Tài khoản A sau khi xử lý ảnh.*

### Bước 2: Kiểm chứng cách ly dữ liệu đa người dùng (Multi-tenant)
1. Giữ nguyên tab của Tài khoản A, bạn mở thêm một tab **Trình duyệt Ẩn danh (Incognito)** hoặc dùng trình duyệt khác (Ví dụ: Mở Cốc Cốc trong khi đang dùng Chrome).
2. Truy cập vào website, thực hiện Đăng ký và Đăng nhập với một địa chỉ **Email hoàn toàn khác** (Tài khoản B).
3. Sau khi đăng nhập thành công, bạn sẽ thấy Bảng Dashboard của Tài khoản B đang hiển thị **0**, và lịch sử thông báo: *"Bạn chưa tải lên ảnh nào"*.
4. Dữ liệu của Tài khoản A hoàn toàn bị cô lập và được bảo vệ tuyệt đối nhờ cơ chế JWT Token của Cognito và điều hướng của API Gateway.

![alt text](/Workshop/images/4/4.12/2.2.png)
*Chú thích ảnh: Khả năng cách ly dữ liệu bảo mật giữa các tài khoản.*

### Bước 3: Giám sát hệ thống với Amazon CloudWatch
Hệ thống Serverless không có máy chủ để bạn truy cập vào xem log trực tiếp, do đó AWS cung cấp CloudWatch để thu thập toàn bộ dấu vết thực thi.

1. Đăng nhập vào AWS Management Console, tìm kiếm và chọn dịch vụ **CloudWatch**.
2. Ở thanh menu bên trái, phần *Logs*, chọn **Log groups**.
3. Tìm và nhấp vào nhóm log của hàm xử lý ảnh: `/aws/lambda/HamXuLyAnh`.
4. Nhấp vào bản ghi luồng sự kiện (Log stream) mới nhất trên cùng.
5. Tại đây, bạn sẽ thấy các thông báo hệ thống được in ra (Ví dụ: *Nén ảnh và phân tích AI thành công!*), kèm theo thông số **Billed Duration** (Thời gian tính phí tính bằng mili-giây) và **Memory Used** (Lượng RAM thực tế mà hàm đã sử dụng để xử lý đồ họa).

![alt text](/Workshop/images/4/4.12/2.3.png)
*Chú thích ảnh: Giám sát quá trình thực thi hàm Lambda qua CloudWatch Logs.*

---

## TỔNG KẾT CÁC DỊCH VỤ AWS ĐƯỢC SỬ DỤNG

Trong quá trình xây dựng kiến trúc Enterprise này, hệ thống đã ứng dụng một hệ sinh thái mạnh mẽ gồm các dịch vụ đám mây AWS sau:

| Dịch vụ AWS | Vai trò trong hệ thống |
| :--- | :--- |
| **Amazon Cognito** | Quản lý định danh, đăng ký, đăng nhập và cấp phát JWT Token bảo mật. |
| **Amazon API Gateway** | Cổng giao tiếp REST API trung tâm, xác thực Token và bảo vệ Lambda khỏi các truy cập trái phép. |
| **AWS Lambda** | Cụm vi dịch vụ (Microservices) chịu trách nhiệm cấp quyền URL, xử lý đồ họa, truy vấn lịch sử. |
| **Amazon Rekognition** | Ứng dụng Trí tuệ nhân tạo (Machine Learning) để nhận diện chủ thể và gắn nhãn dán bức ảnh. |
| **Amazon S3** | Kho lưu trữ Object an toàn dành cho hình ảnh gốc (Input) và hình ảnh thu nhỏ (Output). |
| **Amazon DynamoDB** | Cơ sở dữ liệu NoSQL lưu vết toàn bộ metadata, phục vụ truy vấn Dashboard thống kê. |
| **AWS IAM** | Cấp quyền bảo mật tối thiểu (Least Privilege) giữa các dịch vụ đám mây với nhau. |
| **Amazon CloudWatch**| Thu thập nhật ký hệ thống (Logs), giám sát lỗi và đo lường hiệu suất tự động. |

Việc toàn bộ hệ thống hoạt động ổn định và chính xác chứng minh rằng bạn đã triển khai thành công một kiến trúc Web phi máy chủ (Serverless) hoàn thiện, đáp ứng các tiêu chuẩn bảo mật và hiệu suất của một hệ thống Doanh nghiệp thực thụ.