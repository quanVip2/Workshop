---
title: "2. Tích hợp API & Dashboard AI"
weight: 2
pre: " <b> 4.11.2 </b> "
---

## 1. Nhúng API Gateway URL
Trình duyệt web không gọi trực tiếp Lambda mà thông qua **API Gateway**.
1. Vẫn trong file `index.html`, tìm đến phần cấu hình API Gateway.
2. Dán đường link **Invoke URL** (bạn copy ở bài 4.8) vào các hằng số:
   * `API_GATEWAY_URL`: URL kèm đuôi `/get-upload-url` và `/get-download-url`
   * `API_HISTORY_URL`: URL kèm đuôi `/get-history`

## 2. Trình diễn Bảng thống kê (Analytics Dashboard)
Thay vì tạo thêm gánh nặng cho Backend, hàm `loadHistory()` ở Frontend đã được lập trình để nhận mảng dữ liệu JSON từ Lambda và tự động tính toán các chỉ số ngay trên trình duyệt (Client-side rendering):
* **Tổng số ảnh:** Đếm số lượng object trả về.
* **Tổng dung lượng gốc & Nén:** Tính tổng cột `KichThuocGoc` và `KichThuocNen`.
* **Phần trăm tiết kiệm:** Áp dụng công thức `((Gốc - Nén) / Gốc) * 100` để hiển thị tỷ lệ % băng thông đã tối ưu được.

## 3. Hiển thị Nhãn dán Trí tuệ nhân tạo (AI Tags)
Trong vòng lặp tạo bảng lịch sử, hệ thống sẽ trích xuất cột `NhanDanAI` từ DynamoDB (do Amazon Rekognition phân tích) và in ra giao diện. Nếu ảnh không có nhãn dán, hệ thống hiển thị giá trị `N/A`.

![alt text](/Workshop/images/4/4.11/2.4.png)
*Chú thích ảnh: Dashboard thống kê tối ưu dung lượng theo thời gian thực.*

![alt text](/Workshop/images/4/4.11/2.5.png)
*Chú thích ảnh: Trí tuệ nhân tạo Rekognition tự động gán nhãn chủ thể bức ảnh.*