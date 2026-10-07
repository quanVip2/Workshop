---
title: "Xây dựng cổng API Gateway"
weight: 8
pre: " <b> 4.8 </b> "
---

## Mục tiêu
Thiết lập **Amazon API Gateway** đóng vai trò là "Cửa ngõ trung tâm" (Front Door) để giao diện Web Frontend giao tiếp với hệ thống Backend an toàn. 

## Tổng quan kiến trúc API
Trong hệ thống Serverless Enterprise của chúng ta, Frontend tuyệt đối không được gọi trực tiếp vào Database hay S3. Thay vào đó, nó phải đi qua API Gateway. 
API Gateway thực hiện 2 nhiệm vụ tối quan trọng:
1. **Kiểm duyệt bảo mật:** Chặn người lạ bằng cách kiểm tra thẻ `JWT Token` thông qua Cognito Authorizer.
2. **Định tuyến (Routing):** Phân luồng các yêu cầu (Upload, Lấy Lịch sử, Download) tới đúng hàm AWS Lambda tương ứng để xử lý.

*(Lưu ý: Hàm `HamXuLyAnh` sẽ không được kết nối vào API Gateway vì nó chạy ngầm (Background Job) thông qua sự kiện S3 Trigger).*

## Nội dung thực hành
Chúng ta sẽ chia quy trình thiết lập API Gateway thành 4 giai đoạn tương ứng với 4 bài lab nhỏ:
* **4.8.1 Khởi tạo HTTP API:** Xây dựng khung API nền tảng.
* **4.8.2 Cấu hình Cognito JWT Authorizer:** Tích hợp lớp bảo vệ bằng Token.
* **4.8.3 Thiết lập Routes & Integrations:** Tạo 3 tuyến đường kết nối với 3 hàm Lambda.
* **4.8.4 Cấu hình CORS & Lấy URL:** Mở khóa giao tiếp trình duyệt và hoàn tất triển khai.

9. [Vai trò trung tâm của Amazon API Gateway trong hệ thống](/Workshop/images/so_do.png)
