---
title: "Phân quyền cho Lambda"
weight: 2
pre: " <b> 4.5.2 </b> "
---



**Bước 1: Lựa chọn các bộ quy tắc (Policies)**
Tại bước **Add permissions** (Thêm quyền hạn), AWS cung cấp hàng ngàn bộ chính sách khác nhau. Bạn sử dụng ô tìm kiếm (Search bar) để tìm và đánh dấu tích (☑) vào ô vuông bên cạnh chính xác 3 Policy sau:

*   Gõ `AmazonS3FullAccess` ➔ Đánh dấu tích.
    *(Mục đích: Cho phép Lambda lấy ảnh từ S3 Input và lưu ảnh sau khi nén sang S3 Output).*
    ![alt text](/images/4/4.4/image4.png)
*   Xóa ô tìm kiếm, gõ tiếp `AmazonDynamoDBFullAccess` ➔ Đánh dấu tích.
    *(Mục đích: Cho phép Lambda ghi log lịch sử - Metadata vào bảng dữ liệu NoSQL).*
    ![alt text](/images/4/4.4/image5.png)
*   Xóa ô tìm kiếm, gõ tiếp `AWSLambdaBasicExecutionRole` ➔ Đánh dấu tích.
    *(Mục đích: Đây là Policy cốt lõi đáp ứng yêu cầu Kiểm thử và Đo lường (Monitoring) của dự án, cho phép Lambda có quyền tạo Log Group và ghi nhật ký hoạt động/lỗi lên Amazon CloudWatch).*
    ![alt text](/images/4/4.4/image6.png)


Sau khi tích đủ 3 mục, nhấn nút **Next**.

**Bước 2: Đặt tên và hoàn tất**
Tại bước **Name, review, and create**:

*   **Role name (Tên vai trò):** Nhập tên có ý nghĩa, ví dụ: `RoleChoLambda`.
*   **Description (Mô tả):** Có thể ghi chú: *Cấp quyền S3, DynamoDB và CloudWatch cho hàm nén ảnh Thumbnail Generator.*

Cuộn màn hình xuống phần **Permissions boundary**, kiểm tra lại danh sách các policy để chắc chắn rằng cả 3 Policy (`AmazonS3FullAccess`, `AmazonDynamoDBFullAccess`, `AWSLambdaBasicExecutionRole`) đều đã có mặt.

Nhấn nút **Create role** (Tạo vai trò) ở góc dưới cùng để hoàn tất.
![alt text](/images/4/4.4/image7.png)