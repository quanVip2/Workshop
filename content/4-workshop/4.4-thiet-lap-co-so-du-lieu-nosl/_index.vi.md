---
title: "Thiết lập cơ sở dữ liệu NOSQL"
weight: 4
pre: " <b> 4.4 </b> "
---

## Mục tiêu
Khởi tạo một bảng cơ sở dữ liệu phi quan hệ (NoSQL) trên AWS để lưu trữ lịch sử xử lý ảnh (Metadata) bao gồm: Tên file (kèm mã ẩn danh của người dùng), kích thước file sau khi nén, và thời gian xử lý. Đảm bảo bất kỳ ai đọc tài liệu đều có thể tự tái tạo lại được cấu trúc dữ liệu này.

## Lý do lựa chọn dịch vụ (Architecture Design)
Trong kiến trúc Serverless, Amazon DynamoDB được lựa chọn thay thế cho các cơ sở dữ liệu quan hệ truyền thống (như MySQL/PostgreSQL trên Amazon RDS) vì 3 lý do cốt lõi:

* **Hoàn toàn Serverless:** Không cần khởi tạo, quản lý hay bảo trì máy chủ ảo.
* **Linh hoạt (Schema-less):** Dễ dàng thêm bớt các trường dữ liệu (như Kích thước, Loại file) ở các bản cập nhật sau mà không làm vỡ cấu trúc bảng.
* **Tối ưu chi phí (Cost Optimization):** Tính phí theo từng lượt đọc/ghi (Pay-per-request). Khi ứng dụng không có người dùng, chi phí lưu trữ cơ sở dữ liệu gần như bằng 0.

## Các bước thực hiện (End-to-End Deployment)

**Bước 1: Truy cập dịch vụ DynamoDB**
1. Tại giao diện AWS Management Console, sử dụng thanh tìm kiếm (Search bar) trên cùng, gõ **DynamoDB** và chọn dịch vụ cơ sở dữ liệu này.
2. Đảm bảo Region ở góc trên bên phải vẫn đang là **us-east-1 (N. Virginia)**.

**Bước 2: Khởi tạo bảng dữ liệu (Create Table)**
1. Tại bảng điều khiển (Dashboard) của DynamoDB, nhấn nút màu cam **Create table** (Tạo bảng).
2. Trình duyệt sẽ chuyển sang trang cấu hình chi tiết, bạn cần điền chính xác các thông số sau (để khớp với mã nguồn Frontend đã chuẩn bị):
   * **Table name (Tên bảng):** Nhập `ThongTinAnh`
   * **Partition key (Khóa phân vùng):** Nhập `TenHinhAnh`. Kế bên, giữ nguyên kiểu dữ liệu là **String**. *(Đây là khóa chính (Primary Key) dùng để phân biệt các bức ảnh và là điều kiện bắt buộc để giao diện Web có thể thực thi lệnh `deleteItem` xóa ảnh).*
   * **Sort key:** Để trống.
![Ảnh](/Workshop/images/4/4.3/image1.png)

**Bước 3: Tối ưu hóa chi phí và Bảo mật cơ bản**
1. Kéo xuống phần **Table settings** (Cài đặt bảng). Thay vì để Default, hãy chọn **Customize settings** (Tùy chỉnh cài đặt) để tối ưu chi phí cho đồ án.
2. Tại mục **Read/write capacity settings** (Cài đặt dung lượng đọc/ghi):
   * Chọn **On-demand** (Theo yêu cầu). Thiết lập này giúp bảng dữ liệu hoạt động đúng chuẩn Serverless: chỉ tính tiền khi có phát sinh lệnh đọc/ghi, giải quyết bài toán tối ưu chi phí (Cost optimization) cho hệ thống khi rảnh rỗi.
3. Cuộn xuống dưới cùng và nhấn **Create table**.

![alt text](/Workshop/images/4/4.3/image2.png)

**Bước 4: Kiểm thử trạng thái khởi tạo (Metric/Log Checkpoint)**
Hệ thống AWS sẽ mất khoảng vài chục giây để cấp phát tài nguyên.
1. Bạn hãy quay lại màn hình danh sách **Tables**.
2. Quan sát cột **Status** (Trạng thái) của bảng `ThongTinAnh`. Khi trạng thái chuyển từ `Creating` sang **Active** (màu xanh lá), quá trình khởi tạo đã hoàn tất.

## Kết quả mong đợi
* Bảng cơ sở dữ liệu NoSQL `ThongTinAnh` đã được khởi tạo thành công với trạng thái **Active**.
* Khóa chính (Partition Key) được thiết lập chính xác là `TenHinhAnh`, tương thích hoàn toàn với API trên giao diện Web.
* Hệ thống được cấu hình theo dạng **On-Demand**, đáp ứng tiêu chuẩn tối ưu hóa chi phí cho một ứng dụng Serverless thực tế.